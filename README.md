name: Generate latte snake

on:
  schedule:
    - cron: "0 */12 * * *"
  workflow_dispatch:
  push:
    branches: [main]

permissions:
  contents: write

jobs:
  generate:
    runs-on: ubuntu-latest
    steps:
      - uses: Platane/snk@v3
        with:
          github_user_name: ${{ github.repository_owner }}
          outputs: |
            dist/github-contribution-grid-snake.svg?color_snake=#6F4E37&color_dots=#F5EDE0,#E8D5B7,#D4B896,#C8A27A,#8B6B4E
            dist/github-contribution-grid-snake-dark.svg?color_snake=#D4B896&color_dots=#2A1F1A,#5A4234,#8B6B4E,#C8A27A,#F5EDE0

      - uses: crazy-max/ghaction-github-pages@v4
        with:
          target_branch: output
          build_dir: dist
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
