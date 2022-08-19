---
layout: post
title: "Issues with Rendering on Github Pages"
author: "SJ Lee"
tags: Other
---

Today I moved my posts on [medium](https://medium.com/@sjl_ee/) to my new Github blog.
During the process, I ran into several problems.
Features that showed perfectly well on the Preview tab would not render properly in the blog itself.
Among the numerous solutions on the internet, here are the ones that worked for me.

# 1. Math expressions would not render

I added the following code to the bottom of my **_config.yml** file above **</head>**.

```
<script type="text/x-mathjax-config"> MathJax.Hub.Config({ TeX: { equationNumbers: { autoNumber: "all" } } }); </script>
<script type="text/x-mathjax-config">
  MathJax.Hub.Config({
    tex2jax: {
      inlineMath: [ ['$','$'], ["\\(","\\)"] ],
      processEscapes: true
    }
  });
</script>
<script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>
```

# 2. Images would not render

I added `?raw=true` to the end of my link.

Before: `<img src="https://github.com/lsj0410/lsj0410.github.io/blob/master/assets/images/dsp-02/unit_step.png" />`

After: `<img src="https://github.com/lsj0410/lsj0410.github.io/blob/master/assets/images/dsp-02/unit_step.png?raw=true" />`

# 3. Tables would not render

I changed the build settings in my **_config.yml** file to `markdown: GFM` instead of `markdown: kramdown`

After I made this change, the borders in my tables disappeared.
However this does not really interfere with my intentions of using tables, so I don't have a problem with this.
