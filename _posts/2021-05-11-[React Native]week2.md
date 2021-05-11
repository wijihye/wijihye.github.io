---
layout: post
title: '[React Native] Week 2: using navigation'
tags: [study, react_native, navigation]
---

#### [React Native] practice navigation

Date: May 11, 2021

### Preview

<img src="https://user-images.githubusercontent.com/58647487/117794517-45b94c00-b288-11eb-9a54-ceac0bda0549.gif" width="250" height="520">

### Technical Stack

1. React Native
   - [View](https://reactnative.dev/docs/view)
   - [Text](https://reactnative.dev/docs/text)
   - [Image](https://reactnative.dev/docs/image)
   - [ScrollView](https://reactnative.dev/docs/scrollview)
   - [TouchableOpacity](https://reactnative.dev/docs/touchableopacity)
   - [Navigation](https://reactnavigation.org/)

### Code

1. App.js (initial file)

   - navigation stack을 이용해서 home, student_card, music_list를 연결해놓는다.
   - initialRouteName을 이용해 맨 처음 화면을 지정하고 screenOption을 이용해서 navigation이 될 때 나타나는 option을 지정한다.
   - Screen API를 이용하여 name을 각자 다르게 지정하여 navigation으로 이동할 화면들을 구성한다.

   ```jsx
   import React from 'react';
   import { Text, View, Image, Touchable, StyleSheet } from 'react-native';
   import { createStackNavigator } from '@react-navigation/stack';
   import { NavigationContainer } from '@react-navigation/native';
   import 'react-native-gesture-handler';

   import home from './sources/week2_navigation/home';
   import studentCard from './sources/week2_navigation/student_card';
   import musicList from './sources/week2_navigation/music_list';

   const page_stack = createStackNavigator();

   const App = () => {
     return (
       <NavigationContainer>
         <page_stack.Navigator
           initialRouteName="home"
           screenOptions={{ headerShown: false }}
         >
           <page_stack.Screen name="home" component={home} />
           <page_stack.Screen name="studentCard" component={studentCard} />
           <page_stack.Screen name="musicList" component={musicList} />
         </page_stack.Navigator>
       </NavigationContainer>
     );
   };

   export default App;
   ```

2. home.js

   - 맨 처음 버튼들이 있는 화면을 만든다.
   - 두 가지 이상의 style이 적용디면 style을 따로 빼서 만듦. => 정작 컴포넌트 안에서는 그 구조만 한 눈에 보였으면 해서.
   - {navigation} 매개변수를 이용해서 TouchableOpacity를 onPress 했을 때 다른 화면으로 이동할 수 있도록 함.

   ```jsx
   import React from 'react';
   import {
     StyleSheet,
     Text,
     View,
     Button,
     TouchableOpacity,
     Touchable,
     Linking,
   } from 'react-native';

   const style = StyleSheet.create({
     container: {
       backgroundColor: 'black',
       height: '100%',
       alignItems: 'center',
       paddingTop: 50,
     },
     buttonContainer: {
       textAlign: 'center',
       width: '80%',
     },
     button: {
       height: 120,
       margin: 20,
     },
     buttonText: {
       fontSize: 30,
       textAlign: 'center',
       lineHeight: 120,
     },
   });

   const home = ({ navigation }) => {
     return (
       <View style={style.container}>
         <Text style={{ fontSize: 50, color: '#5c6bc0', marginBottom: 40 }}>
           HOME MENU
         </Text>
         <View style={style.buttonContainer}>
           <View style={{ margin: 10 }}>
             <TouchableOpacity
               style={(style.button, { backgroundColor: 'yellow' })}
               onPress={() => navigation.navigate('studentCard')}
             >
               <Text style={style.buttonText}>Student Card</Text>
             </TouchableOpacity>
           </View>
           <View style={{ margin: 10 }}>
             <TouchableOpacity
               style={(style.button, { backgroundColor: 'skyblue' })}
               onPress={() => navigation.navigate('musicList')}
             >
               <Text style={style.buttonText}>Music List</Text>
             </TouchableOpacity>
           </View>
           <View style={{ margin: 10 }}>
             <TouchableOpacity
               style={(style.button, { backgroundColor: 'yellowgreen' })}
               onPress={() => Linking.openURL('https://naver.com')}
             >
               <Text style={style.buttonText}>Go to Naver</Text>
             </TouchableOpacity>
           </View>
         </View>
       </View>
     );
   };

   export default home;
   ```

3. music_list.js

   - map을 이용하여 반복문처럼 구성함. forEach는 반환형이 없는 단순연산이므로 배열을 반환하는 map을 이용하여 반복을 구현함.

   - music_data.js를 만들어서 cover라는 key에 require 자체를 담아 놓는다. 이를 빼서 dynamic한 Image source를 이용할 수 있도록 함.

   - music_data.js

     ```jsx
     const musicList = [
       {
         title: 'Boat',
         singer: '죠지(george)',
         cover: require('../../assets/week2_navigation/boat.png'),
         album: 'Boat',
         date: '2017',
       },
       {
         title: '멜로디',
         singer: 'ASH ISLAND',
         cover: require('../../assets/week2_navigation/melody.png'),
         album: 'ISLAND',
         date: '2021',
       },
       {
         title: 'VERY NICE(아주 NICE)',
         singer: '세븐틴',
         cover: require('../../assets/week2_navigation/very_nice.png'),
         album: '[FIRST ‘LOVE&LETTER’]',
         date: '2016',
       },
       {
         title: 'Off My Face',
         singer: 'Justin Beiber',
         cover: require('../../assets/week2_navigation/off_my_face.png'),
         album: 'Justice',
         date: '2021',
       },
       {
         title: 'Sit Still, Look Pretty',
         singer: 'Daya',
         cover: require('../../assets/week2_navigation/sit_still_look_pretty.png'),
         album: 'Sit Still, Look Pretty',
         date: '2016',
       },
       {
         title: 'unlucky',
         singer: 'IU(아이유)',
         cover: require('../../assets/week2_navigation/unlucky.png'),
         album: 'Love poem',
         date: '2019',
       },
     ];

     export default musicList;
     ```

   ```jsx
   // music_list.js
   import React from 'react';
   import musicList from './music_data.js';

   import {
     Image,
     StyleSheet,
     Text,
     View,
     Button,
     TouchableOpacity,
     ScrollView,
   } from 'react-native';

   const style = StyleSheet.create({
     container: {
       justifyContent: 'center',
       alignItems: 'center',
     },
     musicBox: {
       flexDirection: 'row',
       alignItems: 'center',
       margin: 10,
       width: '95%',
       height: 160,
       backgroundColor: 'white',
       borderWidth: 1,
     },
     coverImg: {
       width: 150,
       height: 150,
       marginLeft: 5,
       marginRight: 15,
     },
     homeBtn: {
       width: 100,
       height: 30,
       backgroundColor: 'salmon',
       borderRadius: 15,
       margin: 30,
     },
   });

   const music_list = ({ navigation }) => {
     return (
       <ScrollView>
         <Text style={{ textAlign: 'center', color: 'green', fontSize: 30 }}>
           MUSIC LIST
         </Text>
         {musicList.map((value, idx) => (
           <View key={idx} style={style.musicBox}>
             <Image style={style.coverImg} source={value.cover} />
             <View style={{ justifyContent: 'center' }}>
               <Text>Title: {value.title}</Text>
               <Text>Singer: {value.singer}</Text>
               <Text>Album: {value.album}</Text>
               <Text>Date: {value.date}</Text>
             </View>
           </View>
         ))}
         <View style={style.container}>
           <TouchableOpacity
             style={style.homeBtn}
             onPress={() => navigation.navigate('home')}
           >
             <Text style={{ textAlign: 'center', lineHeight: 30 }}>
               뒤로가기
             </Text>
           </TouchableOpacity>
         </View>
       </ScrollView>
     );
   };

   export default music_list;
   ```

4. student_card.js

   - 1주차 실습이었던 학생증 모양을 그대로 구현하면 되는 거였음.
   - 그떄는 그냥 복붙으로 했는데 하나하나 보니 생각보다 어렵지 않아서 직접 style을 줘가며 짰음.

   ```jsx
   import { CardStyleInterpolators } from '@react-navigation/stack';
   import React from 'react';
   import {
     Image,
     StyleSheet,
     Text,
     View,
     Button,
     TouchableOpacity,
   } from 'react-native';

   const style = StyleSheet.create({
     container: {
       justifyContent: 'center',
       alignItems: 'center',
       marginTop: 50,
       marginBottom: 50,
       height: '80%',
     },
     studentCard: {
       justifyContent: 'center',
       flexDirection: 'row',
       width: 250,
       height: 150,
       borderColor: 'black',
       borderWidth: 1,
     },
     stduentImage: {
       width: 100,
       height: 100,
       margin: 10,
       marginTop: 20,
     },
     studentInfo: {
       marginRight: 10,
       marginTop: 30,
       marginBottom: 20,
     },
     homeBtn: {
       width: 100,
       height: 30,
       backgroundColor: 'salmon',
       borderRadius: 15,
       margin: 30,
     },
   });

   const student_card = ({ navigation }) => {
     return (
       <View style={style.container}>
         <Text style={{ fontSize: 20, marginBottom: 50 }}>학생증</Text>
         <View style={style.studentCard}>
           <Image
             source={require('../../assets/ThisIs.png')}
             style={style.stduentImage}
           />
           <View style={style.studentInfo}>
             <Text>이름 : 장지혜</Text>
             <Text>학번 : 1824542</Text>
             <Text>학과 : 컴퓨터공학과</Text>
             <Text>단과대학 : 공과대학</Text>
           </View>
         </View>
         <TouchableOpacity
           style={style.homeBtn}
           onPress={() => navigation.navigate('home')}
         >
           <Text style={{ textAlign: 'center', lineHeight: 30 }}>뒤로가기</Text>
         </TouchableOpacity>
       </View>
     );
   };

   export default student_card;
   ```

### Note

![1](https://user-images.githubusercontent.com/58647487/117830853-fe928180-b2ae-11eb-90b4-99246a2c6946.png)

![2](https://user-images.githubusercontent.com/58647487/117830872-00f4db80-b2af-11eb-9fda-cabfa4d29d04.png)
