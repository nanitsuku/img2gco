# img2gco
[Japanese](README_ja.md)

Image to reprap gcode converter

See http://wiki.nebarnix.com/wiki/Img2gco for overall project details!

Todo:
- [ ] Change to relative coordinates for ease of fine positioning
- [ ] Implement bi-directional etching
- [ ] header and footer gcode script
- [ ] alpha channel handling ( current, a pixel that has alpha channel value 0, it treated as "black" pixel )
- [ ] preview that reflects following parameters

Usage details:

* Laser On Command: - specify a command outputs laser ( e.g. M3 )
* Laser Off Command: - specify a command stops laser ( e.g. M5 )
* PWM Control: - A command which specifies PWM parameter. Put that after laser on command or M106
* M106 Option: - some laser engraver needs a optional parameter after M106. e.g. if that needs M106 P1 S255, specify P1 for this.

* Laser Min Power [0-255]: - This is the laser power that corresponds to WHITE
* Laser Max Power [0-255]: - This is the laser power that corresponds to BLACK
* Laser 'Off' Power [0-255]: - This is the laser power that will not mark the wood at all, even if it just sits there. Usually this is the bare minimum that your PWM board will respond to.
* Skip over values above [0-255]: This defines the white level. In a JPEG the white level probably contains some compression artifacts so you might have to go down to 252 or so. PNG images should have white at 255 so 254 is a good value. (TODO: preview the image with this level hi-lighted)
* Travel (noncutting) Rate [mm/min]:" - Slewing between places speed.
* Scan (cutting) Rate [mm/min]: - Speed to move while lasering. This is usually limited by the commands per second rate of your firmware, you can go faster from an SDcard than over USB. You will need to find this speed, and note that the power levels will need tweaked if this speed is changed.
* Overscan Distance (prevents twang from showing) [mm]: - This sets a 'blank' distance before the start of the line to give the belts time to settle down and the motors to reach constant speed.
* Flip Image Upside Down: - if you prefer image's right top as gcode (0,0) check this. you prefer left botom as gcode (0,0) uncheck this.
* Height (width autocalculated) [mm]: - set the height, the script will autosize the width. (TODO: add an either/or option)
* Horizontal Resolution [mm/pixel]: - mm between pixels. If you make this larger you can attain faster speeds, but at the price of some detail loss. 0.1 is really amazing 0.15 is nearly so. 0.2 starts to look a little fuzzy. Beyond that you will probably see pixelization.
* Scangap [mm/line]: - This is the distance between lines which is a function of your laser spot size. You need to make this small enough so there aren't visible unburned lines. For my laser this is 0.05 though I can usually get away with 0.075 because its faster. 0.1 leaves visible lines, which is kind of a cool effect. You can try to defocus your laser to make thicker lines for shorter overall total time, but you will have to increase your power. Note that if lines start to overlap you might need to bring your power down slightly.
* Start X [mm from 0 for right of image]: - X value to start image from. The laser will start here and move in the positive direction as it scans.These X,Y points correspond to the *top right* of the image.
* Start Y [mm from 0 for top of image]: - Y value to start image from. The laser will start here and move in the positive direction as it scans.These X,Y points correspond to the *top right* of the image.
