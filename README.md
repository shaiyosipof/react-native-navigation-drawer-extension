# React Native Navigation Drawer Extension

[React Native Navigation by Wix](https://wix.github.io/react-native-navigation/#/) does not offer an in-built solution for displaying a drawer on iOS. Their current side-menu has limited functionality on both iOS and Android. This is a drawer solution using showOverlay under the hood to display a drawer on iOS and Android.

<p align="left">
  <a href="https://www.npmjs.com/package/react-native-navigation-drawer-extension" rel="nofollow">
  <img src="https://img.shields.io/npm/v/react-native-navigation-drawer-extension.svg?style=flat-square" alt="version" style="max-width:100%;" />
  </a>
  <a href="https://www.npmjs.com/package/react-native-navigation-drawer-extension" rel="nofollow">
  <img src="http://img.shields.io/npm/l/react-native-navigation-drawer-extension.svg?style=flat-square" alt="license" style="max-width:100%;" />
  </a>

  <hr />
</p>

<img align="left" src="https://raw.githubusercontent.com/LukeBrandonFarrell/open-source-images/master/react-native-navigation-drawer-extension/left-drawer.gif" width="48%" />
<img src="https://raw.githubusercontent.com/LukeBrandonFarrell/open-source-images/master/react-native-navigation-drawer-extension/bottom-drawer.gif" width="48%" />

## Install

Install via npm:
```sh
 npm install react-native-navigation-drawer-extension --save
```

## Usage

You need to register your drawer component with RNN. To do this use the register method and wrap your component in the RNNDrawer HOC.

```js
import { Navigation } from "react-native-navigation";
import { RNNDrawer } from "react-native-navigation-drawer-extension";

// register our drawer component with RNN
Navigation.registerComponent("CustomDrawer", () => RNNDrawer(CustomDrawer));
```

You can then use the drawer by calling a custom method.

````js
import { Navigation } from "react-native-navigation";

// Show drawer
Navigation.showDrawer({
  component: {
    name: "CustomDrawer",
    passProps: {
      animationOpenTime: 300,
      animationCloseTime: 300,
      direction: "left",
      dismissWhenTouchOutside: true,
      fadeOpacity: 0.6,
      drawerScreenWidth: 0.8,
      drawerScreenHeight: 1,
      style: { // Styles the drawer, supports any react-native style
        backgroundColor: "red",
      },
      parentComponentId: this.props.componentId,
    },
  }
});
```

```js
// Dismiss drawer
Navigation.dismissDrawer(this.props.componentId);
````

To navigate from the drawer you must pass the parent `componentId` and use that to navigate. e.g:

```js
// From drawer component
Navigation.push(parentComponentId, {
  component: {
    name: "CustomScreenFromDrawer",
  },
});
```

## Props

| Prop                | Type          | Optional  | Default | Description                                                                             |
| ------------------- | ------------- | --------- | ------- | --------------------------------------------------------------------------------------- |
| animationOpenTime   | float         | Yes       | 300     | Time in milliseconds to execute the drawer opening animation.                           |
| animationCloseTime  | float         | Yes       | 300     | Time in milliseconds to execute the drawer closing animation.                           |
| direction           | string        | Yes       | left    | Direction to open the collage, one of: ["left", "right", "top", "bottom"].              |
| dismissWhenTouchOutside | bool      | Yes       | true    | Should the drawer be dismissed when a click is registered outside?                      |
| fadeOpacity         | number        | Yes       | 0.6     | Opacity of the screen outside the drawer.                                               |
| drawerScreenWidth   | number        | Yes       | 0.8     | 0 - 1, width of drawer in relation to the screen.                                       |
| drawerScreenHeight  | number        | Yes       | 1       | 0 - 1, height of drawer in relation to the screen.                                      |                              

## Issues

When using `Navigation.dismissDrawer` animation will not be triggered, the drawer will be hidden instantly.
Resolving [#3030](https://github.com/wix/react-native-navigation/issues/3030) should allow us to fix this.
