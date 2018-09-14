# lkHighcharts - Looker's fork of Highcharts

Highcharts is extremely extendable, so why would we need to fork it? As it turns down, in the root of Highchart's bootstrap code, it throws an error if Highcharts is already defined on the global scope. This is bad for us, since we potentially have two versions of Highcharts loading - one for custom visualizations, and a second one that we use internally. That being said, this fork makes exactly one change - it changes the name of that global variable from `Highcharts` to `lkHighcharts`. This prevents any additional highcharts loads from custom visualizations or anywhere else from interferring with our internal Highcharts. The great part about it is that it still exports a variable named `Highcharts`, so if you use the import syntax, you do not have to make any code changes to the codebase. You can still call `Highcharts.whatever_you_want`.

## Supporting this Fork

As was said above, there is exactly one codebase change in this fork to change the name of that global variable.

## Updating, building the code, and releasing.

If your upstream origin doesn't exist, you can add it with:

```
git remote add upstream https://github.com/highcharts/highcharts.git
```

Then run:
```
git fetch upstream
```

<<<<<<< HEAD
and:
=======
## Load Highcharts as an AMD module
Highcharts is compatible with AMD module loaders (such as RequireJS). Module files require an initialization step in order to reference Highcharts. To accomplish this, pass Highcharts to the function returned by loading the module. The following example demonstrates loading Highcharts along with two modules using RequireJS. No special RequireJS config is necessary for this example to work.
```js
requirejs([
    'path/to/highcharts.js',
    'path/to/modules/exporting.js',
    'path/to/modules/accessibility.src.js'
], function (Highcharts, exporting, accessibility) {
    // This function runs when the above files have been loaded

    // We need to initialize module files and pass in Highcharts
    exporting(Highcharts); // Load exporting before accessibility
    accessibility(Highcharts);

    // Create a test chart
    Highcharts.chart('container', {
        series: [{
            data: [1,2,3,4,5]
        }]
    });
});
```

## Load Highcharts as a CommonJS module
Highcharts is using an UMD module pattern, as a result it has support for CommonJS.
*The following examples presumes you are using npm to install Highcharts, see [Download and install Highcharts](#download-and-install-highcharts) for more details.*
```js
// Load Highcharts
var Highcharts = require('highcharts');
// Alternatively, this is how to load Highstock. Highmaps is similar.
// var Highcharts = require('highcharts/highstock');
>>>>>>> e4b7bf00819ca82f8aa593713d1f99084a3c21d7

```
git pull upstream vX.Y.Z
```

This will pull in the specified from highcharts. There should not be any conflicts, but if there are, refer to the changes above to resolve them correctly.

Once you have pulled in a new version and/or made your change. You have to build a new distribution. You can do this with:

```
npm install && gulp dist
```

The `dist` gulp task will build all of the files to the `code` directory. This will take a few minutes. Once it is complete, commit your code and PR it into this fork's master branch. Make sure all of the tests pass.

Lastly, bump up the version number in the `package.json` and run:

```
npm publish
```
This will publish the repository to our nexus to be installable by helltool.
