# EvenUtil
跨浏览器的事件处理程序
```javascript
var EvenUtil = {
        \\监听事件后的操作
        addHandler :function(element, type, handler){
            if(element.addEventListener){
                element.addEventListener(type, handler,false);
            } else if(element.attachEven){
                element.attachEven("on" + type,handler);
            }else{
                element["on" + type] = handler;
            }
        },

        \\获取事件
        getEvent: function(event){
            return event ? event : window.event;
        },

        \\获取目标
        getTarget: function(event){
            return event.target || event.srcElement;
        },

        \\阻止默认功能
        preventDefault: function(event){
            if(event.preventDefault){
                event.preventDefault();
            }else{
                event.returnValue = false;
            }
        },
        
        \\获取编码值
        getCharCode: function(event){
            if(typeof event.charCode == "number"){
                return event.charCode;
            }else{
                return event.keyCode;
            }
        },

        \\取消事件的操作
        removeHandler: function(element,type,handler){
            if(element.addEventListener){
                element.addEventListener(type, handler,false);
            } else if(element.attachEven){
                element.attachEven("on" + type,handler);
            }else{
                element["on" + type] = handler;
            }
        },
        
        \\取消事件的默认功能
        stopPropagation: function(event){
            if(event.stopPropagation){
                event.stopPropagation;
            }else{
                event.cancelBubble = true;
            }
        }
    };
    var btn = document.getElementById("mybtn");
    var fuc = function(){
          alert(this.id + "hello");
    }
    EvenUtil.addHandler(btn,"click",fuc);
    EvenUtil.removeHandler(btn,"click",fuc);
```


事件对象
```JavaScript
    var btn = document.getElementById("mybtn");
    var handler = function(event){
        switch(event.type){
            case "click" :
                alert("clicked");
                break;
            case "mouseover":
                event.target.style.backgroundColor = "red";
                break;
            case "mouseout":
                event.target.style.backgroundColor = "";
                break;
        }
    };
    btn.onclick = handler;
    btn.onmouseover = handler;
    btn.onmouseout = handler;
 ```
表单操作
```javascript
  var form = document.getElementById("myForm");
    EvenUtil.addHandler(form,"sumbit",function(event){
        event = EvenUtil.getEvent(event);//取得事件对象
        EvenUtil.preventDefault(event); //阻止默认事件
    });

    //避免多次提交表单
    EvenUtil.addHandler(form,"sumbit",function(event){
        event = EvenUtil.getEvent(event);
        var target = EvenUtil.getTarget(event);
    //取得提交按钮
        var btn = target.element["myForm"];
    //禁用
        btn.disabled = true;
    })
```

共有的表单字段事件
```javascript
 var textbox = document.forms[0].elements[0];
    EvenUtil.addHandler(textbox,"focus",function(event){
        event = EvenUtil.getEvent(event);
        var target = EvenUtil.getTarget(event);

        if(target.style.backgroundColor != "red"){
            target.style.backgroundColor = "yellow";
        }
    });

    EvenUtil.addHandler(textbox,"blur",function(event){
        event = EvenUtil.getEvent(event);
        var target = EvenUtil.getTarget(event);

        if(/[^\d]/.test(target.value)){
            target.style.backgroundColor = "red";
        }else{
            target.style.backgroundColor = "";
        }
    });

    EvenUtil.addHandler(textbox,"change",function(event){
        event = EvenUtil.getEvent(event);
        var target = EvenUtil.getTarget(event);

        if(/[^\d]/.test(target.value)){
            target.style.backgroundColor = "red";
        }else{
            target.style.backgroundColor = "";
        }
    });
```
