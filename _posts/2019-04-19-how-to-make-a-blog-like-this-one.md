---
layout: post
title: How to make a blog like this one
categories: [Misc]
---

Here's my new math blogging workflow:

- I write my posts in [Typora](https://typora.io/), which is a wysiwyg Markdown editor with Latex math support. (It's really nice and you should check it out!)
- I then push my project folder to Github and I get published in a few seconds.

It's very easy to write math in this way. No need to struggle with formatting and rendering errors on Wordpress. You have an editor with instant preview and complete control over the appearence of the site.

<!--more-->

### Setting the site

You will first need a Github account. I would recommend applying for a free "[Student Developer Pack](https://education.github.com/pack)" on Github - if you are eligible - to get a free account with unlimited public and private repositories.

You can then create a new repository, such as "\<username\>/blog". After you create a README file, edit the repository's settings to enable [Github Pages](https://pages.github.com/). You site will then appear at the adress \<username\>.github.io/blog.

### Blogging with Jekyll

There's a neat feature on Github pages which allows you to automatically transform markdown files uploaded to the repository to static webpages: [Jekyll support](https://jekyllrb.com/docs/github-pages/). The easiest way to get started is to copy my blog repository (or someone else's) and to hack it to make it yours. Read through the files. You'll find that the structure is pretty much self-explanatory.

### MathJax support

To enable Latex math support, make sure to include the following code in the html template for the site's pages:

```html
<script type="text/x-mathjax-config">
  MathJax.Hub.Config({
    tex2jax: {
      inlineMath: [['$', '$']],
      displayMath: [['$$', '$$']],
      processEscapes: true
    }
  });
</script>
<script
  type="text/javascript"
  charset="utf-8"
  src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML"
></script>
```

It's already there in my templace, and everything should work fine and dandy. Let me know if you're trying to make a math blog and run into issues. It'd be a pleasure to help!