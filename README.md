# Palantír Pocket

_**Note:** this is currently under heavy development!_

## Table of Contents

1. [Introduction](#introduction)
1. [Setting Up](#setting-up)
1. [Bookmarklet Ideas](#bookmarklet-ideas)

## Introduction

The original [Palantír](http://mynameisrienk.com/?palantir) is a Chrome extension to quickly open bookmarks, bookmarklets and apps. Using bookmarklets in iOS Chrome (and to a lesser extend in iOS Safari) is quite cumbersome, to say the least. **Palantír Pocket** will be a simple solution to implement bookmarklets on your iOS device!

**Palantír Pocket** will launch an in-screen window with your preset bookmarks/bookmarklets. The bookmarks are imported from a json(p) file you will have to provide (since your bookmarks are not accessible using in-browser javascript).

By using the power of custom URL schemes (see [this git repository](https://github.com/christopherdwhite/iosWorkflows) and [handleopenurl.com](http://handleopenurl.com/)) and the [x-callback-url](http://x-callback-url.com/) specification, you can even use bookmarklets to interact with other apps!

[↩ Table of Contents](#table-of-contents)

## Setting Up


`javascript:(function(){if(typeof%20palantirCallback=='function'){document.getElementById('palantir').style.display=%22block%22;}else{PP_SCRIPT=document.createElement('SCRIPT');PP_SCRIPT.type='text/javascript';PP_SCRIPT.src='http://mynameisrienk.github.io/palantirpocket/script.js';document.getElementsByTagName('head')[0].appendChild(PP_SCRIPT);}})();`

… displayed as not url-encoded Javascript:

	javascript:(function() {
		if (typeof palantirCallback == 'function') { 
		  document.getElementById('palantir').style.display="block";
		} else {
			PP_SCRIPT = document.createElement('SCRIPT');
			PP_SCRIPT.type = 'text/javascript';
			PP_SCRIPT.src = 'http://mynameisrienk.github.io/palantirpocket/script.js';
		document.getElementsByTagName('head')[0].appendChild(PP_SCRIPT);
		}
	})();

[↩ Table of Contents](#table-of-contents)

### For iOS Chrome

Bookmarklets in the mobile Chrome can only be launched through the omnibox.

[↩ Table of Contents](#table-of-contents)

## Bookmarklet Ideas

Tweet your bookmarklet "URLs" to [@MyNameIsRienk](http://twitter.com/mynameisrienk/) or add them yourself as new pull requests. Please keep the formatting the same.

[↩ Table of Contents](#table-of-contents)

### Open in Chrome and Return to Safari

Open the current web page in Chrome for iOS and display a button to return to Safari (from [iosWorkflows](https://github.com/christopherdwhite/iosWorkflows/blob/master/_bookmarklets.md#open-in-chrome--return-to-safari)

    javascript:window.location='googlechrome-x-callback://x-callback-url/open/?url='+encodeURIComponent(location.href)+'&x-source=Safari&x-success='+encodeURIComponent(location.href);
