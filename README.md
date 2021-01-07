# basic-linters
Добавление основных линтеров в проект.

### Необходимые пакеты npm
1. stylelint-scss
2. stylelint-prettier
3. stylelint-order
4. stylelint-config-rational-order
5. stylelint-config-prettier@7.0.0
6. stylelint-config-airbnb
7. stylelint
8. prettier
9. lint-staged
10. husky
11. eslint
12. eslint-config-prettier
13. eslint-plugin-prettier
### Установка пакетов
npm i stylelint-scss stylelint-prettier stylelint-order stylelint-config-rational-order stylelint-config-prettier@7.0.0 stylelint-config-airbnb stylelint prettier lint-staged husky eslint eslint-config-prettier eslint-plugin-prettier --save-dev

### Блок scripts в package.json
Добавляем в блок scripts команды для запуска линтеров для проверки проекта на ошибки.    
```html 
"scripts": {  
  "lint:js": "eslint src/**/*.js",  
  "lint:style": "stylelint src/**/*.scss",
  "lint:style-fix": "stylelint src/**/*.scss --fix",
  "lint": "npm run lint:js && npm run lint:style-fix"  
}
```
### Запуск линтеров перед созданием коммита
В package.json добавляем настройки для husky и lint-staged.    
#### Важный момент!
Если линтер встраивается в текущий проект,    
то в хуках husky необходимо прописать "pre-commit": "npm run lint". После исправления ошибок линтера (если таковые будут), создания коммита, необходимо переписать хук на "lint-staged", т.е. "pre-commit": "lint-staged".
***
```html
"husky": {  
    "hooks": {  
      "pre-commit": "lint-staged"  
    }  
  },  
  "lint-staged": {  
    "*.js": "eslint",
    "*.scss": "stylelint --syntax=scss"
  }
```
### Файл stylelint.config.js
В корне проекта создаем файл stylelint.config.js.  
В нем прописываем следующие настройки:
```html
module.exports = {  
    extends: ["stylelint-config-airbnb",
    "stylelint-config-rational-order",
    "stylelint-prettier/recommended"],
    plugins: [
      "stylelint-order", "stylelint-scss"
    ],
    rules: {
      "prettier/prettier": true
    }
  }
```
### Файл .prettierrc
В корне проекта создаем файл .prettierrc
В него добавляем настройки:
```html
{  
  "useTabs": false,  
  "printWidth": 120,  
  "semi": true,  
  "singleQuote": true,  
  "arrowParens": "avoid"  
}
```
### Файл .prettierignore
В корне проекта создаем файл .prettierrc
В него добавляем строки:  
.DS_Store  
node_modules  
package-lock.json  
dist  
npm-debug.log*  
### Файл .eslint
В корне проекта создаем файл .eslintrc
В него добавляем настройки:   
```html
{  
    "parserOptions": {  
      "sourceType": "module",  
      "allowImportExportEverywhere": true  
    },  
      "env": {  
          "es6": true  
      }  
  }
```
### Файл .eslint.js
В корне проекта создаем файл .eslint.js
В него добавляем настройки:    
```html
module.exports = {  
    parser: "babel-eslint",  
    parserOptions: {  
      "sourceType": "module",  
      "allowImportExportEverywhere": true  
    },  
    root: true,  
    env: {  
      browser: true,  
      node: true,  
      "es6": true  
    },  
    extends: [
      'prettier',
      'plugin:prettier/recommended',
    ],
    plugins: ['prettier'],
    // add your custom rules here
    rules: {  
    "unicode-bom": "never"  
    },  
  }
```
### Настройки редактора vs code
В корне проекта создаем файл .editorconfig  
В нем создаем следующие настройки:  
```html
root = true  
[*]  
indent_style = space  
indent_size = 2  
end_of_line = lf  
charset = utf-8  
trim_trailing_whitespace = true  
insert_final_newline = true  

[*.md]  
trim_trailing_whitespace = false  
```
### Настройки валидации в vs code  
В корне проекта создаем папку .vscode  
В ней создаем файл settings.json  
В нем добавляем настройки:  
```html
{  
    "scss.validate": false,  
    "css.validate": false,  
    "less.validate": false,  
     "editor.codeActionsOnSave": {  
       "source.fixAll.stylelint": true  
     },  
   } 
```
