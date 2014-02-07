# Palantír Pocket

_**Note:** this is currently under heavy development!_

<<<<<<< HEAD
---

=======
>>>>>>> 588f1cb1471e31989e6c74569aaf30d4298a3786
## Table of Contents

1. [Introduction](#introduction)
1. [Setting Up](#setting-up)
	1. [For iOS Chrome](#for-ios-chrome)
	1. [Parameters](#parameters)
	1. [The JSONP data file](#the-jsonp-data-file)
1. [Bookmarklet Ideas](#bookmarklet-ideas)
<<<<<<< HEAD
	1. [Open in Chrome and return to Safari](#open-in-chrome-and-return-to-safari)

---
=======
>>>>>>> 588f1cb1471e31989e6c74569aaf30d4298a3786

## Introduction

The original [Palantír](http://mynameisrienk.com/?palantir) is a Chrome extension to quickly open bookmarks, bookmarklets and apps. Using bookmarklets in iOS Chrome (and to a lesser extend in iOS Safari) is quite cumbersome, to say the least. **Palantír Pocket** will be a simple solution to implement bookmarklets on your iOS device!

**Palantír Pocket** will launch an in-screen window with your preset bookmarks/bookmarklets. The bookmarks are imported from a json(p) file you will have to provide (since your bookmarks are not accessible using in-browser javascript).

By using the power of custom URL schemes (see [this git repository](https://github.com/christopherdwhite/iosWorkflows) and [handleopenurl.com](http://handleopenurl.com/)) and the [x-callback-url](http://x-callback-url.com/) specification, you can even use bookmarklets to interact with other apps!

[↩ Table of Contents](#table-of-contents)

## Setting Up

Just create a bookmark with the following URL:

<<<<<<< HEAD
	javascript:(function(){if(typeof%20palantirCallback%20!='function'){PP_FILE='//mynameisrienk.github.io/palantirpocket/data.json';PP_SCRIPT=document.createElement('SCRIPT');PP_SCRIPT.type='text/javascript';PP_SCRIPT.src='//mynameisrienk.github.io/palantirpocket/script.js';document.getElementsByTagName('head')[0].appendChild(PP_SCRIPT);}})();
=======
	javascript:(function(){if(typeof%20palantirCallback%20!='function'){PP_SCRIPT=document.createElement('SCRIPT');PP_SCRIPT.type='text/javascript';PP_SCRIPT.src='//mynameisrienk.github.io/palantirpocket/script.js';document.getElementsByTagName('head')[0].appendChild(PP_SCRIPT);}})();
>>>>>>> 588f1cb1471e31989e6c74569aaf30d4298a3786

… displayed as not url-encoded Javascript:

	javascript:(function() {
		if (typeof palantirCallback != 'function') { 
<<<<<<< HEAD
			PP_FILE   = '//mynameisrienk.github.io/palantirpocket/data.json';
=======
>>>>>>> 588f1cb1471e31989e6c74569aaf30d4298a3786
			PP_SCRIPT = document.createElement('SCRIPT');
			PP_SCRIPT.type = 'text/javascript';
			PP_SCRIPT.src = '//mynameisrienk.github.io/palantirpocket/script.js';
		document.getElementsByTagName('head')[0].appendChild(PP_SCRIPT);
		}
	})();

[↩ Table of Contents](#table-of-contents)

### For iOS Chrome

Bookmarklets in the mobile Chrome can only be launched through the omnibox. Therefore, give your bookmarklet a simple name, like `PP`. To launch it type `PP` into the omnibox and select the bookmarklet from the recommendations menu.

[↩ Table of Contents](#table-of-contents)

### Parameters

`PP_FILE` is the URL to your JSONP data file. You can also optionally set the `PP_CSS` variable to the URL for your own CSS stylesheet.

**Please note:** I am working on a solution to easily implement your own JSONP data file for bookmarklets and URL schemes. For now, you will have to host your own JSONP file or use the default one I am curating for my personal use.

[↩ Table of Contents](#table-of-contents)

### The JSONP

The bookmarklets are listed in a JSONP file (iOS doesn't allow for javascript access to your browser's bookmarks) wrapped in a function callback named `palantirCallback`.

The following keys are supported in the object:
* `title` (string; required): the name of the bookmark(let).
* `description` (string | null): a brief description of what the bookmark(let) opens/does.
* `url` (url-encoded string; required): the url/javascript function. Use Chris Zarate's [Bookmarkleter](http://chriszarate.github.io/bookmarkleter/) to easily url-encode your javascript into a bookmarklet url.
* `icon` (string || null): a base64-encoded image string. Use AskApache's [Base64 Image Converter](http://www.askapache.com/online-tools/base64-image-converter/). The image will be resized to 16x16px using CSS3's `background-size` property.

**Example:**

	palantirCallback([
    {
        "title": "Safari to Chrome",
        "description": "Open the current page in Chrome iOS",
        "url": "javascript:(function(){window.location='googlechrome-x-callback://x-callback-url/open/%3Furl='+encodeURIComponent(location.href)+'%26x-source=Safari%26x-success='+encodeURIComponent(location.href);})();",
        "icon": "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABAAAAAQCAYAAAAf8/9hAAAABmJLR0QA/wD/AP+gvaeTAAAACXBIWXMAAAsTAAALEwEAmpwYAAAAB3RJTUUH3gIGFSoGJ67TxQAAA0JJREFUOMtdk0tsVWUQgL/5/3PubXvbQqlAA6YF7IOmVQmmUKqlwRQk8Z1KNIIiJhqNC2JSTNTgQoiahpVGE4nRxphYFy5IiSgSH0CA6sL4SKDVUlRCH7eF9t7b3sc5/xkXhWr8VrOZb2YyMwLw+orlvHZlnMzmVlt68pw7/3DnpsUVZVuNZ+tEVQuZ7HBmJnV87Renz+baNtiiMz84riPPJso4PJsG4NT65vo1y5f8WFRWUo7v5bHW4BxRIYw0W4jn0nNXh8cmN2wZ/GN4QXAj+K72ls31Syu+J+arxD0xnkWMoE7R0BEVAqJcoORDuTQ1ve3Oe9pPyAefqAw31tqT2Ux1Z6ziosYt4nuIbxCxYAAXoapo4IgKIVpwEER8O5WsvrW09IoAdBzbOnjwpUu1N8+KERFMPIbL5ynf+SjiK6mLvVgbRyRABMRoEPjhbzXvjK6Xlp476qqalw4Vp0P27xum1I9Tcu92vtn9KoPjeVCoryrhvuLn8XNH8WKKGMUI7H8ru8w27Krv8ku97dliaytHZqm4MMnpgx/RPzBKLh+SzuT4ZWSKRNXjNMXfhchBBKiwdo0/ZYxIdaSodUrf3hqC1haOXUiRKTiSMzkmprOksyFvfzUEXhX/IYp7ttFzgToiFAPWKf13e+TmclydzSIioIpTEByi2euLU1SNFPLWmSAV/E6Ef0N7tmmOB5ojRsbHmEpdYyo9w+XkBG8+tJIonAQUEKLAk+SEDJhfPz3/pZtTo+G8IGZ9jhQO8PFTjZSTYhEzfPh0E3WuHTQClMhZsukY6568dlgANvW09ZWtSnR5xcYT+++Q5bEEUSHCn5mgt+mn+cqhJT8XK1z+M3a0cedol2w81GYGus94He9tyccrPLUlImIFMSAizGbg64ZTaCSEgU9h1nPTk8W25pG/zIE9i+dPWVWJrUosa9nbMp5YEgtNEdb4RsQo7V6SFyr/hsBoPusH08mYfa5nbOWJ47WTVO1yC79w/7nHpL+1T297eWNvSWXR7uJSH2PgyIohUnmPTAZGk9rb0T2yR0dut7L6Z8f/WbSuUg7p+wag+sHVW595saH7s1eq973xxE2d853uMDvuSojq5ws5/wCJenBwRGyXfQAAAABJRU5ErkJggg=="
    }]);

[↩ Table of Contents](#table-of-contents)

## Bookmarklet Ideas

Tweet your bookmarklet "URLs" to [@MyNameIsRienk](http://twitter.com/mynameisrienk/) or add them yourself as new pull requests. Please keep the formatting the same.

[↩ Table of Contents](#table-of-contents)

### Open in Chrome and return to Safari

Open the current web page in Chrome for iOS and display a button to return to Safari (from [iosWorkflows](https://github.com/christopherdwhite/iosWorkflows/blob/master/_bookmarklets.md#open-in-chrome--return-to-safari)

    javascript:window.location='googlechrome-x-callback://x-callback-url/open/?url='+encodeURIComponent(location.href)+'&x-source=Safari&x-success='+encodeURIComponent(location.href);
