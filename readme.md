# Tools Site Tech and References
General overview of stuff blah blah blah

1. [Layout](#Layout)
2. [Tech Stack](#Tech-Stack)
3. [Dev Recipes](#Dev-Recipes)
4. [Code Layout](#Code-Layout)
5. [Standards](#Standards)
    1. [Modules](#Modules)
    2. [Transpiler](#Transpiler)
    3. [Styles](#Styles)
    4. [Build tools](#Build-tools)
    5. [Libraries](#Libraries)

***

More normal text
## Layout
A rough outline for directory structure for development layout is shown below. The files are just examples.

```
webroot/
??? docs/
?   ??? index.html
?   ??? modules.list.html
?   ??? img/
?   ?   ??? glyphicons-halflings.png
?   ?   ??? glyphicons-halflings-white.png
?   ??? styles/
?   ?   ??? darkstrap.css
?   ?   ??? jsdoc-default.css
?   ??? invmap.html
??? swagger-ui/
??? node_modules/
??? bin/
?   ??? update-db.sh
?   ??? glob-updates
?   ??? ses
??? img/
?   ??? picture.png
?   ??? small/
?   ?   ??? picture.png
?   ??? medium/
?       ??? picture.png
??? dist/
?   ??? index.html
?   ??? js/
?   ?   ??? all.js
?   ??? vendor/
?   ?   ??? jquery.min.js
?   ?   ??? lodash.min.js
?   ??? styles/
?       ??? all.css
??? vendor/
?   ??? jquery/
?   ?   ??? dist/
?   ?   ??? jquery.js
?   ??? lodash/
?       ??? dist/
?       ??? lodash.js
??? templates/
?   ??? tmpl-1.hbs
??? schemas/
?   ??? story.json
??? src/
?   ??? server.js
?   ??? source2.test.js
?   ??? source3.test.js
?   ??? lib/
?       ??? views/
?       ?   ??? navbar/
?       ?   ?   ??? navbar.js
?       ?   ??? dropdown/
?       ?       ??? dropdown.js
?       ??? controllers/
?       ?   ??? dispatcher/
?       ?   ?   ??? dispatcher.js
?       ?   ??? async/
?       ?       ??? ajax.js
?       ??? database/
?       ?   ??? mongo.interface.js
?       ?   ??? mysql.interface.js
?       ??? require-conf.js
??? test/
?   ??? source2.test.js
?   ??? source3.test.js
?   ??? lib/
?       ??? views/
?       ??? controllers/
?       ??? database/
??? mongodb/
?   ??? admin.0
?   ??? admin.1
?   ??? journal/
?       ??? prealloc.1
?       ??? prealloc.2
??? uploads/
?   ??? from-user.dat
??? fonts/
?   ??? flaticon.ttf
?   ??? flaticon.wof
?   ??? flaticon.eot
??? css/
?   ??? examples.css
??? sass/
?   ??? examples.sass
??? LICENSE
??? README.md
??? bower.json
??? package.json
??? .bowerrc
??? index.html
??? server.js
```

## Tech Stack

Component | Application | Notes
---:|---|---
Web server | ***Node.js*** | Because it's *fast*, *powerful*, and *gorgeous*
OS | ***Linux*** *(Ubuntu/Debian)* | The best and most reliable OS in the world, why use anything else?
Source Repo | ***git*** | Widely used for larger projects, highly resistant to loss, fast, each copy is a full repo (no central repo).
Database | ***MongoDB*** | One-to-one correspondence with native objects, scales extremely well, very fast, very simple.

## Dev Recipes
How to code and stuff
## Code Layout
More important stuff
## Standards
Now for the nitty-gritty
### Modules
For this project, we'll probably go with the ES6 module system. It's still lacking native support but a good shim is available and will suffice until support goes native. When that'll happen is unclear.

I tend to always go with *AMD* using **RequireJS** but will consider using **browserify** for this project. It has some distinct advantages, as well as some stylistic drawbacks. The advantages are that there is only one install directory and only one install method. It also has the largest library selection through **npm**. 

It results in code that looks identical to the server-side modules, i.e.:

```javascript
var $ = require( 'jquery' ),
    _ = require( 'lodash' );

module.exports.MyClass = function( whatever ) {
    // Constructor code here...
};
```
Not very pleasing, honestly. I don't really like the **CommonJS** module system.

By using **bower** for module management and **RequireJS** for the loader, we end up with the much more appealing code, for example:

```javascript
define( 'myclass', [ 'jquery', 'lodash' ], function( $, _ ) {

    var privateVar = 10;

    function MyClass( whatever )
    {
        // Constructor code here...
    }

    return MyClass;
});
```

I really like the latter approach but it may be time to try something new. Let's discuss.

### Transpiler
We need to support the new ES6 standard coming out in the next couple of months. Initially through a transpiler because **class** is not yet supported on **Chrome** and **Edge** and **arrow** functions are not yet supported on **Chrome**. Once **Edge** is out at the end of July, we should stop transpiling and go straight ES6 despite a few lacking features. Since this is an internal tool, this should not pose a problem. Be aware that all 3 supported browsers (**Chrome**, **Edge**, and **Firefox**) will need to have the *"Support experimental JavaScript flags"* turned on.

For transpiling, it will be **Babel** + **core-js** or **Traceur** with the former being prefered but the latter being easier to set up.

### Styles
Semantic-UI, I'm thinking
### Build tools
1. Gulp
2. Bower/Browserify/npm
3. SCSS

### Libraries
jQuery, Lodash, Moment, bluebird
