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
This post will be updated if new problems emerge or better solutions are found.

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

# 3. Images would not render

I added `?raw=true` to the end of my link.

Before: 

```
<img src="https://github.com/lsj0410/lsj0410.github.io/blob/master/assets/images/dsp-02/unit_step.png" />
```

After:

```
<img src="https://github.com/lsj0410/lsj0410.github.io/blob/master/assets/images/dsp-02/unit_step.png?raw=true" />
```

# 3. Tables would not render

I tried changing the build settings in my **_config.yml** file to `markdown: GFM` instead of `markdown: kramdown`

After I made this change, the table was rendered properly but without borders.
Another problem was that the math went rather weird.
In the end the problem was not resolved and I removed the tables.

# 4. Multi-line equations were not numbered

I changed `aligned` to `split`.

Before:

```
$$
\begin{equation}
\begin{aligned}
\int_a^b \delta(t)f(t) dt {} & ={\int_a^{0-} \delta(t)f(t) dt} + {\int_{0-}^{0+} \delta(t)f(t) dt} + {\int_{0+}^b \delta(t)f(t) dt} \\
      &= \int_{0-}^{0+} \delta(t)f(t) dt = \int_{0-}^{0+} \delta(t)f(0) dt = \int_{-\infty}^{\infty} \delta(t)f(0) dt = f(0)
\end{aligned}
\end{equation}
$$
```

After:

```
$$
\begin{equation}
\begin{split}
\int_a^b \delta(t)f(t) dt {} & ={\int_a^{0-} \delta(t)f(t) dt} + {\int_{0-}^{0+} \delta(t)f(t) dt} + {\int_{0+}^b \delta(t)f(t) dt} \\
      &= \int_{0-}^{0+} \delta(t)f(t) dt = \int_{0-}^{0+} \delta(t)f(0) dt = \int_{-\infty}^{\infty} \delta(t)f(0) dt = f(0)
\end{split}
\end{equation}
$$
```
