# ramda

> "You can call a function with fewer arguments than it expects. It returns a function that takes the remaining arguments."

- Demo: https://petrosh.github.io/ramda
- More info: http://petrosh.it/2016/07/06/ramda-anything-else-would-be-a-bold-face-lie/
- [Ramda 0.21.0 docs](http://ramdajs.com/0.21.0/docs/)
- [RequireJS 2.2.0](http://requirejs.org/docs/start.html)

**Include scripts**

```html
<!-- data-main attribute tells require.js to load main.js after require.js loads. -->
<script data-main="main.js" src="require.js"></script>
```

```js
requirejs.config({
	paths: {
		ramda: 'https://cdnjs.cloudflare.com/ajax/libs/ramda/0.13.0/ramda.min',
		jquery: 'https://ajax.googleapis.com/ajax/libs/jquery/2.1.1/jquery.min',
	},
});

require([
	'ramda',
	'jquery',
],
function(_, $) {
	// app goes here
});
```

**App**

Given a keyword:

1. Pull images from `api.flickr`
2. loop through items and inject images in the page

```js
//  response JSON: [{media: {m: 'http: ... '}}], [{media: {m: 'http: ... '}}], ...

// Utils follow
// url:			string		-> API url
// img:			url				-> img element with src
// setHtml: elements	-> append html elements
// getJSON:	callback	-> apply JSON response to callback

// mediaUrl: object -> string, take media.m from an object
var mediaUrl = _.compose(_.prop('m'), _.prop('media'));

// mediaToImg: string -> element, compose img to url array
var mediaToImg = _.compose(img, mediaUrl);

// images: array -> elements, take JSON response and return elements
var images = _.compose(_.map(mediaToImg), _.prop('items'));

// renderImages: elements -> append, compose setHTML (input = 'section') and images
var renderImages = _.compose(Impure.setHtml('section'), images);

// app: string -> append, compose getJSON (input = renderImages) and url
var app = _.compose(Impure.getJSON(renderImages), url);

// usage
app('javascript');
```
