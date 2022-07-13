---
title: "Jinja2模板修改循环外变量的值"
date: 2019-06-17T10:50:27+08:00
draft: false
tags: ["python"]
---
### 前言

> 由于jinja模板的作用域的原因，在循环内无法修改循环外变量的值，可用另外一种方法来实现

### 问题复现

```
{% set number = 0 %}
{% for i in range(4) %}
{% set number = number + 1 %}
{{ number }}  <!--结果依次打印为：1，2，3，4-->
{% endfor %}
{{ number }}  <!--依旧为0-->
```

### 解决方法

```
{% set number = [0] %}
{% for i in range(4) %}
{% if number.append(number.pop() + 1) %}{% endif %}
{% endfor %}
{{ number[0] }} <!--结果为4-->
```
