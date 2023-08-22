# AutoGreen

刷足迹噻

Settings -> Action -> General -> Workflow permissions and choose read and write permissions

```
name: ci

on:
  push:
    branches:
      - master
  schedule:
    - cron: "* */78 * * *"

jobs:
  autogreen:
    runs-on: ubuntu-latest
    steps:
      - name: Clone repository
        uses: actions/checkout@v2

      - name: Auto green
        run: |
          git config --local user.email "xmanv@gmail.com"
          git config --local user.name "xmanv"
          git remote set-url origin https://${{ github.actor }}:${{ secrets.GITHUB_TOKEN }}@github.com/${{ github.repository }}
          git pull --rebase
          git commit --allow-empty -m "A commit a day keeps your girlfriend away"
          git push
```
