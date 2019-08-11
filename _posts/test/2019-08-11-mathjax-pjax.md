---
layout: post
title: MathJax 渲染问题
category: 技术
tags: markdown mathjax
---

## 配置 MathJax 支持
在 Jekyll 中添加 MathJax 的支持很简单，只需在 `_config.yml`中设置 `markdown: kramdown`，并在 `_layout` 目录下的 `default.html` 中添加小段 JavaScript 代码，，以下代码配置实现了公式编号、错误提示功能
```html
<script type="text/x-mathjax-config">
    MathJax.Hub.Config({
        TeX: {
          equationNumbers: {
            autoNumber: "AMS"
          }
        },
        tex2jax: {
        inlineMath: [ ['$', '$'] ],
        displayMath: [ ['$$', '$$'] ],
        processEscapes: true,
      }
    });
    MathJax.Hub.Register.MessageHook("Math Processing Error",function (message) {
          alert("Math Processing Error: "+message[1]);
        });
    MathJax.Hub.Register.MessageHook("TeX Jax - parse error",function (message) {
          alert("Math Processing Error: "+message[1]);
        });
</script>
<script type="text/javascript" async
  src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.1/MathJax.js?config=TeX-AMS-MML_HTMLorMML">
</script>
```

## 解决 pjax 渲染问题

添加上述代码后，单独页面的渲染没有问题，但由于 3-Jekyll 这一主题使用了 pjax 来实现侧边栏的动态效果，所以点击侧边栏后，新页面并没有生成渲染。

[这篇博文](https://yelog.org/2017/07/05/MathJax-pjax/)也注意到了该问题，但按照他的方法在对含有 `\label` 的页面，还是会产生 `multiply defined label` 这一错误。

尝试了一圈之后，还是在MathJax 官方文档中找到了解决方案: [Reset Automatic Equation Numbering](http://docs.mathjax.org/en/latest/advanced/typeset.html#reset-equation-numbers)。

针对 3-Jekyll 这一主题，在 `assets/js/main.js` 中找到 `'pjax:end'` 部分进行修改
```js
$(document).on({
    'pjax:click': function () {
    NProgress.start();
    main.removeClass('fadeIn');
    },
    'pjax:end': function () {

    $.getScript("https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.1/MathJax.js?config=TeX-AMS-MML_HTMLorMML", function () {
        MathJax.Hub.Queue(
        ["resetEquationNumbers", MathJax.InputJax.TeX],
        ["PreProcess", MathJax.Hub],
        ["Reprocess", MathJax.Hub]
        );
    });
    // location.reload();
    afterPjax();
    NProgress.done();
    main.scrollTop(0).addClass('fadeIn');
    // only remove open in small screen
    if ($(window).width() <= 1024) {
        menu.add(sidebar).add(main).removeClass('open');
    };
    },
});
```





