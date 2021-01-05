# basic-linters
Добавление основных линтеров в проект

### Необходимые пакеты npm
1. stylelint-scss
2. stylelint-prettier
3. stylelint-order
4. stylelint-config-rational-order
5. stylelint-config-prettier
6. stylelint-config-airbnb
7. stylelint
8. prettier
9. lint-staged
10. husky
11. eslint
12. eslint-config-prettier
13. eslint-plugin-prettier
### Установка пакетов
npm i stylelint-scss stylelint-prettier stylelint-order stylelint-config-rational-order stylelint-config-prettier stylelint-config-airbnb stylelint prettier lint-staged husky eslint eslint-config-prettier eslint-plugin-prettier --save-dev

### Блок scripts в package.json
Добавляем к остальным скриптам в блоке скрипта для проверки проекта на ошибки  
"scripts": {  
  "lint:js": "eslint src/**/*.js",  
  "lint:style": "stylelint src/**/*.scss",  
  "lint": "npm run lint:js && npm run lint:style"  
}
### Запуск линтеров перед созданием коммита
В package.json добавляем настройки для husky и lint-staged  
"husky": {  
    "hooks": {  
      "pre-commit": "lint-staged"  
    }  
  },  
  "lint-staged": {  
    "*.js": [
      "lint:js"
    ],  
    "*.scss": "lint:style"  
  }
### Файл stylelint.config.js
В корне проекта создаем файл stylelint.config.js  
В нем прописываем следующие настройки  
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
### Файл .prettierrc
В корне проекта создаем файл .prettierrc
В него добавляем настройки:  
{  
  "useTabs": false,  
  "printWidth": 120,  
  "semi": true,  
  "singleQuote": true,  
  "arrowParens": "avoid"  
}
### Файл .prettierignore
В корне проекта создаем файл .prettierrc
В него добавляем настройки:  
.DS_Store  
node_modules  
package-lock.json  
dist  
npm-debug.log*  
### Файл .eslint
В корне проекта создаем файл .eslint
В него добавляем настройки:    
{  
    "parserOptions": {  
      "sourceType": "module",  
      "allowImportExportEverywhere": true  
    },  
      "env": {  
          "es6": true  
      }  
  }  
### Файл .eslint.js
В корне проекта создаем файл .eslint.js
В него добавляем настройки:    
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
    rules: {},
  }
### Настройки редактора vs code
В корне проекта создаем файл .editorconfig  
В нем создаем следующие настройки:  
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
### Настройки валидации в vs code  
В корне проекта создаем папку .vscode  
В ней создаем файл settings.json  
В нем добавляем настройки:  
{  
    "scss.validate": false,  
    "css.validate": false,  
    "less.validate": false,  
     "editor.codeActionsOnSave": {  
       "source.fixAll.stylelint": true  
     },  
   }  
