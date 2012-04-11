#  cookie.js – simplifying cookies in JavaScript
cookie.js is a tiny JavaScript library that simplifies cookies. It is capable of setting, getting and removing cookies, accepts a variety of parameters, and supports chaining. cookie.js is released under the [MIT/X11 license](https://github.com/js-coder/cookie.js/blob/master/license). It doesn't have any dependencies and if minified it's only ~1.4 KiB large (~0.7 KiB if minified and gzipped).

This script will add an object called `cookie` to your global scope. 

## Why would you want to use it?
Working with cookies in JavaScript sucks. `document.cookie` is definitely one of the ugly parts of JavaScript. This library aims to simplify working with cookies and make them more fun to use.

## Usage

Download [cookie.min.js](https://raw.github.com/js-coder/cookie.js/master/cookie.min.js) and include it in your HTML document:

```html
<script src="cookie.min.js"></script>
```

After that you can call any of methods that are explained in the following.

## cookie.set()
You can use the `cookie.set` method to set cookies. The value will automatically be escaped for you.

```javascript
cookie.set('key', 'value');
```

You can also set several values at once:

```javascript
cookie.set({
   key1: 'value1',
   key2: 'value2'
});
```

If you need more options, like setting the expiry date, you can add an object with options as the third parameter:

```javascript
cookie.set('key', 'value', {
   expires: 60 * 60 * 24 * 7, // expires in one week
});
```

The following fields can be added to the mentioned object:

 - `expires`: Either a number containing the seconds until the expiry, a
   date in the GMTString format or a date object. (e.g.: `60 * 60 * 24 * 7` for a week.) If you omit this field the cookie will be removed when the browser closes.
 - `domain`: Allow other domains to access your cookie. (e.g.: `example.com`.) The default value is the current domain.
 - `path`: Limit the access to the cookie to some path. (e.g.: `dir/`.) The default value is the current domain.
 - `secure`: A boolean indicating whether the cookie shall only be accessable over a secure connection.

## cookie.get()
This method allows you to retrieve your cookies, you can use it by simply passing the key of the cookie:

```javascript
cookie.get('key');
```

Passing just one key like this will return a string, containing the value of the cookie. You can also pass an array of keys:

```javascript
cookie.get['key1', 'key2']);
```

This will always return an object. The keys of this object will be the keys you passed and the values are the corresponding values.

In case you want to add a default value you can use the second parameter. The default value will be returned if the cookie*(s)* could not be found:

```javascript
cookie.get('key', 'default value');
```

This also works with several keys:

```javascript
cookie.get(['key1', 'key2'], 'default value');
```

`cookie()` is a shortcut for `cookie.get()`. 

```javascript
cookie.get('key'); 
// is the same as
cookie('key');
```

## cookie.all()

```javascript
var cookies = cookie.all()
```

To get all of the currently saved cookies simply call `cookie.all`. In this case the variable `cookies` will return an object with all the current cookies.

## cookie.remove()

This method allows you to remove cookies. It accepts an infinite number of keys or an array of keys.

```javascript
cookie.remove('key');
cookie.remove('key1', 'key2');
cookie.remove(['key1', 'key2']);
```

## cookie.empty()

Sometimes you may want to remove all cookies. Simply call `cookie.empty()` and every cookie will be removed.

## cookie.enabled()

This method allows you to test if the cookies are enabled. It returns `true` if you can work with cookies and `false` if you cannot. You might want to use a fallback if they are disabled:

```javascript
if (cookie.enabled()) {
   // Do stuff with cookies
} else {
   // Display error message or use localStorage
}
```

## Chaining

The methods `set`, `remove` and `empty` return the cookie object and therefore enable chaining. 

```javascript
cookie.empty().set('key', 'value').set('key2', 'value2').remove('key1');
```

## Contribute

If you find any bugs in this script or have ideas how to improve it please let me know. You are also very welcome to contribute to the code here on github.