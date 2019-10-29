
通过react-native-tab-navigator实现下面这样的底部Tab切换

###### 1. 安装

        npm install react-native-tab-navigator --save
        
        
##### 2. 相关API


<style>
table th:first-of-type {
	width: 30%;
}
</style>

2.1 TabNavigator 属性

| 属性名 | 描述    | 
| :------ | :---------: |
| sceneStyle | 切换的每一屏的样式，等同于每一屏根View的样式 | 
| tabBarStyle | TabBar的样式，控制Item的样式，和tabStyle有点类似 | 
| tabBarShadowStyle | TabBar阴影的样式 | 
| hidesTabTouch | true关闭点击的透明变化效果，false反之 | 


需要文字及图标居中可在 TabNavigator 的 tabBarStyles 设置：

    <TabNavigator tabBarStyle={styles.tabBar}>
        <TabNavigator.Item>
            <item.component  navigation={navigation}/>
        </TabNavigator.Item>
    </TabNavigator>
    
    
    const styles = StyleSheet.create({
        tabBar:{
            alignItems:'center',   //设置居中
            height:60,             //设置高度
            paddingBottom:10       //根据不用客户端进行条件判断增加
        }
    })


2.2 TabNavigator.Item 属性

| 属性名 | 描述    | 
| :------ | :---------: |
| renderIcon | TabBar未选中的Icon | 
| renderSelectedIcon | TabBar选中的Icon | 
| badgeText | 右上角提示的文字 | 
| renderBadge | 提示角标渲染方式，function类型 | 
| title | tabBar的标题 | 
| titleStyle | TabBar未选中的标题样式 | 
| selectedTitleStyle | TabBar选中的标题样式 | 
| tabStyle | 设置TabBar的样式 | 
| selected | 是否选中 | 
| onPress | 点击事件的回调函数，控制state | 
| allowFontScaling | 是否允许字体缩放，默认false | 


##### 3. 具体代码编写（以本次项目为例）：

3.1  新建 TabBarContainer.js

    import React, {Component} from 'react'
    import {StyleSheet, View, Image} from 'react-native'
    import TabNavigator from 'react-native-tab-navigator'
    import Home from './page/home/Home'
    import User from './page/user/User'
    
    const dataSource = [
        {icon:require('../assets/images/icon-daily.png'),selectedIcon:require('../assets/images/icon-daily-active.png'),tabPage:'Home',tabName:'主页',component:Home},
        {icon:require('../assets/images/icon-user.png'),selectedIcon:require('../assets/images/icon-user-active.png'),tabPage:'User',tabName:'我的',component:User}
    ]
    
    var navigation = null;
    export default class MainPage extends Component {
    
      constructor(props) {
        super(props)
        navigation = this.props.navigation
        this.state = {
          selectedTab: 'Home'
        }
      }
    
        render() {
            let tabViews = dataSource.map((item,i) => {
              return (
                  <TabNavigator.Item
                      title={item.tabName}
                      selected={this.state.selectedTab===item.tabPage}
                      titleStyle={{color:'#77869E'}}
                      selectedTitleStyle={{color:'#0047CC'}}
                      renderIcon={()=><Image style={styles.tabIcon} source={item.icon}/>}
                      renderSelectedIcon = {() => <Image style={styles.tabIcon} source={item.selectedIcon} />}
                      onPress = {() => {this.setState({selectedTab:item.tabPage})}}
                      key={i}
                  >
                      <item.component  navigation={navigation}/>
                  </TabNavigator.Item>
              );
            })
            return (
              <View style={styles.container}>
                <TabNavigator tabBarStyle={styles.tabBar}>
                    {tabViews}
                </TabNavigator>
              </View>
            )
        }
    }
    
    const styles = StyleSheet.create({
        container: {
            flex: 1,
            backgroundColor:'#fff'
        },
        tabIcon:{
            width:23,
            height:23,
        },
        tabBar:{
            height:70,
            paddingBottom:10,
            alignItems:'center'
        }
    })
    
    
    /*
    *
    *  renderIcon:可使用图片或者icon，使用图片时
    *             本地图片引入方式：source={require('../assets/images/icon-daily.png')}
    *             网络图片引入方式：source={{uri: 'https://facebook.github.io/origami/public/images/birds.jpg'}}
    *
    *  selected:设置默认选中场景
    *
    */


3.2 新建 Home.js

    import React,{ Component } from 'react';
    import {
        StyleSheet,
        Text,
        View,
    } from 'react-native'
    import {commonStyles} from "../../../assets/style/commonStyles"
    
    
    export default class Home extends Component{
        constructor(props){
            super(props)
            this.state={
                dailyLength:0
            }
        }
    
        componentDidMount() {
    
        }
    
        render(){
            return (
                <View style={styles.container}>
                      <Text>主页</Text>
                </View>
            );
        }
    }
    const styles = StyleSheet.create({
        container:{
            flex:1,
            backgroundColor:'#e9edef'
        }
    });


3.3 新建 User.js

    import React,{ Component } from 'react';
    import {
        StyleSheet,
        Text,
        View,
    } from 'react-native'
    import {commonStyles} from "../../../assets/style/commonStyles"
    
    
    export default class User extends Component{
        constructor(props){
            super(props)
            this.state={
                dailyLength:0
            }
        }
    
        componentDidMount() {
    
        }
    
        render(){
            return (
                <View style={styles.container}>
                      <Text>用户中心</Text>
                </View>
            );
        }
    }
    const styles = StyleSheet.create({
        container:{
            flex:1,
            backgroundColor:'#e9edef'
        }
    });


##### 注意

TypeError: undefined is not an object (evaluating ‘this.props.navigation.navigate’)

通过这个传递navigation，然后在每一屏里面进行跳转。

    <item.component navigation={navigation}/>














