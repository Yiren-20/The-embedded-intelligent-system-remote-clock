-   核心代码位于clock_main.c和button_control.c中

- 外部BUILD.gn文件编写方式如下：

```c
import("//build/lite/config/component/lite_component.gni")
lite_component("app") {
    features = [ "smartClock:SmartClock", ]
}
```
