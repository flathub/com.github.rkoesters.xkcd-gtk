---

name: CI

"on": [push, pull_request]

jobs:
  flatpak-builder:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v2

      - name: Set up flatpak-builder
        run: |
          sudo apt-get update -q
          sudo apt-get install -y -q flatpak flatpak-builder

      - name: Set up Go cache
        uses: actions/cache@v2
        with:
          path: .flatpak-builder
          key: >
            flatpak-builder-${{
            hashFiles('com.github.rkoesters.xkcd-gtk.yaml')
            }}

      - run: >
          flatpak --user remote-add --if-not-exists
          flathub https://flathub.org/repo/flathub.flatpakrepo
      - run: >
          flatpak-builder --user --install-deps-from=flathub
          build com.github.rkoesters.xkcd-gtk.yaml

  yamllint:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v2

      - name: Set up yamllint
        run: |
          sudo apt-get update -q
          sudo apt-get install -y -q yamllint

      - run: yamllint com.github.rkoesters.xkcd-gtk.yaml .github/workflows/*.yml
