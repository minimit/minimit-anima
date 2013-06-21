# [minimit-anima](http://www.minimit.com/projects/code/minimit-anima-plugin)

**Hardware accelerated css3 animations with fallback on older browsers.**

It's built to have fast animation execution, and it has an api similar to jquery animate, with animations queueing.

By default the anima method do **automatic fallback animation** on browsers without transitions or transform3d.

It also does scale, rotate and skew animations on browsers without transitions thanks to <a href="https://github.com/louisremi/jquery.transform.js" target="_blank">jquery.transform.js</a> included in the plugin.

#### Browser support
IE9+, Firefox 3.5+, Safari 3+, Opera 10.5+, Chrome, Iphone, Ipad, Android, Windows Phone.

Api
-------

Use the **anima** method to have automatic fallback:

``` javascript
anima(properties:object, duration:number, easing:string, options:object);
```

Use the **anima3d** method to execute animations only on browser with transitions and transform3d:

``` javascript
anima3d(properties:object, duration:number, easing:string, options:object);
```

Use the **anima2d** method to execute animations only on browsers without transitions or transform3d:

``` javascript
anima2d(properties:object, duration:number, easing:string, options:object);
```

Use the **stopAnima** method to stop current running animations:

``` javascript
stopAnima(clearQueue:boolean, jumpToEnd:boolean);
```

Use the **delayAnima** method to delay the animations queue:

``` javascript
delayAnima(time:number);
```

Use the **clearAnima** method to clear the queued animations:

``` javascript
clearAnima();
```

Parameters
-------

**Instant animations** are default:

``` javascript
$(this).anima({x:20, y:20});
```

You can specify a **duration**, default easing is "easeOut":

``` javascript
$(this).anima({x:20, y:20}, 400);
```

You can specify a **custom easing** or a **preset easing**:

``` javascript
$(this).anima({x:20, y:20}, 400, ".19,1,.22,1");
$(this).anima({x:0, y:0}, 400, "linear");
```

You can set a function to execute on animation **complete**:

``` javascript
$(this).anima({x:20, y:20}, 400, ".19,1,.22,1", {complete:function(){alert("done");}});
```

You can **skip automatic fallback** animations:

``` javascript
$(this).anima({x:20, y:20}, 400, ".19,1,.22,1", {skip2d:true});
```

The properties you can animate can be:
* **any css**, use string if it has a hypen like {"margin-top":20}
* **any transform**, like x, y, z, skew, skewX, skewY, scale, scaleX, scaleY, scaleZ, rotate, rotateX, rotateY, rotateZ, perspective

The easing property can be:
* a **custom bezier**, you can make your own at [cubic-bezier.com](http://cubic-bezier.com).
* a **preset**, like linear, ease, easeIn, easeOut, easeInOut, easeInQuad, easeInCubic, easeInQuart, easeInQuint, easeInSine, easeInExpo, easeInCirc, easeInBack, easeOutQuad, easeOutCubic, easeOutQuart, easeOutQuint, easeOutSine, easeOutExpo, easeOutCirc, easeOutBack, easeInOutQuad, easeInOutCubic, easeInOutQuart, easeInOutQuint, easeInOutSine, easeInOutExpo, easeInOutCirc, easeInOutBack

Usage
-------

####Setup

Include minimit-anima after jQuery:

``` html
<script src='jquery.js'></script>
<script src='minimit-anima.min.js'></script>
```

####Css

You can animate **any css** (still have to test all) listed [here](http://developer.mozilla.org/en-US/docs/Web/CSS/CSS_animated_properties?redirectlocale=en-US&redirectslug=CSS%2FCSS_animated_properties):

``` javascript
$(this).anima({"padding-left":20, opacity:0.6}, 400);
```

####Translate

Use **x** , **y**, or **z** property:

``` javascript
$(this).anima({x:20, y:20}, 400);
```

####Scale

You can use **scale**, **scaleX**, **scaleY** or **scaleZ**:

``` javascript
$(this).anima({scaleX:0.6, scaleY:0.6}, 400);
```

####Rotate

You can use **rotate**, **rotateX**, **rotateY** or **rotateZ**:

``` javascript
$(this).anima({rotate:"45deg"}, 400);
```

####Skew

You can use **skew**, **skewX** or **skewY**:

``` javascript
$(this).anima({skewX:"20deg", skewY:"20deg"}, 400);
```

####Stop

Stop the current running animation:

``` javascript
$(this).anima({x:20}, 400); // this get stopped
$(this).delayAnima(400).anima({y:20}, 400);
$(this).stopAnima();
```

Stop the current running animations and clear all delayed animations:

``` javascript
$(this).anima({x:20}, 400); // this get stopped
$(this).delayAnima(400).anima({y:20}, 400); // this get cleared
$(this).stopAnima(true);
```

Stop the current running animations and jump to end:

``` javascript
$(this).anima({x:20}, 400); // this get stopped and jumped to end
$(this).delayAnima(400).anima({y:20}, 400);
$(this).stopAnima(false, true);
```

####Delay

Delay the animations queue:

``` javascript
$(this).delayAnima(200).anima({x:20}, 400);
$(this).delayAnima(200).anima({y:20}, 400);
```

####Clear

Clear all delayed animations that have not yet been run:

``` javascript
$(this).anima({x:20}, 400);
$(this).delayAnima(400).anima({y:20}, 400); // this get cleared
$(this).clearAnima();
```

####3D and 2D

Do different animations based on browser support of transition and transform3d:

``` javascript
$(this).anima3d({rotateX:"10deg", rotateY:"10deg", rotateZ:"10deg"}, 800).anima2d({scale:0.8}, 800);
```

Tricks and fixes
-------

Trigger **hardware accelerated** animations, by animating the **z** and the **perspective** property:

``` javascript
$(this).anima({x:200, z:0, perspective:1000}, 800);
```

Fix browser bug in chrome, 1 pixel shift:

``` javascript
$(this).css("backface-visibility", "hidden");
```

Acknowledgements
-------
Copyright © 2013 Riccardo Caroli. Licensed under [MIT license](http://www.opensource.org/licenses/mit-license.php).

This plugin uses some open source code:
* Modernizr http://modernizr.com
* Bez http://github.com/rdallasgray/bez
* Transform http://github.com/louisremi/jquery.transform.js
