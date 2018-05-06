## React-Native

[TOC]

### 属性绑定/样式绑定/基础组件

```javascript
//import 导入 意为 '导入 模块儿 从 react 模块儿导入'
import React, {Component} from 'react';
import {
    AppRegistry, // 注册APP入口
    StyleSheet, //样式表组件
    Text, //文字组件,它里面只能放文字 类似于 span 标签
    View //结构组件,它类似于 div 标签
} from 'react-native';

//创建一个 MyApp 组件
class MyApp extends Component {

    a(){
        alert("天海移速");
    }
    //onPress 属性,设置Text组件的点击效果
    //numberOfLines 设置Text里面一共可以容纳多少行,
    //如果超出所设置的行数,则用...代替

    render() {
        return (
            <View style={styles.wp}>
                 <View style={styles.son}>
                    <Text style={styles.setColor}>李白乘舟将欲行,</Text>
                    <Text>忽闻岸上踏歌声.</Text>
                    <Text>桃花潭水深千尺,</Text>
                    <Text>不及汪伦送我情.</Text>
                </View>
                <View style={styles.son}>
                    <Text>李白乘舟将欲行,</Text>
                    <Text>忽闻岸上踏歌声.</Text>
                    <Text>桃花潭水深千尺,</Text>
                    <Text>不及汪伦送我情.</Text>
                </View>
                <View style={styles.son} >
                    <Text numberOfLines={3} onPress={this.a}> 我的我饿 no二维 UIwe 第二维护费任何就热火牛肉妞儿韩国忽热以为入耳会热回归任何牛二哈为hiUR以rehiaureiuhiu
                        任务房间软件而加热啤酒以而回归会如果介入韩国第二日韩国二胡韩国恶如韩国热乎瑞韩国</Text>
                </View>
                <View style={styles.wp}>
                    <View style={styles.txt}>
                        <View style={styles.son}><Text>精</Text></View>
                        <View style={styles.son}><Text>忠</Text></View>
                    </View>
                    <View style={styles.txt}>
                        <View style={styles.son}><Text>报</Text></View>
                        <View style={styles.son}><Text>国</Text></View>
                    </View>
                </View>

            </View>
        );
    }
}

//设置样式
const styles = StyleSheet.create({
    wp: {
        marginTop: 30,
        backgroundColor: '#f00',
        flexDirection: 'row',
        flex:1
    },

    setColor: {
        color: '#ff0',
    },
    son: {
        alignItems: 'center',
        justifyContent: 'center',
        flex: 1,
        borderWidth: 2,
        borderColor: 'blue'
    },
    txt: {
        flex:1
    }
});


//注册app,其中 'myapp'是指工程名,'MyApp'是创建的组件名
AppRegistry.registerComponent('myapp', () => MyApp);
```

### 图片组件

```javascript
//import 导入 意为 '导入 模块儿 从 react 模块儿导入'
import React, {Component} from 'react';
import {
    AppRegistry, // 注册APP入口
    StyleSheet, //样式表组件
    Text, //文字组件,它里面只能放文字 类似于 span 标签
    View, //结构组件,它类似于 div 标签
    Image // 图片组件,一般使用单标签,类似于 html 中的 JS
} from 'react-native';
import Head from './header';

//创建一个 MyApp 组件
class MyApp extends Component {
    aa() {
        alert("道可道,非常道");
    }
    render() {
        return (
            <View>
                <View>
                    <View style={styles.wp}>
                        <Image style={styles.img} resizeMode='contain' source={{uri:'http://pic29.photophoto.cn/20131204/0034034499213463_b.jpg'}}
                        />
                    </View>
                    <View style={styles.wp}>
                        {/*加载成功之后*/}
                        <Image onLoad={this.aa} style={styles.img} resizeMode='contain' source={require('./aa/1.jpg')}
                        />
                    </View>
                </View>

                <View>
                    <Head />
                </View>
            </View>
        );
    }
}

//设置样式
const styles = StyleSheet.create({
    wp: {
        marginTop: 30,
        borderColor: '#f00',
        borderWidth: 2,
        height: 200,
        width: 200,
    },
    img: {
        width: 200,
        height: 200
    }
});

//注册app,其中 'myapp'是指工程名,'MyApp'是创建的组件名
AppRegistry.registerComponent('myapp', () => MyApp);
```

### 自定义组件

```javascript
//import 导入 意为 '导入 模块儿 从 react 模块儿导入'
import React, {Component} from 'react';
import {AppRegistry, StyleSheet, Text, View, Image} from 'react-native';

// 创建组件
class Head extends Component {
    render() {
        return (
            <View style={styles.wp}>
                <Text style={styles.head}>我来组成头部</Text>
            </View>
        );
    }
}

const styles = StyleSheet.create({
    wp:{
        marginTop: 30,
        backgroundColor:'#0f0',
        paddingTop:10,
        paddingBottom:10
    },
    head:{
        color: '#f00',
        fontSize:30,
    }
});

module.exports = Head;
```

### 引用组件

```javascript
//import 导入 意为 '导入 模块儿 从 react 模块儿导入'
import React, {Component} from 'react';
import {
    AppRegistry, // 注册APP入口
    StyleSheet, //样式表组件
    Text, //文字组件,它里面只能放文字 类似于 span 标签
    View, //结构组件,它类似于 div 标签
    Image,
    TextInput // 引入输入组件,

} from 'react-native';

//创建一个 MyApp 组件
class MyApp extends Component {
    constructor() {
        super();
        this.state = {
            val: '百里玄策'
        }
    }

    // onChangeText 默认接收一个参数,该参数是用户接收的值
    changeVal(val) {
        this.setState({
            val:val
        })
    }

    render() {
        return (
            <View style={styles.wp}>
                <TextInput
                    style={styles.input}
                    placeholder='请输入支付宝密码'
                    placeholderTextColor='#f00'
                    // password={true}
                    // multiline={true}
                    clearButtonMode='always'
                    value={this.state.val}
                    onChangeText={this.changeVal.bind(this)}
                />
                <View>
                    <Text>{this.state.val}</Text>
                </View>
            </View>
        );
    }
}

//设置样式
const styles = StyleSheet.create({
    wp: {
        marginTop: 30,
    },
    input: {
        borderColor: '#0f0',
        borderWidth: 2,
        marginLeft: 40,
        height: 40,
        lineHeight: 40,
        paddingLeft: 20,
        width: 300
    }
});

//注册app,其中 'myapp'是指工程名,'MyApp'是创建的组件名
AppRegistry.registerComponent('myapp', () => MyApp);
```

