# .github-workflows-update-menu.yml
name: Update Menu Data

on:
  repository_dispatch:
    types: [update-menu]

jobs:
  update:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3

      - name: Write new menu data
        run: |
          echo '${{ toJson(github.event.client_payload) }}' > src/data/menu_data.json

      - name: Commit and push
        run: |
          git config user.name "Zynd Bot"
          git config user.email "bot@yourdomain.com"
          git add src/data/menu_data.json
          git commit -m "Auto-update menu prices"
          git push
