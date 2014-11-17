# git-guppy-pre-commit-hook 
[![Travis](https://travis-ci.org/marcellodesales/git-guppy-commit-hook.svg)](https://travis-ci.org/marcellodesales/git-guppy-commit-hook) [![NPM version](https://badge.fury.io/js/git-guppy-pre-commit-hook.png)](http://badge.fury.io/js/git-guppy-pre-commit-hook) [![Dependency Status](https://david-dm.org/marcellodesales/git-guppy-pre-commit-hook.svg)](https://david-dm.org/marcellodesales/git-guppy-pre-commit-hook)

> Git pre-commit hook for Git Guppy, a Simple git-hook integration for your gulp workflows.

Go to https://github.com/therealklanni/git-guppy to install "git-guppy", which is the core module!

## Git Documentation

Details about this hook at http://git-scm.com/docs/githooks#_pre_commit

## Install

Install with [npm](npmjs.org):

```
$ npm install --save git-guppy-pre-commit-hook
npm http GET https://registry.npmjs.org/named-regexp
npm http 304 https://registry.npmjs.org/named-regexp
npm http GET https://registry.npmjs.org/lazypipe
npm http GET https://registry.npmjs.org/lodash
npm http GET https://registry.npmjs.org/shelljs
npm http 304 https://registry.npmjs.org/lodash
npm http 304 https://registry.npmjs.org/shelljs
npm http 304 https://registry.npmjs.org/lazypipe
npm http GET https://registry.npmjs.org/stream-combiner
npm http 304 https://registry.npmjs.org/stream-combiner
npm http GET https://registry.npmjs.org/duplexer
npm http GET https://registry.npmjs.org/through
npm http 304 https://registry.npmjs.org/duplexer
npm http 304 https://registry.npmjs.org/through

> git-guppy@0.2.1 postinstall /tmp/sp-quality/node_modules/git-guppy-pre-commit-hook/node_modules/git-guppy
> scripts/install.js

/tmp/sp-quality
Thanks for installing git-guppy! Install any of the hooks available now!
npm install --save git-guppy-pre-commit git-guppy-pre-commit git-guppy-post-commit ...
Go to https://github.com/therealklanni/git-guppy for a complete list!

> git-guppy-pre-commit-hook@0.1.0 postinstall /tmp/sp-quality/node_modules/git-guppy-pre-commit-hook
> ../git-guppy/scripts/install.js pre-commit

/tmp/sp-quality
pre-commit installed successfully
git-guppy-pre-commit-hook@0.1.0 node_modules/git-guppy-pre-commit-hook
├── named-regexp@0.1.1
└── git-guppy@0.2.1 (shelljs@0.3.0, lodash@2.4.1, lazypipe@0.2.2)
```

After the installation is complete, the hook is installed at `APP/.git/hook/pre-commit`.

## Usage

Follow the example below to get up and running!

### Git and Gulp integration

Usually, pre-commit hooks can be used to trigger lint, code check, among other things. The following example
creates a task called "check", which uses lint and jscs to verify the code prior to a commit. If the verification
fails, the commit process halts as expected. If it passes, profit! and commit!

```
  var gulp = require("gulp");

  gulp.task("check", function() {
    // Check all the source and the test cases together
    return gulp.src(appSourcePaths.concat(testSourcePaths))
      .pipe(jshint(SP_QUALITY_MODULE_CONFIG_DIR + "/.jshintrc"))
      .pipe(jshint.reporter(stylish))
      .pipe(jscs(SP_QUALITY_MODULE_CONFIG_DIR + "/.jscsrc"))
      .on("error", function() {
        process.exit(-1);
      })
      .on("end", function() {
        process.exit();
      });
  });

  // define guppy and its dependency hook to pre-commit.
  var guppy = require("guppy);
  guppy.init(gulp)
  guppy.tasks["pre-commit"].dep.push("check")
```

An attempt to commit will result in failure if the code does not pass the check.

```
mdesales@ubuntu [11/16/201416:28:31] /tmp/sp-quality (master *+) $ git commit
[16:28:34] Using gulpfile /tmp/sp-quality/Gulpfile.js
[16:28:34] Starting 'check'...
[16:28:35] Finished 'check' after 69 ms
[16:28:35] Starting 'pre-commit'...

/tmp/sp-quality/src/index.js
  line 34  col 33  Missing semicolon.
  line 52  col 19  Missing semicolon.
  line 53  col 46  Missing semicolon.

✖ 3 problems
```

However, you will be able to commit the code if the check passes!

```
mdesales@ubuntu [11/16/201416:26:57] /tmp/sp-quality (master *+) $ git commit
[16:27:02] Using gulpfile /tmp/sp-quality/Gulpfile.js
[16:27:02] Starting 'check'...
[16:27:02] Finished 'check' after 71 ms
[16:27:02] Starting 'pre-commit'...
```

If you are certain to by-pass the errors, you can use git's switch --no-verify.
That way, the hook will NOT even be triggered!

# Git Guppy Core

For full detail about the core of the project, please go to https://github.com/therealklanni/git-guppy.

## Authors

**Kevin Lanni**
 
+ [github/therealklanni](https://github.com/therealklanni)
+ [twitter/therealklanni](http://twitter.com/therealklanni) 

** Modular Hooks Architecture **

+ [github/marcellodesales](http://github.com/marcellodesales)
+ [twitter/marcellodesales](http://twitter.com/marcellodesales)

## License
Copyright (c) 2014 Marcello de Sales, contributors.
Released under the MIT license
***
