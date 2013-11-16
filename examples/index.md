# 演示文档

---

<div id="targetBox" style="position:absolute;width:200px;height:30px;border:1px solid red;display:none;">hello world</div>

````html
 <p><a id="trigger1" href="javascript:;" rel="targetBox" style="position:relative;">默认rel加载</a></p>

````
````javascript
seajs.use('iPopup.css');
seajs.use('iPopup', function(){
    var $ = jQuery;
    console.log($("#trigger1"))
    console.log($.fn)
    //通过默认rel属性加载
   $("#trigger1").powerFloat({offsets:{x:0, y:10},eventType:'click'});
   $("#trigger10").powerFloat({
    targetMode: "list"  
});
$(".pwdTrigger").powerFloat({
    eventType: "focus",
    targetMode: "remind",
    targetAttr: "placeholder",
    position: "1-4"
});


var fnPosTri = function() {
    var oPosTri = $("#posTrigger1"), vPosTri = $.trim(oPosTri.val());
    if (vPosTri === "") {
        oPosTri.powerFloat({
            eventType: null,
            targetMode: "remind",
            target: "输入内容不能为空！",
            position: "1-4"
        }).focus();
    } else if (/\W/g.test(vPosTri)) {
        oPosTri.powerFloat({
            eventType: null,
            targetMode: "remind",
            target: "只能输入英文字符、数字和下划线",
            position: "1-4"
        }).focus(); 
    } else {
        $.powerFloat.hide();
    }
};
$("#trigger11").bind("click", fnPosTri);
$("#posTrigger1").bind("blur", fnPosTri);

$(".operateTrigger").click(function() {
    var txt = $(this).text();
    //IE6位置
    if (!window.XMLHttpRequest) {
        $("#targetFixed").css("top", $(document).scrollTop() + 2);  
    }
    //创建半透明遮罩层
    if (!$("#overLay").size()) {
        $('<div id="overLay"></div>').prependTo($("body"));
        $("#overLay").css({
            width: "100%",
            backgroundColor: "#000",
            opacity: 0.2,
            position: "absolute",
            left: 0,
            top: 0,
            zIndex: 99
        }).height($(document).height());
    }
    //显示操作提示，最关键核心代码
    $("#targetFixed").powerFloat({
        eventType: null,
        targetMode: "doing",    
        target: "正在" + txt + "中...",
        position: "1-2"
    });
    //定时关闭，测试用
    setTimeout(function() {
        $("#overLay").remove();
        $.powerFloat.hide();
    }, 2000);
});

$("#trigger13").powerFloat({
    eventType: "click",
    targetMode: null,
    targetAttr: "src",
    
    container: $("#customContainer")
});


$("#trigger14").powerFloat({
    targetMode: "ajax",
    targetAttr: "href",
    hoverFollow: "y",
    position: "6-8"
});



});



````

## 无列表数据
````html
 <a id="trigger10" href="#">无列表数据显示</a>
````

## 简单提示

````html
输入密码：<input class="pwdTrigger" type="password" placeholder="6~20个字符" />
再次输入：<input class="pwdTrigger" type="password" placeholder="输入与上面一样的密码" />
````

---

点击确定按钮或失去焦点后显示提示(文本框数据留空/输入奇怪字符等)：
````html
<input id="posTrigger1" type="text" /> <button id="trigger11">确定</button>
````

---

右上角固定位置的操作提示层(ajax请求中提示，页面跳转中提示等)：

<style>
    .target_fixed { height:25px; padding:1px; position:fixed; _position:absolute; top:0; right:0; }
</style>

````html
<span id="targetFixed" class="target_fixed"></span>
<button class="operateTrigger">登录</button>
<button class="operateTrigger">提交</button>
<button class="operateTrigger">刷新</button>
````


## 自定义装载容器
<style>
    .dib { display: inline-block; }
</style>

````html
<input id="trigger13" type="button" src="targetBox" value="点击我" />
````


````html
<a class="dib" id="trigger14" href="http://image.zhangxinxu.com/image/study/s/s256/mm1.jpg">
    <img src="http://image.zhangxinxu.com/image/study/s/s128/mm1.jpg" />
</a>
````