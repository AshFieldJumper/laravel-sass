laravel-sass
============

Automatic Sass-to-CSS compiling for Laravel 4 (and any other framework by the way) while being in development.
Every time you run your app (hitting index.php) laravel-sass will automatically compile all .scss files in your scss
folder to .css files in your css folder. Support latest version of Sass (scss syntax) and mixins. Boom!

## Installation & Usage

Add this to your composer.json, please note that this is a **require-dev**, not a normal **require**. This devides
real dependencies from ones you only need for local development.

```json
"require-dev": {
    "rickry/laravel-sass": "1.0"
}
```

Add this line into your `public/index.php` in Laravel, right **before** `$app->run();`.

```php
SassCompiler::run("../resources/sass/", "css/");
```

The first parameter is the relative path to your scss folder (create one) and the second parameter is the relative
path to your css folder. Usually it totally makes sense to create those folders in the public folder.
Make sure PHP can write into the css folder by giving the folder
`sudo chmod -R 777 public/css` (when being in /var/www).
**Note:** 777 is just for development, in a production server there's no need to give that folder any write-rights.

Install or update your Composer dependencies to add laravel-sass by doing `composer install` or `composer update`.
Composer automatically installs everything in require-dev by default.

**IMPORTANT:** When you later deploy your application and don't want to install the require-dev stuff, then do
`composer install --no-dev` (or `composer update --no-dev`).

## Optional feature

There's an optional third parameter for `SassCompiler::run()` that expects one of the strings explained on
http://leafo.net/scssphp/docs/#output_formatting. This defines the desired output. `scss_formatter` is the standard
laravel-sass uses, choose `scss_formatter_compressed` if you need a minimized css file. `scss_formatter_nested` is
for nested output, optimized for readability.

## Testing

To test if everything works okay, simply add this to the head of `app/views/hello.php`:
`<link rel="stylesheet" type="text/css" href="css/style.css">` and put a file called style.scss in your scss folder.
Now run the app and play around with the (s)css rules in your style.scss, after each refresh you should see the changes
instantly!

## How @import works

The `@import` of sass rules from other files works now perfectly. Make sure to import the files like it should be:
If the file is called _colors.scss and is in the basic scss folder:
```
@import 'colors';
```
If the file is called _colors.scss and is in the subfolder `modules` of the basic scss folder:
```
@import 'modules/colors';
```
Read the official docs for more.

## When deploying ...

.. then make sure you comment out this line again: `SassCompiler::run("scss/", "css/");`. Future releases of this
tool will have a development/production switch/recognizer.

## To use the very latest features of Sass:

Currently php-sass fetches v0.0.14 (August 2014) of *leafo/scssphp* as a compiler. For latest features you might want a 
newer version, so have a look here https://github.com/leafo/scssphp/releases and edit the composer.json accordingly.

## Used scripts

This tool uses the excellent [scssphp Sass compiler](http://leafo.net/scssphp/).
scssphp supports the latest SCSS syntax (3.2.12).

## Other projects

- https://github.com/panique/huge (a framework with full login system behind)
- https://github.com/panique/mini2 (a naked application on top of Slim)
- https://github.com/panique/mini (a super-simple naked barebone application)
- https://github.com/panique/php-sass (SASS compiling in pure PHP)
- https://github.com/panique/php-long-polling (long-polling with PHP, extremely simple)
- My blog DEV METAL: http://www.dev-metal.com

## License

Licensed under [MIT](http://www.opensource.org/licenses/mit-license.php). Totally free for private or commercial
projects.

## Support

If you think this script is useful, then think about supporting the project by renting your next server at
[Host1Plus](https://affiliates.host1plus.com/ref/devmetal/36f4d828.html) or 
[DigitalOcean](https://www.digitalocean.com/?refcode=40d978532a20).
