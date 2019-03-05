# react-native-androw

## NOTE

This version is still under development and in beta. The reason its published is for easier testing.


## Motivation

The problem is that a shadows does not work with React Native in Android. This view takes its children's, 
creates a bitmap representation, blur it and color it to styles shadow values like in iOS

## Limitations

* Not tested with lists and animations
* Android has a bitmap limitation of 2048x2048, but this might depend on API version.
* This plugin uses Software layer and might experience performance issues.


## Getting started

`$ npm install react-native-androw --save`

### Mostly automatic installation

`$ react-native link react-native-view-overflow`

## Usage
```javascript
import Androw from 'react-native-androw';

<Androw style={styles.shadow}>
  {//Act as a regular view but with shadow support in Android}
</Androw>

const styles = Stylesheet.create({
  shadow:{
      shadowColor: '#000000',
      shadowOffset:{
		width: 5, 
        height: 5,
      },
      shadowOpacity:.5,
      shadowRadius: .3
    }
});
```

## Usage with Flatlist
To make this work with FlatList and related components you need to replace `CellRendererComponent` with `Androw`, for example:

```jsx
<FlatList
  data={this.state.data}
  keyExtractor={item => item.id}
  CellRendererComponent={Androw}
  renderItem={({ item, index }) => (
      <ViewOverflow style={styles.item}>
      // item....
      </ViewOverflow>
   )}
/>
```

## Usage with Animated Views
To make this work in place of an `Animated.View`, you need to use `Animated.createAnimatedComponent` to create an animatable version of `Androw`. For example:

```
import Androw from 'react-native-androw';
const AnimatedViewOverflow = Animated.createAnimatedComponent(Androw);
```

You can then use `AnimatedViewOverflow` in place of `Animated.View`.

### Manual installation

1. Open up `android/app/src/main/java/[...]/MainApplication.java`
  - Add `import com.entria.views.RNViewOverflowPackage;` to the imports at the top of the file
  - Add `new RNAndrowPackage()` to the list returned by the `getPackages()` method
2. Append the following lines to `android/settings.gradle`:
  	```
  	include ':react-native-androw'
  	project(':react-native-androw').projectDir = new File(rootProject.projectDir, 	'../node_modules/react-native-androw/android')
  	```
3. Insert the following lines inside the dependencies block in `android/app/build.gradle`:
  	```
      implementation project(':react-native-androw')
  	```