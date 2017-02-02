# forms.control

# Development notes

- [Trello development board](https://trello.com/b/TbbnXZIc/mise-en-place-development)
- [Github organisation](https://github.com/mise-en-place)

--

### Packaging
#### Naming Modules
Modules should be named with the `mep-` prefix, followed by their full repo name, for example `mep-utilities.clearfix`
#### Naming Stylesheets
Stylesheets should be named with the (singular) `type-` prefix, followed by their individual name, for example `_tool-base-spacing.scss`

#### Conditions
- Eyeglass aware modules must have the `eyeglass-module` keyword attached to them
- The `main` path **must** match the top level module name, or the specificied eyeglass name (see code block below)

An example `package.json` should look something like this:

```
{
  "name": "mep-tools.base-spacing",
  "version": "1.0.0",
  "description": "Base spacing tool",
  "main": "stylesheets/_tool-base-spacing.scss",
  "eyeglass": {
    "needs": "^1.0.0",
    "name": "tool-base-spacing",
    "exports": "eyeglass-exports.js"
  },
  "keywords": [
    "eyeglass-module",
    "sass",
    "mise-en-place"
  ],
  "repository": {
    "type": "git",
    "url": "https://github.com/mise-en-place/tools.base-spacing.git"
  },
  "author": "Kind",
  "license": "MIT"
}

```

--

### Eyeglassifying
#### Structuring Modules
File structure for eyeglass modules should be as follows

```
tools.base-spacing
|-stylesheets
|--_tool.base-spacing.scss
|-eyeglass-exports.js
|-package.json
```


#### Making Exportable

To be exportable as an eyeglass mode, an `eyeglass-exports.js` file will be needed. It should consist of the following:
```
var path = require('path');

module.exports = function(eyeglass, sass) {
  return {
    sassDir: path.join(__dirname, 'stylesheets')
  }
}
```

#### Eyeglass Inception
Most of our eyeglass modules require their own eyeglass based dependencies, for example, most utilities depend on their tool counterparts. These need to be defined in the `package.json` as dependencies. As a basic example, the `rem-calc` tool depends on the `type-config` tool being available, therefore it's required as a dependency as below:

```
{
  "name": "mep-tools.rem-calc",
  "version": "1.0.0",
  "description": "Rem Calc Tool",
  "main": "stylesheets/_tool-rem-calc.scss",
  "eyeglass": {
    "needs": "^1.0.0",
    "name": "tool-rem-calc",
    "exports": "eyeglass-exports.js"
  },
  "keywords": [
    "eyeglass-module",
    "sass",
    "mise-en-place"
  ],
  "repository": {
    "type": "git",
    "url": "https://github.com/mise-en-place/tools.rem-calc.git"
  },
  "author": "Kind",
  "license": "MIT",
  "dependencies": {
    "mep-tools.type-config": "github:mise-en-place/tools.type-config"
  }
}

```


--
### Installation
Mise-En-Place requires the following to run:

- [Node](#)
- [NPM](#)
