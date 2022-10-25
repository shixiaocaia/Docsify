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
body, html {
    width: 100%;
    height: 100%;
    display: flex;
}

.g-container {
    position: relative;
    margin: auto;
    width: 200px;
    height: 200px;
}

.g-progress {
    position: relative;
    margin: auto;
    width: 200px;
    height: 200px;
    border-radius: 50%;
    background: conic-gradient(#FFCDB2 0, #FFCDB2 25%, #B5838D 25%, #B5838D);
    mask: radial-gradient(transparent, transparent 80px, #000 80.5px, #000 0);
}

.g-circle {
    position: absolute;
    top: 0;
    left: 0;
    &::before,
    &::after {
        content: "";
        position: absolute;
        top: 90px;
        left: 90px;
        width: 20px;
        height: 20px;
        border-radius: 50%;
        background: #FFCDB2;
        z-index: 1;
    }
    
    &::before {
        transform: translate(0, -90px);
    }
    
    &::after {
        transform: rotate(90deg) translate(0, -90px) ;
    }
}
</style>
<div class="g-progress"></div>
<div class="g-container">
    <div class="g-progress"></div>
    <div class="g-circle"></div>
</div>
