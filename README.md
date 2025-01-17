# React Native Honeywell Scanner

> **This package is not maintained! [This fork](https://github.com/AMI3GOLtd/react-native-honeywell-scanner) might work better.**

This package was forked off the react-native-honeywell-scanner repository.  That repository supported CT50 devices, but the CT60 structures
its data returned from the scanner a little differently.  While the old version still works, it runs into some issues with typescript installed.

**Tip**: Use [react-native-camera](https://github.com/react-native-community/react-native-camera) as fallback for devices that don't have an integrated scanner; it has an integrated barcode scanner by using the camera.

## Installation

```
yarn add react-native-honeywell-scanner
```

To install the native dependencies:

```
react-native link react-native-honeywell-scanner
```

## Usage

First you'll want to check whether the device is a Honeywell scanner:

```js
import HoneywellScanner from 'react-native-honeywell-scanner';

HoneywellScanner.isCompatible // true or false
```

The barcode reader needs to be "claimed" by your application; meanwhile no other application can use it. You can do that like this:

```js
HoneywellScanner.startReader().then((claimed) => {
    console.log(claimed ? 'Barcode reader is claimed' : 'Barcode reader is busy');
});
```

To free the claim and stop the reader, also freeing up resources:

```js
HoneywellScanner.stopReader().then(() => {
    console.log('Freedom!');
});
```

To get events from the barcode scanner:

```js
HoneywellScanner.on('barcodeReadSuccess', event => {
    console.log('Received data', event.data);
});

HoneywellScanner.on('barcodeReadFail', () => {
    console.log('Barcode read failed');
});
```

To stop receiving events:

```js
function barcodeReadFail = () => console.log('Barcode read failed');
HoneywellScanner.off('barcodeReadFail', handler);
```


## Inspiration

The [react-native-bluetooth-serial](https://github.com/rusel1989/react-native-bluetooth-serial) project was used as inspiration. [cordova-honeywell](https://github.com/icsfl/cordova-honeywell) also served as some inspiration.
