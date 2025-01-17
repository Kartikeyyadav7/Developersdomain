---
template: blog-post
title: Creating Custom Buttons in React Native
slug: /creating-custom-buttons-in-react-native
date: 2021-04-12 15:55
description: Creating a custom button gives you a great and seamlessly
  consistent UI irrespective of OS. This becomes of utmost importance to
  implement as the core UI button of react-native looks different in different
  OS.
featuredImage: /assets/frame-1.png
---
## Introduction

React Native is an open-source mobile application framework created by Facebook, Inc. It is used to develop applications for Android, Android TV, iOS, macOS, tvOS, Web, Windows, and UWP by enabling developers to use React's framework along with native platform capabilities. React Native is one of the best platforms to create a cross-platform application that works on both Android as well as iOS. The core UI components in react native help us to speed up and scale up the development

But.. this core UI element Looks different in a different platform as in android and iOS same goes with the Button  component look different on each platform, and there are limited styling and customization options to these components. For this and many other reasons, it’s critical to know how to create buttons that look consistent regardless of the operating system.

![Buttons in different OS](/assets/frame-13-1-.png)

For a user interface to look seamless and the same on every platform it becomes very important to create our custom components. In this blog, we will be dealing with several methods to create our custom button.

<!--EndFragment-->

<!--StartFragment-->

## Setting Up

Assuming you all guys know the basics of React and React-native let's get right into constructing custom buttons component in react-native.

Start with setting up a general React native app by typing the following in the command prompt

<!--EndFragment-->

```javascript
npm react-native init AviateButtonDemo
```

<!--StartFragment-->

Clear down the all default code written in the App.js and start with the fresh window. Then type the following to get the basic component of a button in react-native

<!--EndFragment-->

```javascript
import React from "react";
import { View, Button, StyleSheet } from "react-native";

const App = () => {
  return (
    <View style={styles.Container}>
      <Button title="Hii dev!" />
    </View>
  );
};

const styles = StyleSheet.create({
  Container: {
    flex: 1,
    justifyContent: "center",
    padding: 18
  }
});

export default App;
```

<!--StartFragment-->

In the above code, we have created a button that is the core UI component of the react-native which is wrapped inside the container which is the View component of the react-native. In react-native, we are provided with the Stylesheet where we can style our component we can say it comes as an analogy of CSS or abstraction to CSS stylesheets.

<!--EndFragment-->

<!--StartFragment-->

## The Custom Button Component

As we have now done with the home page set up with the general button component and in this, you can see how it appears different on different OS. Now to cope up with this we will make our custom button which will be a functional component.

<!--EndFragment-->

```javascript
const CustomButton = () => (
   
)
```

<!--StartFragment-->

Name the custom button as *CustomButton*

As we are going to make a custom button so we will make use of the TouchableOpacity component to make a touchable component and manipulate it as we need so for this we will be required to import certain components which are

`<TouchableOpacity/>` and we have to include `<Text/>`component to add text in it. So import them from react-native.

<!--EndFragment-->

```javascript
 import { View, Button, StyleSheet, TouchableOpacity, Text } from "react-native";
```

<!--StartFragment-->

Now, let's code the custom button. In this, we need to add onPress to the TouchableOpacity and add the text we need to have on button.

<!--EndFragment-->

```javascript
const CustomButton = ({ onPress, title }) => (
  <TouchableOpacity onPress={onPress} style={styles.customButton}>
    <Text style={styles.customButtonText}>{title}</Text>
  </TouchableOpacity>
);
```

<!--StartFragment-->

`<TouchableOpacity/>` this component provides a robust behavior of change in opacity while clicking or touching we can customize that too with its properties one such property is activeOpacity. So we can control opacity by bypassing this prop to the component. Similarly, we can add various props to these components as per our needs and customize them. Go through the [doc](https://reactnative.dev/docs/touchableopacity) of the same for more props and its feature.

<!--EndFragment-->

```javascript
const CustomButton = ({ onPress, title }) => (
  <TouchableOpacity
    activeOpacity={0.6}
    onPress={onPress}
    style={styles.appButtonContainer}
  >
    <Text style={styles.appButtonText}>{title}</Text>
  </TouchableOpacity>
);
```

<!--StartFragment-->

## Styling

As our main motive is to make our UI consistent and seamless in both OS so let's start styling the custom button component.

<!--EndFragment-->

```javascript
const styles = StyleSheet.create({
customButton: {
    elevation: 10,
    backgroundColor: "#FFFE00",
    borderRadius: 15,
    paddingVertical: 10,
    paddingHorizontal: 10 
  },
  customButtonText: {
   fontSize: 25,
    color: "#000000",
    fontWeight: "bold",
    alignSelf: "center",
    
  }
});
```

<!--StartFragment-->

It should look some what like this

<!--EndFragment-->

![Demonstration on emulator](/assets/3.png)

<!--StartFragment-->

Wondering how to give gradient or another styling to our buttons! Here react-native has a solution to it. React-native provides a library that gives us the option to apply linear gradient as there is no by default API to include linear gradient in our button so we need to import the library for it of linear-gradient, do the following for importing the same

<!--EndFragment-->

<!--StartFragment-->

```jsx
npm i react-native-linear-gradient
```

<!--EndFragment-->

<!--StartFragment-->

Now we have to import `<LinearGradient/>` library from react-native-linear-gradient

We just need a little tweaking to our previous code in `<CustomButton/>` we have to wrap the `<TouchableOpacity/>` component by `<LinearGradient/>` and add some props to it. Basically, we will add color props to it which will define the gradient of the button. Basically, the color prop in LinearGradient accepts an array of colors through which a gradient is created.

```jsx
const CustomButton = ({ onPress, title }) => (
  <TouchableOpacity onPress={onPress}>
    <LinearGradient
      colors={["#FFFE00", "#C5C417"]}
      style={styles.appButtonContainer}
    >
      <Text style={styles.appButtonText}>{title}</Text>
    </LinearGradient>
  </TouchableOpacity>
);
```

It should now look somewhat like this-

![With gradient](/assets/2.png)

Full Source code of the tutorial is here given below,

```jsx
import React from "react";
import { View, StyleSheet, TouchableOpacity, Text } from "react-native";
import LinearGradient from "react-native-linear-gradient";

const CustomButton = ({ onPress, title }) => (
  <TouchableOpacity 
     onPress={onPress}
    activeOpacity={0.6}>
    <LinearGradient
      colors={["#FFFE00", "C5C417"]}
      style={styles.customButton}
    >
      <Text style={styles.customButtonText}>{title}</Text>
    </LinearGradient>
  </TouchableOpacity>
);

const App = () => {
  return (
    <View style={styles.screenContainer}>
      < CustomButton title="Hi dev!"  backgroundColor="#312D2D" />
    </View>
  );
};

const styles = StyleSheet.create({

  customButton: {
      elevation: 10,
      backgroundColor: "#FFFE00",
      borderRadius: 15,
      paddingVertical: 10,
      paddingHorizontal: 10 
    },
    customButtonText: {
     fontSize: 25,
      color: "#000000",
      fontWeight: "bold",
      alignSelf: "center",
      
    }
  });

export default App;
```

## Epilogue

Here, I would like to conclude by just stating that as a developer it's our core responsibility to make the user interface look-alike irrespective of OS a user is using so this stands to be of utmost importance to have learned the process of making look button similar to each and every platform in react-native. There’s so much more you can do, but the steps in this blog will help you find your footing as you start creating custom UI components with React Native. 

Reach out to us on [](https://twitter.com/kartikey_yadav7)[Twitter](https://twitter.com/aviatecoders) and [Instagram](https://instagram.com/aviatecoders) where we try to provide more value in threads and carousal formats

Thank You for your time

Keep learning, Keep coding :)

<!--EndFragment-->