# minimit-anima

**Hardware accelerated css3 animations with fallback on older browsers.**

It's built to have fast animation execution, and it has an api similar to jquery animate, with animations queueing.

By default the anima method do **automatic fallback animations** on browsers without transitions or transform3d, and instant animations on browsers without transform.

It also does scale, rotate and skew animations on browsers without transitions thanks to <a href="https://github.com/louisremi/jquery.transform.js" target="_blank">jquery.transform.js</a> included in the plugin.

#### Browser support
IE8+, Firefox 3.5+, Safari 3+, Opera 10.5+, Chrome, Iphone, Ipad, Android, Windows Phone.

#### [Demo](http://htmlpreview.github.io/?http://github.com/minimit/minimit-anima/blob/master/demo.html)

My website [minimit.com](http://www.minimit.com) and my [twitter](http://twitter.com/beaver82minimit).

Api
-------

Include minimit-anima after jQuery (v1.6.4+):

``` html
<script src='jquery.js'></script>
<script src='minimit-anima.min.js'></script>
```

Use the **anima** method to have automatic fallback:

``` javascript
anima(properties:object, duration:number, easing:string, options:object);
```

Combine the **anima3d** method to execute animations only on browser with transitions and transform3d, with the **anima2d** method to execute animations on fallback browsers:

``` javascript
anima3d(properties:object, duration:number, easing:string, options:object);
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
$(this).anima({x:20, y:20}, 400, ".19,1,.22,1", {complete:function(){$(this).anima({x:-20, y:-20}, 400, "linear");}});
```

You can skip instant animations on browser with no transforms support:

``` javascript
$(this).anima({x:20, y:20}, 400, ".19,1,.22,1", {skipInstant:true});
```

The properties you can animate can be:
* **any css**, use string if it has a hypen like {"margin-top":20}
* **any transform**, like x, y, z, skew, skewX, skewY, scale, scaleX, scaleY, scaleZ, rotate, rotateX, rotateY, rotateZ, perspective

The easing property can be:
* a **custom bezier**, you can make your own at [cubic-bezier.com](http://cubic-bezier.com).
* a **preset**, like linear, ease, easeIn, easeOut, easeInOut, easeInQuad, easeInCubic, easeInQuart, easeInQuint, easeInSine, easeInExpo, easeInCirc, easeInBack, easeOutQuad, easeOutCubic, easeOutQuart, easeOutQuint, easeOutSine, easeOutExpo, easeOutCirc, easeOutBack, easeInOutQuad, easeInOutCubic, easeInOutQuart, easeInOutQuint, easeInOutSine, easeInOutExpo, easeInOutCirc, easeInOutBack

Properties
-------

####Css

You can animate **any css** (still have to test all) listed [here](http://developer.mozilla.org/en-US/docs/Web/CSS/CSS_animated_properties?redirectlocale=en-US&redirectslug=CSS%2FCSS_animated_properties):

``` javascript
$(this).anima({"padding-right":"20px", opacity:0.6}, 400);
```

####Translate

Use **x** , **y**, or **z** property:

``` javascript
$(this).anima({x:20, y:20}, 400); // px is default unit for x, y, z
$(this).anima({x:"0%", y:"0%"}, 400);
```

####Scale

You can use **scale**, **scaleX**, **scaleY** or **scaleZ**:

``` javascript
$(this).anima({scaleX:0.6, scaleY:0.6}, 400);
$(this).anima({scale:"1, 1"}, 400);
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
$(this).anima({skew:"0deg, 0deg"}, 400);
```

####Transform origin

You can set **transform-origin** on the element that you animate:

``` javascript
$(this).anima({"transform-origin":"0% 0%"});
$(this).anima({rotate:"45deg"}, 400);
```

Utils
-------

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
$(this).anima({x:20, y:0}, 400);
$(this).delayAnima(400).anima({x:20, y:20}, 400); // this get delayed
$(this).delayAnima(400).anima({x:0, y:20}, 400); // this get delayed
```

####Clear

Clear all delayed animations that have not yet been run:

``` javascript
$(this).anima({x:20}, 400);
$(this).delayAnima(400).anima({y:20}, 400); // this get cleared
$(this).clearAnima();
```

Advanced usage
-------

####Fix chrome and safari flicker

Fix chrome 1 pixel shift and safari flicker:

``` javascript
$(this).css("backface-visibility", "hidden");
```

####Hardware acceleration

Trigger hardware accelerated animations by adding the **z** and the **perspective** properties:

``` javascript
$(this).anima({x:200, z:0, perspective:1000}, 800);
```

####3D and 2D

Do different animations based on browser support of transition and transform3d:

``` javascript
$(this).anima3d({rotateX:"100deg", rotateY:"100deg", rotateZ:"100deg"}, 400).anima2d({scale:0.6}, 400);
$(this).anima3d({rotateX:"0deg", rotateY:"0deg", rotateZ:"0deg"}, 400).anima2d({scale:1}, 400);
```

####Transform values retain

Since transform animations haven't persistent values, you have to include them in every anima if you want to retain the values:

``` javascript
$(this).anima({x:20, y:20});
$(this).anima({x:20, y:20, rotate:"40deg"}, 400);
```

Or it will transform to the default value like this:

``` javascript
$(this).anima({x:20, y:20});
$(this).anima({rotate:"40deg"}, 400);
```

It's different in some circumstances like on 3D animations.

####3D transform values retain

Because browsers inconsistency, use this syntax to avoid browser bugs:
* put the perspective before the animations and in every animate (firefox fix)
* put the positions in each animate also if they aren't changing (ie10 fix)

``` javascript
$(this).anima({perspective:"100px", rotateX:"0deg", rotateY:"0deg"});
$(this).anima({perspective:"100px", rotateX:"180deg", rotateY:"0deg"}, 400);
$(this).anima({perspective:"100px", rotateX:"180deg", rotateY:"180deg"}, 400);
```

There is an alternate version that fixes ie10 keeping the animation free on other browsers (they retain the 3D value):

``` javascript
if(typeof document.body.style.msPerspective != "undefined"){ // ie10
	$(this).anima({perspective:"100px", rotateX:"0deg", rotateY:"0deg"});
}else{
	$(this).anima({perspective:"100px"});
}
if(typeof document.body.style.msPerspective != "undefined"){ // ie10
	$(this).anima({perspective:"100px", rotateX:"180deg", rotateY:"0deg"}, 400);
}else{
	$(this).anima({perspective:"100px", rotateX:"180deg"}, 400);
}
if(typeof document.body.style.msPerspective != "undefined"){ // ie10
	$(this).anima({perspective:"100px", rotateX:"180deg", rotateY:"180deg"}, 400);
}else{
	$(this).anima({perspective:"100px", rotateZ:"180deg"}, 400);
}
```

If ie10 do strange things with the transform, just put the starting values before on a anima with duration 10

``` javascript
if(typeof document.body.style.msPerspective != "undefined"){ // ie10
    path.anima({perspective:"800px", rotateX:"0deg", rotateY:"0deg", rotateZ:"0deg", scale:"1", opacity:1}, 10); // IE10 fix
}
path.anima({perspective:"800px", rotateX:"0deg", rotateY:"90.1deg", rotateZ:"0deg", scale:"0.8", opacity:0.6}, 400, ".19,1,.22,1");
```

Acknowledgements
-------
Copyright © 2013 Riccardo Caroli. Licensed under [MIT license](http://www.opensource.org/licenses/mit-license.php).

This plugin uses some open source code:
* Modernizr http://modernizr.com
* Bez http://github.com/rdallasgray/bez
* Transform http://github.com/louisremi/jquery.transform.js
