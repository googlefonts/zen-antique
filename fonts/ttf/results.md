## Fontbakery report

Fontbakery version: 0.7.37

<details>
<summary><b>[1] Family checks</b></summary>
<details>
<summary>⚠ <b>WARN:</b> Is the command `ftxvalidator` (Apple Font Tool Suite) available?</summary>

* [com.google.fonts/check/ftxvalidator_is_available](https://font-bakery.readthedocs.io/en/latest/fontbakery/profiles/universal.html#com.google.fonts/check/ftxvalidator_is_available)
<pre>--- Rationale ---
There&#x27;s no reasonable (and legal) way to run the command `ftxvalidator` of the
Apple Font Tool Suite on a non-macOS machine. I.e. on GNU+Linux or Windows etc.
If Font Bakery is not running on an OSX machine, the machine running Font Bakery
could access `ftxvalidator` on OSX, e.g. via ssh or a remote procedure call
(rpc).
There&#x27;s an ssh example implementation at:
https://github.com/googlefonts/fontbakery/blob/main/prebuilt/workarounds
/ftxvalidator/ssh-implementation/ftxvalidator</pre>

* ⚠ **WARN** Could not find ftxvalidator. [code: ftxvalidator-available]

</details>
<br>
</details>
<details>
<summary><b>[9] ZenAntique-Regular.ttf</b></summary>
<details>
<summary>🔥 <b>FAIL:</b> Font enables smart dropout control in "prep" table instructions?</summary>

* [com.google.fonts/check/smart_dropout](https://font-bakery.readthedocs.io/en/latest/fontbakery/profiles/googlefonts.html#com.google.fonts/check/smart_dropout)
<pre>--- Rationale ---
This setup is meant to ensure consistent rendering quality for fonts across all
devices (with different rendering/hinting capabilities).
Below is the snippet of instructions we expect to see in the fonts:
B8 01 FF    PUSHW 0x01FF
85          SCANCTRL (unconditinally turn on
                      dropout control mode)
B0 04       PUSHB 0x04
8D          SCANTYPE (enable smart dropout control)
&quot;Smart dropout control&quot; means activating rules 1, 2 and 5:
Rule 1: If a pixel&#x27;s center falls within the glyph outline,
        that pixel is turned on.
Rule 2: If a contour falls exactly on a pixel&#x27;s center,
        that pixel is turned on.
Rule 5: If a scan line between two adjacent pixel centers
        (either vertical or horizontal) is intersected
        by both an on-Transition contour and an off-Transition
        contour and neither of the pixels was already turned on
        by rules 1 and 2, turn on the pixel which is closer to
        the midpoint between the on-Transition contour and
        off-Transition contour. This is &quot;Smart&quot; dropout control.
For more detailed info (such as other rules not enabled in this snippet), please
refer to the TrueType Instruction Set documentation.</pre>

* 🔥 **FAIL** The 'prep' table does not contain TrueType instructions enabling smart dropout control. To fix, export the font with autohinting enabled, or run ttfautohint on the font, or run the `gftools fix-nonhinting` script. [code: lacks-smart-dropout]

</details>
<details>
<summary>⚠ <b>WARN:</b> Is the Grid-fitting and Scan-conversion Procedure ('gasp') table set to optimize rendering?</summary>

* [com.google.fonts/check/gasp](https://font-bakery.readthedocs.io/en/latest/fontbakery/profiles/googlefonts.html#com.google.fonts/check/gasp)
<pre>--- Rationale ---
Traditionally version 0 &#x27;gasp&#x27; tables were set so that font sizes below 8 ppem
had no grid fitting but did have antialiasing. From 9-16 ppem, just grid
fitting. And fonts above 17ppem had both antialiasing and grid fitting toggled
on. The use of accelerated graphics cards and higher resolution screens make
this approach obsolete. Microsoft&#x27;s DirectWrite pushed this even further with
much improved rendering built into the OS and apps.
In this scenario it makes sense to simply toggle all 4 flags ON for all font
sizes.</pre>

* ⚠ **WARN** The gasp range 0xFFFF value 0x0A should be set to 0x0F. [code: unset-flags]

</details>
<details>
<summary>⚠ <b>WARN:</b> Check if each glyph has the recommended amount of contours.</summary>

* [com.google.fonts/check/contour_count](https://font-bakery.readthedocs.io/en/latest/fontbakery/profiles/googlefonts.html#com.google.fonts/check/contour_count)
<pre>--- Rationale ---
Visually QAing thousands of glyphs by hand is tiring. Most glyphs can only be
constructured in a handful of ways. This means a glyph&#x27;s contour count will only
differ slightly amongst different fonts, e.g a &#x27;g&#x27; could either be 2 or 3
contours, depending on whether its double story or single story.
However, a quotedbl should have 2 contours, unless the font belongs to a display
family.
This check currently does not cover variable fonts because there&#x27;s plenty of
alternative ways of constructing glyphs with multiple outlines for each feature
in a VarFont. The expected contour count data for this check is currently
optimized for the typical construction of glyphs in static fonts.</pre>

* ⚠ **WARN** This check inspects the glyph outlines and detects the total number of contours in each of them. The expected values are infered from the typical ammounts of contours observed in a large collection of reference font families. The divergences listed below may simply indicate a significantly different design on some of your glyphs. On the other hand, some of these may flag actual bugs in the font such as glyphs mapped to an incorrect codepoint. Please consider reviewing the design and codepoint assignment of these to make sure they are correct.

The following glyphs do not have the recommended number of contours:

Glyph name: Q	Contours detected: 3	Expected: 2
Glyph name: dieresistonos	Contours detected: 2	Expected: 3
Glyph name: iotadieresistonos	Contours detected: 3	Expected: 4
Glyph name: upsilondieresistonos	Contours detected: 3	Expected: 4
Glyph name: beta	Contours detected: 1	Expected: 2
Glyph name: delta	Contours detected: 1	Expected: 2
Glyph name: rho	Contours detected: 1	Expected: 2
Glyph name: sigma	Contours detected: 1	Expected: 2
Glyph name: Q	Contours detected: 3	Expected: 2
Glyph name: beta	Contours detected: 1	Expected: 2
Glyph name: delta	Contours detected: 1	Expected: 2
Glyph name: dieresistonos	Contours detected: 2	Expected: 3
Glyph name: iotadieresistonos	Contours detected: 3	Expected: 4
Glyph name: rho	Contours detected: 1	Expected: 2
Glyph name: sigma	Contours detected: 1	Expected: 2
Glyph name: upsilondieresistonos	Contours detected: 3	Expected: 4 [code: contour-count]

</details>
<details>
<summary>⚠ <b>WARN:</b> Font contains '.notdef' as its first glyph?</summary>

* [com.google.fonts/check/mandatory_glyphs](https://font-bakery.readthedocs.io/en/latest/fontbakery/profiles/universal.html#com.google.fonts/check/mandatory_glyphs)
<pre>--- Rationale ---
The OpenType specification v1.8.2 recommends that the first glyph is the
&#x27;.notdef&#x27; glyph without a codepoint assigned and with a drawing.
https://docs.microsoft.com/en-us/typography/opentype/spec
/recom#glyph-0-the-notdef-glyph
Pre-v1.8, it was recommended that fonts should also contain &#x27;space&#x27;, &#x27;CR&#x27; and
&#x27;.null&#x27; glyphs. This might have been relevant for MacOS 9 applications.</pre>

* ⚠ **WARN** Glyph '.notdef' should contain a drawing, but it is empty. [code: empty]

</details>
<details>
<summary>⚠ <b>WARN:</b> Check mark characters are in GDEF mark glyph class)</summary>

* [com.google.fonts/check/gdef_spacing_marks](https://font-bakery.readthedocs.io/en/latest/fontbakery/profiles/gdef.html#com.google.fonts/check/gdef_spacing_marks)
<pre>--- Rationale ---
Glyphs in the GDEF mark glyph class should be non-spacing.
Spacing glyphs in the GDEF mark glyph class may have incorrect anchor
positioning that was only intended for building composite glyphs during design.</pre>

* ⚠ **WARN** The following spacing glyphs may be in the GDEF mark glyph class by mistake:
	 dieresistonos, macron and tonos [code: spacing-mark-glyphs]

</details>
<details>
<summary>⚠ <b>WARN:</b> Check mark characters are in GDEF mark glyph class</summary>

* [com.google.fonts/check/gdef_mark_chars](https://font-bakery.readthedocs.io/en/latest/fontbakery/profiles/gdef.html#com.google.fonts/check/gdef_mark_chars)
<pre>--- Rationale ---
Mark characters should be in the GDEF mark glyph class.</pre>

* ⚠ **WARN** The following mark characters could be in the GDEF mark glyph class:
	 U+20DD [code: mark-chars]

</details>
<details>
<summary>⚠ <b>WARN:</b> Check GDEF mark glyph class doesn't have characters that are not marks)</summary>

* [com.google.fonts/check/gdef_non_mark_chars](https://font-bakery.readthedocs.io/en/latest/fontbakery/profiles/gdef.html#com.google.fonts/check/gdef_non_mark_chars)
<pre>--- Rationale ---
Glyphs in the GDEF mark glyph class become non-spacing and may be repositioned
if they have mark anchors.
Only combining mark glyphs should be in that class. Any non-mark glyph must not
be in that class, in particular spacing glyphs.</pre>

* ⚠ **WARN** The following non-mark characters should not be in the GDEF mark glyph class:
	 U+00AF, U+0384 and U+0385 [code: non-mark-chars]

</details>
<details>
<summary>⚠ <b>WARN:</b> Do outlines contain any jaggy segments?</summary>

* [com.google.fonts/check/outline_jaggy_segments](https://font-bakery.readthedocs.io/en/latest/fontbakery/profiles/<Section: Outline Correctness Checks>.html#com.google.fonts/check/outline_jaggy_segments)
<pre>--- Rationale ---
This check heuristically detects outline segments which form a particularly
small angle, indicative of an outline error. This may cause false positives in
cases such as extreme ink traps, so should be regarded as advisory and backed up
by manual inspection.</pre>

* ⚠ **WARN** The following glyphs have jaggy segments:
	* Y: B<<132.0,618.0>-<115.0,652.0>-<117.0,650.0>>/B<<117.0,650.0>-<97.0,679.0>-<80.0,688.0>> = 10.407711312490015
	* Yacute: B<<132.0,618.0>-<115.0,652.0>-<117.0,650.0>>/B<<117.0,650.0>-<97.0,679.0>-<80.0,688.0>> = 10.407711312490015
	* Ycircumflex: B<<132.0,618.0>-<115.0,652.0>-<117.0,650.0>>/B<<117.0,650.0>-<97.0,679.0>-<80.0,688.0>> = 10.407711312490015
	* Ydieresis: B<<132.0,618.0>-<115.0,652.0>-<117.0,650.0>>/B<<117.0,650.0>-<97.0,679.0>-<80.0,688.0>> = 10.407711312490015
	* Ygrave: B<<132.0,618.0>-<115.0,652.0>-<117.0,650.0>>/B<<117.0,650.0>-<97.0,679.0>-<80.0,688.0>> = 10.407711312490015
	* three: B<<390.5,416.5>-<346.0,389.0>-<290.0,382.0>>/B<<290.0,382.0>-<353.0,390.0>-<405.0,366.5>> = 0.1119056770624411
	* threequarters: B<<305.5,501.5>-<274.0,481.0>-<234.0,476.0>>/B<<234.0,476.0>-<279.0,480.0>-<316.0,462.0>> = 2.0454084888870154
	* uni00B3: B<<305.5,501.5>-<274.0,481.0>-<234.0,476.0>>/B<<234.0,476.0>-<279.0,480.0>-<316.0,462.0>> = 2.0454084888870154
	* uni0417: B<<446.0,423.5>-<401.0,401.0>-<344.0,389.0>>/B<<344.0,389.0>-<409.0,387.0>-<461.0,364.5>> = 13.65104906328846
	* uni042D: B<<475.0,223.0>-<492.0,293.0>-<486.0,392.0>>/B<<486.0,392.0>-<479.0,354.0>-<460.5,332.5>> = 13.905704610035306 and 1244 more. [code: found-jaggy-segments]

</details>
<details>
<summary>⚠ <b>WARN:</b> Do outlines contain any semi-vertical or semi-horizontal lines?</summary>

* [com.google.fonts/check/outline_semi_vertical](https://font-bakery.readthedocs.io/en/latest/fontbakery/profiles/<Section: Outline Correctness Checks>.html#com.google.fonts/check/outline_semi_vertical)
<pre>--- Rationale ---
This check detects line segments which are nearly, but not quite, exactly
horizontal or vertical. Sometimes such lines are created by design, but often
they are indicative of a design error.
This check is disabled for italic styles, which often contain nearly-upright
lines.</pre>

* ⚠ **WARN** The following glyphs have semi-vertical/semi-horizontal lines:
 * uni3296: L<<659.0,514.0>--<658.0,633.0>>
 * uni4E98: L<<659.0,566.0>--<326.0,567.0>>
 * uni4E9E: L<<450.0,205.0>--<449.0,18.0>>
 * uni4E9E: L<<654.0,716.0>--<655.0,533.0>>
 * uni4ED9: L<<474.0,553.0>--<475.0,74.0>>
 * uni4F91: L<<740.0,352.0>--<741.0,470.0>>
 * uni5012: L<<909.0,744.0>--<910.0,465.0>>
 * uni5042: L<<608.0,438.0>--<610.0,39.0>>
 * uni5072: L<<457.0,-3.0>--<458.0,217.0>>
 * uni5100: L<<508.0,160.0>--<509.0,25.0>> and 320 more. [code: found-semi-vertical]

</details>
<br>
</details>
<details>
<summary><b>[9] ZenAntiqueS-Regular.ttf</b></summary>
<details>
<summary>🔥 <b>FAIL:</b> Font enables smart dropout control in "prep" table instructions?</summary>

* [com.google.fonts/check/smart_dropout](https://font-bakery.readthedocs.io/en/latest/fontbakery/profiles/googlefonts.html#com.google.fonts/check/smart_dropout)
<pre>--- Rationale ---
This setup is meant to ensure consistent rendering quality for fonts across all
devices (with different rendering/hinting capabilities).
Below is the snippet of instructions we expect to see in the fonts:
B8 01 FF    PUSHW 0x01FF
85          SCANCTRL (unconditinally turn on
                      dropout control mode)
B0 04       PUSHB 0x04
8D          SCANTYPE (enable smart dropout control)
&quot;Smart dropout control&quot; means activating rules 1, 2 and 5:
Rule 1: If a pixel&#x27;s center falls within the glyph outline,
        that pixel is turned on.
Rule 2: If a contour falls exactly on a pixel&#x27;s center,
        that pixel is turned on.
Rule 5: If a scan line between two adjacent pixel centers
        (either vertical or horizontal) is intersected
        by both an on-Transition contour and an off-Transition
        contour and neither of the pixels was already turned on
        by rules 1 and 2, turn on the pixel which is closer to
        the midpoint between the on-Transition contour and
        off-Transition contour. This is &quot;Smart&quot; dropout control.
For more detailed info (such as other rules not enabled in this snippet), please
refer to the TrueType Instruction Set documentation.</pre>

* 🔥 **FAIL** The 'prep' table does not contain TrueType instructions enabling smart dropout control. To fix, export the font with autohinting enabled, or run ttfautohint on the font, or run the `gftools fix-nonhinting` script. [code: lacks-smart-dropout]

</details>
<details>
<summary>⚠ <b>WARN:</b> Is the Grid-fitting and Scan-conversion Procedure ('gasp') table set to optimize rendering?</summary>

* [com.google.fonts/check/gasp](https://font-bakery.readthedocs.io/en/latest/fontbakery/profiles/googlefonts.html#com.google.fonts/check/gasp)
<pre>--- Rationale ---
Traditionally version 0 &#x27;gasp&#x27; tables were set so that font sizes below 8 ppem
had no grid fitting but did have antialiasing. From 9-16 ppem, just grid
fitting. And fonts above 17ppem had both antialiasing and grid fitting toggled
on. The use of accelerated graphics cards and higher resolution screens make
this approach obsolete. Microsoft&#x27;s DirectWrite pushed this even further with
much improved rendering built into the OS and apps.
In this scenario it makes sense to simply toggle all 4 flags ON for all font
sizes.</pre>

* ⚠ **WARN** The gasp range 0xFFFF value 0x0A should be set to 0x0F. [code: unset-flags]

</details>
<details>
<summary>⚠ <b>WARN:</b> Check if each glyph has the recommended amount of contours.</summary>

* [com.google.fonts/check/contour_count](https://font-bakery.readthedocs.io/en/latest/fontbakery/profiles/googlefonts.html#com.google.fonts/check/contour_count)
<pre>--- Rationale ---
Visually QAing thousands of glyphs by hand is tiring. Most glyphs can only be
constructured in a handful of ways. This means a glyph&#x27;s contour count will only
differ slightly amongst different fonts, e.g a &#x27;g&#x27; could either be 2 or 3
contours, depending on whether its double story or single story.
However, a quotedbl should have 2 contours, unless the font belongs to a display
family.
This check currently does not cover variable fonts because there&#x27;s plenty of
alternative ways of constructing glyphs with multiple outlines for each feature
in a VarFont. The expected contour count data for this check is currently
optimized for the typical construction of glyphs in static fonts.</pre>

* ⚠ **WARN** This check inspects the glyph outlines and detects the total number of contours in each of them. The expected values are infered from the typical ammounts of contours observed in a large collection of reference font families. The divergences listed below may simply indicate a significantly different design on some of your glyphs. On the other hand, some of these may flag actual bugs in the font such as glyphs mapped to an incorrect codepoint. Please consider reviewing the design and codepoint assignment of these to make sure they are correct.

The following glyphs do not have the recommended number of contours:

Glyph name: Q	Contours detected: 3	Expected: 2
Glyph name: dieresistonos	Contours detected: 2	Expected: 3
Glyph name: iotadieresistonos	Contours detected: 3	Expected: 4
Glyph name: upsilondieresistonos	Contours detected: 3	Expected: 4
Glyph name: beta	Contours detected: 1	Expected: 2
Glyph name: delta	Contours detected: 1	Expected: 2
Glyph name: rho	Contours detected: 1	Expected: 2
Glyph name: sigma	Contours detected: 1	Expected: 2
Glyph name: Q	Contours detected: 3	Expected: 2
Glyph name: beta	Contours detected: 1	Expected: 2
Glyph name: delta	Contours detected: 1	Expected: 2
Glyph name: dieresistonos	Contours detected: 2	Expected: 3
Glyph name: iotadieresistonos	Contours detected: 3	Expected: 4
Glyph name: rho	Contours detected: 1	Expected: 2
Glyph name: sigma	Contours detected: 1	Expected: 2
Glyph name: upsilondieresistonos	Contours detected: 3	Expected: 4 [code: contour-count]

</details>
<details>
<summary>⚠ <b>WARN:</b> Font contains '.notdef' as its first glyph?</summary>

* [com.google.fonts/check/mandatory_glyphs](https://font-bakery.readthedocs.io/en/latest/fontbakery/profiles/universal.html#com.google.fonts/check/mandatory_glyphs)
<pre>--- Rationale ---
The OpenType specification v1.8.2 recommends that the first glyph is the
&#x27;.notdef&#x27; glyph without a codepoint assigned and with a drawing.
https://docs.microsoft.com/en-us/typography/opentype/spec
/recom#glyph-0-the-notdef-glyph
Pre-v1.8, it was recommended that fonts should also contain &#x27;space&#x27;, &#x27;CR&#x27; and
&#x27;.null&#x27; glyphs. This might have been relevant for MacOS 9 applications.</pre>

* ⚠ **WARN** Glyph '.notdef' should contain a drawing, but it is empty. [code: empty]

</details>
<details>
<summary>⚠ <b>WARN:</b> Check mark characters are in GDEF mark glyph class)</summary>

* [com.google.fonts/check/gdef_spacing_marks](https://font-bakery.readthedocs.io/en/latest/fontbakery/profiles/gdef.html#com.google.fonts/check/gdef_spacing_marks)
<pre>--- Rationale ---
Glyphs in the GDEF mark glyph class should be non-spacing.
Spacing glyphs in the GDEF mark glyph class may have incorrect anchor
positioning that was only intended for building composite glyphs during design.</pre>

* ⚠ **WARN** The following spacing glyphs may be in the GDEF mark glyph class by mistake:
	 dieresistonos, macron and tonos [code: spacing-mark-glyphs]

</details>
<details>
<summary>⚠ <b>WARN:</b> Check mark characters are in GDEF mark glyph class</summary>

* [com.google.fonts/check/gdef_mark_chars](https://font-bakery.readthedocs.io/en/latest/fontbakery/profiles/gdef.html#com.google.fonts/check/gdef_mark_chars)
<pre>--- Rationale ---
Mark characters should be in the GDEF mark glyph class.</pre>

* ⚠ **WARN** The following mark characters could be in the GDEF mark glyph class:
	 U+20DD [code: mark-chars]

</details>
<details>
<summary>⚠ <b>WARN:</b> Check GDEF mark glyph class doesn't have characters that are not marks)</summary>

* [com.google.fonts/check/gdef_non_mark_chars](https://font-bakery.readthedocs.io/en/latest/fontbakery/profiles/gdef.html#com.google.fonts/check/gdef_non_mark_chars)
<pre>--- Rationale ---
Glyphs in the GDEF mark glyph class become non-spacing and may be repositioned
if they have mark anchors.
Only combining mark glyphs should be in that class. Any non-mark glyph must not
be in that class, in particular spacing glyphs.</pre>

* ⚠ **WARN** The following non-mark characters should not be in the GDEF mark glyph class:
	 U+00AF, U+0384 and U+0385 [code: non-mark-chars]

</details>
<details>
<summary>⚠ <b>WARN:</b> Do outlines contain any jaggy segments?</summary>

* [com.google.fonts/check/outline_jaggy_segments](https://font-bakery.readthedocs.io/en/latest/fontbakery/profiles/<Section: Outline Correctness Checks>.html#com.google.fonts/check/outline_jaggy_segments)
<pre>--- Rationale ---
This check heuristically detects outline segments which form a particularly
small angle, indicative of an outline error. This may cause false positives in
cases such as extreme ink traps, so should be regarded as advisory and backed up
by manual inspection.</pre>

* ⚠ **WARN** The following glyphs have jaggy segments:
	* W: B<<485.0,543.0>-<479.0,546.0>-<477.0,541.0>>/B<<477.0,541.0>-<478.0,547.0>-<472.0,526.0>> = 12.33908727832618
	* Wacute: B<<485.0,543.0>-<479.0,546.0>-<477.0,541.0>>/B<<477.0,541.0>-<478.0,547.0>-<472.0,526.0>> = 12.33908727832618
	* Wcircumflex: B<<485.0,543.0>-<479.0,546.0>-<477.0,541.0>>/B<<477.0,541.0>-<478.0,547.0>-<472.0,526.0>> = 12.33908727832618
	* Wdieresis: B<<485.0,543.0>-<479.0,546.0>-<477.0,541.0>>/B<<477.0,541.0>-<478.0,547.0>-<472.0,526.0>> = 12.33908727832618
	* Wgrave: B<<485.0,543.0>-<479.0,546.0>-<477.0,541.0>>/B<<477.0,541.0>-<478.0,547.0>-<472.0,526.0>> = 12.33908727832618
	* uni4E82: B<<217.5,225.5>-<223.0,225.0>-<229.0,224.0>>/B<<229.0,224.0>-<225.0,225.0>-<222.0,230.0>> = 4.573921259900818
	* uni4E82: B<<236.0,225.0>-<235.0,224.0>-<233.0,224.0>>/B<<233.0,224.0>-<240.0,223.0>-<246.0,223.0>> = 8.13010235415596
	* uni5294: B<<344.0,243.0>-<345.0,249.0>-<349.0,250.0>>/B<<349.0,250.0>-<344.0,249.0>-<339.0,249.0>> = 2.726310993906212
	* uni5294: B<<384.0,258.5>-<371.0,253.0>-<354.0,251.0>>/L<<354.0,251.0>--<355.0,251.0>> = 6.709836807756896
	* uni58DE: B<<861.0,437.0>-<862.0,439.0>-<866.0,441.0>>/B<<866.0,441.0>-<854.0,438.0>-<840.0,436.0>> = 12.528807709151463 and 75 more. [code: found-jaggy-segments]

</details>
<details>
<summary>⚠ <b>WARN:</b> Do outlines contain any semi-vertical or semi-horizontal lines?</summary>

* [com.google.fonts/check/outline_semi_vertical](https://font-bakery.readthedocs.io/en/latest/fontbakery/profiles/<Section: Outline Correctness Checks>.html#com.google.fonts/check/outline_semi_vertical)
<pre>--- Rationale ---
This check detects line segments which are nearly, but not quite, exactly
horizontal or vertical. Sometimes such lines are created by design, but often
they are indicative of a design error.
This check is disabled for italic styles, which often contain nearly-upright
lines.</pre>

* ⚠ **WARN** The following glyphs have semi-vertical/semi-horizontal lines:
 * uni3236: L<<672.0,118.0>--<670.0,354.0>>
 * uni4E17: L<<702.0,33.0>--<701.0,455.0>>
 * uni4E9E: L<<449.0,204.0>--<448.0,35.0>>
 * uni4ED9: L<<473.0,552.0>--<474.0,92.0>>
 * uni4F8B: L<<232.0,327.0>--<231.0,20.0>>
 * uni4FD7: L<<527.0,301.0>--<675.0,300.0>>
 * uni5012: L<<908.0,743.0>--<909.0,464.0>>
 * uni5042: L<<607.0,437.0>--<609.0,38.0>>
 * uni5072: L<<456.0,-4.0>--<457.0,216.0>>
 * uni5100: L<<507.0,141.0>--<508.0,24.0>> and 206 more. [code: found-semi-vertical]

</details>
<br>
</details>

### Summary

| 💔 ERROR | 🔥 FAIL | ⚠ WARN | 💤 SKIP | ℹ INFO | 🍞 PASS | 🔎 DEBUG |
|:-----:|:----:|:----:|:----:|:----:|:----:|:----:|
| 0 | 2 | 17 | 205 | 13 | 156 | 0 |
| 0% | 1% | 4% | 52% | 3% | 40% | 0% |

**Note:** The following loglevels were omitted in this report:
* **SKIP**
* **INFO**
* **PASS**
* **DEBUG**
