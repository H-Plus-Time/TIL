## Polymerfire - messaging

As it happens, firebase-messaging is sensitively dependent on the timing used to instantiate the firebase app object (via firebase.initializeApp(conf)). The safest way to deal with this element is to place the initializeApp call before the containing element of firebase-messaging (foo-app). Placing the call in the ready or attached callback of foo-app ***does not work***.

Correct usage:

```html
	<!-- provided this is a synchronous import, firebase is guaranteed to be available.
        Otherwise, import firebase-messaging.html here as well (or anything else that
        includes firebase.js
    -->
	<link rel="import" href="foo-app.html">
	<script>
    	firebase.initializeApp({messagingSenderId: '123foo'});
    </script>
    <foo-app>
    </foo-app>
```

Also correct usage:

```html
	<link rel="import" href="/path/to/polymerfire/firebase-messaging.html">
	<dom-module id="foo-app">
    	<template>
        	<firebase-messaging></firebase-messaging>
        <template>
        <script>
        	Polymer({
            	is: 'foo-app',
                created() {
                	firebase.initializeApp({messagingSenderId: '123foo'});
                }
            })
        </script>
   </dom-module>
```

Incorrect usage:

```html
	<link rel="import" href="/path/to/polymerfire/firebase-messaging.html">
	<dom-module id="foo-app">
    	<template>
        	<firebase-messaging></firebase-messaging>
        <template>
        <script>
        	Polymer({
            	is: 'foo-app',
                ready() {
                	firebase.initializeApp({messagingSenderId: '123foo'});
                }
            })
        </script>
   </dom-module>
```
