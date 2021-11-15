# new-react-native-cli-steps
A guideline for creating a new React Native CLI project

## :sparkles: React Native Essential Libraries
Here are a list of React Native libraries needed to start any project.
Follow the steps to install all the libraries smoothly in both Android and iOS.

## :open_book: Table of Contents  
1. [Create a project](#new)  
2. [RN Navigation](#navigation)  
3. [RN SVG Transformer](#svg)  
4. [RN Vector Icons](#icons)
5. [RN Elements](#elements)
6. [RN NativeBase](#nativebase)
7. [RN Functional Component Template](#template)

<a name="new"/>

## Create a New React Native Project

```
npx react-native init “Project Name”
```
<a name="navigation"/>

## React Native Navigation

```
npm install @react-navigation/native
```
```
npm install react-native-screens react-native-safe-area-context
```
```
npx pod-install ios
```
```
npm install @react-navigation/native-stack
```
```
npm install @react-navigation/bottom-tabs
```
In MainActivity.js add:
```
import android.os.Bundle; //Navigation
```
> In the bottom Add
```
// Navigation
  @Override
  protected void onCreate(Bundle savedInstanceState) {
  super.onCreate(null);
  }
```

<a name="svg"/>

## React Native SVG transformer

```
npm install --dev react-native-svg-transformer
```
Replace metro.config.js with this
```
const {getDefaultConfig} = require('metro-config');

module.exports = (async () => {
  const {
    resolver: {sourceExts, assetExts},
  } = await getDefaultConfig();
  return {
    transformer: {
      getTransformOptions: async () => ({
        transform: {
          experimentalImportSupport: false,
          inlineRequires: true,
        },
      }),
      babelTransformerPath: require.resolve('react-native-svg-transformer'),
    },
    resolver: {
      assetExts: assetExts.filter(ext => ext !== 'svg'),
      sourceExts: [...sourceExts, 'svg'],
    },
  };
})();
```

<a name="icons"/>

## React Native Vector Icons

```
npm install --save react-native-vector-icons
```
```
npx pod-install ios
```
Browse to node_modules/react-native-vector-icons and drag the folder Fonts (or just the ones you want) to your project in Xcode.

![vector1](https://user-images.githubusercontent.com/53459406/141814204-5cb51457-41d4-4457-b0ce-5c235d177d5e.png)

Edit Info.plist and add a property called Fonts provided by application and type in the files you just added.

![image](https://user-images.githubusercontent.com/53459406/141820996-522696f0-7c79-4366-8653-a79645a00dda.png)

Remove the font from Bundle Resources to avoid multiple command (references) error.

![image](https://user-images.githubusercontent.com/53459406/141821088-a39cd404-d909-4fcd-8c74-b71fd1f1548b.png)

For android, edit android/app/build.gradle :
```
apply from: “../../node_modules/react-native-vector-icons/fonts.gradle"
```

Add this to info.plist:
```
<key>UIAppFonts</key>
    <array>
        <string>AntDesign.ttf</string>
        <string>Entypo.ttf</string>
        <string>EvilIcons.ttf</string>
        <string>Feather.ttf</string>
        <string>FontAwesome.ttf</string>
        <string>FontAwesome5_Brands.ttf</string>
        <string>FontAwesome5_Regular.ttf</string>
        <string>FontAwesome5_Solid.ttf</string>
        <string>Foundation.ttf</string>
        <string>Ionicons.ttf</string>
        <string>MaterialIcons.ttf</string>
        <string>MaterialCommunityIcons.ttf</string>
        <string>SimpleLineIcons.ttf</string>
        <string>Octicons.ttf</string>
        <string>Zocial.ttf</string>
        <string>Fontisto.ttf</string>
    </array>
```

<a name="elements"/>

## React Native Elements

```
npm install react-native-elements
```

<a name="nativebase"/>

## Native Base

```
npm install native-base react-native-svg styled-components styled-system react-native-safe-area-context
```
```
npx pod-install ios
```
Edit Index.js
```
import React from 'react';
import {AppRegistry} from 'react-native';
import App from './App';
import {name as appName} from './app.json';
import {NativeBaseProvider} from 'native-base';

const ProjectName = () => (
  <NativeBaseProvider>
    <App />
  </NativeBaseProvider>
);

AppRegistry.registerComponent(appName, () => ProjectName);
```

<a name="template"/>

## React Native Functional Component Template

```
import React from 'react';
import {SafeAreaView, View, Text} from 'react-native';

const ComponentName = props => {
  return (
    <SafeAreaView style={{flex: 1, width: '100%', height: '100%', alignItems: 'center', justifyContent: 'center', backgroundColor: '#FFF'}}>
      <Text>Home Screen!</Text>
    </SafeAreaView>
  );
};

export default ComponentName;
```
