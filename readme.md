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

and:

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
