# SpringBoot框架

## 散记一些（Vue）

- 一般来说，创建组件的时候，放在components里面

- 创建.vue文件的时候，规定文件名要有两个大写字母，如NavBar.vue

- 其中 html的内容写在`<template></template>`之中

- JavaScript脚本写在`<script></script>`里面

- css写在`<style></style>`里面，一般要写成`<style scoped></style>`，scoped的作用是在当前组件中写的css文件加上一个随机字符串，使得样式不会影响组件以外的部分

- 推荐：Bootstrap

  ```
  网址：https://v5.bootcss.com/
  ```

  可以帮助程序员做美工，只需要挑选样式就可以了

  抄了样式的时候要导入Bootstrap的css和js

  `import "bootstrap/dist/css/bootstrap.min.css"`

  `import "bootstrap/dist/js/bootstrap"`

- 导入组件的方式：`import NavBar from './components/NavBar.vue'`from后面放引入的地址

- 使用组件的方式：

  ```vue
  export default{
    components:{
      NavBar
    }
  }
  ```

  放在components里面就可以了！

- ` <div class="container-fluid">`-fluid是让间距变宽

- 每一个页面也写成一个组件，但是不放在components，放在views里面

- 