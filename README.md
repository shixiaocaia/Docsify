<h1>XIAOCAI's Notes</h1>

📪 简介

你好，这里是小蔡的个人笔记站点，用于记录读研期间乃至以后工作中学习的内容，定期自我复盘。

> 站点源文件来源[MurphyChen](https://docs.mphy.top/#/), 通过将博主源文件删改，保留自己需要的功能。主要用于记录，并不想过于折腾。
>
> 更多修改请参考[Docsify中文文档](https://docsify.js.org/#/zh-cn/)。
>
> 🚧更新变化：
>
> - shell、cpp高亮渲染，注意同时引入cpp，c文件，否则无法生效。
> - 为了正常使用search功能，注意将所有笔记文件放在根目录中，避免`Note/C++/ch01`这样的形式，应该限制了范围。


---

🏕 [个人博客](https://shixiaocaia.fun)

博客主要记录个人生活，与主要的学习笔记分开记录，在互联网上开辟自己一片空间嘟嘟自己情绪和想法。欢迎大家来成为赛博邻居。

Stay foolish, Stay hungry.

---

🍳最近在做点什么呢

⬜C++ primer + 侯捷老师课程

⬜深入浅出计算机网络

⬜牛客Webserver项目学习

⬜三维模型轻量化处理学习

⬜研一第一年课程划过

<style>
  .circle_process {
    position: relative;
    width: 199px;
    height: 200px;
  }
  .circle_process .wrapper {
    width: 100px;
    height: 200px;
    position: absolute;
    top: 0;
    overflow: hidden;
  }
  .circle_process .right {
    right: 0;
  }
  .circle_process .left {
    left: 0;
  }
  .circle_process .circle {
    width: 200px;
    height: 200px;
    border: 20px solid transparent;
    border-radius: 50%;
    box-sizing: border-box;
    position: absolute;
    top: 0;
    transform: rotate(-135deg);
  }
  .circle_process .rightcircle {
    border-top: 20px solid green;
    border-right: 20px solid green;
    right: 0;
    -webkit-animation: circle_right 5s linear infinite;
  }
  .circle_process .leftcircle {
    border-bottom: 20px solid green;
    border-left: 20px solid green;
    left: 0;
    -webkit-animation: circle_left 5s linear infinite;
  }
  @-webkit-keyframes circle_right {
    0% {
      -webkit-transform: rotate(-135deg);
    }
    50%,
    100% {
      -webkit-transform: rotate(45deg);
    }
  }
  @-webkit-keyframes circle_left {
    0%,
    50% {
      -webkit-transform: rotate(-135deg);
    }
    100% {
      -webkit-transform: rotate(45deg);
    }
  }
</style>
<div class="circle_process">
  <div class="wrapper right">
    <div class="circle rightcircle"></div>
  </div>
  <div class="wrapper left">
    <div class="circle leftcircle" id="leftcircle"></div>
  </div>
</div>
