# Angular Linting + Prettier

A basic guided demo to show how to introduce [ESLint](https://eslint.org/), [StyleLint](https://stylelint.io/) and [Prettier](https://prettier.io/) in your Angular project.

--- 
### Table of contents
- [ESLint]()
  - [🚀 Installing]()
  - [⚙️ Configuring]()
  - [👨‍💻 Usage]()
- [stylelint]()
  - [🚀 Installing]()
  - [⚙️ Configuring]()
  - [👨‍💻 Usage]()
- [Prettier]()
  - [🚀 Installing]()
  - [⚙️ Configuring]()
  - [👨‍💻 Usage]()
- [💫 Feedback]()
- [📑 License]()

---
### Todo list:
- [x] [ESLint]()
- [x] [stylelint]()
- [x] [Prettier]()
- [x] Icons
- [ ] Husky
- [ ] GIFs
- [ ] Anchors links

---

## ![ESLint icon](https://raw.githubusercontent.com/alexander-panchuk-oril/angular-lint-prettier-husky/main/src/assets/eslint_32x32.png) ESLint

> By default for linting Angular project use [TSLint](https://palantir.github.io/tslint/), but it has been deprecated as of 2019. So to keep your project linting we have to use the [ESLint](https://eslint.org/).

ESLint is a tool that analyses your code for identifying and reporting on patterns found in code as a result of making code more consistent and avoiding bugs.

[GIF Image]

### 🚀 Installing

1. Use [AngularCLI](https://angular.io/cli) to add ESLint schematics:

```bash
ng add @angular-eslint/schematics
```

2. It's time to remove TSLint and replace it with the ESLint (also by using Use [AngularCLI](https://angular.io/cli)):

```bash
ng g @angular-eslint/schematics:convert-tslint-to-eslint --remove-tslint-if-no-more-tslint-targets --ignore-existing-tslint-config
```

3. Find a `"scripts"` object in a `panckage.json` and add two more scripts on it:

```json
    "lint": "ng lint",
    "lint--fix": "tsc --noEmit && eslint . --ext ts --fix"
```

🛎️ From this time we already can use linting in a project, but I hardly recommend adding a bit of setting in that file.

### ⚙️ Configuring

After successful installing, we will have an ESLint config file in the root folder `.eslintrc.json`.

1. Find a `"extends"` object in a `.eslintrc.json` and replace it with:

```json
"extends": [
        "plugin:@angular-eslint/ng-cli-compat",
        "plugin:@angular-eslint/ng-cli-compat--formatting-add-on",
        "plugin:@angular-eslint/template/process-inline-templates"
      ],
```

2.  Find a `"rules"` object in a `.eslintrc.json` and replace it with:

```json
"rules": {
        "@typescript-eslint/naming-convention": [
          "error",
          {
            "selector": "enumMember",
            "format": ["UPPER_CASE"]
          },
          {
            "selector": "interface",
            "prefix": ["I"],
            "format": ["StrictPascalCase"]
          }
        ],
        "@angular-eslint/directive-selector": "error",
        "jsdoc/no-types": "off",
        "no-underscore-dangle": "off",
        "max-len": ["error", 145, 4],
        "newline-before-return": 2,
        "lines-between-class-members": 2,
        "no-shadow": "off",
        "@typescript-eslint/no-shadow": ["error"]
      }
```

3. Use [npm](https://www.npmjs.com/) to install dependencies by running:

```bash
npm install -D eslint-plugin-jsdoc eslint-plugin-import eslint-plugin-prefer-arrow
```

### 👨‍💻 Usage

There are two ways how we can use [ESLint](https://eslint.org/):

1. Via IDE:

- For VS Code you can use [ESLint plugin](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint), or you can find this plugin by extension id: `dbaeumer.vscode-eslint`

2. Via [npm](https://www.npmjs.com/):

- Run `npm run lint` to analyze code
- Run `npm run lint--fix` to autofix code

## ![stylelint icon](https://raw.githubusercontent.com/alexander-panchuk-oril/angular-lint-prettier-husky/main/src/assets/stylelint_32x32.png) stylelint

> A mighty, modern linter that helps you avoid errors and enforce conventions in your styles.

Same purpose as an ESLint, but instead of working with JS, TS and JSON [stylelint](https://stylelint.io/) works with CSS/SCSS/SASS.

[GIF Image]

### 🚀 Installing

Use [npm](https://www.npmjs.com/) to install [stylelint](https://stylelint.io/) and configs for [SASS](https://sass-lang.com/) and [BEM](http://getbem.com/):

```bash
npm install --save-dev stylelint stylelint-config-sass-guidelines stylelint-selector-bem-pattern
```

### ⚙️ Configuring

1. In your project root folder create a `.stylelintrc` file and paste content in it:

```json
{
  "extends": "stylelint-config-sass-guidelines",
  "plugins": [
    "stylelint-selector-bem-pattern"
  ],
  "rules": {
    "indentation": 2,
    "number-leading-zero": null,
    "max-nesting-depth": 5,
    "plugin/selector-bem-pattern": {
      "componentName": "[A-Z]+",
      "componentSelectors": {
        "initial": "^\\.{componentName}(?:-[a-z]+)?$",
        "combined": "^\\.combined-{componentName}-[a-z]+$"
      },
      "utilitySelectors": "^\\.util-[a-z]+$"
    },
    "selector-class-pattern": [
      "^(?:(?:o|c|u|t|s|is|has|_|js|qa)-)?[a-zA-Z0-9]+(?:-[a-zA-Z0-9]+)*(?:__[a-zA-Z0-9]+(?:-[a-zA-Z0-9]+)*)?(?:--[a-zA-Z0-9]+(?:-[a-zA-Z0-9]+)*)?(?:\\[.+\\])?$",
      {
        "message": "Class names should match the SUIT CSS naming convention"
      }
    ],
    "selector-no-qualifying-type": [ 
      true, 
      {
          "ignore": [ "attribute", "class", "id" ]
      }
    ]
  }
}
```

2. Find a `"scripts"` object in a `panckage.json` and add two more scripts on it:

```json
    "lint:style": "stylelint 'src/**/*.scss' -f verbose",
    "lint:style--fix": "stylelint 'src/**/*.scss' --fix"
```

### 👨‍💻 Usage

There are two ways how we can use [stylelint](https://stylelint.io/):

1. Via IDE:

- For VS Code you can use [stylelint plugin](https://marketplace.visualstudio.com/items?itemName=stylelint.vscode-stylelint), or you can find this plugin by extension id: `stylelint.vscode-stylelint`

2. Via [npm](https://www.npmjs.com/):

- Run `npm run lint:style` to analyze code
- Run `npm run lint:style--fix` to autofix code

## ![Prettier icon](https://raw.githubusercontent.com/alexander-panchuk-oril/angular-lint-prettier-husky/main/src/assets/prettier_32x32.png)  Prettier

[Prettier](https://prettier.io/) is a code formatter that enforces a consistent code style across your entire codebase.

[GIF Image]

### 🚀 Installing

Use [npm](https://www.npmjs.com/) to install [Prettier](https://prettier.io/):

```bash
npm i prettier eslint-config-prettier prettier-eslint --save-dev
```

### ⚙️ Configuring

1. In your project root folder create a `.prettierrc` file and paste content in it:

```json
{
  "singleQuote": true,
  "trailingComma": "none",
  "endOfLine": "auto",
  "printWidth": 145
}
```

2. In your project root folder create a `.prettierignore` file and paste content in it:

```
# Ignore artifacts:
build
coverage
e2e
node_modules
dist
```

3. Modify your `.eslintrc.json` by adding `"prettier"` string to `"extends"` object:

```json
 "extends": [
        ...
        ...
        ...
        "prettier"
      ],
```

4. Find a `"scripts"` object in a `panckage.json` and add a script on it:

```json
    "format": "prettier 'src/**/*.{ts,js,json}' --write"
```

### 👨‍💻 Usage

There are two ways how we can use [Prettier](https://prettier.io/):

1. Via IDE:

- For VS Code you can use [Prettier - Code formatter](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode), or you can find this plugin by extension id: `esbenp.prettier-vscode`

2. Via [npm](https://www.npmjs.com/):

- Run `npm run format ` to autoformat code

## 💫 Feedback

Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

Please make sure to update tests as appropriate.

## 📑 License

[MIT](https://choosealicense.com/licenses/mit/)
