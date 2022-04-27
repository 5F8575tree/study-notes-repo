# Figma

Figma is a free design program that allows you to design web and app projects. It is the fastest growing design tool (overtaking Adobe XD), and can be used directly in your browser. It is a good idea to download the program directly to your CPU, however.

## Figma versus XD versus Sketch

It is hard to say that any one of these design programs is better than the others. It comes down to preference. The output is the same.

At the end of the day, any clients you have will not care which program you use. It is far more important to you to get the design right than to get the program right.

# HotKeys

    ctrl+N: New File
    ctrl+mousewheel: Zoom
    space+click: Grab and move (panning)
    shift+1: 1x zoom
    shift+0: 100% zoom

    alt + click/drag: Duplicates an item
    alt + shift + click/drag: Duplicates an item and ensures it drags in a straight line

    [: Send an Item Back
    ]: Send an Item Forward

    r: Rectangle Tool
    o: Oval Tool
    f: Brings up the frame tool, allowing you to select a template frame from the right-hand panel.
    v: Move Tool
    ctrl+shift + K: Insert Image

# Misc Tips

If you are grabbing everything and you accidentally grab the frame, too. Press enter to deselect the frame, and you will be left with the selection of all the items within the frame only.

## Community

In the community tab you can see multiple plugins, templates, and other resources. To start with, you should learn the principles of web design before exploring the styles and fancy add-ons in the community tab.

## Basics

If you drag a rectangle onto the canvas it will bring up some options on the right-hand side. You can click the color box and choose a different color and then hit [esc] to exit the color picker.

In the home screen, double-click on a project to open it up for editing. Right-click on theproject to bring up further options, including delete (if you delete by accident got to Drafts > Deleted).

**NOTE** The projects are not saved on your local computer - everything is saved on the Cloud.

### Desktop Frame

The default size for the desktop frame is too small, however, so you should be sure to change it to **1920 x 1080**.

### Layers Panel Frames

When you move an item within a frame on the canvas, it automatically updates and is added 'within' the frame on the left-hand panel.

### Moving an item with shift+arrow keys

When you have an item selected, you can move it around in 10px increments by holding shift and tapping the arrow keys. If the item is within a frame, you can utilise the auto-align buttons on the right-hand panel.

Of course, the alignment tools work when you select more than one item, but it aligns the items _with one another_, rather than _with the frame_.

## Figma's Interface

The tools array at the top of a file's canvas is deceptively simple. You will essentially only use move, rectangle, frame, and text. You won't need pen as it is better to use icons from the web. The key is that when you click on a particular item on your canvas, it will bring up a corresponding menu on the right-hand panel to allow you to edit it.

## Design and Inspect Modes

It is incredibly useful that you can visually create your design, and then by clicking on inspect you can actually see the CSS code that can be copied and pasted into your CSS styles.

The 'play' icon at the top-right of the panel allows you to view the page without any distractions, and also allows for prototyping if you have made the design to be a 'working' prototype.

You also have the share button, which allows you to share with someone by sending a link via email or social media, etc. The beauty is that you can then continue to work on it and the link is updated as you make changes so a client can follow changes.

## Scale Tool

If you have an icon, for example, you will find that dragging a corner to resize it will actually make the lines run thinner (if you enlarge it) or thicker (if you shrink it). This is where the scale tool comes in.

With the scale tool you can simply drag a corner out (no need to hold shift) and the item will scale properly without distortion.

You can do this on several icon items at once by selecting them all.

**NOTE** After downloading the icon you wish to use, you can inspect it's layers in the layers panel and you can usually edit just one inner layer - for example, just the color of a particular line, etc.

**TOP TIP** With a downloaded batch of icons, you can often select them all together and then click on the color swatch and exchange that color across all of the items - really useful!

# Creating Buttons

In other design tools, you would usually create a button by drawing a rectangle, adding text, aligning them, and making it a grouped item.

However, in Figma **you want to use frames rather than rectangles!** This will make it much easier to organise your project and also to making your designs **responsive**.

Part of the reason is that frames are required to make your prototypes interactive, for example clicking a button to see where that button leads, etc.

You can of course nest frames, and in fact that is the natural way to work. Don't misunderstand that frames are like artboards in PhotoShop.

In short, don't use groups, use frames for everything you can!

Here's the perfect way to build a button in Figma:

1. Grab the text tool and type the text
2. Press shift + A
3. Rename the frame as something descriptive (e.g. 'submit-btn')
4. Click the fill color swatch and choose a color for both your text and your background (you will need to switch selections in the layers panel)
5. Round out the edges if you like with the radius tool on the right-hand panel (with the frame selected)
6. From the same panel, look for 'Auto Layout' and select the padding you want **NOTE** the small icon on the far right of the Auto Layout section allows you to adjust the padding on each side separately, so you can have wider padding on the right and left and narrowed padding on the top and bottom.
7. That same button allows you to center the text within the button, so that you can resize and keep the text centered.
8. If you decide to add an icon to the button, you can also use the Auto Layout tool of 'distance between' items.

Now you can move on to other styling if you wish, but you have your basic button to work with.

**NOTE** If you are starting a project, remember to use a Design Sheet to organise your project and keep the styling consistent throughout your pages.

# Colors

Of course, you want to use colors that a styled and consistent and refer to them with the HEX code. You can type the HEX code in.

You can add linear gradients by changing 'solid' to linear from the top of the color swatch pop-out. This, again, is really useful for precise CSS code generation.

Of course, there are other gradients besides linear, but **linear is the only one you should really use.**

You can alter the angle, length of gradient, and the opacity, along with the two colors that will merge. You can also add a third color by clicking the square box on the item and selecting a color from the swatch.

You can insert an image by clicking on the image selector in the same panel as 'solid' and 'linear'. If you select this, you can insert an image to the shape you have drawn, and you can also use the + sign on the right-hand panel fill to add an overlay of color or a gradient over your image.

Adding a gradient over an image is an excellent technique in darkening a section of an image just enough to show any light-colored text that you may want over the top.

On projects, you will want a color scheme and can save each color in Figma itself. To the right-side of the FILL tool, you will see four-dots in a square shape. If you click that icon you can click the + sign and save the color to a style. The next time you click the four-circle icon, you will see the color you saved.

Not only is this quicker when you are creating new items for the page, but if you are working on a product for a client, when you have nothing selected you can see your color styles in the top-right of the panel. You can click on a color that the client perhaps wants to be changed, and changing it here in the base style will change it throughout the whole project. Of course, you can also detach from the FILL selector by clicking the 'chain' icon.

**GIVE DESCRIPTIVE STYLE NAMES** Don't save your colors with names like 'light blue', or 'lightest blue'. Instead, use more descriptive _terms based on how you intend to use them_ like 'button color', 'background color', 'text color', etc. This will also be convenient for writing Sass code.

**NOTE** Picking a bright color: about 2cm down and 1cm from the right of the color pop-our swatch is a good place to start as most colors you go through from there will look bright and modern.

# Images

**Place your images inside rectangles**: This is certainly one case where you want to use rectangles (or circles) instead of frames, as the image will be centered immediately to look good. You can resize the image by clicking on crop in the centre menu directly above the canvas. This will allow you to place the image better in the rectangle and allow you to resize it if you want (remember to hold shift to retain the aspect ratio).

To replace an image you can't just drag another image from your file over the existing image. Instead you need to change it with the FILL tool on the right-hand panel. You can drag the image and drop it over the FILL image selector.

## Figuring Out Sizes

One way to figure out the desired size of an image (perhaps you want it to be exactly 1/3 of the width of the page) is to use the 'width' and 'height' properties of the image. First, place the rectangle in one of the corners of the page. If our total width is 1920, for example, you can type into width '1920/3' and height '1080/3' to get the desired size.

Being precise with things like this, and working to the law of three, is a great way to make your design better and also improve responsiveness.

If you duplicate colors, you can add 'Stroke' from the right-hand panel to see the color of the borders to distinguish each item. You can change the stroke color to white, and increase the thickness to 2 or 3 for the best effect.

## Masking in Figma

Add an image to the page, and draw out a circle (or rectangle). Make sure the shape is behind the image. Select both the image and the shape, and click on the 'mask' icon that is in the top menu directly above the canvas (looks like a crescent moon).

It is actually not as good as using the general image technique - dropping an image in as the fill for a shape. However, if you have a really complicated shape - perhaps text that you want to have some funky polka dots behind, then this masking method would work best.

You can also make a group out of the shape and the image so that you can move it around as you like.

# Text

There are two ways to add text with the Text Tool: click and start typing, or drag out a box and type.

While you can resize the text box, you can also choose the two other options from the Text options on the right-hand panel: auto width (the same as clicking and typing), auto height (bunches to the height of your text), and fixed size (which is the 'draw a box' version mentioned before).

You can also space the letters and/or the line height: **both of which will be represented in the generated CSS code**!!

**NOTE**: It's important to have your text box tight around your text, since if you are going to align with other items, Figma will read the text border as the text item to be aligned, and not the text itself.