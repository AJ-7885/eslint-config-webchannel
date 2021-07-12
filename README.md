# WebChannel Eslint and Prettier Setup

These are WebChannel.DEV settings for ESLint and Prettier

You might like them - or you might not. Don't worry you can always change them.


![Node.js Package](https://github.com/AJ-7885/eslint-config-webchannel/workflows/Node.js%20Package/badge.svg)

[![Open in Visual Studio Code](https://open.vscode.dev/badges/open-in-vscode.svg)](https://open.vscode.dev/AJ-7885/eslint-config-webchannel)



<img src="https://www.commitstrip.com/wp-content/uploads/2020/06/Strip-Visual-Studio-Code-650-finalenglish.jpg"
alt="Showreel" width="100%" border="10" />

## What it does

* Lints JavaScript based on the latest standards
* Fixes issues and formatting errors with Prettier
* Lints + Fixes inside of html script tags
* Lints + Fixes React via eslint-config-airbnb

## Installing

You can use eslint globally and/or locally per project.

It's usually best to install this locally once per project, that way you can have project specific settings as well as
sync those settings with others working on your project via git.

I also install globally so that any project or rogue JS file I write will have linting and formatting applied without
having to go through the setup.

## Local / Per Project Install

1. If you don't already have a `package.json` file, create one with `yarn init`.

2. Then we need to install everything needed by the config:

```
npx install-peerdeps --dev eslint-config-webchannel
```

or

```
yarn create install-peerdeps --dev eslint-config-webchannel
```

3. You can see in your package.json there are now a big list of devDependencies.

4. Create a `.eslintrc` file in the root of your project's directory (it should live where package.json does).
   Your `.eslintrc` file should look like this:

```json
{
    "extends": [
        "webchannel"
    ]
}
```

Tip: You can alternatively put this object in your `package.json` under the property `"eslintConfig":`. This makes one
less file in your project.

5. You can add two scripts to your package.json to lint and/or fix:

```json
"scripts": {
"lint": "eslint .",
"lint:fix": "eslint . --fix"
},
```

6. Now you can manually lint your code by running `yarn lint` and fix all fixable issues with `yarn lint:fix`. You
   probably want your editor to do this though.

## Global Install

> Note: Global Install may not be working as it's been removed in ESLint 7.x. Investigating now...

1. First install everything needed:

```
npx install-peerdeps --global eslint-config-webchannel
```

or

```
yarn create install-peerdeps --global eslint-config-webchannel
```

(**note:** npx is not a spelling mistake of **npm**. `npx` comes with when `node` and `npm` are installed and makes
script running easier)

2. Then you need to make a global `.eslintrc` file:

ESLint will look for one in your home directory

* `~/.eslintrc` for mac
* `C:\Users\username\.eslintrc` for windows

In your `.eslintrc` file, it should look like this:

```json
{
    "extends": [
        "webchannel"
    ]
}
```

3. To use from the CLI, you can now run `eslint .` or configure your editor as we show next.

## Settings

If you'd like to overwrite eslint or prettier settings, you can add the rules in your `.eslintrc` file.
The [ESLint rules](https://eslint.org/docs/rules/) go directly under `"rules"`
while [prettier options](https://prettier.io/docs/en/options.html) go under `"prettier/prettier"`. Note that prettier
rules overwrite anything in my config (trailing comma, and single quote), so you'll need to include those as well.

```js
{
  "extends": [
    "webchannel"
  ],
  "rules": {
    "no-console": 2,
    "prettier/prettier": [
      "error",
      {
        "trailingComma": "es5",
        "singleQuote": true,
        "printWidth": 120,
        "tabWidth": 8,
      }
    ]
  }
}
```

## With VS Code

You should read this entire thing. Serious!

Once you have done one, or both, of the above installs. You probably want your editor to lint and fix for you. Here are
the instructions for VS Code:

1. Install the [ESLint package](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)
2. Now we need to setup some VS Code settings via `Code/File` → `Preferences` → `Settings`. It's easier to enter these
   settings while editing the `settings.json` file, so click the Open (Open Settings) icon in the top right corner:

  ```js
  // These are all my auto-save configs
  "editor.formatOnSave": true,
  // turn it off for JS and JSX, we will do this via eslint
  "[javascript]": {
    "editor.formatOnSave": false
  },
  "[javascriptreact]": {
    "editor.formatOnSave": false
  },
  // show eslint icon at bottom toolbar
  "eslint.alwaysShowStatus": true,
  // tell the ESLint plugin to run on save
  "editor.codeActionsOnSave": {
    "source.fixAll": true
  },
  // Optional BUT IMPORTANT: If you have the prettier extension enabled for other languages like CSS and HTML, turn it off for JS since we are doing it through Eslint already
  "prettier.disableLanguages": ["javascript", "javascriptreact"],
  ```

After attempting to lint your file for the first time, you may need to click on 'ESLint' in the bottom right and
select 'Allow Everywhere' in the alert window.

Finally you'll usually need to restart VS code. They say you don't need to, but it's never worked for me until I
restart.

## With Create React App

1. Run `npx install-peerdeps --dev eslint-config-webchannel`
1. Crack open your `package.json` and replace `"extends": "react-app"` with `"extends": "webchannel"`

## With Gatsby

1. Run `npx install-peerdeps --dev eslint-config-webchannel`
1. If you have an existing `.prettierrc` file, delete it.
1. follow the `Local / Per Project Install` steps above

## With WSL

Can someone add this?

## With Intellij Products

Can someone who uses intellij write some good instructions

## With Typescript

Needs some instructions

## With Yarn

It should just work, but if they aren't showing up in your package.json,
try `npx install-peerdeps --dev eslint-config-webchannel -Y`

## 🤬🤬🤬🤬 IT'S NOT WORKING

Start fresh. Sometimes global modules can goof you up. This will remove them all:

```
npm remove --global eslint-config-webchannel husky lint-staged stylelint stylelint-config-recommended  stylelint-config-styled-components  stylelint-processor-styled-components babel-eslint eslint eslint-config-prettier eslint-config-airbnb eslint-plugin-html eslint-plugin-prettier eslint-plugin-import eslint-plugin-jsx-a11y eslint-plugin-react prettier eslint-plugin-react-hooks
```

To do the above for local, omit the `--global` flag.

Then if you are using a local install, remove your `package-lock.json` file and delete the `node_modules/` directory.

Then follow the above instructions again.
