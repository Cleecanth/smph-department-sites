# Using Gulp (gulpfile.js)

For gulp installation, see the [Node and Gulp Set up Readme](set-up.md).

For general gulp help see [gulp's documentation](https://github.com/gulpjs/gulp/tree/master/docs).

---

The `gulpfile.js` in the [project root](../../) controls the compilation of files from the `/_partials` folder of this project.


## How to run

There are a number of tasks that gulp can perform on this project, but there are three main tasks that will concern your work. To run a task, simply run `gulp taskname` from the command line. You can, and should, string tasks together by running `gulp task othertask`.

* `serve`: Watches files for changes, and spins up a local server where you can see your project in the browser. **This is recommended for most workflows.**

* `prod`: Runs through the `/_partials` folder, processes all files, and minifies them. Other than images and kits, minified files get a `.min` suffix added to their file names (`utility.js` will output `utility.min.js`). Does not watch files on its own (run `gulp prod watch` for that).

* `default`: Runs through all files in `/_partials`, processing them without minifying. Does not watch files on its own (run `gulp default watch` for that). If you just run `gulp` by itself, this task will run.

_If you want to minify and run a local server, use `gulp prod serve`._


## Required plugins

At the top of the `gulpfile.js`, you'll see a bunch of variables with `require('some-module')` values. Gulp by itself doesn't do much, but its power comes in the form of small, reusable plugins. So, in this section, we are importing those plugins and storing them as variables to be called on later.


## Configuration variables

Under our plugin imports, there are three configurable variables. Variables written in all caps denote project-specific, user settings.

* `AUTOPREFIXER_BROWSERS` (array): Used by the [autoprefixer](https://github.com/postcss/autoprefixer) plugin to add vendor prefixes to your compiled CSS. This controls what browsers you want in your project. For browser support syntax, see https://www.github.com/ai/browserslist#queries .

* `PATHS` (object): Tells gulp where to look, and where to to place files after compilation.
    * `scss`: Sass file paths.
    * `js`: Javascript file paths.
    * `kits`: Kit file paths.
    * `images`: Image file paths.
    * `watch` (array): Tells gulp what files it should check for changes. This can accept many
    * `main` (array): This is only used by `scss` since it might be different from your watch command.
    * `dest` (string): Destination **folder** path for compiled files.

* `BROWSER_SYNC_WATCH` (array): Used by the local gulp server [Browsersync](https://www.browsersync.io/docs/gulp/), so it can refresh your browser when it sees changes. It's recommended that you have browserSync watch only compiled files, since those are the files are the ones it will be serving to the browser.

* _A note about file paths_: File paths are written in the [Node Glob] (https://github.com/isaacs/node-glob) syntax. Here are some basics:
  * `./` is your project root. It's almost always the same place as your `gulpfile.js` location.
  * `**` is any file or folder of any depth. If you aren't sure how deeply nested your project is, using `./**` will cover all files and folder from your project root onwards.
  * `*` is any file within the current path. `./*` would be all files in the root of your project.
  * `!` before any pattern means "not this". This only works if as an exception to a positive match, so you must use something like `'./*' , '!./*.js'` (all files in the root, except those that end in `.js`).
  * `./**/*.js` would get you all files in your project ending in `.js`. Using qualifiers at the end of your path globs is a good way to keep things organized and performant.
  * Generally, the more specific you can be, the better. This prevents gulp from watching too many unnecessary files.


## Tasks

For tasks that run a string of other tasks see [How to run](#how-to-run) for use cases. These are the most commonly used.

**Singular Tasks**

These are tasks that do one thing, and - while not commonly used on their own -  create the backbone of our gulp file. You can run these like any other task (`gulp task`).

* `watch`: Watches files for changes and run other tasks when changes are detected. This uses the `PATHS` variable to know where to look.

* `browserSync`: Uses the [Browsersync](https://www.browsersync.io/docs/gulp/) plugin to serve up your files locally. See the [Browsersync documentation](https://www.browsersync.io/docs/options/) for configuration options. The default options should work for most projects, but is capable of doing much more (including proxying to a live server).

* `sass`: Runs your `scss` files through the [Sass](http://sass-lang.com/) (via node-sass and libSass libraries) pre-processor and the [autoprefixer](https://github.com/postcss/autoprefixer) library.

* `js`: Concatenates and (optionally) minifies javascript files via  [gulp-include](https://www.npmjs.com/package/gulp-include) and [uglify](https://www.npmjs.com/package/gulp-uglify).

* `kits`: Concatenates and prettifies (normalizes spacing) your `.kit` files into `.html` files via [gulp-kit](https://www.npmjs.com/package/gulp-kit) and [prettify](https://www.npmjs.com/package/gulp-prettify).

* `...`: Outputs a nice message saying that Gulp has started. Useless on its own.

## Notes

There may be some additional lines in the `gulpfile.js` that are worth a quick explanation.

* `plumber()` is just a way of triaging error messages from each task into a single format. [gulp-plumber](https://www.npmjs.com/package/gulp-plumber) prevents gulp from quitting when it hits a simple error from a plugin. This is mostly useful when a `kit` or `scss` file has a syntax error.

* `changed()` makes sure that only changed files are run through tasks. Tasks that concatenate other files tend to falsely pull every file of that type into a gulp task, which is a waste of time.

* `gIf()` works like a simple `if-else` statement, preventing us from having separate minification tasks when `prod` is used.

* `notify()` adds a GUI notification to the desktop when an error has occurred. This should help when the command line is behind another window.
