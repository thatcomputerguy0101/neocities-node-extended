# Neocities-Extended Node.js Client Library
A node.js library for interacting with the [Neocities](https://neocities.org/api) api that actually has more capabilities than the original api itself.

## Installation

WARNING - This module is not yet on NPM; the following command will not work
```
$ npm install neocities-extended
```

Instead, clone this repository where you want it to be installed, and reference the folder directly in the require statement.

## Usage

First, require the library and initialize:

``` javascript
var Neocities = require('neocities-extended') // or reference to the folder
var api = new Neocities('YOURUSERNAME', 'YOURPASSWORD')
```

### Uploading files to your site

``` javascript
// local file path is ./index.js, saved on site as derp.js

api.upload([
  {name: 'derp.js', path: './index.js'}
           ], function(resp) {
  console.log(resp)
})
```

### Downloading files from your site

``` javascript
// site path is derp.js, saved on client as index.js

api.download([
    {name: 'derp.js', path: 'index.js'}
             ], function(resp) {
    console.log(resp)
})
```

### Deleting files from your site

``` javascript
api.delete(['derp.js'], function(resp) {
  console.log(resp)
})
```

### List the files on your site

``` javascript
api.list('dirname', function(resp) {
    console.log(resp)
})
```

### Get site info (hits, et cetera)

``` javascript
api.info(function(resp) {
  console.log(resp)
})
```

``` javascript
api.info('youpi', function(resp) {
  console.log(resp)
})
```

### Use an API Key

The API key is a more secure way to upload data, since it doesn't store or send your username or password. First, Log in normally with a callback for the key option. (This then uses the key once it is aquired instead of your username and password.)

``` javascript
var api = new Neocities('YOURUSERNAME', 'YOURPASSWORD', {key: function(key) {/* store your key here */}})
```

Then, use the key instead of the username or password the next time you log in.

``` javascript
var api = new Neocities('YOURAPIKEY')
```

### Pushing a folder

``` javascript
// foo is the local folder, images is what it will be named on your site
// hidden.json is not uploaded, nor any file ending with .conf.json

api.push('foo/', 'images/', ['hidden.json', /\.conf\.json$/])
```

### Pulling a folder

Similar to download, but for folders

``` javascript
// same argument syntax as push

api.pull('foo/', 'images', ['site.png'])
```
