---
title: VueJS中的rules校验
categories:
  - web
date: 2017-07-19 23:00:25
---
```js
rules: {
    rulesOne: [
        { required: true, message: '请输入', trigger: 'blur' }
    ],
    rulesTwo: [
        { max: 100, message: '长度在 100个字符以内', trigger: 'blur' }
    ],
    rulesThree: [
        { required: true, message: '请选择', trigger: 'change' }
    ],
    rulesFour: [
        { type: 'array', required: true, message: '请至少选择一个', trigger: 'change' }
    ],
    rulesFive: [
        { validator: checkSomething, trigger: 'blur' }
    ]
}
```
trigger: 'blur'为离开输入框
trigger: 'change'为更换下拉框或多选框
validator为自定义规则方法名
