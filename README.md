# babel-plugin-custom-import-path-transform

A [babel](http://babeljs.io) plugin to rewrite module imports (and `require`) using a custom function.

## Description

You can supply a replace function to dynamically replace module paths when Babel traverses them.

## Usage

Install the plugin:

```bash
$ yarn add -D babel-plugin-custom-import-path-transform
```

Specify the plugin in your `.babelrc` with the file that exports the replace function.

```json
{
    "plugins": [
        [
            "babel-plugin-custom-import-path-transform",
            {
                "transformImportPath": "./scripts/transformImportPath.js"
            }
        ]
    ]
}
```

Let's say you want `~/moduleFile` to be replaced to `utils/moduleFile` if the calling file is in `utils`, and `common/moduleFile` otherwise.
So in your `replace-module-paths.js`, just export:

```js
function transformImportPath(originalPath, callingFileName, options) {
    if (callingFileName.indexOf('/utils/') !== -1) {
        return originalPath.replace('~', 'utils');
    } else {
        return originalPath.replace('~', 'common');
    }
}

module.exports = transformImportPath;
```

## License

MIT
