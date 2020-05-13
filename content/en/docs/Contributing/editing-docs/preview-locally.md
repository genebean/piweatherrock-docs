---
title: "Previewing your changes locally"
linkTitle: "Preview locally"
weight: 30
description: >
  How to run your own local Hugo server to preview your changes
---

If you want to run your own local Hugo server to preview your changes as you work:

1. Follow the instructions in Docsy's [Getting started](https://www.docsy.dev/docs/getting-started/) guide to install Hugo and any other tools you need. You'll need at least **Hugo version 0.63.1** (we recommend using the most recent available version), and it must be the **extended** version, which supports SCSS (the version installed by Homebrew on macOS is the right version).
2. Fork the [PiWeatherRock Docs repo](https://github.com/genebean/piweatherrock-docs) repo as talked about above and then create a local copy using [`git clone --recurse-submodules`](https://www.git-scm.com/docs/git-clone#Documentation/git-clone.txt---recurse-submodulesltpathspec). Be sure to use `--recurse-submodules` or you won’t pull down some of the code you need to generate a working site.

    ```bash
    git clone --recurse-submodules --depth 1 \
    https://github.com/<your username>/piweatherrock-docs.git
    ```

3. Run `hugo server` from inside the piweatherrock-docs folder. By default your site will be available at http://localhost:1313/. Now that you're serving your site locally, Hugo will watch for changes to the content and automatically refresh your site.
4. Continue with the usual GitHub workflow described above to edit files, commit them, push the changes up to your fork, and create a pull request.
