Add table of contents here

# Hugo

## Creating a blog in 10 minutes

This tutorial uses github for repositories.

1.  Install Hugo (Ubuntu)

    ```bash
    sudo apt install hugo
    ```

2.  Create 2 GitHub repos
    -   "blog" repo to store the code - public repo
    -   "blog.github.io" repo that has the static assets in github
        pages - where we deploy from
3.  Clone the blog repo and create the website

    ```bash
    git clone blog.git cd blog # enter de directory 
    hugo new site blogname # create a new site named blogname
    ```
    This will create a directory inside blog called blogname where it has the
    code for the website.

4.  Clone the chosen theme for the blog and set it as the default theme

    ```bash
    cd themes/ 
    git clone chosen-theme 
    cd .. nvim config.toml # open the config file for the website
    ``` 
    Insert inside the configuration file the line:

    ```toml
    baseURL = "theurlofthepage"
    title = "blogname"
    theme = "chosen-theme"
    ```

5.  Check if the website is working properly by looking is locally

    ```bash
    hugo server # it should return a localhost url
    ```

6.  Create a new Post

    ```bash
    hugo new posts/title-for-the-post.md 
    nvim contents/posts/title-for-the-post.md # markdown file
    ```

7.  Before cloning, you have to do a first commit and create a branch
    called \"main\".

    ```bash
    cd # move out of the repo directory 
    git clone blog.github.io.git 
    cd blog.github.io.git/ 
    git checkout -b main # creates the new branch 
    touch readme.md 
    git add . 
    git commit -m "first commit" 
    git push origin main # pushed the changes to the main branch
    cd rm -rf blog.github.io.git/
    ```

8.  Clone the \"blog.github.io\" repo as a submodule of the \"blog\"
    repo: that is where the static assets generated are going to be
    stored

    ```bash
    cd blog/blogname/ #inside the generated blog directory 
    git submodule add -b main blog.github.io.git public # the static contents generated are going to be automatically added to this public folder
    ```

9.  Build the code

    ```bash
    hugo -t chosen-theme # will add pages and a sitemap to the public folder 
    cd public/ 
    ls # check if the files are there 
    git add . 
    git commit -m "initial commit" 
    git push origin main
    ```

For more information see:

-   [Git -
    Submodules](https://git-scm.com/book/en/v2/Git-Tools-Submodules)

## Managing content in Hugo

In Hugo, every file you create using the command `hugo new filename` will store the file inside the folder `content`. So if you want to create a file inside a `dir1` folder you can do that by typing the commando `hugo new dir1/filename`.

The cool thing about having directories is that you can create list pages for those directories. What that means is that when your type the url with `dir1`, there will be a list page with all the pages that were saved inside the `dir1` directory.

If there is a second directory inside a primary folder, you can create a list page by creating a `_index.md` inside this second directory to list all posts there are stored there. And inside this `_index.md` file you can edit and put anything you want and will still list the other pages. If the list page was created automatically, you can also edit just creating a "missing" `_index.md` file. See [more](https://gohugo.io/content-management/page-bundles/).

You can create a predefined front matter by editing the file `archetype.md`. If you create a new file inside the `archetype` folder, this new configurations could be used in the future when creating a new file. For example, you created a new file archetype file named `dir1.md`. Now when you create a file using the command `hugo new dir1/file`, the front matter will follow what is saved inside this new archetype file and also will be placed inside the folder `dir1`.

## Shortcodes inside Hugo

You can do that by typing for example the following command for a youtube shortcode.

```
{{< youtube 2xkNJL4gJ9E >}}
```

For mode shortcode visit the [Hugo](https://gohugo.io/templates/shortcode-templates/) page.

## Taxonomies

You can group content in a website by using tags or categories and that is done inside the front matter.

For tags this is done by typing inside an array:
```toml
tags: ["tag1", "tag2"]
categories: ["category1", "category2"]
```

They might show inside the content card for the post. What is cool is that Hugo will automatically create pages for each tag or category that were directed at the posts.

The interesting thing is that you can create whatever kind of similar thing, like "moods", "authors", "sources", "kind" and etc. But to do that you have to go to the `config.toml` file and insert the new taxonomies that you want.

```toml
[taxonomies]
    tag: "tags"
    category: "categories"
    mood: "moods"
```
[See more](https://www.youtube.com/watch?v=pCPCQgqC8RA)

## Themes

Inside the `themes` folder you will find the `layouts` folder the contains the templates for list pages and single pages in `html` format. There are many things that you can do with this by the main one is that you can change the layout of your website by changing these template files.

[See more](https://www.youtube.com/watch?v=8b2YTSMdMps)

Essentially you can build different templates for:
- List pages;
- Single pages;
- Home page;
- Section pages.

Another way to do is using base templates and blocks. First thing you have to do is create the following file `layouts/_defaults/baseof.html`. This file will be the overarching template for the website, it is a higher level template and will cease the need to copy and paste sections of code for each template file. Just watch this [video](https://www.youtube.com/watch?v=QVOMCYitLEc&list=PLLAZ4kZ9dFpOnyRlyS-liKL5ReHDcj4G3&index=16) to understand how it is using blocks to build any pages.

## Variables

Look at all the [variables available for Hugo](https://gohugo.io/variables/). The interesting use would mainly be when modifying an existing template to add or remove things that would show up on the page.

You can access create variables inside the front matter by typing:

```yaml
var: "page"

```
And call it at the `html` page using `{{ .Params.var }}`, and when the html is rendered it will show the value set for `var`.

You can also create variables locally, not being set in another file. To do this follow the syntax bellow:

```html
{{ $myVar := "String" }}
{{ $myVar := 3 }}
{{ $myVar := true }}

```

## Functions

Can only be used inside the layouts folder. The syntax is:

```html
{{ funcName param1 param2 }}

```

See more at the Hugo page for [functions](https://gohugo.io/functions/).

Can add more complexity by using [if statements](https://www.youtube.com/watch?v=juSnHsCX9RU&list=PLLAZ4kZ9dFpOnyRlyS-liKL5ReHDcj4G3&index=19).

## Data folders

The files have to be in json, toml or yaml. You can display data by calling the file withe the function `.Site.Data.filename`.

## Hosting

When you insert in the command line `hugo`, the website will be built and its contents will be stored inside the `public` folder to be uploaded to the webserver. There is nothing more to do after this.

# Docker

# Release history
