# Forked Repository

Gradle 7 버전 이후 호환성을 위해 라이브러리 Forked.

# React-Native-Local-Resource

This library allows you to include resources of any type in your javascript source folders and load
them without having to do anything special. It supports iOS and Android, 
including **Android release mode**.

## Getting started

`$ yarn add react-native-local-resource`

or

`$ npm install react-native-local-resource --save`

### Mostly automatic installation

Native installation is required to support Android release mode. 

`$ react-native link react-native-local-resource`

### Manual installation


#### Android

1. Open up `android/app/src/main/java/[...]/MainActivity.java`
  - Add `import com.igorbelyayev.rnlocalresource.RNLocalResourcePackage;` to the imports at the top of the file
  - Add `new RNLocalResourcePackage()` to the list returned by the `getPackages()` method
2. Append the following lines to `android/settings.gradle`:
  	```
  	include ':react-native-local-resource'
  	project(':react-native-local-resource').projectDir = new File(rootProject.projectDir, 	'../node_modules/react-native-local-resource/android')
  	```
3. Insert the following lines inside the dependencies block in `android/app/build.gradle`:
  	```
      compile project(':react-native-local-resource')
  	```

#### iOS

Not required.

## Usage

#### Specify file extensions

Specifying which file extensions you want to support is slightly different depending on which version of React Native your project is using.

##### React Native versions >= 0.59

You will need a [metro.config.js](https://facebook.github.io/metro/docs/en/configuration.html)
file in order to use this library. You should already probably have this file in your root project directory, but if you don't, create it.

Then, inside a `module.exports` object,
create a key called `resolver` with another object with a key called `assetExts`. 
The value of `assetExts` should be an array of the resource file extensions you want to support. 

For example, if you want to support `md` and `txt` files, your `metro.config.js` would like like this:
```javascript
module.exports = {
    resolver: {
        assetExts: ["md", "txt"]
    }
}
```


##### React Native versions >= 0.57 and < 0.59

You will need a [rn-cli.config.js](https://facebook.github.io/react-native/docs/understanding-cli#cli-configs
) file in order to use this library. Check your root project directory to see if you
already have this file and if you don't, create it.

Then, inside a `module.exports` object,
create a key called `resolver` with another object with a key called `assetExts`. 
The value of `assetExts` should be an array of the resource file extensions you want to support. 

For example, if you want to support `md` and `txt` files, your `rn-cli.config.js` would like like this:
```javascript
module.exports = {
    resolver: {
        assetExts: ["md", "txt"]
    }
}
```

##### React Native versions < 0.57

You will need a [rn-cli.config.js](https://facebook.github.io/react-native/docs/understanding-cli#cli-configs
) file in order to use this library. Check your root project directory to see if you
already have this file and if you don't, create it.

Then, inside a `module.exports` object,
create a function called `getAssetExts` which returns an array of the resource file
extensions you want to support. 

For example, if you want to support `md` and `txt` files, your `rn-cli.config.js` would like like this:
```javascript
module.exports = {
    getAssetExts() {
        return ["md", "txt"]
    }
}
```


#### Calling the library

The library exposes a single `async` function which accepts the source of the resource as the argument
and returns the string content of the resource. 

Example usage:

```javascript
import loadLocalResource from 'react-native-local-resource'
import myResource from './my_resource.txt'

function example() {
    loadLocalResource(myResource).then((myResourceContent) => {
            console.log("myResource was loaded: " + myResourceContent)
        }
    )
}
```
  
## Demo Project

This repo contains a demo project in the [`demo_project`](/demo_project) folder.
