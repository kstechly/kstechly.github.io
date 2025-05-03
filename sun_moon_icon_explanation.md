 # Integrating Sun/Moon Theme Toggle Icons with Tabler Icons

 This guide will help you add three Tabler Icons (`sun-moon`, `moon-filled`, `sun-filled`) to a new web project without requiring a Sass build. You will:
 1. Self-host the Tabler Icons webfont files.
 2. Create a minimal CSS file to load the font and define icon classes.
 3. Use the icons in your HTML markup.

 ---

 ## 1. Download and Place the Webfont Files

 1. Go to the Tabler Icons GitHub releases page: https://github.com/tabler/tabler-icons/releases
 2. Download these files from the `iconfont` folder:
    - `tabler-icons.woff2`
    - `tabler-icons.woff`
    - `tabler-icons.ttf`
 3. Place them in your project directory, for example:
    ```
    your-project/
    ├── assets/
    │   └── fonts/
    │       ├── tabler-icons.woff2
    │       ├── tabler-icons.woff
    │       └── tabler-icons.ttf
    └── ...
    ```

 ## 2. Create the Icon CSS

 Create a CSS file (e.g. `assets/css/tabler-icons.css`) with the following content:

 ```css
 /* 2.1 Load the Tabler Icons font */
 @font-face {
   font-family: 'tabler-icons';
   font-style: normal;
   font-weight: 400;
   src: url('../fonts/tabler-icons.woff2?v3.0.1') format('woff2'),
        url('../fonts/tabler-icons.woff?v3.0.1')  format('woff'),
        url('../fonts/tabler-icons.ttf?v3.0.1')   format('truetype');
 }

 /* 2.2 Base class: use the icon font */
 .ti {
   display: inline-block;
   font-family: 'tabler-icons' !important;
   font-style: normal;
   font-weight: normal;
   font-variant: normal;
   text-transform: none;
   line-height: 1;
   /* Better font rendering */
   -webkit-font-smoothing: antialiased;
   -moz-osx-font-smoothing: grayscale;
 }

 /* 2.3 Icon-specific classes */
 .ti-sun-moon::before    { content: "\f4a3"; } /* system theme */
 .ti-moon-filled::before { content: "\f684"; } /* dark mode */
 .ti-sun-filled::before  { content: "\f6a9"; } /* light mode */
 ```

 Adjust the `src` paths if your directory structure differs.

 ## 3. Include the CSS in Your HTML

 In the `<head>` of your HTML pages, add:

 ```html
 <link rel="stylesheet" href="assets/css/tabler-icons.css">
 ```

 Now your `.ti` classes will render the Tabler Icons font.

 ## 4. Use the Icons in Markup

 In your HTML, use the following pattern:

 ```html
 <button id="theme-toggle" title="Toggle theme">
   <!-- System preference icon -->
   <i class="ti ti-sun-moon"    title="System theme"></i>
   <!-- Dark mode icon -->
   <i class="ti ti-moon-filled" title="Dark mode"></i>
   <!-- Light mode icon -->
   <i class="ti ti-sun-filled"  title="Light mode"></i>
 </button>
 ```

 Each `<i>` element uses the `.ti` base class plus a modifier (`.ti-sun-moon`, etc.) to display the correct glyph.

 ---

 ## 5. (Optional) Use the CDN or NPM Package

 If you prefer not to self-host the font, you can include the official Tabler Icons CSS directly:

 ```html
 <!-- CDN -->
 <link
   rel="stylesheet"
   href="https://unpkg.com/tabler-icons@latest/iconfont/tabler-icons.min.css"
 >
 ```

 Or install via NPM and copy the `iconfont` folder:

 ```bash
 npm install tabler-icons
 # then copy node_modules/tabler-icons/iconfont into your assets/fonts/
 ```

 With either approach, you can skip the `@font-face` block and only need the icon-specific rules (or simply rely on the pre-built CSS).  