---
title: "How to build your static site with Hugo"
date: 2019-07-15T20:38:49-04:00
draft: false
type: "post"
description: "Using Hugo to create a static site hosted on Azure storage"
tags: ["azure", "hugo"]
---

In a pair of previous posts I described how to [host a static site in Azure storage](../azure-site) and also how to [use a CDN to map a custom domain to your site with https](../azure-cdn). For each of those examples I used a simple 'hello world' html page, but in the real world we are going to want more out of our site. In my research I came across [Hugo](https://gohugo.io/) and decided to give it a go.

---

### What is Hugo?

Hugo is an open source static site generator. If you really want to be sold on it, go browse [their docs](https://gohugo.io/about/) to learn everything you might want to know. As an end-user, Hugo feels great because:

- It uses simple, Go-based templating engine to layout your site.
- The number of templates available to download and use means you can get started quickly.
- You write all of your content in markdown.
- Hugo has shortcodes to add flexibility where markdown is not sufficient.
- Its CLI makes it easy to run your site local and generate content to deploy to production.

If you are interested in giving it a try, then read on.

---

### Prerequisites

We will be working locally, so we need to set up our local environment. Hopefully this part is as easy as *one*, *two*, *three*.

#### Code Editor

Since we will be working on our site locally and deploying it to Azure, we will need a code editor. I prefer to work with [Visual Studio Code](https://code.visualstudio.com/), so we will use that for this example.

Step *one* is to [download and install VS Code](https://code.visualstudio.com/docs/setup/setup-overview).

There are a nunber of useful [extensions](https://marketplace.visualstudio.com/vscode) you can install for VS Code, but the one we will use for this example is the Azure Storage extension, which will allow us to update our static site on Azure right from our editor.

Step *two* is to [download and install the Azure Storage extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurestorage).

#### Hugo

Since we will be building out our site with Hugo, we will need to install it first.

Step *three* is to follow the [instructions here to install Hugo](https://gohugo.io/getting-started/installing) and then come back.

---

### Making a site with Hugo

Now we should be ready to build our our site with Hugo. I recommend opening VS Code and bringing up the terminal (either View -> Terminal, or ``ctrl-` ``). To confirm you have Hugo installed you can run `hugo version`. With Hugo installed, you can get started with the command:
```
hugo new site staticsite
```
This will create a new Hugo site in a folder named staticsite. From here we want to navigate to that folder and open it in our editor:
```
cd staticsite
code .
```
This will open a new instance of VS Code. It should look a little like this:
{{< imgproc azure-hugo-1 Resize "800x" "vs code hugo project" "Figure 1" />}}
You can see the structure of our Hugo site in the explorer window:

- archetypes
- content
- data
- layouts
- static
- themes
- config.toml

Although the scaffolding for the site is there, it doesn't do anything yet. It lacks any implementation. While we could build it ourselves, we will take the easier route for the time being and use an existing [theme](https://themes.gohugo.io/).

---

### Hallo

For our example, we will use the [Hallo theme](https://themes.gohugo.io/hallo-hugo/) because it is simple and has an MIT license. To install it, first make sure you are in the `staticsite` directory we created earlier. Then run the following from the terminal in VS Code:

```
git clone  https://github.com/EmielH/hallo-hugo.git themes/hallo
```

You should now see a "hallo" folder under the themes folder. Open the "config.toml" file in your project and add the line `theme = "hallo"`. Your project should look like:

{{< imgproc azure-hugo-2 Resize "800x" "vs code hallo theme" "Figure 2" />}}

Run the command `hugo server` from the terminal to launch your project locally. Navigate to the url provided for the web server to see your page:

{{< imgproc azure-hugo-3 Resize "800x" "hallo theme" "Figure 3" />}}

---

### Update your site

We can personalize our new site before deploying it. We will update the picture, the name, the color scheme, and the introduction text.

- To update the picture, create an "images" folder under the "static" folder of your site and upload the picture of our choice to it as "portrait.jpg".
- To update the name, and color scheme, add the following to your config.toml file:

```
[Author]
name = "<your name>"

[params.colors]
background = "#4463AE"
foreground = "#C8D6E9"
```

- To update the introduction text, create a folder named "partials" under the "layouts" folder. Add a file called "introduction.html" that contains your introduction text to that folder.

If your site is looking like this you are on the right track:
{{< imgproc azure-hugo-4 Resize "800x" "hallo updates" "Figure 4" />}}

If you have kept your site running locally, check it out. If you stopped it, the simply run `hugo server` again to see the result:
{{< imgproc azure-hugo-5 Resize "800x" "hallo updates" "Figure 5" />}}

---

### Publish to Azure

Now that we have our site looking the way we want, all that is left it so publish it to Azure. This process is quick and easy.

#### Step One: Build your Hugo Site

First we need to build our proud Hugo site. From our the root "staticsite" folder we have been working on navigate to the terminal in VS Code and run:

```
hugo
```

This command will run very fast. If you look closely, you will notice a new folder named "public" in your project. This project contains the static version of your Hugo site.

### Step Two: Deploy to Static Website...

If you right click on the new "public" folder in the Explorer pane of VS Code, you will see an option to "Deploy to Static Website...". 

{{< imgproc azure-hugo-6 Resize "800x" "deploy" "Figure 6" />}}

This option was included with the "Azure Storage" extension we installed earlier. After you click it you will see a follow-up dialog to pick a Storage Account. Choose the one you created in our previous walkthrough. You will liekly be promted to delete the files that exist in your site and deply the new ones. Choose yes and wait for your site to be copied.

---

That's it. You should now be able to see your new Hugo site hosted on Azure. If you mapped your site to a [custom domain using a CDN](../azure-cdn), you should now also see it at that address. (If it doesn't show up right away you might want to purge your CDN endpoint.)

There is a lot more you can do with Hugo, but I hope this has helped you get started.

Thanks!
