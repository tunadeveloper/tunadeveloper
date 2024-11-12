name: Update Profile README

on:
  schedule:
    - cron: '0 0 * * *'  
  workflow_dispatch:

jobs:
  update-readme:
    runs-on: ubuntu-latest

    steps:
      - name: Profil README Repoyu Klonla
        uses: actions/checkout@v2

      - name: Gistten Veri Çek
        env:
          GITHUB_TOKEN: ${{ secrets.MY_SECRET_KEYS }}
        run: |
          curl -H "Authorization: token $GITHUB_TOKEN" \
            https://api.github.com/gists/d77e95668bd2768a09a40c3cff5cc1ba \
            | jq -r '.files["my_hidden_content.txt"].content' >> README.md

      - name: Güncellemeyi Yükle
        run: |
          git config --global user.email "tunabusiness25@gmail.com"
          git config --global user.name "tunadeveloper"
          git add README.md
          git commit -m "Profil README Güncellendi"
          git push
