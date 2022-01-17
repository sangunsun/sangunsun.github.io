
让github-pages支持latex数学公式和画图

[toc]

### 几个数学公式和画图的效果展示
#### 一些数学公式显示例子

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

#### 画流程图

+ 有道云笔记语法(不支持)

```
graph TB
start(开始)-->setKeyNums(设置按键数量)
setKeyNums-->setKey(设置各按键参数)
setKey-->loopStart(循环开始)
loopStart-->readPin{扫描是否有按键按下?}
readPin--Yes-->playMidi(发送按键对应MIDI信号)
readPin--No-->loopEnd(循环结束)
playMidi-->loopEnd
loopEnd-->loopStart

```

+ typora使用的mermaid语法(支持)

```mermaid
graph TB
start(开始)-->setKeyNums(设置按键数量)
setKeyNums-->setKey(设置各按键参数)
setKey-->loopStart(循环开始)
loopStart-->readPin{扫描是否有按键按下?}
readPin--Yes-->playMidi(发送按键对应MIDI信号)
readPin--No-->loopEnd(循环结束)
playMidi-->loopEnd
loopEnd-->loopStart
```

### 配置步骤
#### 创建一个github pages仓库A并发布
+ 请参考官方说明文档
+ 英文：https://docs.github.com/en/pages/quickstart
+ 中文：https://docs.github.com/cn/pages/quickstart

#### 修改_config.yml文件，加入如下内容
```
markdown: kramdown
kramdown:
  math_engine: katex
```

#### 在根目录下创建_includes/header.html文件,并在文件中加入如下代码
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
	
	
    	<script src="//cdnjs.cloudflare.com/ajax/libs/mermaid/8.6.0/mermaid.min.js"></script>
	<script>
		var config = {
		  startOnLoad: true,
		  theme: "forest",
		  flowchart:{
		    useMaxWidth: true,
		    htmlLabels: true
		  }
		};
		mermaid.initialize(config);
		window.mermaid.init(undefined, document.querySelectorAll('.language-mermaid'));
	</script>
</head>
```
#### 在根目录下创建_layouts/default.html文件，并在文件中加入如下代码
```
<!DOCTYPE html>
<html lang="en">
\{\% include header.html \%\}

<style>
.center {
  margin: auto;
  width: 50%;
  border: 1px solid #F5F5F5;
  padding: 10px;
}
</style>
</head>

<body>	
<div class="center">
    \{\{ content \}\}	

</div>
</body>

<script>
var config = {
    startOnLoad:true,
    flowchart:{
            useMaxWidth:true,
            htmlLabels:true
        }
};
mermaid.initialize(config);
window.mermaid.init(undefined, document.querySelectorAll('.language-mermaid'));
</script>

</html>
```

#### 编辑markdown文档，就可以使用mermaid语法画图，使用latex语法写数学公式

### 遗留问题
+ 启用_layouts/default.html模板文件后，丢失了原来自带的样式，得自己写css控制样式，我又不会前端，所以你们看到的这个文章很难看。

### 下面是在学习这个知识中参考过的一些网页

+ http://leohope.com/%E8%A7%A3%E9%97%AE%E9%A2%98/2017/09/08/page-with-latex/

+ https://lloyar.github.io/2018/10/08/mathjax-in-jekyll.html

+ 在GitHub上创建和托管个人网站(下)：https://blog.csdn.net/qq_26927285/article/details/78762237


+ jekyll的目录结构：https://jekyllrb.com/docs/structure/


+ jekyll文档:
http://jekyllcn.com/docs/templates/
