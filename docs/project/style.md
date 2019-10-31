
在React Native中，你并不需要学习什么特殊的语法来定义样式。我们仍然是使用JavaScript来写样式。所有的核心组件都接受名为style的属性。这些样式名基本上是遵循了web上的CSS的命名，只是按照JS的语法要求使用了驼峰命名法，例如将`background-color`改为`backgroundColor`。

`style`属性可以是一个普通的JavaScript对象。这是最简单的用法，因而在示例代码中很常见。你还可以传入一个数组——在数组中位置居后的样式对象比居前的优先级更高，这样你可以间接实现样式的继承。


-----


##### 样式应用

外联布局：`style={styles.container}`

内联布局：`style={{flex:1,flexDirection: 'column'}}`

多个布局：`style={[styles.container,{width:50,height:100}]}`

------

##### 界面尺寸自适应

在项目中编写了一套自适应工具，需在界面引入，只做参考，如有更好方案，欢迎 issues

地址： baseApp/src/assets/utils/screen.js

    /**
     * Created by dachu_liu on 2019/9/18.
     * 屏幕工具类
     * 
     * width:375
     * height:812
     */
    import {Dimensions, PixelRatio} from 'react-native'
    // 获取屏幕的dp
    
    let screenW = Dimensions.get('window').width;
    let screenH = Dimensions.get('window').height;
    let fontScale = PixelRatio.getFontScale();
    let pixelRatio = PixelRatio.get();
    // 高保真的宽度和高度   可调整该尺寸
    const designWidth = 375.0;
    const designHeight = 812.0;
    
    // 根据dp获取屏幕的px
    let screenPxW = PixelRatio.getPixelSizeForLayoutSize(screenW);
    let screenPxH = PixelRatio.getPixelSizeForLayoutSize(screenH);
    
    /**
     * 设置text
     * @param size  px
     * @returns {Number} dp
     */
    export function setSpText(size: Number) {
        console.log("screenW======" + screenW)
        console.log("screenPxW======" + screenPxW)
        var scaleWidth = screenW / designWidth;
        var scaleHeight = screenH / designHeight;
        var scale = Math.min(scaleWidth, scaleHeight);
        size = Math.round(size * scale / fontScale + 0.5);
        return size;
    }
    
    /**
     * 设置高度
     * @param size  px
     * @returns {Number} dp
     */
    export function scaleSizeH(size: Number) {
        var scaleHeight = size * screenPxH / designHeight;
        size = Math.round((scaleHeight / pixelRatio + 0.5));
        return size;
    }
    
    /**
     * 设置宽度
     * @param size  px
     * @returns {Number} dp
     */
    export function scaleSizeW(size: Number) {
        var scaleWidth = size * screenPxW / designWidth;
        size = Math.round((scaleWidth / pixelRatio + 0.5));
        return size;
    }


在项目中绝大部分布局请使用flex布局


-----



##### Flexbox

具体属性不一一详细介绍，可参考 [阮一峰 Flex 布局教程](http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html?utm_source=tuicool)

属性值与css有所不同，一些值在react-native被阉割

| 属性名 | 取值    | 描述 |
| :------ | :--------- | :--------- | 
| flex | number |  test | 
| flexDirection | row（排）, column（列） |  决定主轴的方向 | 
| flexWrap | wrap, nowrap |  决定容器内项目是否换行 | 
| justifyContent | flex-start, flex-end, center, space-between, space-around |  定义了项目在主轴的对齐方式。 | 
| alignItems | flex-start, flex-end, center, stretch |  定义了项目在交叉轴上的对齐方式 | 
| alignSelf | auto, flex-start, flex-end, center, stretch |  定义flex容器内被选中项目的对齐方式 | 




























