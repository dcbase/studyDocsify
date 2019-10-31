概述

1.react-native-router-flux是一个第三方的路由组件，目前的最新V4版本已经基于react-navigation实现。

2.react-native-router-flux包含了官方推荐react-navigation一些没有实现的功能，如：modal,refresh等。



#### 1. 安装

安装依赖包

        npm install react-native-router-flux --save
        

#### 2. 常用功能


* 正向跳转

* 正向跳转并传值

* 反向跳转

* 反向跳转并传值

* 指定页面跳转

* 指定页面跳转并传值


###### 正向跳转

假设情景：从Home页跳转到Detail页面，Detail场景的key值为detail

 * 不带参数 `onPress={() => {Actions.detail()}}`

 * 带参数  `onPress={() => {Actions.detail({key: value})}}`

在 Detail 界面接受参数：<font color="#dd0000">this.props.detailId</font>


###### 反向跳转

假设情景：从Detail页跳转到Home页面

 * 返回上一页面，不带参数 `Actions.pop()`
 
 * 返回上一页面，带参数 `Actions.pop({refresh: ({key: value})})`
 
 * 指定回退页面数 `Actions.pop({popNum: 2})`
 
 * 指定回退页面数，带参数 `Actions.pop({popNum: 2, refresh:({key: value})})`
 
 * 返回指定页面 `Actions.popTo('home')`
 

##### 注意


 <font color="#dd0000">*</font> refresh是框架自带函数，可用于刷新属性（props）

 <font color="#dd0000">*</font> Actions.pop({refresh: ({key: value})}) // 用于刷新回退到的页面的属性

 <font color="#dd0000">*</font> Actions.refresh('params') // 用于刷新当前页面的属性对应回退页面刷新属性，即接受传递的参数



### 3. 实现

在入口文件 <font color="#dd0000">App.js</font> 文件中使用Scene组件定义你的scenes，并且Scene组件作为Router的子节点。因为后面Scene将由Router来控制其行为。

如下App.js代码实例

    import React, {Component} from "react"
    import {Scene, Router, Actions, Modal, Stack, Lightbox} from "react-native-router-flux"
    
    
    import TabBar from './TabBarContainer'
    import Login from './page/user/Login'
    
    
    const getSceneStyle = () => ({
        backgroundColor: "#e9edef",
        shadowOpacity: 1,
        shadowRadius: 3,
    })
    
    
    const scenes = Actions.create(
        <Scene key="root">
            <Modal key="modal" hideNavBar>
                <Lightbox key="lightbox" hideNavBar={true}>
                    <Stack key="init" back>
                        <Scene key="main" initial back={false} hideNavBar component={TabBar}/>
                    </Stack>
                </Lightbox>
                <Stack key="login" hideNavBar titleStyle={{alignSelf: "center"}}>
                    <Scene key="loginModal" initial component={Login} title="Login" back={false} hideNavBar/>
                </Stack>
            </Modal>
        </Scene>
    )
    
    class App extends Component {
        constructor(props) {
            super(props)
        }
    
        render() {
            return (
                <Router
                    scenes={scenes}
                    tintColor='white'
                    getSceneStyle={getSceneStyle}
                />
            )
        }
    }
    
    
    const initApp = () => {
        return (
            <App/>
        )
    }
    
    export default initApp




在项目中，我们常用的组件通信方式多为父子组件通信，或兄弟组件通信
在react-native中实现通信方式与react一致，更多详细可查看下一章



