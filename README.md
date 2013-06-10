# [minimit-anima](http://www.minimit.com/projects/code/minimit-anima)
#### Jquery plugin to animate with css3 transforms and transitions

My website [minimit.com](http://www.minimit.com) and my [twitter](http://twitter.com/beaver82minimit)

Description
-------
Hardware accelerated css3 animations with fallback for older browsers.

It's built to have fast animation execution and it has an Api very similar to Jquery animate.

By default the plugin do automatic fallback animation on browsers not supporting transitions or transform3d, and instant animation on browser not supporting transforms.

You can specify a different animations based on the browser support using anima2d and anima3d, for example to have a specific animation on ie9- use anima2d, on ie10+ use anima3d.

It also does scale, rotate and skew on browsers without transform3d thanks to <a href="https://github.com/louisremi/jquery.transform.js" target="_blank">jquery.transform.js</a> included in the plugin.

Usage
-------

``` javascript
anima(properties:object, duration:number, easing:string, options:object);
anima2d(properties:object, duration:number, easing:string, options:object);
anima3d(properties:object, duration:number, easing:string, options:object);
```

The properties you can animate can be any css (use string if it's not a valid javascript variable like {"margin-top":500}) or transform like x, y, z, skew, skewX, skewY, scale, scaleX, scaleY, scaleZ, rotate, rotateX, rotateY, rotateZ, perspective
The easing property can be a custom bezier or a preset like linear, ease, easeIn, easeOut, easeInOut, easeInQuad, easeInCubic, easeInQuart, easeInQuint, easeInSine, easeInExpo, easeInCirc, easeInBack, easeOutQuad, easeOutCubic, easeOutQuart, easeOutQuint, easeOutSine, easeOutExpo, easeOutCirc, easeOutBack, easeInOutQuad, easeInOutCubic, easeInOutQuart, easeInOutQuint, easeInOutSine, easeInOutExpo, easeInOutCirc, easeInOutBack

``` javascript
$(".mydivs").anima({x:100}); // instant animation of transformX
$(".mydivs").anima({scale:0.8}, 800, ".19,1,.22,1"); // animation of scale with duration and custom easing
$(".mydivs").anima({"margin-top":500}, 200, ".19,1,.22,1", {complete:function(){$(this).css("display","none");}}); // example with css property animation and complete function
$(".mydivs").anima3d({x:200}, 800).anima2d({x:100}, 800); // different animations based on browser support of transition and transform3d
$(".mydivs").anima({x:200}, 800, "linear", {skipNoSupport:true}); // skip the animation on browser without transform support
```

License
-------
Licensed under MIT licenses.

© 2013 Minimit
