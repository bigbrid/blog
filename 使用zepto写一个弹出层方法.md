## 使用zepto写一个弹出层方法

```
var $pop;
function showPop(e){
    if ($pop) {
        closePop()
    };
    $pop = $(e);
    $pop.fadeIn()
    $("body").append("<div class='mask' style='position: fixed;width: 100%;height: 100%;background-color:rgba(0,0,0,0.8);top: 0;left: 0;'></div>")
}
function closePop(){
    $pop.hide()
    $(".mask").remove()
}
```

