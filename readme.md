#Browsersync - Gulp, SASS + Jade Templates

## Installation/Usage:

To try this example, follow these 5 simple steps. 

**Step 1**: Clone this entire repo
```bash
$ git clone https://github.com/blenderdeluxe/gulp-jade.git
```

**Step 3**: Clear cache NPM
```bash
$ npm cache clean
```

**Step 3**: Install dependencies
```bash
$ npm install
```

In case that npm start not work because node-sass you need rebuild this with this command
```bash
npm rebuild node-sass
```

If this not work again you try with this
Uninstall sass
```bash
$ npm uninstall --save-dev gulp-sass
```

Reinstall sass
```bash
$ npm install --save-dev gulp-sass
```

**Step 4**: Run the example
```bash
$ npm start
```

### Additional Info:



### Preview of `gulpfile.js`:
```js
var gulp        = require('gulp');
var browserSync = require('browser-sync');
var sass        = require('gulp-sass');
var jade        = require('gulp-jade');
var reload      = browserSync.reload;

/**
 * Compile jade files into HTML
 */
gulp.task('templates', function() {

    var YOUR_LOCALS = {};

    return gulp.src('./app/*.jade')
        .pipe(jade({
            locals: YOUR_LOCALS
        }))
        .pipe(gulp.dest('./dist/'))
});

/**
 * Important!!
 * Separate task for the reaction to `.jade` files
 */
gulp.task('jade-watch', ['templates'], reload);

/**
 * Sass task for live injecting into all browsers
 */
gulp.task('sass', function () {
    return gulp.src('./app/scss/*.scss')
        .pipe(sass())
        .pipe(gulp.dest('./dist/css'))
        .pipe(reload({stream: true}));
});

/**
 * Serve and watch the scss/jade files for changes
 */
gulp.task('default', ['sass', 'templates'], function () {

    browserSync({server: './dist'});

    gulp.watch('./app/scss/*.scss', ['sass']);
    gulp.watch('./app/*.jade',      ['jade-watch']);
});

```

