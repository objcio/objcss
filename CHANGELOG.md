# objcss Changelog

## Collections

### Globals, Settings, Setup

* Changed XL breakpoint to 1100px.

### Namespaces

* Added an Inline Code namespace, for paragraphs or section with inline `<code>` tags.

### Components

* Added `tight` variant to Button.
* Added a 22:10 variant to Ratio.

### Utilities

* Added `+++` variants of negative spacing to Spacing utility.
* Added Gradient utility `gradient-episode-color` for ST episode tint effect.
* Added Text utilities `lh-135` and `hyphens`.
* Added Sizing utility `width-1/6`.
* Added Effect utility `transition-scale`.
* Changed Text utility `fz-16` to use em-based sizing.
* Renamed Effect utility `transition-scale` to `transition-transform`.
* Added Effect utility `hover-scale-1.25x`
* Changed Effect utilities `hover-*` to force GPU animation.
* Added Icon utility `icon-46`.
* Added Text utility `text-shadow-25`.
* Added Border utilities `border-color-subtle-blue`, `border-color-lighten-10`.
* Changed Button component to work better with `<button>` elements.
* Added Display utilities `position-stretch-h` and `position-stretch-v`, to complement already existing `position-stretch`.
* Added Display utilities `inline-descendants` and `inline-children`. These make its descendants/children become inline elements. Together with `nowrap` and `overflow-hidden`, it can clip a sequence of paragraphs to a single line of text.
* Added breakpoint prefixing to negative Spacing utilities.


## Books & Bundles, Spring/Summer 2017

### NEW: Theming

* Set up a new, more powerful and flexible theming system. There are three groups of themes: 1) the default theme, 2) book themes, and 3) bundle themes. The book and bundle themes are used on book and bundle pages and components, and the default theme is used everywhere else. More themes can be added in the future for special parts of the site.
* Themes are defined in the `$themes` map variable, which automatically takes in book and bundle color variables `$book-colors` and `$bundle-colors` defined in Settings to create book an bundle themes. The default theme is added manually.
* The name of the default theme is `default`, and the book and bundle themes are named after their respective slug.
* Each theme defines at least two colors: a `main` color, and a `highlight` color. For the default and book themes, these are different colors. For the bundle themes, these are the same color. Both are always defined so that theme-dependent color utility classes such as `color-theme-highlight` or `bgcolor-theme-main` can be used regardless of the current theme and always produce a color.
* Each theme can also defined a `nav` color. This is a color used for navigational elements such as the site-wide navigation links, or active tabs. If not defined, a fallback color to be used can be supplied when accessing theme colors using the `theme-color` or `theming` Sass functions. More on this topic later.
* Themes are defined with the class `theme-[theme_name]`.
* Themes can be defined at three levels:
  1. Global. The theme is set at the `<body>`, and utility classes such as `color-theme-main` will use that theme’s colors.
  2. Scope. The theme is set at node level (usually a complex component) with `theme-[theme_name] is-scoped-theme`. Utility classes inside that component will use that component’s theme colors, not the global theme colors. Scopes can’t be nested.
  3. Element. The theme is set at node level, with `theme-[theme_name] is-element-theme`, and utility classes *on that node* will use that element’s theme colors, but descendants *won’t*. This is not often used, but useful to limit the theme’s application.
* The theme-dependent utility classes are `color-theme-[color_keyword]` and `bgcolor-theme-[keyword]`, setting the `color` or `background-property` colors to that theme’s keyword color (`main`, `highlight`, `nav`).
* There are also the utility classes `hover-color-theme-[color_keyword]` and `hover-bgcolor-theme-[keyword]`, which work like above, *except only* for Global level themes and `main` and `highlight` colors.
* For setting properties other than `color` and `background-color` based on themes, the *mixin* `theming($filter)` is available.
  * When called and passed some CSS declarations as `@content`, it will iterate through themes, nesting those declarations under the  the theme’s `.theme-[theme_name]` selector.
  * During each iteration step, the `theming($keyword, $fallback: null)` *function* accesses the current iteration step’s themes colors by keyword, also taking an optional fallback if such color doesn’t exist (as it can happened with `nav` colors). For more low-level access, the iteration step’s theme is available in the `$_theme` global variable.
  * When used, the `$filter` option in the mixin will limit iteration through the theme names passed in `$filter`. Usually, these will be be `$books` or `$bundles`.
  * The `theming()` mixin only works with Global themes.


### Globals, Settings, Setup

* Reorganized the Settings file, grouping colors in Sass maps and adding quick access functions: `$colors` & `color()`, `$bgcolors` & `bgcolor()`, `$book-colors` & `book-color()`, `$bundle-colors` & `bundle-color()`.
* Added `$books` and `$bundles` global variables.
* Changed some spacing units and made gutters smaller in Settings.
* Added a global style to reset `<hr>` appearance.
* Added individual import files for each of the codebase’s main file types. This allows websites using `objcss` to customize import order, letting them place custom components or utilities in the right import order.

### Namespaces

* Added theming to the Links namespace.
* Added a Numbered namespace, which prefixes elements with increasing numbers. Used for numbering `h1` on Online Previews of Books.
* Added theming to the Text namespace.
* Added special styles to the Text namespace to deal with code formatting in Books’ Online Previews.

### Components

* Added simpler, no-nonsense button components:
  * `button` is a simple button. `button--themed` colors it according to the theme’s colors.
  * `bordered-button` is a simple ghost button. `bordered-button--themed` colors it according to the theme’s colors.
  * `arrowed-button` is used together with one of the ones before, and it adds a → to the right side of the button.
  * Idea here is to eventually phase out the old buttons in favor of simpler ones.
* Added a Scroller component, for horizontal content scrollers, as used to show Books and Bundles.
* Added a mixin to Logo component to help style the logo’s parts `objc` / `↑↓` in different colors, but one single color on hover.
* Added theming to the `--themed` modifier of the Logo component.
* Added a `--white` modifier to the Logo component.
* Added theming to the Table of Contents component
* Added struck-through headings to the Table of Contents component
* Tweaked spacing on Label component.
* Transformed Patterns from component to utilities file.
* Moved `objcio/website`-specific components outside of `objcss`, namely `article`, `blog-post`, `blog-postlist`, `book`, `buy`, `contributors`, `feature-books`, `feature-newsletter`, `issue-unit`, `issue`, `post-article`, `post-issue`, and `store-modal`. This reduces file size on the `objcio/video-backend` project.
* Removed the Book Box component. Changed display of books.
* Removed the Book Button component. Changed to a different button style.
* Removed the Page Header component. Now styled with utility classes.
* Removed the Preview Header and Preview Banner components
* Removed the Sample component. It wasn't used anymore.
* Removed the Search component. Now styled with utility classes.
* Removed the Header component. Now styled with utility classes.
* Removed the Footer component. Now styled with utility classes.

### Utilities

* Added Color utilities for Bundles: `color-[bundle_slug]` and `bgcolor-[bundle_slug]`.
* Added Color utilities for Books: `color-[book_slug]-(top/bottom)` and `bgcolor-[book_slug]-(top/bottom)`.
* Added Color utilities for all named colors in `$colors`, as `color-[color_name]`, generated dynamically.
* Added Color utilities for all named background colors in `$bgcolors`, plus all in `$colors`, as `bgcolor-[color_name]`, generated dynamically.
* Added Color utilities for translucent black colors and background colors: `color-darken-(35/50/65)` and `bgcolor-darken-(35/50/65)`.
* Added Color utilities for theme colors, as described above.
* Renamed Color utilities `bg-gradient` to `gradient` and moved them to their own file.
* Added Border utilities `no-radius-top`, `no-radius-bottom`, which override border radius.
* Added Border utility `border-stack`, which places borders in-between consecutive elements using the utility class name.
* Added Display utilities `position-outside-n`, `position-outside-e`, `position-outside-s`, `position-outside-w`, which position elements at `100%` of `bottom`, `left`, `top`, and `right`, respectively. This allows for positioning elements at the outside edges of its relative container.
* Added Display utilities `overflow-visible`, `overflow-scroll`.
* Added Display utility `appearance-none`.
* Added Display utility `position-sticky`.
* Added Flex utility `flex-1-1-0`, for growing and shrinking, but basis set to 0.
* Added Effects utilities `transform-origin-[X]`, with X being `center` or each of the cardinal and intercardinal directions.
* Added Hover utility `hover-scale`.
* Added Hover utilities for theme colors, as described above.
* Added Hover utility `hover-bgcolor-gray-97`.
* Added Icon utility `icon-26` for 26px square icons.
* Added Icon utilities `icon-scale-50` and `icon-scale-100` for scaling icons by 50% or 100% of their original size. This is done with the `font-size` property, not transforms.
* Added Sizing utilities `height-(1-10)`, `height-auto`, `height-full`, `width-auto`.
* Added Sizing utilities for book thumbnail and large book thumbnail: `width-book-thumb`, `max-width-book-thumb`, `width-book-thumb-large`, and `max-width-book-thumb-large`.
* Added Text utility `text-overflow-ellipsis`.
* Simplified the Spacing utilities by writing them manually instead of an unreadable and hard-customize mixin of nested iterators.
* Added breakpoint prefixing to Spacing utilities `pa`, `pt`, `pr`, `pb`, `pl`; and `ma`, `mt`, `mr`, `mb`, `ml`.
* Added a `cover-peek` modifier to the `ratio` utility, and removed the `cover-cropped` modifier.
