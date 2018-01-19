## HTML5 新标签

[TOC]

### 1.mark  - - 标记(行元素)

```html
H5新的标签<mark>标记</mark>
<!--
      mark 标记 背景黄色
      定义带有记号的文本。
      <行元素>
    -->
```

### 2.time - - 时间标签,没有任何样式,只有语义化(行元素)

```html
<time>2月10号</time>就可以放假了
```

### 3.nav - - 导航,没有任何样式.(块元素)

```html
<nav>导航栏</nav>
```

### 4.section - - 区段 (块元素)

```html
<section>第一个区段</section>
<section>第二个区段</section>
```

### 5.article - -文章段落 (块元素)

```html
<article>我是一段文章</article>
```

### 6.aside - - 侧边栏(块元素)

```html
<aside>定义侧边栏</aside>
```

### 7.ruby - - 定义 ruby注释 (行元素)

```html
<ruby>
  汉<rp>(</rp><rt>Han</rt><rp>)</rp>
  字<rp>(</rp><rt>Zi</rt><rp>)</rp>
</ruby>

<!-- 支持它的浏览器中注释在汉字上方,在 IE6,7中显示为 汉(Han)字(Zi) -->
```

### 8.wbr - - 单词换行

```html
hello Henry,<wbr>welcome to beijing.
<!--避免那种英文单词过长,在换行时造成的单词差分,加入<wbr>会使得长度较长的单词全部切换到下一行-->
```

### 9.fieldset - - 将表单内的元素进行分组(块元素)

```html
<fieldset></fieldset>
```

### 10.legend - - 给 fieldset设置标题

```html
<fieldset>
  <legend>fieldset标题</legend>
</fieldset>
```

### 11.meter - - 条状度量衡 (行元素)

```html
<meter low="20" high="80" value="90" min="0" max="100">
  您的浏览器不支持,请更新浏览器!
</meter>
```

### 12.progress - - 进度条 (行元素)

```html
<progress value="50" max="100">
  您的浏览器不支持,请更新您的浏览器
</progress>
```

### 13.details - - 下拉列表 (块元素)

### 14.summary - - 为details设置标题

```html
<details>
  <summary>点击选择</summary>
  <p>1.抽烟</p>  
  <p>2.喝酒</p>
  <div>3.烫头</div>
</details>
```

### 15.figure - - 独立的流内容(块元素)

```html
<figure>
  <img width="300" src="./img/1.png" alt="无法显示图片" />
  <figcaption>这是一张图片</figcaption>
</figure>
```

### 16.datalist - - 为 input 设置可能的选项列表

```html
<!-- 
	支持性较差 建议少用
	input 设置 list 属性 属性值为 datalist 的 id 属性值
-->
<input list="emails" name="email" />
<datalist id="emails">
  <option value="111"></option>  
  <option value="222"></option>
  <option value="333"></option>
</datalist>
```

### 17.audio - - 音频文件 (块元素)

```html
<audio src="./video/1.mp3" controls loop autoplay muted preload="auto">
  浏览器不支持,请升级浏览器或更换浏览器
</audio>
<!-- 
	controls:控制面板
	loop: 控制是否循环,属性默认循环
	autoplay:自动播放
	muted:设置静音
	proload="auto":当网页加载时,音频是否默认被加载,以及如何被加载
-->

<!--
	兼容性写法:
	使用<source>元素 src 引入资源
-->
```

### 18.viedo - - 视频文件 (块元素)

```html
<!--
	使用基本与音频文件用法类似
	只是视频文件多了属性: width 和 height
	poster:指定封面上的显示图片
	兼容写法与音频文件类似
-->

<video>
  您的浏览器不支持,请升级您的浏览器或者更换您的浏览器
</video>
```























