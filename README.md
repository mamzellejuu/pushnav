- - -


#Pushnav

Version: Alpha

*Pushnav* is a plugin that automates ajax navigation using html5 push-state.

- - -

### Compatibility:

##### HTML5 Browser
- Firefox 4+
- Chrome 8+
- Opera 11.5
- Safari 5.0+
- Safari iOS 4.3+

##### HTML4 Browser
- Internet Explorer 7+


### Dependencies:
- jQuery 1.7.2 (http://jquery.com/)
- History.js (You have to use our version)
- jQuery URL Decoder 1.0 (http://urldecoderonline.com/)

## Still Missing:
- Get back the native anchor behaviour (we disable it to make the plugin works under IE)
- Write the documentation for the transitions


##Documentation in progress

The documentation is still a work in progress.

## Usage

Simply download all dependencies (with the right version). You have to add dependencies to your project like this:
``` javascript
<script src="js/libs/jquery-1.7.2.min.js"></script>
<script src="js/libs/jquery.urldecoder.min.js"></script>
<script src="js/libs/jquery.history.min.js"></script>
```




Pushnav is packaged as a single javascript file which can be loaded either as a script tag in the browser. Simply download the latest stable release from GitHub and add it to your project like this:
``` javascript
<script src="js/pushnav.js"></script>
```


#### Initialization

The general way to setup it is as follows
``` javascript
$.pushnav({

     // Define the default Ajax refresh target (used when they is no target defined)
     defaultTarget: ".pushnav_defaulttarget"     
  
});
```

To instantiate a link, you just have to add data-ajax-target with the DOM selector (a class or id) as value :
``` javascript
<a href="example/description.html" data-ajax-target="#content">Axafiy link</a>
```


###$.pushnav.attach
A second way to instantiate a link could be like this:
####$.pushnav.attach(selector, event, target, getLink)

Param :

	- selector = element selector
	- event = jquery event : click, change, focus
	- target = container to replace
	- getLink (optional) = function to get the destination url : this function must return a url

Like This:
``` javascript
$.pushnav.attach("a", "click", "#content");
```

For a more customs links url generated by javascript you could also do this:
the fourth parameter(optional) is a function receiving the event of the selector and return an url
``` javascript
$.pushnav.attach("a", "click", "#content", function(evt){
    var $this = $(evt.currentTarget).find("option:selected"),
    url = $this.data("pushnav-url");
    return url;
});

```

With pushnav.attach() we can combine it with transition:

###$.pushnav.transition()
``` javascript
$.pushnav.attach().transition()
```

Like this:
``` javascript
$.pushnav
.attach("a", "click", "#content")
.transition('', '', adjustMainMenu)
.transition('things', 'home', fromThingsToHome)
```

####Plugin's options
| Option        | Default value          | Description                                                                        |
|:--------------|:-----------------------|:-----------------------------------------------------------------------------------|
| defaultTarget | .pushnav-defaulttarget | Define the **default Ajax refresh target** (*used when they is no target defined*) |
| disableNotModern | false | Lets **disable** the plugin on browsers that **do not support pushstate** |
| debug | false | Throw debug trace (in the **console.log**)|

## Events
#### Events available

| event                             | When it occurs?                                                                     |
|:----------------------------------|:------------------------------------------------------------------------------------|
| state_change.pushnav              | When the state change (*Triggered* ***before*** *we load* ***new content***)        |
| content_change.pushnav            | When the content is loaded with ajax and the content is already affected to the DOM |
| content_loadingfail.pushnav       | When the content fail to load in ajax                                               |
| content_startloading.pushnav      | When the content start to load in ajax                                              |
| content_loadingcompleted.pushnav  | When the content completed to load                                                  |

#### How to listen
``` javascript
$(document).on("content_change.pushnav", function(event, params) {
   // Insert your script here
});
```

## Notice
To make the plugin compatible with Internet Explorer, we disabled the native anchor behaviour (*the page doesn't scroll to the anchor position*).For all anchor href in the current page, we dynamically add this at the end "?isAjax=false&swaptarget=currentpage_url"

If you create dynamically traditionnal anchor tag, you have to add "?isAjax=false&swaptarget=currentpage_url", like this:
``` javascript
<a href="#myAnchor?isAjax=false&swaptarget=currentpage_url">Anchor Link</a>
```



## Authors
- Julie Cardinal
- Mathieu Sylvain

## License
Licensed under the MIT license.
