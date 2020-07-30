# 各lintの設定
## stylelintの設定

1. 下記パッケージをインストールする
- prettier
- stylelint
- stylelint-config-prettier
- stylelint-config-recess-order
- stylelint-config-recommended-scss
- stylelint-order
- stylelint-prettier
- stylelint-scss

```
npm i -D prettier stylelint stylelint-config-prettier stylelint-config-recess-order stylelint-config-recommended-scss stylelint-order stylelint-prettier stylelint-scss
```

2. ```.stylelintrc.json```ファイルをルートに作成し下記コードを記述する。
```
{
  "extends": [
    "stylelint-config-recommended-scss",
    "stylelint-config-recess-order",
    "stylelint-prettier/recommended"
  ]
}
```

## ESLintの設定
[Standard JS](https://standardjs.com/)のルールに則ったESLintの設定

1. 下記パッケージをインストールする
- prettier
- eslint
- eslint-config-prettier
- eslint-config-standard
- eslint-plugin-import
- eslint-plugin-node
- eslint-plugin-prettier
- eslint-plugin-promise
- eslint-plugin-standard

```
npm i -D prettier eslint eslint-config-prettier eslint-config-standard eslint-plugin-import eslint-plugin-node eslint-plugin-prettier eslint-plugin-promise eslint-plugin-standard
```

2. ```.eslintrc.json```ファイルをルートに作成し下記コードを記述する。
```
{
    "extends": [
        "standard",
        "plugin:prettier/recommended"
    ],
    "plugins": [
        "prettier"
    ],
    "env": {
        "browser": true,
        "es6": true,
        "jquery": true
    },
    "rules": {
        "prettier/prettier": [
        "error",
            {
                "semi": false,
                "allowEmptyReject": true,
                "prefer-promise-reject-errors": ["error", {"allowEmptyReject": true}]
            }
        ]
    },
    "globals": {

    }
}
```

## htmlhintの設定

1. 下記パッケージをインストールする
- prettier
- htmlhint

```
npm i -D prettier htmlhint
```

2. ```.prettierrc.json```ファイルを作成し下記コードを記述する。
```
{
    "semi": false,
    "overrides": [
        {
            "files": ["*.html"],
            "options": {
                "useTabs": true,
                "htmlWhitespaceSensitivity": "ignore",
                "multiline": "never",
                "printWidth": 300
            }
        }
    ]
}
```

## huskyの設定

1. 下記パッケージをインストールする
- lint-staged
- husky

```
npm i -D lint-staged husky
```

2. ```.package.json```ファイルのdevDependenciesの項目の下に下記コードを記述する。
```
  "devDependencies": {
    "xxx": "xxx",
  },
  // この下からコピー
  "husky": {
    "hooks": {
      "pre-commit": "lint-staged"
    }
  },
  "lint-staged": {
    "./*.js": [
      "eslint --fix",
      "git add"
    ],
    "./*.scss": [
      "stylelint --fix",
      "git add"
    ],
    "./*.html": [
      "htmlhint",
      "prettier --write",
      "git add"
    ]
  }
```

各lintの対象ファイルを下記で指定しているので適宜変更してください。  

全てのJSファイルが対象
``` 
"./*.js": [
    "eslint --fix",
    "git add"
],
```

全てのdev配下のJSファイルが対象
``` 
"./dev/**/*.js": [
    "eslint --fix",
    "git add"
],
```

## Visual Studio Codeでlintエラーを確認する
1. 各lintの拡張機能をインストールする
- [eslint](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)
- [stylelint](https://marketplace.visualstudio.com/items?itemName=stylelint.vscode-stylelint)

2. ```shift + ctrl + @```でパネルを表示「問題」タブでlintエラーを確認する。

## Visual Studio Codeでlintエラーを解決する(上記拡張機能を追加した場合)
1. ```Command + shift + p``でコマンドパレットを表示
2. ```fix```と入力すると下記項目が出てくるので適宜選択する
- stylelint: Fix all auto-fixable Problems
- ESLint: Fix all auto-fixable Problems

## 注意点
コミット時はGulp等のタスクランナーのwatchは切っておいてください