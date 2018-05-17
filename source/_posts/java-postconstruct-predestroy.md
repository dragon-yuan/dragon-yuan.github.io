---
title: 什么是@PostConstruct，@PreDestroy注解
categories:
  - Java
date: 2018-05-17 23:19:17
---
首先这两个注解是在JDK1.5增加的，注解@PostConstruct允许在Bean初始化之前执行一些方法，而@PreDestroy是在Bean销毁之前执行的操作。

@PostConstruct（@PreDestroy）:被@PostConstruct修饰的方法会在服务器加载Servlet（Bean）的时候运行，并且只会被服务器调用一次。

生命周期如下：

```
graph LR
PostConstruct-->init
init-->some-methods
some-methods-->destory
destory-->PreDestroy
```

例如如下代码：
```java
/**
 * <p>Title: RegistryCenterConfig. </p>
 * <p>Description 调度作业，Zookeeper配置（ZK集群配置） </p>
 *
 * @author dragon
 * @date 2018/5/7 上午11:08
 */
@Configuration
@ConditionalOnClass(ElasticJob.class)
@ConditionalOnBean(annotation = MarkElasticJob.class)
@EnableConfigurationProperties(ZookeeperRegistryProperties.class)
@ConditionalOnExpression("'${elaticjob.zookeeper.server-lists}'.length() > 0")
public class RegistryCenterConfig {

    private final ZookeeperRegistryProperties regCenterProperties;

    @Autowired
    public RegistryCenterConfig(ZookeeperRegistryProperties regCenterProperties) {
        this.regCenterProperties = regCenterProperties;
    }

    /**
     * <p>Title: regCenter. </p>
     * <p>初始化配置中心 </p>
     *
     * @param serverList 服务列表
     * @param namespace  名称

     * 注意，在console上配置注册中心时，需要注意：
     * 注册中心名称和命名空间->需要和namespace保持一致
     */
    @Bean(initMethod = "init")
    public ZookeeperRegistryCenter regCenter(@Value("${elaticjob.zookeeper.server-lists}") final String serverList,
                                             @Value("${elaticjob.zookeeper.namespace}") final String namespace) {
        ZookeeperConfiguration zookeeperConfiguration = new ZookeeperConfiguration(serverList, namespace);
        zookeeperConfiguration.setBaseSleepTimeMilliseconds(regCenterProperties.getBaseSleepTimeMilliseconds());
        zookeeperConfiguration.setConnectionTimeoutMilliseconds(regCenterProperties.getConnectionTimeoutMilliseconds());
        zookeeperConfiguration.setMaxSleepTimeMilliseconds(regCenterProperties.getMaxSleepTimeMilliseconds());
        zookeeperConfiguration.setSessionTimeoutMilliseconds(regCenterProperties.getSessionTimeoutMilliseconds());
        zookeeperConfiguration.setMaxRetries(regCenterProperties.getMaxRetries());
        zookeeperConfiguration.setDigest(regCenterProperties.getDigest());
        return new ZookeeperRegistryCenter(zookeeperConfiguration);
    }

    /**
     * <p>Title: ElasticJobConfig. </p>
     * <p>在初始化Zookeeper前，注入Elastic-Job，自动扫描开放任务 </p>
     *
     * @author dragon
     * @date 2018/5/9 下午2:35
     */
    @PostConstruct
    public ElasticJobConfig initElasticJob() {
        return new ElasticJobConfig();
    }

    @PreDestroy
    public void preDestoryMethod() {
        System.out.println("preDestoryMethod...");
    }
}
```

对于如上代码，应用场景是elastic-job + zk 的启动方式，需要在zk启动前，先扫描Jobs，然后在执行Zk的init方法。

运行如下：

```
graph LR
RegistryCenterConfig-->ElasticJobConfig
ElasticJobConfig-->Autowired-RegistryCenterConfig
Autowired-RegistryCenterConfig-->init(regCenter)
init(regCenter)-->preDestoryMethod
```
