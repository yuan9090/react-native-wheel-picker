
[![npm version](http://img.shields.io/npm/v/@iftek/react-native-wheel-picker.svg?style=flat-square)](https://npmjs.org/package/@iftek/react-native-wheel-picker "View this project on npm")
[![npm version](http://img.shields.io/npm/dm/@iftek/react-native-wheel-picker.svg?style=flat-square)](https://npmjs.org/package/@iftek/react-native-wheel-picker "View this project on npm")

## @iftek/react-native-wheel-picker

- Fork form [react-native-wheel-picker](https://github.com/lesliesam/react-native-wheel-picker)
- Value accept String [ref: commit](https://github.com/HiZhenyu/react-native-wheel-picker/commit/b61f7d01f8a7f19156b39384ae077bd795168263#diff-8e95451815a1043a66a4af5be7e50bfc)
- Merge [#8 selectedColor](https://github.com/lesliesam/react-native-wheel-picker/pull/8)
- Android: cn.aigestudio.wheelpicker version to 1.1.2
- IOS: PickerIOS code in package [ref: yz1311/react-native-wheel-picker](https://github.com/yz1311/react-native-wheel-picker)

## Introduction
Cross platform Picker component based on React-native.

Since picker is originally supported by ios while Android only supports a ugly Spinner component. If you want to have the same user behaviour, you can use this.

The android component is based on https://github.com/AigeStudio/WheelPicker which runs super fast and smoothly. It also supports curved effect which make it exactly the same looking and feel as the ios picker.
![](https://raw.githubusercontent.com/lesliesam/react-native-wheel-picker/master/demo.gif)
![](https://raw.githubusercontent.com/lesliesam/react-native-wheel-picker/master/demo_android.gif)

## How to use

Run command

For apps using RN 0.40 or higher, please run
```
npm i @iftek/react-native-wheel-picker --save
```
Add in settings.gradle
```
include ':@iftek/react-native-wheel-picker'
project(':@iftek/react-native-wheel-picker').projectDir = new File(settingsDir, '../node_modules/@iftek/react-native-wheel-picker/android')
```
Add in app/build.gradle
```
compile project(':@iftek/react-native-wheel-picker')
```
Modify MainApplication
```
    import com.iftek.ReactNativeWheelPickerPackage;
    ......

    protected List<ReactPackage> getPackages() {
        return Arrays.<ReactPackage>asList(
            new MainReactPackage(), new ReactNativeWheelPickerPackage()
        );
    }
```

## Example code
```
import React, { Component } from 'react';
import {
	Platform,
	StyleSheet,
	Text,
	View,
} from 'react-native';


import Picker from '@iftek/react-native-wheel-picker'
var PickerItem = Picker.Item;

export default class App extends Component<{}> {

	constructor(props) {
		super(props);
		this.state = {
			selectedItem : 2,
			itemList: ['刘备', '张飞', '关羽', '赵云', '黄忠', '马超', '魏延', '诸葛亮']
		};
	}

	onPickerSelect (index) {
		this.setState({
			selectedItem: index,
		})
	}

	onAddItem = () => {
		var name = '司马懿'
		if (this.state.itemList.indexOf(name) == -1) {
			this.state.itemList.push(name)
		}
		this.setState({
			selectedItem: this.state.itemList.indexOf(name),
		})
	}

	render () {
		return (
			<View style={styles.container}>
				<Text style={styles.welcome}>
					Welcome to React Native!
				</Text>
				<Picker style={{width: 150, height: 180}}
					selectedValue={this.state.selectedItem}
					itemStyle={{color:"white", fontSize:26}}
					onValueChange={(index) => this.onPickerSelect(index)}>
						{this.state.itemList.map((value, i) => (
							<PickerItem label={value} value={i} key={"money"+value}/>
						))}
				</Picker>
				<Text style={{margin: 20, color: '#ffffff'}}>
					你最喜欢的是：{this.state.itemList[this.state.selectedItem]}
				</Text>

				<Text style={{margin: 20, color: '#ffffff'}}
						onPress={this.onAddItem}>
			怎么没有司马懿？
				</Text>
			</View>
		);
	}
}

const styles = StyleSheet.create({
	container: {
		flex: 1,
		justifyContent: 'center',
		alignItems: 'center',
		backgroundColor: '#1962dd',
	},
	welcome: {
		fontSize: 20,
		textAlign: 'center',
		margin: 10,
		color: '#ffffff',
	},
	instructions: {
		textAlign: 'center',
		color: '#333333',
		marginBottom: 5,
	},
});
```
