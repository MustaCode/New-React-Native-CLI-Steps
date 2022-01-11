# new-react-native-cli-steps
A guideline for creating a new React Native CLI project

## :sparkles: React Native Essential Libraries
Here are a list of React Native libraries needed to start any project.
Follow the steps to install all the libraries smoothly in both Android and iOS.

## :open_book: Table of Contents  
1. [Create a project](#new)  
2. [Change Engine](#engine)
3. [RN Navigation](#navigation)  
4. [RN SVG Transformer](#svg)  
5. [RN Vector Icons](#icons)
6. [RN Elements](#elements)
7. [RN NativeBase](#nativebase)
8. [RN Functional Component Template](#template)
9. [RN Redux](#redux)
10. [RN Async Storage](#storage)
11. [RN WebView](#webview)
12. [Date fns](#date)
13. [RN Image Crop Picker](#image)

<a name="new"/>

## Create a New React Native Project
```
npx react-native init “Project Name”
```
<a name="engine"/>

## Change Project Engine
### Android
Edit your `android/app/build.gradle` file and make the change illustrated below:
```
 project.ext.react = [
      entryFile: "index.js",
-     enableHermes: false  // clean and rebuild if changing
+     enableHermes: true  // clean and rebuild if changing
  ]
```
Next, if you've already built your app at least once, clean the build:
```
cd android && ./gradlew clean
```
### iOS
To enable Hermes for iOS, edit your `ios/Podfile` file and make the change illustrated below:
```
   use_react_native!(
     :path => config[:reactNativePath],
     # to enable hermes on iOS, change `false` to `true` and then install pods
-    :hermes_enabled => false
+    :hermes_enabled => true
   )
```
Next, install the Hermes pods:
```
cd ios && pod install
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
In `MainActivity.java` add:
```
import android.os.Bundle; //Navigation
```
In the bottom add:
```
// Navigation
  @Override
  protected void onCreate(Bundle savedInstanceState) {
  super.onCreate(null);
  }
```
### Drawer
```
npm install @react-navigation/drawer
```
```
npm install react-native-gesture-handler react-native-reanimated
```
Add Reanimated's babel plugin to your `babel.config.js`:
```
  module.exports = {
      ...
      plugins: [
          ...
          'react-native-reanimated/plugin',
      ],
  };
```
Plug Reanimated in `MainApplication.java`:
```
  import com.facebook.react.bridge.JSIModulePackage; // <- add
  import com.swmansion.reanimated.ReanimatedJSIModulePackage; // <- add
  ...
  private final ReactNativeHost mReactNativeHost = new ReactNativeHost(this) {
  ...

      @Override
      protected String getJSMainModuleName() {
        return "index";
      }

      @Override
      protected JSIModulePackage getJSIModulePackage() {
        return new ReanimatedJSIModulePackage(); // <- add
      }
    };
  ...
```
To finalize installation of `react-native-gesture-handler`, add the following at the top (make sure it's at the top and there's nothing else before it) of your entry file, such as `index.js` or `App.js`:
```
import 'react-native-gesture-handler';
```
```
npx pod-install ios
```
### Bottom Tabs
```
npm install @react-navigation/bottom-tabs
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
apply from: "../../node_modules/react-native-vector-icons/fonts.gradle"
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
If safe-area-context exists then:
```
npm uninstall react-native-safe-area-context
```
```
npm install native-base react-native-svg react-native-safe-area-context
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

<a name="redux"/>

## React Native Redux

```
npm install redux react-redux --save
```
```
npm install redux-thunk
```
In `Index.js` add:
```
import React from ‘react'
import { Provider } from 'react-redux';
import configureStore from './src/store/ConfigureStore';
const store = configureStore();
const RNRedux = () => (
    <Provider store={store}>
            <App />
    </Provider>

AppRegistry.registerComponent(appName, () => RNRedux);
```
Create `ConfigureStore.js` in store folder and add:
```
import { createStore, combineReducers, applyMiddleware } from 'redux'
import thunk from 'redux-thunk'

import OrdersReducer from './reducers/OrdersReducer'

const rootReducer = combineReducers({
    orders: OrdersReducer,
});

const configureStore = () => {
    return createStore(rootReducer, applyMiddleware(thunk));
}
export default configureStore;
```
Create a Reducer `SomethingReducer.js` and add:
```
import {} from '../actions/ActionTypes'

const initialState = {

}

const Reducer = (state = initialState, action) => {
    switch (action.type) {
        default:
            return state;
    }
}
export default Reducer
```
Create `ActionTypes.js` and add:
```
//ORDERS
export const ADD_ORDER = ‘ADD_ORDER';
```
Create Action `Index.js` and add:
```
export {
  addOrder
} from ‘./Orders'
```

<a name="storage"/>

## React Native Async Storage

```
npm install @react-native-async-storage/async-storage
```
```
npx pod-install ios
```

<a name="webview"/>

## React Native WebView

```
npm install --save react-native-webview
```
```
npx pod-install ios
```
Android - react-native-webview version >=6.X.X: Please make sure AndroidX is enabled in your project by editting `android/gradle.properties` and adding 2 lines:
```
org.gradle.jvmargs=-Xmx4g -XX:MaxPermSize=2048m -XX:+HeapDumpOnOutOfMemoryError -Dfile.encoding=UTF-8
android.useAndroidX=true
android.enableJetifier=true
```

<a name="date"/>

## Date fns

```
npm install date-fns --save
```

<a name="image"/>

## React Native Image Crop Picker

```
npm i react-native-image-crop-picker --save
```
```
npx pod-install ios
```
