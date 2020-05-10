---
title: "Sharing your modifications to PiWeatherRock"
linkTitle: "Sharing modifications"
weight: 2
description: >
  A quick guide on sharing your modified version of PiWeatherRock
---

Got an idea for how to make PiWeatherRock better? AWESOME! Just like with these docs, suggested code should be submitted
via a GitHub pull requests. Below is a quick guide on how to share your modifications.

## weather.py

If you did your modifications when almost everything was in `weather.py` then I suggest going to [https://gist.github.com](https://gist.github.com/) and pasting your version into the larger box, entering `weather.py` in the short box just above the large area, and then entering a description of what's special about your version in the top box that says "Gist description." After that click "Create public gist" and then go to [https://github.com/genebean/PiWeatherRock/issues](https://github.com/genebean/PiWeatherRock/issues), click "New issue" and then click "Get started" next to "Feature request." Answer the questions that are in the next page and include the link of the gist you made.

## Editing files on GitHug

If you have made some changes but are not comfortable using git then this is the section for you. It assumes that you want to share changes you have made to `piweatherrock/weather.py`. If you actually want to share changes to some other file the same general process should work so long as you adjust steps 2 and 4 accordingly.

> Caution: please do not post your API key for Dark Sky or any other sensitive information.

1. Go to the [PiWeatherRock GitHub page](https://github.com/genebean/PiWeatherRock)
2. Click on the `piweatherrock` folder and then `weather.py` to view its code
   1. Much of what comes next is adapted from GitHub's [Editing files in another user's repository](https://help.github.com/en/github/managing-files-in-a-repository/editing-files-in-another-users-repository) docs.
3. Just above the code there is a pencil icon on the right side that says "Edit this file" when you mouse over it. Click the pencil.
4. Back on your computer or Pi, open your modified version of `weather.py` in a text editor and copy everything in it.
5. Return to the edit page from step 3 and paste your code. This should replace everything with what you copied from your modified version.
6. Scroll to the bottom. In the small box below the editor, enter a short meaningful description of what your change is.
7. In the large box add any additional information that will provide more context about what your changes are.
8. Just below the big box is a place where you can choose which email address will be shown as the author of your changes.
9. Next, click the green button that says "Propose file change"
10. In the small field at the top enter a description of your change (this may be the same as in step 6)
11. In the large field enter any additional information or context that will help me and others understand what you are proposing.
12. If you are proposing visual changes then please also paste in a screenshot or photo that shows your modifications in action.
13. Finally, click the green "Create Pull Request" button to submit your suggestion.

🎉 Congratulations! You are now well on your way to being a contributor to this project. Keep an eye out for emails from GitHub as myself or others will likely provide feedback on your suggestions. Also feel free to reach out on [Gitter](https://gitter.im/PiWeatherRock/community) to chat about this process.
