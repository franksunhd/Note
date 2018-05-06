## 富文本编辑器

[TOC]

```html
<!DOCTYPE html>
<html>
<head>
    <title>完整demo</title>
    <meta http-equiv="Content-Type" content="text/html;charset=utf-8"/>
    <script type="text/javascript" charset="utf-8" src="ueditor.config.js"></script>
    <script type="text/javascript" charset="utf-8" src="ueditor.all.min.js"> </script>
    <!--建议手动加在语言，避免在ie下有时因为加载语言失败导致编辑器加载失败-->
    <!--这里加载的语言文件会覆盖你在配置项目里添加的语言类型，比如你在配置项目里配置的是英文，这里加载的中文，那最后就是中文-->
    <script type="text/javascript" charset="utf-8" src="lang/zh-cn/zh-cn.js"></script>

    <style type="text/css">
        div{
            width:100%;
        }
    </style>
</head>
<body>
<div>
    <h1>完整demo</h1>
    <script id="editor" type="text/plain" style="width:1024px;height:500px;"></script>
</div>
<div id="btns">
    <div>
        <button onclick="getAllHtml()">获得整个html的内容</button>
        <button onclick="getContent()">获得内容</button>
        <button onclick="setContent()">写入内容</button>
        <button onclick="setContent(true)">追加内容</button>
        <button onclick="getContentTxt()">获得纯文本</button>
        <button onclick="getPlainTxt()">获得带格式的纯文本</button>
        <button onclick="hasContent()">判断是否有内容</button>
        <button onclick="setFocus()">使编辑器获得焦点</button>
        <button onmousedown="isFocus(event)">编辑器是否获得焦点</button>
        <button onmousedown="setblur(event)" >编辑器失去焦点</button>

    </div>
    <div>
        <button onclick="getText()">获得当前选中的文本</button>
        <button onclick="insertHtml()">插入给定的内容</button>
        <button id="enable" onclick="setEnabled()">可以编辑</button>
        <button onclick="setDisabled()">不可编辑</button>
        <button onclick=" UE.getEditor('editor').setHide()">隐藏编辑器</button>
        <button onclick=" UE.getEditor('editor').setShow()">显示编辑器</button>
        <button onclick=" UE.getEditor('editor').setHeight(300)">设置高度为300默认关闭了自动长高</button>
    </div>

    <div>
        <button onclick="getLocalData()" >获取草稿箱内容</button>
        <button onclick="clearLocalData()" >清空草稿箱</button>
    </div>

</div>
<div>
    <button onclick="createEditor()">
    创建编辑器</button>
    <button onclick="deleteEditor()">
    删除编辑器</button>
</div>

<script type="text/javascript">

    //实例化编辑器
    //建议使用工厂方法getEditor创建和引用编辑器实例，如果在某个闭包下引用该编辑器，直接调用UE.getEditor('editor')就能拿到相关的实例
    var ue = UE.getEditor('editor');



// 这些是对编辑框的操作和将修改完的内容获取到而后进行各种操作
    function isFocus(e){
        alert(UE.getEditor('editor').isFocus());
        UE.dom.domUtils.preventDefault(e)
    }
    function setblur(e){
        UE.getEditor('editor').blur();
        UE.dom.domUtils.preventDefault(e)
    }
    function insertHtml() {
        var value = prompt('插入html代码', '');
        UE.getEditor('editor').execCommand('insertHtml', value)
    }
    function createEditor() {
        enableBtn();
        UE.getEditor('editor');
    }
    function getAllHtml() {
        alert(UE.getEditor('editor').getAllHtml())
    }
    function getContent() {
        var arr = [];
        arr.push("使用editor.getContent()方法可以获得编辑器的内容");
        arr.push("内容为：");
        arr.push(UE.getEditor('editor').getContent());
        alert(arr.join("\n"));
    }
    function getPlainTxt() {
        var arr = [];
        arr.push("使用editor.getPlainTxt()方法可以获得编辑器的带格式的纯文本内容");
        arr.push("内容为：");
        arr.push(UE.getEditor('editor').getPlainTxt());
        alert(arr.join('\n'))
    }
    function setContent(isAppendTo) {
        var arr = [];
        arr.push("使用editor.setContent('欢迎使用ueditor')方法可以设置编辑器的内容");
        UE.getEditor('editor').setContent('欢迎使用ueditor', isAppendTo);
        alert(arr.join("\n"));
    }
    function setDisabled() {
        UE.getEditor('editor').setDisabled('fullscreen');
        disableBtn("enable");
    }

    function setEnabled() {
        UE.getEditor('editor').setEnabled();
        enableBtn();
    }

    function getText() {
        //当你点击按钮时编辑区域已经失去了焦点，如果直接用getText将不会得到内容，所以要在选回来，然后取得内容
        var range = UE.getEditor('editor').selection.getRange();
        range.select();
        var txt = UE.getEditor('editor').selection.getText();
        alert(txt)
    }

    function getContentTxt() {
        var arr = [];
        arr.push("使用editor.getContentTxt()方法可以获得编辑器的纯文本内容");
        arr.push("编辑器的纯文本内容为：");
        arr.push(UE.getEditor('editor').getContentTxt());
        alert(arr.join("\n"));
    }
    function hasContent() {
        var arr = [];
        arr.push("使用editor.hasContents()方法判断编辑器里是否有内容");
        arr.push("判断结果为：");
        arr.push(UE.getEditor('editor').hasContents());
        alert(arr.join("\n"));
    }
    function setFocus() {
        UE.getEditor('editor').focus();
    }
    function deleteEditor() {
        disableBtn();
        UE.getEditor('editor').destroy();
    }
    function disableBtn(str) {
        var div = document.getElementById('btns');
        var btns = UE.dom.domUtils.getElementsByTagName(div, "button");
        for (var i = 0, btn; btn = btns[i++];) {
            if (btn.id == str) {
                UE.dom.domUtils.removeAttributes(btn, ["disabled"]);
            } else {
                btn.setAttribute("disabled", "true");
            }
        }
    }
    function enableBtn() {
        var div = document.getElementById('btns');
        var btns = UE.dom.domUtils.getElementsByTagName(div, "button");
        for (var i = 0, btn; btn = btns[i++];) {
            UE.dom.domUtils.removeAttributes(btn, ["disabled"]);
        }
    }

    function getLocalData () {
        alert(UE.getEditor('editor').execCommand( "getlocaldata" ));
    }

    function clearLocalData () {
        UE.getEditor('editor').execCommand( "clearlocaldata" );
        alert("已清空草稿箱")
    }
</script>
</body>
</html>
```

### 1.原理

```html
1.定义   富文本编辑器，Rich Text Editor, 简称 RTE, 是一种可内嵌于浏览器，所见即所得的文本编辑器。
2.对于支持富文本编辑的浏览器来说，事实上就是设置 document 的 designMode 属性为 on 后，再通过运行 document.execCommand('commandName'[, UIFlag[, value]]) 就可以。commandName 和 value 能够在MSDN 上和MDC 上找到，它们就是我们创建各种格式的命令，例如说，我们要加粗字体，运行 document.execCommand('bold', false) 就可以。可是值得注意的是，一般是选中了文本后才运行命令，被选中的文本才被格式化。对于未选中的文本进行这个命令，各浏览器有不同的处理方式，例如 IE 可能是对位于光标中的标签内容进行格式化，而其他浏览器不做不论什么处理，。同一时候须要注意的是，UIFlag 这个參数设置为 true 表示 display any user interface triggered by the command (if any)
    注释1.designMode属性用来指定整个页面是否可编辑，当页面可编辑时，页面中任何支持上文所述的contentEditable属性的元素都变成了可编
辑状态。designMode属性只能在JavaScript脚本里被编辑修改。该属性有两个值—“on”与“off”。属性被指定为“on”时，页面可
编辑；被指定为“off”时，页面不可编辑。使用JavaScript脚本来指定designMode属性的方法如下所示：
document.designMode="on"
针对designMode属性，各浏览器的支持情况也各不相同：
IE8：出于安全考虑，不允许使用designMode属性让页面进入编辑状态。
IE9：允许使用designMode属性让页面进入编辑状态。
Chrome 3和Safari：使用内嵌frame的方式,该内嵌frame是可编辑的。
Firefox和Opera：允许使用designMode属性让页面进入编辑状态。
注释2:execCommand方法是执行一个对当前文档，当前选择或者给出范围的命令。 
document.execCommand()方法处理Html数据时常用语法格式如下: 复制内容到剪贴板 
代码: 
document.execCommand(sCommand[,交互方式, 动态参数]) 其中：sCommand为指令参数（如下例中的"2D-Position"），交互方式参数如果是true的话将显示对话框，如果为false的话，则不显示对话框（下例中的"false"即表示不显示对话框），动态参数一般为一可用值或属性值
```

### 2.使用

```
1.引入三个js 
2.实例化编辑器 
UEDITOR_CONFIG.UEDITOR_HOME_URL = ‘/pugilist_system/ueditor/’; 这个是重点，可以配置在所有的实例化编辑器前面，配置在ueditor.config.js中，指明了编辑器的具体位置
3.修改配置文件
4.补充一，修改配置文件ueditor.config.js，配置Ueditor路径
window.UEDITOR_HOME_URL = "/Ueditor/";//"相对于网站根目录的相对路径"也就是以斜杠开头的形如"/myProject/ueditor/"这样的路径。
  var URL = window.UEDITOR_HOME_URL || getUEBasePath();//获取Ueditor的路径
 , imagePath: URL + "../"                   
 //图片修正地址，引用了fixedImagePath,如有特殊需求，可自行配置
```

### 3.使用百度富文本编辑器UEditor碰到的问题

```html
问题1：配置问题。

原因：下面的配置的顺序不能错，顺序错了可能会导致加载不出来的情况。

<!-- 配置文件 -->
<script type="text/javascript" src="/common/ueditor/ueditor.config.js"></script>
<!-- 编辑器源码文件 -->
<script type="text/javascript" src="/common/ueditor/ueditor.all.js"></script>
下面是我的配置

复制代码
<!-- 实例化编辑器 -->
<script type="text/javascript">
    UEDITOR_CONFIG.UEDITOR_HOME_URL = '/common/ueditor/'; //一定要用这句话，否则你需要去ueditor.config.js修改路径的配置信息
    var ue = UE.getEditor('container',{
        toolbars: [
            ['fullscreen', 'source', 'undo', 'redo', '|', 'fontsize', '|', 'blockquote', 'horizontal', '|', 'removeformat', 'formatmatch', 'link', 'unlink', '}', 'simpleupload', 'insertimage', 'preview'],
            ['bold', 'italic', 'underline', 'forecolor', 'backcolor', '|', 'indent', '|', 'justifyleft', 'justifycenter', 'justifyright', 'justifyjustify', '|',
                'rowspacingtop', 'rowspacingbottom', 'lineheight', '|', 'insertorderedlist', 'insertunorderedlist', '|', 'imagenone', 'imageleft', 'imageright', 'imagecenter']
        ]
        ,autoHeightEnabled: false
        ,autoFloatEnabled: true
        ,initialFrameWidth : 1000//编辑器宽度，默认1000
        ,initialFrameHeight : 500//编辑器高度，默认320
        ,maximumWords : 1000//最大字符数
    });
</script>
复制代码
 

问题2：上传图片功能加载失败

　　我使用的是springmvc idea

总的原因：编辑器初始化的时候会发送一个请求，去请求ueditor/jsp/controller.jsp文件，但是它报了500错误，不能正确的返回json配置。

原因1：jar包没有导入到项目中。

解决：在ueditor/jsp/lib下面有几个jar文件，需要把这几个jar文件导入到项目中，最好是直接复制到WEB-INF/lib下面，不然可能也会出现问题。　

问题又来了，我使用的是maven管理项目的，这个ueditor-1.1.2.jar在中央仓库里面没有，需要自己手动添加到本地仓库中

ueditor/jsp/lib目录下打开命令窗口，运行下面代码

mvn install:install-file -Dfile=ueditor-1.1.2.jar -Dpackaging=jar -DgroupId=com.baidu.ueditor -DartifactId=ueditor -Dversion=1.1.2
```

### 4. 命令集

```html
document.execCommand()方法可用来执行很多我们无法实现的操作. 

execCommand方法是执行一个对当前文档，当前选择或者给出范围的命令。 

document.execCommand()方法处理Html数据时常用语法格式如下: 复制内容到剪贴板 
代码: 
document.execCommand(sCommand[,交互方式, 动态参数]) 其中：sCommand为指令参数（如下例中的"2D-Position"），交互方式参数如果是true的话将显示对话框，如果为false的话，则不显示对话框（下例中的"false"即表示不显示对话框），动态参数一般为一可用值或属性值（如下例中的"true"）。 

document.execCommand("2D-Position","false","true"); 


调用execCommand()可以实现浏览器菜单的很多功能. 如保存文件,打开新文件,撤消、重做操作...等等. 有了这个方法,就可以很容易的实现网页中的文本编辑器. 

如果灵活运用,可以很好的辅助我们完成各种项目. 

使用的例子如下: 


1、〖全选〗命令的实现 
[格式]:document.execCommand("selectAll") 
[说明]将选种网页中的全部内容！ 
[举例]在<body></body>之间加入： 
<a href="#" onclick=document.execCommand("selectAll")>全选</a> 

2、〖打开〗命令的实现 
[格式]:document.execCommand("open") 
[说明]这跟VB等编程设计中的webbrowser控件中的命令有些相似，大家也可依此琢磨琢磨。 
[举例]在<body></body>之间加入： 
<a href="#" onclick=document.execCommand("open")>打开</a> 

3、〖另存为〗命令的实现 
[格式]:document.execCommand("saveAs") 
[说明]将该网页保存到本地盘的其它目录！ 
[举例]在<body></body>之间加入： 
<a href="#" onclick=document.execCommand("saveAs")>另存为</a> 

4、〖打印〗命令的实现 
[格式]:document.execCommand("print") 
[说明]当然，你必须装了打印机！ 
[举例]在<body></body>之间加入： 
<a href="#" onclick=document.execCommand("print")>打印</a> 

Js代码 下面列出的是指令参数及意义 

//相当于单击文件中的打开按钮   
document.execCommand("Open");   
  
//将当前页面另存为   
document.execCommand("SaveAs");   
  
//剪贴选中的文字到剪贴板;   
document.execCommand("Cut","false",null);   
  
//删除选中的文字;   
document.execCommand("Delete","false",null);    
  
//改变选中区域的字体;   
document.execCommand("FontName","false",sFontName);    
  
//改变选中区域的字体大小;   
document.execCommand("FontSize","false",sSize|iSize);    
  
//设置前景颜色;   
document.execCommand("ForeColor","false",sColor);   
  
//使绝对定位的对象可直接拖动;    
document.execCommand("2D-Position","false","true");   
  
//使对象定位变成绝对定位;    
document.execCommand("AbsolutePosition","false","true");   
  
//设置背景颜色;   
document.execCommand("BackColor","false",sColor);   
  
//使选中区域的文字加粗;   
document.execCommand("Bold","false",null);   
  
//复制选中的文字到剪贴板;   
document.execCommand("Copy","false",null);   
  
//设置指定锚点为书签;   
document.execCommand("CreateBookmark","false",sAnchorName);   
  
//将选中文本变成超连接,若第二个参数为true,会出现参数设置对话框;   
document.execCommand("CreateLink","false",sLinkURL);   
  
//设置当前块的标签名;   
document.execCommand("FormatBlock","false",sTagName);  

//相当于单击文件中的打开按钮 
document.execCommand("Open"); 

//将当前页面另存为 
document.execCommand("SaveAs"); 

//剪贴选中的文字到剪贴板; 
document.execCommand("Cut","false",null); 

//删除选中的文字; 
document.execCommand("Delete","false",null); 

//改变选中区域的字体; 
document.execCommand("FontName","false",sFontName); 

//改变选中区域的字体大小; 
document.execCommand("FontSize","false",sSize|iSize); 

//设置前景颜色; 
document.execCommand("ForeColor","false",sColor); 

//使绝对定位的对象可直接拖动; 
document.execCommand("2D-Position","false","true"); 

//使对象定位变成绝对定位; 
document.execCommand("AbsolutePosition","false","true"); 

//设置背景颜色; 
document.execCommand("BackColor","false",sColor); 

//使选中区域的文字加粗; 
document.execCommand("Bold","false",null); 

//复制选中的文字到剪贴板; 
document.execCommand("Copy","false",null); 

//设置指定锚点为书签; 
document.execCommand("CreateBookmark","false",sAnchorName); 

//将选中文本变成超连接,若第二个参数为true,会出现参数设置对话框; 
document.execCommand("CreateLink","false",sLinkURL); 

//设置当前块的标签名; 
document.execCommand("FormatBlock","false",sTagName); 


另外:document.execCommand()还有很多的其它属性.以下是我搜集整理的.可能还漏了很多,希望大家多多补充! 

2D-Position 允许通过拖曳移动绝对定位的对象。 

AbsolutePosition 设定元素的 position 属性为“absolute”(绝对)。 

BackColor 设置或获取当前选中区的背景颜色。 

Bold 切换当前选中区的粗体显示与否。 

Copy 将当前选中区复制到剪贴板。 

CreateBookmark 创建一个书签锚或获取当前选中区或插入点的书签锚的名称。 

CreateLink 在当前选中区上插入超级链接，或显示一个对话框允许用户指定要为当前选中区插入的超级链接的 URL。 

Cut 将当前选中区复制到剪贴板并删除之。 

Delete 删除当前选中区。 

FontName 设置或获取当前选中区的字体。 

FontSize 设置或获取当前选中区的字体大小。 

ForeColor 设置或获取当前选中区的前景(文本)颜色。 

FormatBlock 设置当前块格式化标签。 

Indent 增加选中文本的缩进。 

InsertButton 用按钮控件覆盖当前选中区。 

InsertFieldset 用方框覆盖当前选中区。 

InsertHorizontalRule 用水平线覆盖当前选中区。 

InsertIFrame 用内嵌框架覆盖当前选中区。 

InsertImage 用图像覆盖当前选中区。 

InsertInputButton 用按钮控件覆盖当前选中区。 

InsertInputCheckbox 用复选框控件覆盖当前选中区。 

InsertInputFileUpload 用文件上载控件覆盖当前选中区。 

InsertInputHidden 插入隐藏控件覆盖当前选中区。 

InsertInputImage 用图像控件覆盖当前选中区。 

InsertInputPassword 用密码控件覆盖当前选中区。 

InsertInputRadio 用单选钮控件覆盖当前选中区。 

InsertInputReset 用重置控件覆盖当前选中区。 

InsertInputSubmit 用提交控件覆盖当前选中区。 

InsertInputText 用文本控件覆盖当前选中区。 

InsertMarquee 用空字幕覆盖当前选中区。 

InsertOrderedList 切换当前选中区是编号列表还是常规格式化块。 

InsertParagraph 用换行覆盖当前选中区。 

InsertSelectDropdown 用下拉框控件覆盖当前选中区。 

InsertSelectListbox 用列表框控件覆盖当前选中区。 

InsertTextArea 用多行文本输入控件覆盖当前选中区。 

InsertUnorderedList 切换当前选中区是项目符号列表还是常规格式化块。 

Italic 切换当前选中区斜体显示与否。 

JustifyCenter 将当前选中区在所在格式化块置中。 

JustifyLeft 将当前选中区所在格式化块左对齐。 

JustifyRight 将当前选中区所在格式化块右对齐。 

LiveResize 迫使 MSHTML 编辑器在缩放或移动过程中持续更新元素外观，而不是只在移动或缩放完成后更新。 

MultipleSelection 允许当用户按住 Shift 或 Ctrl 键时一次选中多于一个站点可选元素。 

Open 打开一个文档。 

Outdent 减少选中区所在格式化块的缩进。 

OverWrite 切换文本状态的插入和覆盖。 

Paste 用剪贴板内容覆盖当前选中区。 

Print 打开打印对话框以便用户可以打印当前页。 

Redo 撤消操作,相当于Ctrl+Z。 

Undo 重做。 

Refresh 刷新当前文档。 

RemoveFormat 从当前选中区中删除格式化标签。 

RemoveParaFormat 目前尚未支持。 

SaveAs 将当前 Web 页面保存为文件。 

SelectAll 选中整个文档。 

UnBookmark 从当前选中区中删除全部书签。 

Underline 切换当前选中区的下划线显示与否。 

Unlink 从当前选中区中删除全部超级链接。 

Unselect 清除当前选中区的选中状态。 


------------------------------------------------------------------------------------ 
Javascript的世界真是奇妙. 有时,只是一次不经意的google,都会发现一些以前没见过,或忽略的语法. 当用起来的时候,才发现它的威力. 不知还有多少正隐藏在暗处的方法,等着你我去发现? 
------------------------------------------------------------------------------------ 
(部分内容来源于百度搜索)  


document.execCommand()函数可用参数解析 

<html> 
<head> 
<title>javascript--execcommand指令集</title> 
<script type="text/javascript"> 

<!-- 
/* 
*该function执行copy指令 
*/ 
function fn_doufucopy(){ 
edit.select(); 
document.execCommand('Copy'); 
} 

/* 
*该function执行paste指令 
*/ 

function fn_doufupaste() { 
tt.focus(); 
document.execCommand('paste'); 
} 

/* 
*该function用来创建一个超链接 
*/ 

function fn_creatlink() 
{ 
document.execCommand('CreateLink',true,'true');//弹出一个对话框输入URL 
//document.execCommand('CreateLink',false,'http://bbs.tc800.com'); 
} 
/* 
*该function用来将选中的区块设为指定的背景色 
*/ 

function fn_change_backcolor() 
{ 
document.execCommand('BackColor',true,'#FFbbDD');//true或false都可以 
} 

/* 
*该function用来将选中的区块设为指定的前景色,改变选中区块的字体大小,改变字体,字体变粗变斜 
*/ 

function fn_change_forecolor() 
{ 
//指定前景色 
document.execCommand('ForeColor',false,'#BBDDCC');//true或false都可以 

//指定背景色 
document.execCommand('FontSize',false,7);   //true或false都可以 

//字体必须是系统支持的字体 
document.execCommand('FontName',false,'标楷体');   //true或false都可以 

//字体变粗 
document.execCommand('Bold'); 

//变斜体 
document.execCommand('Italic'); 
} 

/* 
*该function用来将选中的区块加上不同的线条 
*/ 

function fn_change_selection() 
{ 
//将选中的文字加下划线 
document.execCommand('Underline'); 

//在选中的文字上划粗线 
document.execCommand('StrikeThrough'); 

//将选中的部分文字变细 
document.execCommand('SuperScript'); 

//将选中区块的下划线取消掉 
document.execCommand('Underline'); 
} 

/* 
*该function用来将选中的区块排成不同的格式 
*/ 

function fn_format() 
{ 
//有序列排列 
document.execCommand('InsertOrderedList'); 
//实心无序列排列 
document.execCommand('InsertUnorderedList'); 
//空心无序列排列 
document.execCommand('Indent'); 
} 

/* 
*该function用来将选中的区块剪下或是删除掉 
*/ 

function fn_CutOrDel() 
{ 
//删除选中的区块 
//document.execCommand('Delete'); 
//剪下选中的区块 
document.execCommand('Cut'); 
} 

/* 
*该function用来将选中的区块重设为一个相应的物件 
*/ 

document.execCommand()的应用实例 
document.execCommand()的应用实例 



<input type="button" value="剪切" onclick="document.execCommand('Cut')"> 
<input type="button" value="拷贝" onclick="document.execCommand('Copy')"> 
<input type="button" value="粘贴" onclick="document.execCommand('Paste')"> 
<input type="button" value="撤消" onclick="document.execCommand('Undo')"> 
<input type="button" value="重做" onclick="document.execCommand('Redo')" id="button2" name="button2"> 
<input> 
<input type="button" value="删除" onclick="document.execCommand('Delete')"> 
<input type="button" value="黑体" onclick="document.execCommand('Bold')"> 
<input type="button" value="斜体" onclick="document.execCommand('Italic')"> 
<input type="button" value="下划线" onclick="document.execCommand('Underline')"> 
<input type="button" value="停止" onclick="document.execCommand('stop')"> 
<input type="button" value="保存" onclick="document.execCommand('SaveAs')"> 
<input type="button" value="另存为" onclick="document.execCommand('Saveas',false,'c:\\test.htm')"> 
<input type="button" value="字体" onclick="document.execCommand('FontName',false,fn)"> 
<input type="button" value="字体大小" onclick="document.execCommand('FontSize',false,fs)"> 
<input type="button" value="刷新" onclick="document.execCommand('refresh',false,0)"> 
```

