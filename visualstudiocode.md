# Visual Studio Code

## Shortcuts

    - Side-Panel: ctrl+ B
    - Search: ctrl+shift+ F
    - Extensions: ctrl+shift+ X
    - Debugging: ctrl+shift+ D
    - Explorer: ctrl+shift+ E
    - Git Version Control: ctrl+shift+ G

    - Command Palette: ctrl+shift+ P

    - New Terminal: ctrl+shift+ @
    - Toggle Terminal: ctrl+ @

    - Zen Mode: ctrl+ K, let go and press Z

    - Forward Toggle through open files: ctrl + tab
    - Backwards Toggle through open files: ctrl + shift + tab
    - Quick file search: ctrl+ P

    - Close current file: ctrl+ W

## The User Interface

### Setting Up Your Workspace

    - You can drag files that are open with their tab and place them alongside one another to view them at the same time.
    - You can even place files 'on top' of one another if you want to create a grid system (probably need a large monitor...)
    - You can switch between the open 'panes' by pressing ctrl+ (1, 2, 3...)

### Navigating and Manipulating Text

    - Holding ctrl+ <> allows you to jump through code quickly

    - End key takes you to the end of a line, the HOME key above it takes you to the beginning of a line
    - End/Home while holding ctrl will take you to the end or beginning of the entire file

    - ctrl+ D allows you to select a variable or other code name in its entirety, allowing you to delete and retype more quickly
    - Continuing to press ctrl+ D will continue selecting the next instance of that code - VERY useful
    - alt+ click also allows you to add multiple cursors
    - ctrl+ alt+ shift+ arrows will allow you to go full crazy with adding multiple cursors

    - ctrl+ shift+ <> allows you to select code in lengths

    - alt+ up/down arrows allow you to move a line up or down
    - alt+ shift+ up/down will create a copy of the line!
    - ctrl+ X and ctrl+ V are the cut and paste shortcuts (ctrl+ C is of course copy) *To do this for entire lines you DO NOT need to select the whole line, you just need to be on that line when you use the shortcuts

### Search & Replace

    - ctrl+ F brings up the search bar, but if you have already selected a variable with ctrl+ D then you press ctrl+ F it will bring up the bar with that variable already selected
    - After searching, you can press enter to flip through every position of that code (shift+ enter will take you backwards through each position)
    - Use the dropdown arrow on the search bar to reveal "replace" and type what you would like to replace, and press enter to change one instance (keep pressing enter to change more) ___OR___ press ctrl+ enter to change ALL of the instances of that variable name throughout the file at once

    - To replace all of an element/variable name in an entire folder or project, you can use the ctrl+ D and then ctrl+ shift+ F and repeat the above process (but you will need to press ctrl+ alt+ enter and click the warning!)

    - ctrl+ shift+ H goes straight to the replace

### IntelliSense

    - The autocomplete gives great information: for example, a purple box denotes a method or function, whereas a blue box denotes a value. "abc" refers to something you have typed in your code previously.
    - The built-in IntelliSense is great for CSS, HTML, JS, but you need an extension for Python, C++, C#, Java, etc.

### Emmet

    - It is worth making an Emmet cheatsheet and practising as it is a kind of shortcut way to write HTML and CSS
    - Boilerplate HTML: simply type an ! and then press enter to get a boilerplate HTML file
    - You must define the code you want to write in before doing this, however.
    - p + enter will generate a paragraph tag, (div, title, h1, h3, img, a, etc.)

    - Class: If you type .container, then press enter, Emmet will create a div element with the class of container
    - Specifying the element type, e.g. h1.frogman for example, you will get a <h1 class="frogman> etc.
    - You can combine to add class and ID, for example div.container#side-bar

    - To get multiple elements you can use * (e.g. li*5)
    - Even better, you can give each element a numbered ID by using a $ (for example li#item$*5)

    - Auto-populate with child elements can be done with > (for example, div>h2)
    - You can similarly create siblings, for example div>h2+p

## Customization

### Customising Shortcuts

    - Under settings in the bottom left-hand side of the screen, you can select 'keyboard shortcuts'

### Workspace Customisation

    - You can save for either the User or Workspace level
    - You can install FiraCode if you would like to have cool font with ligatures (special signs)

### Popular Extensions

    - In the extensions search bar you can type @installed to see what you have installed
    - If you need to find an extension after installing, try ctrl+ shift+ P, and search
    - Quokka gives you instant output of your JS code within VS code, so it is handy to try out bits of JS
    - Polacode generates a screenshot of your code that you can then send or post to StackOverflow
    - Advanced New File allows you to save a new file directly as you open it to the current work folder (if you like this, you can override the ctrl+ N new file command to work for Advanced New File instead. Very cool.)
    - VSCode Icons are quite cool
    - Auto Rename Tag could be useful as if you rename a HTML tag it will automatically rename the corresponding open or close tag (check if this is now in-built as an option in VS Code now)
    - Live Server allows an auto-updating live server (not necessary if you are using a framework live Webpack)
    - Open In Browser - gives an option to open in a browser if you right-click a file from the workspace
    - Better Comments: Really cool way to bring attention to various types of comments **This is similar to the TODO/FIXME that I currently use
    - JavaScript ES6 Code Snippets: Adds essential snippets automatically to your JS, good for saving time **There are also snippets extensions for REact/Redux/GraphQL/Vue/Angular, etc.
    - Search node_modules allows you a handy way to search your node_modules file
    - Import Cost: When you use import to bring in a module you can see the size of the import, and then reduce that size if you try and just import the part that you need instead
    - DotENV or ENV both add color to your .env files to make them look a bit more readable
    - CSS, HTML, and npm IntelliSense extensions are great, of course

### Settings Sync Extension

    - If you use a different CPU or get a new laptop, you don't want to have to go through an re-enter all of the customizations you have made, so settings sync is really useful
    - It basically provides a way to upload all your VS Code settings to GitHub
    - You can also download all your settings from GitHub and then apply them to your computer

### Themes

    - You can search for these just like you would for extensions, and there are also some in-built themes. Some examples are: Cobalt 2, Shades of Purple, Night Owl, Dracula Official, etc.

## Writing and Formatting Code

### Snippets

    - You can generate snippets of your own by clicking settings and then choosing User Snippets
    - When writing your snippets, if you add $1, that is where the cursor will end up first. You can then add more ($2, $3, etc.) and press tab to move on to them as you finish each one
    - $0 is the end point where your cursor will fall after all the snippets have been completed
    - You can use $ with a word that does the same thing, e.g. $arrayName or $index etc.

### Working with Markdown

    - If you open your command palette you can search Markdown and you have options such as open preview, or export as pdf, etc.
    - Ctrl+K then V will open the Markdown preview to the side (ctrl+ shift+ V will open the preview in a new file tab)
    - Some useful extensions include: Markdown Lint, Markdown Shortcuts, Markdown TOC (auto generates table of contents), and Markdown All in One looks good to me!
    - Ctrl+ shift+ P and search Markdown to allow you to export to pdf

### Organizing Your Code

    - When using import/export, you can use the command palette and search for 'organize imports' to automatically organize your imports
    - If you select a piece of code you can right-click and select 'Refactor" and then you have options, such as changing to a named function, or moving to a new file!!!
    - If you have a named variable, you can right-click and rename and it will rename the variable throughout the code
    - Quick Comment: ctrl+ / will comment in or out a particular line of code (obviously this works for blocks of code if you select them, too)

### Prettier

    - Really useful way to keep your code looking nice and standardized, but needs to be installed, so check the regular VS Code settings first (tab width, semi-colons, single-quotes, trailing comma), but SEE ESLINT BELOW!!

### ESLint

    - In your project you need to install "npm i -D eslint", then "eslint init" and there is an ESLint extension so you can access via the command palette
    - In VS Code settings, turn off 'format on save', then search eslint and select to format on save there

## The Integrated Terminal

### Customization of the terminal

    - You can toggle the terminal (while keeping it open) by pressing ctrl+ @
    - You can color and rename the terminal by right-clicking the default name and changing it (e.g. Server, Frontend, etc.)
    - To change the color theme you can go to settings, then search color customization, which opens a settings.json file. From there you can change the color theme (if it is not there, start a new config at the bottom with double-quotes called workbench.colorCustomizations)

## Git and GitHub

### In-Built Integrations

    - There is a .git file under C:/User/mj which is why I had a huge problem with my 10,000 commits
    - Config your git with "git config --global user.name "Your Name"" and then "git config --global user.email "name@mail.com""
    - Initiate a repository and you can type "git status" if you want to see what is in the repository at the moment
    - You can use 'Source Code Repositories' to change the active repository
    - The folder you are working from shows up under 'Changes' and are initially 'Untracked', but if you click the + sign you can stage them (i.e. 'Add' them)
    - This is good because you now make changes to your file and it does not affect the 'Staged Changes', only the 'Changes', which you would need to again manually + to the 'Staged Changes'
    - If you want to commit the staged changes, you type 'git commit -m "Added files for <whatever reason>" from the terminal __OR__ type your message in the Source Control input field and press ctr+ enter (or press the tick icon)
    - You can click on the ... under Source Control Repositories for multiple options, including adding a new branch





