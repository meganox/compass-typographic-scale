Compass Typographic Scale
=========================

##### Easy setting of font sizes with pleasing typographical heirarchy, without needing to do any calculations.

Note: This extension is based on the forthcoming Compass 0.13.3 which is still
in alpha. You can install the correct version with:

`$ gem install --pre -v 0.13.3.alpha.4 compass` 

Font sizes are set based on a typographic scale, using an arbitrary conversion
factor. By default, 16px on screen at arms length is considered to be equivalent
to 11pt on the printed page, which would normally be viewed from much closer.
Note that this number is arbitrary and only serves to allow altering the font
sizes of elements while maintaining a typographical relationship.

This extension requires the vertical rhythm module and uses its `$base-font size
/ $base-line-height` variables. It uses that module to set line heights, however
it doesn't force the use of vertical rhythm elsewhere.

An example typographic scale: `6, 7, 8, 9, 10, 11, 12, 14, 16, 18, 21, 24, 36, 48, 60, 72`

Installation
------------
Simply put the extension inside the `extensions` directory at the top level of
your compass project. The extension directory can be customised with the
`extensions_dir` directive in your Compass `config.rb`. A gem may be available
in future.

Set `$base-font-size` (default 16px) and `$base-line-height` (default 24px)
and optionally `$rhythm-unit` and `$relative-font-sizing`. See the [Compass
vertical rhythm documentation][1] for more details.
[1]: http://compass-style.org/reference/compass/typography/vertical_rhythm/

Now set `$ts-header-scale` to the desired points scale (default: 36 24 21 18
16 14) and if you are using vertical rhythm set `$ts-rhythm` to the desired
rhythm for top and bottom margins and padding (default: 0 1 1 0).

You can now import the plugin: `@import 'compass-typographic-scale';`

which will also import vertical-rhythm.

Set up base font-size / line-height on the html element using the Vertical
Rhythm module:

`@include establish-baseline;`

this is recommended even if you're not using vertical rhythm.


Variables
---------
- `$ts-header-scale` – The relative scale for headings, in points
- `$ts-rhythm` – Rhythm to pass to vertical-rhythm  
(margin-top padding-top padding-bottom margin-bottom)
- `$ts-base-font-size-points-equiv` – Scale factor i.e. the point size in print that's equivalent to 16px default font size
- `$ts-double-stranded` – Whether to output classes as well as element selectors
- `$ts-double-stranded-classnames` – Class names to use
- `$ts-use-silent-classes` – Whether to use sass pseudo-classes (for use with @extend)
- `$ts-outsize-scale` – An alternate scale
- `$ts-outsize-scale-classnames` – Classnames for alternate scale
- `$ts-outsize-use-silent-classes` – Whether to use sass pseudo-classes


Mixins
------
- `ts-header-scale` – Set h1 - h6 according to the scale
- `ts-header-scale-with-rhythm($rhythm)` – Or with leading/trailing whitespace using rhythm  
`$rhythm` is optional and defaults to `$ts-rhythm`
- `ts-header-scale-with-spacing` – Alias for above
- `ts-scale($level)` – Set any element to a font size on the scale  
where `$level` is the index (counting from one) of the required size in the `$ts-header-scale` list
- `ts-scale-with-rhythm($level, $rhythm)` – With whitespace using rhythm  
- `ts-scale-with-spacing` – Alias for above

The mixin `ts-outsize-scale` gives you an arbitrary scale set up with the
`$ts-outsize-*` variables which you can use in your html or with @extend
independently of the header scale. Of course it also has rhythm versions.

Also included is a convenience function which mirrors Compass' headers()
function but with support for double stranding. Use it like:

`#{ts-headings(1 2)} { /* rules */ }`

Output: `h1, .h1, h2, .h2 { /* rules */ }`

Note that the syntax is slighty different, it accepts a list of header levels
whereas Compass' headings() expects a range.
