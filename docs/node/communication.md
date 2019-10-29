##### 概述

本章主要讲解通信方式为项目中常见方式，使用方式与react相同，了解组件通信方式前，请先阅读下react生命周期；


生命周期文档可阅读"aermin"编写的[详解React生命周期(包括react16版)](https://www.jianshu.com/p/514fe21b9914)

###### 父组件向子组件通信

父组件更新组件状态，通过props传递给子组件，子组件得到后进行更新。

父组件向子组件传订单数据参数params对象。如下代码：

    <Child params={params} />  // 单个参数传递
    
    or
    
    <Child params={params} test={test} />  // 多个参数传递

在子组件里直接通过props获取父组件传递过来的参数，如下：

    let params = this.props.params
    
    or 
    
    let {params, test} = this.props   //多参数传递时


######  子组件向父组件通信


子组件更新组件状态，通过回调函数的方式传递给父组件

子组件调用父组件通过props传给它的函数更新父组件state，进而完成子组件向父组件的通讯


parent.js 文件如下：

    import React, { Component } from 'react';
    import {
        StyleSheet,
        Text,
        View
    } from 'react-native'
    //导入子组件
    import Child from './child'; 

    class Parent extends Component {
      constructor(props){
        super(props);
        this.state = {
          msg: '父组件初始msg'
        }
      }
    
      //父组件回调函数，更新state，进而更新父组件。
      callback=(msg)=>{
        // setState方法,修改msg参数,值是由子组件传过来。
        this.setState({msg});
      }
    
      render() {
        return (
          <View>
            <Text>子组件传值实验: {this.state.msg}</Text>
            <Child callback={this.callback} ></Child>
          </View>
        );
      }
    }
    
    export default Parent;



child.js 文件如下：

    import React, { Component } from 'react';
    import {
        StyleSheet,
        Text,
        View,
        TouchableOpacity
    } from 'react-native'

    class Child extends Component {
      constructor(props){
        super(props);
        this.state={
            msg: '子组件msg传值'
        }
      }
    
      //通过props调用回调函数传值
      trans=()=>{
          this.props.callback(this.state.msg);
      }
      
      render(){
          return(
              <View>
                  <TouchableOpacity onPress={this.trans}>激发trans事件，传值给父组件</button>
              </View>
          )
      }
    }
    
    export default Child;


未完待续。。。。。。  

 
