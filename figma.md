# Figma

Figma is a free (to get started...) design program that allows you to design web and app projects. It is the fastest growing design tool (overtaking Adobe XD), and can be used directly in your browser. It is a good idea to download the program directly to your CPU, however.

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

You can measure the difference between two items by selecting one, then holding alt, and hovering your mouse over the second item.

**CSS to Position Items** You can change the dimensions and position of an item by using the CSS properties: the arrow keys will move the item and you can see the CSS top and left move. If you hold ctrl while using the arrow keys you can alter the height and width of an item. This is good to alter things from, say, width 149 to width 150, giving more readable code.

Selecting an element within a frame can require multiple double-clicks depending on how 'deep' the item is within the frame. Instead, hover your mouse over the item you want to select, hold ctrl and click.

If you have many items in a frame, and want them all selected, first select the frame that contains them and then press enter.

You might want an item 'in between' frames. In this case, grab the item and start moving it on the canvas, then press the space bar and drop it in between the layers where you want it placed.

# Design Tips

In general, you want to work with the development in mind. So, it is far better to use a shade of color than to try and use a color with opacity.

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

## #f2f2f2

It is really worth investing some time in figuring out a nice off-black and a nice off-white to use while you are at least building out the design. It will instantly make the design look better and you can always come back and adjust it later. #F2F2F2 is a decent light grey, and #F5F5F5 is an off-white grey, but you can do better.

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

You can also space the letters and/or the line height: **both of which will be represented in the generated CSS code**!! Remember that it is not a good idea to alter the letter spacing, except for short titles, as it will change the feel and beautiful, careful design of the font.

**GOLDEN RULE FOR LINE HEIGHT: The font size, multiplied by 1.5 (or 150%)**

**NOTE**: It's important to have your text box tight around your text, since if you are going to align with other items, Figma will read the text border as the text item to be aligned, and not the text itself.

In short, probably best for paragraphs of text to draw a random box, insert your text, then switch to auto-height.

## Font-Family

It shouldn't be a quick or easy decision to decide a font. It is a matter of having an eye for style and good taste, just like dressing well.

A very handy resource, however, is to download a font from Google Fonts, or downloading a Github resource called [fonts](https://github.com/google/fonts) which you can then save to your C:\Users\YourName\Windows\Fonts folder.

Always choose a font that has at least 3 styles, since it allows for flexibility across your web application.

You can click on a text item and alter the font size by selecting the font size selector on the right-hand panel. You can press your up and down arrows, and if you do this while holding shift it will incrase/decrease the font size in 10 pixel increments. Unfortunately, the font size has to be in pixels.

Usually you want either left or right alignment. Centered font is difficult to use. There are three dots at the bottom-right of the Font Tool - there you can access many more options, including block text and paragraph indentation.

**NOTE** As with saving color styles, you can save your text styles, for example "heading 1", "heading 2', "paragraph", "button", etc.

**FONT-WEIGHT**: You will probably find that the larger the font size, the smaller you want the font weight to be.

# Effects in Figma

Background blurs can be effective to show up hard-to-read text, a bit like using a gradient. However, you should probably stick to either a white or black background blur if you plan to use it effectively. A value of around 5 or 6 is usually best for the blur. Again, this will also show up in your CSS as backdrop-filter: blur(5px); Of course, you need to put a rectangle with black (or white) over your image and be sure to apply the blur to your rectangle, and _not_ the image itself. Also, do NOT get carried away with this effect, use it sparingly.

For drop shadows, it is best to only alter the Y-axis and leave the X-axis as 0. This is typical in modern web design. Remember, any drop shadow should be incredibly subtle and barely noticeable! A y-axis of 3 is quite good. Keep the opacity low as well, 25%.

For text, any drop shadow should usually be black (maybe white). But for things like buttons or maybe cards, you could use a color. Choose the same color as the button, raise the blur to around 10, and the opacity to around 50%, with the Y-axis set to maybe 6.

Layer blur is another way to blur the 'background', but be mindful that it will alter the image, and not the background _per se_. The corresponding CSS will be applied to the image as filter: blur(6px);

Don't bother with inner shadow.

**THE GOLDEN RULE FOR EFFECTS: Use them sparingly, and be very subtle.**

# Grids

To add a grid you select the frame and then on the right-hand side look for 'Add Grid' under 'Auto Layout'.

For web design, rather than mobile apps, you will want to select columns. **Set 12 columns with a margin of 360**.

Using a grid is really helpful in many, many ways, but particularly useful is when you redesign for smaller screens as you can align things again with the 12 column grid.

Why a margin of 360? This is because it gives you a center of 1,200 pixels, also known as the 'active area', where most of the key information for a web page need to be. Of course, it is no problem at all to have elements outside of this central grid, but only for decorative purposes and not for main content.

Again, this has responsiveness in mind, too. Since 1920x1080 is the most used screen size worldwide, a close second is a width of 1366 - which means our main content will still be fine, with a little bit of wiggled room on either side. Smaller than that, and you want to apply an @media query to your CSS.

Once you have your grid, you can press shift + R to drag across two ruler lines. This means you can take away the grid to see your project better when you are not using it, but still see the outline of the active area.

**NOTE** Use the eye icon to switch the grid on and off as you work (also, reduce the grid opacity to around 3%).

# Components

Even though you may have set a color and font style for 'button', that doesn't alter any other aspects if you want to change the button later throughout the entire document, for example, less rounded corners, or drop shadow, or padding. All of this can be done instead by creating a component. Once you haave designed your button, click the four diamonds at the top menu right above the canvas to create a component.

The clones of the original will constantly update as you make changes, and so you save yourself a lot of work potentially!

Components will get saved in 'Assets' next to the layers panel on the left-hand side. From there you can simply drag any component to anywhere you want, without the need to press alt and drag.

# Grabbing Things From Websites

If you want to practise recreating certain web pages to increase speed, one good tip is to use inspect on a page, then follow the link of a logo and open it in a new tab. Then you can download that logo in it's original form (PNG or SVG) and save it to your local computer for use in Figma.

Your logo should be placed right to the left-hand edge of your 1200px active area.

**Flaticon** is a great resource for icons. Try it [here](https://www.flaticon.com). It is not free, but it is the best of the best by far. We can grab social media icons here easily.

**Choose SVG** as it is crisper in quality than PNG.

# Header

If you use an off-white color for the page background, you can have a pure white header. It's width should be 1920, and it should be centered, with a height of maybe 100px.

Circles are great for social media icons as they will all be the same size. Have them around around a height of 40px, and space 10px between them. Move the to align centrally in the vertical axis of the header and touch the right-hand ruler. Don't leave them black, instead you should grab a brand color for the web page.

Rename the frame as 'Header'.

# Main Menu Bar

It is quite modern to have a minimalistic design for your main menu. You can create another frame, directly below the header, and give it a height of 60px and a fill of the branded color.

Use the text tool and add 14px font size, and a white color. Poppins is a good template font-family. Remove padding. Select the text item itself, not the frame, and use ctrl + D to duplicate it. If you have set auto layout, Figma with place it next to the original.

Once you have written all your menu names out side by side, select the frame on the left-hand panel, and increase the default gap between them.

**IMPORTANT NOTE** Users expect this menu to be on the left-hand side, so space the items out, but don't center them. Let the last item go just over half-way across the horizontal axis of the screen (960px is the center line).

You want to set a color to show which is the current page (or an underline?). A decent choice is fff000 (yellow).

# Search box

It is quite trendy to have around 5px border radius, as well as having a button inside the search box and some placeholder text. Start with text > ctrl + A > Fill background white > Add a stroke and reduce opacity (or select #C9C9C9) > set the height to around the same as your menu height (50px) > Align the text to the left, but then change from 'packed' to 'space between' > Add left padding of around 20px for the text (keeping the rest at 10px).

Select the placeholder text and Add Layer (ctrl + A). Now when you click inside the search frame again and add text for the button, it will be spaced over to the right, with your placeholder text left-aligned! Now you can repeat the fill for the button within the search to a branded color. Change the text to white. Change the placeholder text to #A4A4A4. You will probably also want to return to the search frame and reduce the right-side padding to 5px.

# Cards

Cards are often the most important design feature of the web page, since they are presumably calls to action. Type a header, type a sentence or so, and then combine those (two separate) text items into a frame. Fill the frame with white. Add 20px padding all around. For the card title you could use semi-bold, 20px. Then the descriptive text could be regular, 14px. Ensure you have the auto height setting for the descriptive text to make sure you can see 20px only as the bottom padding.

Set the spacing between items as 10px. Then add a rectangle to the top for the image.

**NOTE** You want to have the text items set to 'resizing' of width: fill container in the right-hand panel.

**CARD WIDTH** With a 1920 width page, 1200 active area, you want a card to be a third: 380px width (card is text + padding).

## Card Improvements

First, make the card a component. Then rename it, and remove it from the page frame. Typically, you will have a separate file containing all your components. Even in a mock up design, you will want to layout the cards in a grid as though you have a full page (unless you are doing something where you know you only need 3-4, for example a pricing plan or something). Around 40px between cards vertically is good, and for the width you set the left and right to the edges of your 1200 active area and then use the space between button.

Again, even in mock ups you need to use different content for each card. After pressing ctrl+shift + K you can select multiple images and then click them in quickly to add them to each card.

Going back to our component, you will now be able to make design changes that affects all cards. Start by trying a bottom-only border radius of 15px. Try a #C9C9C9 stroke color for the card (note that neither of these alterations are made to the top image section of the card).

Rather than using pure black for the text, you could try #222222 to add a little refinement.

# Pagination

Pagination is required on any page where you have items that flow over to other pages. A good example is search results. Pagination is expected since it is something a user will expect having used Google all their life. It basically shows you a certain number of pages, and have the current page highlighted in some manner.

Use text and type 1. Then enable auto layout by pressing shift + A and add a white fill for now. Have 20px padding on the sides and 10px for the top (10px 20px). Set the border radius to maybe 5px. Set an inside black stroke set to 2px - you never want to go lower than 2px for something you want to pop out (whereas with the card stroke we want 1px as it is just to add a hint of texture).

Place it directly against the left-hand line of your 1200px active area.

Make it into a component. Rename it, and remove it from the page frame.

Clone them and set them 30px below the search card results and leave 10px between each pagination item.

Next, return to the component item and change the border and number color to a branded color. You want to hightlight the current page by selecting it, removing the component stroke color, and then switching the two colors associated with just this component.

If your web application has more than 5 pages, then you can add a space between the first 3 and the last 2 and enter a ... to show that you have more pages.

# Footer

Drag out another frame, 1920 width, and around 400px height. Light colors are usually nice for a footer, but we can try #333 for variation. You can add a branded color bar to the top by dragging a rectangle and giving it a width of 1920 and height of 6px. For titles, go for regular weight font, 14px, and uppercase.

Set the distance from the top of the frame to 60px. For the distance between you will want to use your 12 column grid. You need to do a little maths. For 3 titles, you want to set them four columns each. Likewise, if you have 4 titles, you want to set them to three columns each.

Instead of white, you could go for a light grey - maybe #E5E5E5.

For the actual items under the title, you want normal casing for the font. If a particular title has numberous items, then use two columns within the space allowed for that title. If one column has to be longer than the other - it should be the left column.

For any paragraphs of text here (or even long item names under headers) make sure that you don't go over the number of columns you have determined for the title. In fact, paragraphs should go right across all three/four columns.

Key information, such as an email address, should be in a different, brighter color than the other text.

**NOTE** Why is the footer so big? Why not a single line with copyright? Well, most businesses will have legal obligations to include certain information, such as GDPR rules, and you want to leave enough space for this to be available either now, or in the future.

**TIP** Although we gave each title section a certain number of columns, it may not look great depending on the content. A great tip is to make groups out of each of the sections you have, say there are four in total, and then select the four groups and click 'tidy up'. This will move them to a nice balanced position.

**TIP** If you feel you must use a line border at the bottom (not very popular in design at the moment), make sure it is a really subtle color that is just a hint. Try #434343 on a dark background.

# FOUNDATION ONE: Pixel-Perfect Execution

Your items, the font colors, sizes, the images, the **balance**: all of the things must be executed to perfection. This is the basis of good design. You won't win design awards, but you can create multiple excellent designs to a strong level.

## Settings for Your Website

We know the desktop design will be 1920x1080 - i.e. Full HD (active area width 1200), but your maximum height should be no more than 8000px if you have lots of content to scroll down through.

The top portion of the page will be your header - including the logo, navigation, and some buttons like 'log in' or 'sign up', etc.

Immediately below this is the 'hero area'. By far the most important part of a website.

Below, you will likely have a 'sub-hero region' (optional). This could be for main cards, or other key information not required in the hero.

Next, you have the content. Then finally the footer.

If in doubt, ask your: have I seen this layout on a large, mainstream layout? If the answer is no, then you have probably done something wrong.

**KEY** Don't forget to wireframe your website first to make sure you have a solid design framework. This can simply be grey boxes with white boxes and text. But the key is to ensure that it is a standard web page format, while also containing all the elements you need to place on your website.

## Sizing Your Website

It is worth getting a decent browser extension that allows you to take a screen shot (that will include the full web page design only). Then you can insert the screen shot into your project and lay it over your web page design. Then reduce it's opacity to around 50%, and you can easily compare sizing for things like buttons, titles, images, etc.

GoFullPage is a good option for Chrome.

## Text Sizing for Paragraphs

Line Height = Font Size x 1.5 (150%). You can round it out is the resultant number is awkward, i.e. 18 font x 1.5 is 27, but you can use 28 instead.

Ensure a line break with one clear space between paragraphs.

You never want more than a maximum of 4 lines of text per paragraph.

You don't want to have a wayward word or two on the bottom line of a paragraph. So if that is the case, increase the width of the item so that the word joins the above line.

The width of the paragraph item should be around 600-700px, generally. You definitely don't want text that has really long lines, definitely not spanning the width of the web page.

Always left-align text.

**NOTE** Never put paragraphs of text in the hero area, one is about the maximum you can get away with.

## Color Contrast

The two colors need to be 'strinkingly different'. In other words, the contrast for text vis-a-vis background should be either maximum or very close to maximum.

Don't jeopardize the contrast by using a super bright color for a button to make it 'stand out'. The white text will not be visible and there are better ways to make a button stand out.

Pure white is always best on a color background for a button.

Again, remember that dressing a web page is like dressing yourself. The odd hint of fun is great, but you can't beat the classic style principles.

**HINT** To repeat, the best place for finding good background colors (other than off-white and off-black) is around 2cm down from the down right of the color swatch. From there you can use the color scroller to find interesting colors that you can be sure will allow enough contrast for a light text.

Another good rule is that the brighter the color, the less you want it on your page.

Yellow is a very tough color to pull off in terms of contrast. You can make it work, but it is so closely associated with DHL and other 'yellow' companies that it will be hard to shake off that association.

**DON'T** Base your color scheme on the client's logo. The reason is that the logo may be bad, and you will get huge headaches working with it. Instead, either keep the logo on something simple like off-white or off-black, or redesign the logo.

## Hero Alignment

The difficulty with poor alignment is that client's will not know how to tell you, they will only be able to see a poor design or say that 'something is not quite right'.

If you have a title, short paragraph and a button, you should treat those as one group and ensure they are aligned correctly within the hero - i.e. left-aligned within the 1200px active area, and central between top and bottom of the hero. If you don't do this, you will be leaving some blank area somewhere for no good reason.

Another key rule, you placement of the information is **paramount**. The background image is simply design and should not dictate the placement of your content - even if you feel like a tree branch is in the way or something, you just need a better image or to alter the image to make it work with the correct placement of the content. In short, **content first**.

## Icons

The key rule is to use the same set of icons. But if you have social media icons, and then instead you have more intricate 'product' icons then they can be two separate sets.

This is a great reason to use Flaticon, as you can simply download packs.

Again, only use **SVG** icons.

If you plan to use large icons somewhere, never go with filled icon packs. They are way too heavy and they are boring. You can use more intricate icons because you have the space. On the other hand, for small icons use simple, filled icons.

**GOLDEN RULE** Icons can sometimes be tricky (unless you use contained circles or squares), since one icon in a pack may be square and another a rectangle, or odd shape. Say you square is 90 x 90 pixels, the golden rule is to keep the longest length of the other icons to 90 pixels and just let the aspect ratio handle the smaller length.

# FOUNDATION TWO: Understanding the Clint's Needs

Can you put yourself in the client's shoes? What is their core purpose?

A website is just a tool - a means to an end. You must be crystal clear on what the website is trying to achieve, and forget everything else. This will give you laser focus to look at the website from the user's perspective, i.e. **is it really obvious what I need to do next?**

Aesthetics are secondary to purpose - just like clothing!

The business owner (client) should be able to give you a really clear idea of who the user is, their persona. So, it is key in your prep work to answer these questions:

    - What is the user persona?
    - What do they need to do next?

This is a sniper rifle approach, not a shotgun approach.

Remember also that user's are irrational and the have zero patience. They may be visiting 20 websites and **you only have seconds to get across the message and also not offend them with ugly or depressing design.**

A high bounce rate is an expensive problem for a business owner. Not only are they losing potential business, but they have also paid for advertisement which is based on pay-per-click, perhaps.

## Statistics

Both as an entrepreneur and a web designer, you need to measure things and make every decision based on statistics.

During initial design, you can only truly make your best educated guess. But after the website is live, you can view analytics to see where performance can be improved. For example, users may be adding items to their cart, yet not actually purchasing. Figure out the problem: are the shipping costs clear? Is the payment method clear? etc.

Google Analytics is your friend, and most ad campaign tools will also give excellent statistics (such as FaceBook ads).

Another key thing to remember is that 90% of visitors to a web page are viewing it on a mobile device. **THE GOLDEN RULE: Mobile-First.**

In short, everything you design has to be tested. Charge a fixed price for a project, then charge an hourly rate for the follow-up changes!

If the client is a good business person, they will be able to tell you the **KPI's** that they are seeking to achieve.

## Templates?

There are a lot of benefits to WordPress Themes, ThemeForest, EnvatoMarket, and Elementor Pro. And it certainly means web designers are not entirely secure in their career forever.

Why are templates not so great?

    1. They are actually quite hard work to use, even for a designer.
    2. **Time** is the most important thing for a business owner. Business owners are not thinking about money, they are thinking about time.
    3. People want quality, and something tailored to their own needs. This goes back to the clothing analogy - UniQlo might work for underwear, but not for a fitted shirt. If you client is a business owner, it is probably the thing they love most in the world, they don't want a cheap version that any one can use.

In short, the markets are different: both can coexist. Web designers are simply the 'premium' service.

## What happens if your design is sub-par after coding?

It depends on the problem and whether or not there is an impact on the purpose of the website. Most business owners will overlook a slight odd design aspect that was a result of bad coding, but would need to jump straight to action if they found that when a user buys a product from the site the money doesn't process, or another critical problem.

It is just like code development - you handle the critical problems first and then iron out any slight details when you have time.

## Case Study(s)

Think of two opposite market: luxury shoppers, and kids games. A luxury brand will like clean, white, spacious designs. Kids will want bright colors will overly popping designs! These are extremes, but the idea is valid: the client is looking for something that will work for them.

Another way of thinking about it is that if you are building a website for a vegan food store, you don't go with photo's of meat. You first need to research a ton of vegan-related websites and even read some blog articles to discover what it is that vegan people like: their persona. This is the key.

## Landing Pages

Typically a landing page differs from a website in the sense that it sets it's goal as getting just one thing. This is usually either capturing the user's information, i.e. getting them to sign up so you have their email; or it is to make a sale.

The landing page is the ultimate one-purpose design. They are usually linked to an advertising campaign that has already grabbed you based on the fact that you clicked the advertisement.

Gathering information is lead generation, because it is proven that a customer has a certain tipping point during interaction with you after which they become an 'addicted' user. For example, FaceBook users once the get to 8 friends, or someone who 'likes' more than 10 songs on Spotify. Netflix users who take the free trial for a month are also extremely likely to continue using the paid service. These are all researched points where someone goes from just taking a look to becoming a full-on user (read 'Principles of Data Wrangling' if that is a subject you are interested in, bet still, read **'Algorithms to Live By'**).

Certain customer persona's are far, far more likely to like a slow approach, but generally all people prefer the slow burn approach anyway.

You want to keep a landing page short and sweet for this reason. The longer the page, the more likely it is that the user will abandon the site. The **first headline** becomes absolutely key, and further headlines should just hammer home the same point in differently phrased ways.

Zibbet.com is a great example of a strong landing page.

Essentially, however, you don't need a cheesy landing page. A landing page is just a web page, but with only one single purpose: information grab or sales. The design principles should be the same.

**We are all motivated by two things: pleasure, and avoiding pain**. This is because we are irrational and have no patience, but you can use that to increase the probability of success.

Landing pages usually have a bad reputation as they are often used for pyramid scheme meetings, weight loss pills, or some other psuedo product or service. Clients probably _want_ a gimmicky, overbearing, 'poor' design, as it attracts who they are aiming to attract (note: serious businesses use landing pages, take Zibbet or Uber, for example). **It is up to you if you want to make money by freelancing and making landing pages, but it may offend your own ideas of web design to actually be good at it!** There is a scam to use landing pages just by playing the numbers and realising that if you advertise to a large enough group of people, you will find enough idiots to purchase and give the scammer profit.

## Testing Your Work

You work is never 'finished'. It's imperative to use [GoodUI](https://goodui.org).

A/B testing is fantastic, but unreasonably expensive to run. You make the same website, but perhaps on the A version you have a 'SIGN UP' button, whereas on the B version you have an email entry field alongside the sign up button (this is what Netflix did in December 2019). You then look at the analytics and see which version converted better.

Running A/B tests is too expensive unless you are a major business, but implementing the results are not. You could therefore use goodui.org to gain insights into what has worked better for other web designs (Netflix went with the B version) and use it in your design. You will also be able to test out the other version if the first version doesn't seem to be converting as well as you predicted.

# FOUNDATION THREE: Attention to Detail

It is often the small details that make a design great. An example is the use of off-black rather than pure black. Most people won't notice, but it will be perceived subconsciously. All the small changes all add up and together become very powerful.

## UX
