---
title: async validator 代码片段
date: 2024-01-02 13:13:38
tags: snippets
---

写校验的几种方式
<!-- more -->
```
  rules: {
        projectCode: [
          { required: true, message: '结算项目CODE不能为空' },
          { min: 5, max: 10, message: '长度在 5-10 个字符', trigger: 'blur' },
          { pattern: /^[_a-zA-Z0-9]+$/, message: '仅支持字母及数字，不区分大小写' }
        ],
        projectName: [
          { required: true, message: '结算项目名称不能为空' },
          { validator: this.validateProject, trigger: 'blur' }
        ],
        taxRate: [
          { required: true, message: '税率不能为空' },
        ],
        bizType: [
          { required: true, message: '业务类型不能为空' },
          { min: 5, max: 20, message: '长度在 5-20 个字符', trigger: 'blur' },
          { pattern: /^[_a-zA-Z0-9]+$/, message: '仅支持字母及数字，不区分大小写' }
        ],
        bizTypeDesc: [
          { min: 0, max: 40, message: '长度在 0-40 个字符', trigger: 'blur' }
        ],
        enableStatus:[
          { required: true, message: '状态不能为空' },
        ],
      }

```