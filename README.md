# Tech site
## Add posts
To create a new post you’ll need to create a new markdown file in folder `_posts` with a file name in this format:
```
YYYY-MM-DD-title.md
```
The format is four-digit year, followed by a hyphen then two-digit month, followed by another hyphen and two-digit day, followed by a hyphenated title and ending with the markdown file extension.
So for example today’s date is May 29, 2016 and I want to create a new post called I love eating pizza. It would look something like this:

```
├── _posts
│   ├── 2016-04-06-welcome-to-jekyll.md
│   └── 2016-05-29-i-love-pizza.md
```
Now that you’ve got your new post file, you’ll have to add in a few more things before you’re ready to write your post.

Up at the top of your new post file, you’ll have to add in some Front Matter. Front Matter is the stuff you find at the top of posts and pages between a pair of --- triple-dashes. It is written in YAML, also known as YAML Ain’t Markup Language.

At a minimum, a post file should have two keys. A layout and a title key. So for my, I love pizza post, this is what the Front Matter will look like.
```
---
layout: post
title: CRANBERRY CRÈME TARTS
author: Victoria
categories:
    - vegan
image:
    feature: IMG_0924.jpg
---
```
The post content is in markdown format:
[Basic Syntax](https://www.markdownguide.org/basic-syntax)

## Add Image
- Upload images to a folder `assets/images/`
- Insert the image to the post with the markdown:
```
[![Philadelphia's Magic Gardens. This place was so cool!](/assets/images/philly-magic-gardens.jpg "Philadelphia's Magic Gardens")](#)
```
Please use relative pathes like `assets/images/image-name.jpg`.
## Add Category
- Create a file in the folder: `_category` with category lowercase category name.
- Add to the file Front Matter with a name of the category.
```
---
name: Brekfast
---
```
## Development
```
bundle exec jekyll serve
```
