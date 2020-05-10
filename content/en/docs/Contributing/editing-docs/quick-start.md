---
title: "Quick start"
linkTitle: "Quick start"
weight: 10
description: >
  A quick guide to updating the docs when you already know GitHub
---

Here's a quick guide to updating the docs. It assumes you're familiar with the
GitHub workflow and you're happy to use the automated preview of your doc
updates:

1. Fork the [PiWeatherRock Docs repo](https://github.com/genebean/piweatherrock-docs) on GitHub.
2. Create a new branch for your work
3. Make your changes and send a pull request (PR).
4. If you're not yet ready for a review, add "WIP" to the PR name to indicate
   it's a work in progress. (**Don't** add the Hugo property
   "draft = true" to the page front matter, because that prevents the
   auto-deployment of the content preview described in the next point.)
5. Wait for the automated PR workflow to do some checks. When it's ready,
   you should see a comment like this: **deploy/netlify — Deploy preview ready!**
6. Click **Details** to the right of "Deploy preview ready" to see a preview
   of your updates.
7. Continue updating your doc and pushing your changes until you're happy with
   the content.
8. When you're ready for a review, add a comment to the PR, and remove any
   "WIP" markers.
