# snk

[![GitHub Workflow Status](https://img.shields.io/github/actions/workflow/status/platane/platane/main.yml?label=action&style=flat-square)](https://github.com/Platane/Platane/actions/workflows/main.yml)
[![GitHub release](https://img.shields.io/github/release/platane/snk.svg?style=flat-square)](https://github.com/platane/snk/releases/latest)
[![GitHub marketplace](https://img.shields.io/badge/marketplace-snake-blue?logo=github&style=flat-square)](https://github.com/marketplace/actions/generate-snake-game-from-github-contribution-grid)
![type definitions](https://img.shields.io/npm/types/typescript?style=flat-square)
![code style](https://img.shields.io/badge/code_style-prettier-ff69b4.svg?style=flat-square)

GitHubユーザーのコントリビューション（草）グラフから、ヘビゲームを生成します。

<picture>
  <source
    media="(prefers-color-scheme: dark)"
    srcset="https://raw.githubusercontent.com/platane/snk/output/github-contribution-grid-snake-dark.svg"
  />
  <source
    media="(prefers-color-scheme: light)"
    srcset="https://raw.githubusercontent.com/platane/snk/output/github-contribution-grid-snake.svg"
  />
  <img
    alt="github contribution grid snake animation"
    src="https://raw.githubusercontent.com/platane/snk/output/github-contribution-grid-snake.svg"
  />
</picture>

GitHubユーザーのコントリビューションデータを取得し、それをヘビゲームにします。ヘビが順番にマス目を食べていくアニメーションパスを生成します。

[gif](https://github.com/Platane/snk/raw/output/github-contribution-grid-snake.gif) または [svg](https://github.com/Platane/snk/raw/output/github-contribution-grid-snake.svg) image. Colors 画像を生成できます。色は[カスタマイズ](https://raw.githubusercontent.com/platane/snk/output/github-contribution-grid-snake-grey.svg) [可能](https://raw.githubusercontent.com/platane/snk/output/github-contribution-grid-snake-ocean.svg) です。

GitHub Actionsとして利用可能です。毎日新しい画像を自動生成できるため、 [github profile readme](https://docs.github.com/en/free-pro-team@latest/github/setting-up-and-managing-your-github-profile/managing-your-profile-readme)

## Usage

### **github action**

```yaml
- uses: Platane/snk@v3
  with:
    # コントリビューションを取得するGitHubユーザー名（**必須**）
    # `github.repository_owner` 変数、または特定のユーザー名を指定します
    github_user_name: ${{ github.repository_owner }}

    # 生成するファイルのリスト。
    # 1行に1ファイル記述。各出力はクエリ文字列でオプションをカスタマイズできます。
    #
    # サポートされているオプション:
    #  - palette:          色のプリセット。 [github, github-dark, github-light] のいずれか
    #  - color_snake:      ヘビの色
    #  - color_dots:       カンマ区切りのドット（草）の色リスト。
    #                      1番目が0貢献、以降、貢献度に合わせて低い順から高い順へ指定。
    #                      正確に5色の指定が必要です。
    #  - color_background: 背景色（gifのみ有効）
    outputs: |
      dist/github-snake.svg
      dist/github-snake-dark.svg?palette=github-dark
      dist/ocean.gif?color_snake=orange&color_dots=#bfd6f6,#8dbdff,#64a1f4,#4b91f1,#3c7dd9&color_background=#aaaaaa
```

[example with cron job](https://github.com/Platane/Platane/blob/master/.github/workflows/main.yml#L26-L33)

### **svg**

GIFを必要とせずSVGのみを生成したい場合は、より高速なAction `uses: Platane/snk/svg-only@v3`の使用を検討してください。

### **dark mode**

![dark mode](https://github.com/user-attachments/assets/6b900b64-0cdc-43f0-a234-e11dba8e786e)

GitHubでのダークモード対応には、README内で以下の [special syntax](https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax#specifying-the-theme-an-image-is-shown-to) を使用してください。

```html
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="github-snake-dark.svg" />
  <source media="(prefers-color-scheme: light)" srcset="github-snake.svg" />
  <img alt="github-snake" src="github-snake.svg" />
</picture>
```

### **interactive demo**

<a href="https://platane.github.io/snk">
  <img height="300px" src="https://user-images.githubusercontent.com/1659820/121798244-7c86d700-cc25-11eb-8c1c-b8e65556ac0d.gif" ></img>
</a>

[platane.github.io/snk](https://platane.github.io/snk)

### **local**

```sh
npm install

npm run dev:demo
```

## Implementation

[solver algorithm](./packages/solver/README.md)


