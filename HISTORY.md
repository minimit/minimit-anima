
v1.33
---------------------
	
	* fixed chaining more than 3 anima
	* removed options.skip2d
	* removed option argument in favor of complete function

v1.32
---------------------

	* fixed complete function get called on browser with no transition support
	* fixed queueing with no transition support
	* fix now anima2d and anima3d don't queue each other

v1.31
---------------------

	* removed 2d and 3d method of delayAnima clearAnima stopAnima
	* fixed transforms on browsers with transforms and no transitions
	* removed instant animation on browser with no transforms support
	* removed options.skipNoSupport and renamed options.skipPartialSupport to options.skip2d
	* fixed css easing on browser with no transition support

v1.3
---------------------

	* removed delay inside anima method in favor of delayAnima
	* fixed queueing and delaying

v1.2
---------------------

	* fixed stopAnima with jumpToEnd false

v1.1
---------------------

	* removed delayAnima in favor of delay inside anima method
	* now animations don't queue, they run asynchronously
	* fixed bug on safary on stop() with jumptoend false
	* removed options backfaceVisibility

v1.0
---------------------

	* Initial official release.
