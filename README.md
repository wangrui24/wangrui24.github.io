## 1. Overview

This is a template for an academic personal website. It was created with grad students and postdocs in mind, however, others may find it a helpful template as well! We're hopeful that it will be relevant to those seeking industry as well as academic positions, however we are more familiar with academic websites. See the rendered template here: <https://ngalanter.github.io/academic-website-template>. 
This goal of this template is to provide several types of pages that might be relevant, but most personal websites don't have all of these pages!

This template uses quarto, you can learn more about quarto websites here: <https://quarto.org/docs/websites>.

This template is published via github pages. Section 2 uses the first suggested workflow on [quarto github pages documentation](https://quarto.org/docs/publishing/github-pages.html). That page also lists other possible github pages workflows. There are many other options for publishing quarto websites, see [this page](https://quarto.org/docs/publishing/) for more information.

Secton 3 goes over some quick ways to customize how your website looks.

This template also allows for auto-updating of page content. You can use the template without enabling auto-updating, just delete/ignore the `auto_update.R` file and delete/ignore all blocks that start with `::: {.content-hidden unless-format="markdown"}`. For more information about auto-updating, see the section 4 of this readme.

## 2. How to use this template with Github pages

1. Create a new repository from this template (see [here](https://docs.github.com/en/repositories/creating-and-managing-repositories/creating-a-repository-from-a-template)) and create a local copy on your computer (for example with github desktop).
    - A good option is to call the repository `your_github_username.github.io`, which gives it the URL `https://your_github_username.github.io`.
    - Otherwise, the URL will be `https://your_github_username.github.io/reponame/`.
2. **(Already set up in template)** Make sure that the rendered pages go to a docs folder, by having `output-dir: docs` in the `quarto.yml` file.
3. **(Already set up in template)** Add a `.nojekyll` file to the root of your repository so that github pages doesn't attempt to use Jekyll to render the site. You can do this via the terminal command: `touch .nojekyll` (Mac/Linx) or `copy NUL .nojekyll` (Windows).
4. Personalize the template in the editor of your choice, such as RStudio
5. Type the command `quarto render` into the terminal to make sure the site is fully rendered.
6. Commit the website to your local repository and then push it to github.
7. Go to the repository on the github website, then go to "Settings" and then click on the "Pages" section. Make sure the source is set to "Deploy from a Branch" and choose the "main" branch and the "/docs" folder.
8. Your site will now be updated and re-deployed anytime you push commits to the main branch. You can go the the "Actions" tab of the repository to see a record of these deployments and whether they ran successfully.

## 3. Quick customizations

- Theme: This template uses the `minty` theme with slight color customization, to change the theme go to the `_quarto.yml` file. See [here](https://quarto.org/docs/output-formats/html-themes.html) for more details about themes and see [here](https://bootswatch.com/) for a preview of what the pre-made themes generally look like.
    - To change just the header color (`primary`) or the color that the drop-down menu options change to when the cursor is over them (`secondary`) use the `custom.scss` file and pick new hex colors.
- Index/about page set-up: There are built in arrangements for the picture and text on the index/about page. This template uses `solana` but there are 4 other options [here](https://quarto.org/docs/websites/website-about.html#templates).
    - For the `jolla`, `solana`, and `trestles` layouts you can choose between `rectangle`, `round`, and `rounded` image shapes
- Navigation placement (navigation details [here](https://quarto.org/docs/websites/website-navigation.html))
    - This template has nagivation in a top navigation bar to the right, specified by putting all items under `right:`. It is also possible to put items under `left:` instead or both `left:` and `right:`.
    - It is also possible to have a sidebar for nagivation instead, see [here](https://quarto.org/docs/websites/website-navigation.html#side-navigation)
    - To add a table of contents to each page, add `toc: true` to `_quarto.yml` under `html:` within `format:`. This is useful if you have long pages in your website. (You can also do this just for a specific page, see the `cv_resume1.qmd` page for an example)
- Adding/removing pages: To add a new page, create a new qmd file and add a reference to it in the `_quarto.yml` file under `navbar:`. To remove a page, remove it from `navbar:` and then delete the corresponding qmd file.

## 4. Auto update option

This template has the option to store publications, presentatations, posters, and other content in a `csv` and then run an R script to update the relevant sections of pages whenever you publish a new paper, have a new presentation, etc. and add to the `csv`. See `sample_content.csv` for an example of what this `csv` could look like. The `auto_update.R` file contains the update script, which was used to generate some of the pages in this template. We expect that you will want to customize the updating and have written the file to try to make it straightforward to do so. 

We recognize that creating the `csv` of site content and creating a version of the script that works for you will take a bit of time and may not be a good use of time for everyone! As mentioned above, you can still use this template and ignore the auto updating feature. If you do want to use the auto updating, an overview of the workflow is:

1. Section off the parts of website pages which will be generated by the update script using the format
```
::: {.content-hidden unless-format="markdown"}
string_describing_section_start
:::
```

```
::: {.content-hidden unless-format="markdown"}
string_describing_section_end
:::
```
2. Create a `csv` with relevant publications, presentations, software, etc. using `sample_content.csv` as a guide. You may want to add additional fields or remove irrelevant fields.
    - one step that might be helpful is going to your google scholar page and exporting the entries there as a csv, though this does not include article urls
4. Using the helper functions in the `auto_update.R` file and modifying them as needed, create a function for each page of the website which will be auto updated.
5. As shown in the example in `auto_update.R`, add code to read in the old page, save a backup (optional), update the page, and then rewrite the old page with the new version.
6. The `auto_update.R` code will only run when *you* decide to run it. So you can add or modify content within an auto-update section (to add page breaks in the cv pdf version, for example) and these changes will not be overwritten unless/until you run `auto_update.R` again. Additionally, as long as the update functions work as intended, no content outside of the update sections will be changed.
7. It's best to make sure any past edits are committed before running `auto_update.R`. The script also saves a backup but (as written) the backup filename is the same every time to avoid unncessary files, so running the script twice will completely overwrite the current pages.
