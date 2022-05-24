# Hosting Parsons on Github Template
This repo is a template to help you quickly and easily host Parson's problems on GitHub.

I recommend using [this Parson's problem generator](https://viraj-cse.github.io/parsons-puzzle-ui/dist/), which is a slightly modified version of [Codio's generator](https://codio.github.io/parsons-puzzle-ui/dist/). The key change is the **addition of a feedback box**. After creating the Parson's problems, paste them into this template. [Visit the Codio repo's main page for help on using the generator.](https://codio.github.io/parsons-puzzle-ui/)

## How to host your own Parson's Problems

1. Create a Github account (if you don't have one already). A free account works great for this!

1. Fork this repo using the "Fork" button 

1. In **your fork** click on "Settings" and then "Pages"

1. Set the GitHub Pages Source to Master branch and `/(root)` using the drop down, then click "Save"
    
## How to Add Generated Parson's Problems

1. Use [this Parson's problem generator](https://viraj-cse.github.io/parsons-puzzle-ui/dist/) to create a Parsons problem

1. Click "Export" in the top left

1. Enter a prefix (e.g., `p01`) and click "Update Prefix"

1. (If necessary) Click "Switch to Code"

1. Copy the code into `index.markdown`

*Note*: Do **not** delete the `giveFeedback()` function that has been added to `index.markdown`!
