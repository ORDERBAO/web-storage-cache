# WebStorageCache  
[![Build Status](https://travis-ci.org/WQTeam/web-storage-cache.svg?branch=master)](https://travis-ci.org/WQTeam/web-storage-cache)
[![Circle CI](https://circleci.com/gh/WQTeam/web-storage-cache.svg?style=svg)](https://circleci.com/gh/WQTeam/web-storage-cache)
[![npm](https://img.shields.io/npm/dt/web-storage-cache.svg)]()
<a href='https://gitter.im/WQTeam/web-storage-cache'>
<img src='https://badges.gitter.im/Join%20Chat.svg' alt='Gitter Chat' />
</a>

WebStorageCache backed by [storage interface](http://www.w3.org/TR/webstorage/#storage).  

### Language
[中文](https://github.com/WQTeam/web-storage-cache/blob/master/README_zh_CN.md)

# Usage

[Download](https://github.com/WQTeam/web-storage-cache/releases) the latest WebStorageCache from GitHub.

To use WebStorageCache, just drop a single JavaScript file into your page:
```html
<script src="src/web-storage-cache.js"></script>
<script>
// create WebStorageCache instance.
var wsCache = new WebStorageCache();
// cache 'wqteam' at 'username', expired in 100 seconds
wsCache.set('username', 'wqteam', {exp : 100});
</script>
```
You can also use WebStorageCache with RequireJS:
```javascript
define(['web-storage-cache'], function(WebStorageCache) {
    // create WebStorageCache instance.
    var wsCache = new WebStorageCache();
    // cache 'wqteam' at 'username', expired in 100 seconds
    wsCache.set('username', 'wqteam', {exp : 100});
});
```

## Demo
```javascript
var wsCache = new WebStorageCache();

// cache 'wqteam' at 'username', expired in 100 seconds
wsCache.set('username', 'wqteam', {exp : 100});

// deadline in  May 18 2015
wsCache.set('username', 'wqteam', {exp : new Date('2015 5 18')});

// get 'username'
wsCache.get('username');

// cache an object literal - default uses JSON.stringify under the hood
wsCache.set('user', { name: 'Wu', organization: 'wqteam'});

// Get the cache object - default uses JSON.parse under the hood
var user = wsCache.get('user');
alert(user.name + ' belongs to ' + user.organization);

// delete 'username'
wsCache.delete('username');

// manually delete all expires CacheItem. return deleted key's array.
wsCache.deleteAllExpires();

// Clear all keys
wsCache.clear();

// Set a new expiration time for an existing key.
wsCache.touch('username',  1);

// Add key-value item to cache, success only when the key is not exists in cache
wsCache.add('username2', 'wqteam', {exp : 1});

// Replace the key's data item in cache, success only when the key's data item is exists in cache.
wsCache.replace('username', 'new wqteam', {exp : 1});

// check if the 'storage' supported by the user browser. if it`s not supported by the user browser all the  WebStorageCache API methods will do noting.
wsCache.isSupported();

```
# API

## Constructor
```javascript
var wsCache = new WebStorageCache({
    // [option] 'localStorage', 'sessionStorage', window.localStorage, window.sessionStorage or
    // other storage instance implement [Storage API].
    // default 'localStorage'.
    storage: 'localStorage',
    // [option] //An expiration time, in seconds. default never .
    exp: Infinity
});
```

## isSupported
Check if the `Storage API` be supported by the browser.
```javascript
wsCache.isSupported(); // return Boolean.
```

## set
Set a new `CacheItem` to `storage`.
```javascript
wsCache.set(key, value, options);
```

## get
Get a cached item by `key`.
```javascript
wsCache.get(key);
```

## delete
Delete a cached item by 'key'.
```javascript
wsCache.delete(key);
```
## deleteAllExpires
Delete all expired item.
```javascript
wsCache.deleteAllExpires();
```
## clear
Delete all items in the storage, not only save by `wsCache`.
```javascript
wsCache.clear();
```
## touch
Set a new expire time for the cache item.
```javascript
wsCache.touch(key, exp: 1);
```
## add
add a new cache item to the `storage`,success only when the key is not exists.
```javascript
wsCache.add(key, value, options);
```
## replace
Replace the key's cache item in storage,success only when the key's data item is exists in memcached.
```javascript
wsCache.replace(key, value, options);
```
