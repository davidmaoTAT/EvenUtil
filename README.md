# EvenUtil
跨浏览器的事件处理程序
```JAVA
var EvenUtil = {
        addHandler :function(element, type, handler){
            if(element.addEventListener){
                element.addEventListener(type, handler,false);
            } else if(element.attachEven){
                element.attachEven("on" + type,handler);
            }else{
                element["on" + type] = handler;
            }
        },
        removeHandler: function(element,type,handler){
            if(element.addEventListener){
                element.addEventListener(type, handler,false);
            } else if(element.attachEven){
                element.attachEven("on" + type,handler);
            }else{
                element["on" + type] = handler;
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
