{% include header.html %}

让github-pages支持latex数学公式

[toc]

### 创建一个github pages仓库A并发布
+ 请参考官方说明文档
+ 英文：https://docs.github.com/en/pages/quickstart
+ 中文：https://docs.github.com/cn/pages/quickstart

### 修改_config.yml文件，加入如下内容
```
markdown: kramdown
kramdown:
  math_engine: katex
```

### 在A目录下创建_includes/header.html文件并在文件中加入如下代码
```
<head>
	<script type="text/x-mathjax-config"> 
   		MathJax.Hub.Config({ TeX: { equationNumbers: { autoNumber: "all" } } }); 
   	</script>
    <script type="text/x-mathjax-config">
    	MathJax.Hub.Config({tex2jax: {
             inlineMath: [ ['$','$'], ["\\(","\\)"] ],
             processEscapes: true
           }
         });
    </script>
    
    <script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript">
    </script>
</head>
```
### 在每一个md文档的首行加入如下代码
```
\{ \% include header.html \% \}
```

### 现在就可以在`\$ \$`中间写入行内公式，在`\$\$ \$\$`中间写跨行公式

### 一些数学公式显示例子

符号|读音|意义
|---|---|---|
$\forall$|forall、any|任意给定的
$\exists$|exists|存在
$\sum$|sum、sigma|求和、连加
$\prod$|prod、pi|求积、连剩
Q|Q|有理数
$Q^c$||无理数

德摩根律： $\overline{A\cap B}=\overline A\cup \overline B$,$\overline{A\cup B}=\overline A\cap \overline B$

$$
E^{(r)}_{m\times n}=
\left(
\begin{matrix}
E_r&O\\
O&O
\end{matrix}
\right)
$$

$$
A_{m\times n}\xrightarrow[行变换]{初等}行阶梯形矩阵\xrightarrow[行变换]{初等}行最简形矩阵\xrightarrow[列变换]{初等}等价标准形矩阵E^{(r)}_{m\times n}
$$


### 下面是在学习这个知识中参考过的一些网页

+ http://leohope.com/%E8%A7%A3%E9%97%AE%E9%A2%98/2017/09/08/page-with-latex/

+ https://lloyar.github.io/2018/10/08/mathjax-in-jekyll.html

+ 在GitHub上创建和托管个人网站(下)：https://blog.csdn.net/qq_26927285/article/details/78762237


+ jekyll的目录结构：https://jekyllrb.com/docs/structure/


+ jekyll文档:
http://jekyllcn.com/docs/templates/
