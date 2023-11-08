---
title: "How to build a new blog with Hugo and blowfish"
date: 2023-10-09
tags: [ "blog", "Hugo", "blowfish theme" ]
summary: "Step by step tutorial of how to build a blog with Hugo and blowfish"
categories: ["Code Tutorial" ]
series: ["blog"]
series_order: 2
---

## Introduction

Creating a blog is an exciting venture that allows you to share your thoughts, ideas, and experiences with the world. With the combination of Hugo, a fast and flexible static site generator, and the visually appealing Blowfish theme, you can build an impressive and fully functional blog. In this guide, we will take you through the step-by-step process of building your blog using Hugo and the Blowfish theme.

## Step 1: Install Hugo

Before diving into the blog-building process, you need to install Hugo on your computer. Hugo works on Windows, macOS, and Linux, making it widely accessible. Visit the Hugo website or check the documentation for detailed installation instructions based on your operating system.

## Step 2: Create a New Hugo Site

Once Hugo is installed, open your terminal or command prompt and navigate to the desired directory where you want to create your blog. Use the following command to create a new Hugo site:

```
hugo new site your-blog-name
```

This command will create a new directory with the name you specified, which will serve as the root folder for your blog.

## Step 3: Choose the Blowfish Theme

Next, you need to choose and install the Blowfish theme. Navigate to the themes directory of your Hugo site by using the following command:

```
cd your-blog-name/themes
```

Inside the themes directory, clone the Blowfish theme repository from GitHub:

```
git clone https://github.com/yoshiharuyamashita/blowfish.git
```

This will download the Blowfish theme into the themes directory of your Hugo site.

## Step 4: Configure the Blog

Now, it's time to configure your blog. Open the config.toml file located in the root directory of your Hugo site using a text editor. Customize the necessary settings according to your preferences, such as site title, author information, and language settings. You can also specify other advanced configurations like the base URL, navigation menu, and social media links.

## Step 5: Add Content

To start adding content to your blog, navigate to the content directory within your Hugo site using the command:

```
cd your-blog-name/content
```

Inside the content directory, create a new directory for each blog post or article. For example, you can create a directory called "my-first-blog-post" using the following command:

```
hugo new my-first-blog-post/index.md
```

This will create an index.md file where you can enter your content using Markdown syntax.

## Step 6: Customize the Blowfish Theme

To personalize the Blowfish theme, navigate to the themes/blowfish directory within your Hugo site using the command:

```
cd your-blog-name/themes/blowfish
```

Here, you can edit the theme's configuration files, CSS stylesheets, and HTML templates to match your desired design. Refer to the theme's documentation or README file for specific instructions on customization options.

## Step 7: Preview and Deploy

To preview your blog locally, go back to the root directory of your Hugo site and run the following command:

```
hugo server -D
```

This will start a local development server, allowing you to see your blog in action on your computer.

When you are satisfied with the final look of your blog, it's time to deploy it to a hosting platform. You have several options, such as using a service like Netlify, GitHub Pages, or deploying it manually to a web server.

## Conclusion:

By following these step-by-step instructions, you can successfully build your blog using Hugo and the visually appealing Blowfish theme. Whether you are a beginner or experienced blogger, Hugo's simplicity and flexibility, combined with the customizable and engaging Blowfish theme, will enable you to showcase your content in an attractive and functional manner. Get ready to share your ideas and embark on a rewarding blogging journey with Hugo and the Blowfish theme!