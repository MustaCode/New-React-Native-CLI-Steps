# new-react-native-cli-steps
A guideline for creating a new React Native CLI project

## :sparkles: React Native Essential Libraries

## :open_book: Table of Contents  
1. [Create a project](#new)  
2. [RN Navigation](#navigation)  
3. [RN SVG Transformer](#svg)  
4. [RN Vector Icons](#icons)
5. [RN Elements](#elements)
6. [RN NativeBase](#nativebase)

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


<a name="elements"/>

## React Native Elements

```
npx react-native init “elements”
```

<a name="nativebase"/>

## Native Base

```
npx react-native init “elements”
```
