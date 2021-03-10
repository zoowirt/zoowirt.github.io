---
layout: post
title:  "Setting up a website like this on GitHub Pages"
tags: github-pages jekyll hamilton-theme adjusting-jekyll-theme
math: true
---

In this post we explain a little how this website is set up on GitHub Pages with Jekyll.

## Hosting on Github Pages
This static website is hosted for free on Github Pages. It is written in Markdown (the language of the git `README` files), but one can use HTML and JavaScript at any time as well. 
The source code is stored in a github repository - [see here](https://github.com/zoowirt/zoowirt.github.io) for the repository corresponding to this website. 
The url is by default of the form `<github_username>.github.io`.

See [pages.github.com](https://pages.github.com/) for an introduction how to set up a GitHub Page.

## Jekyll and Themes
The website's theme with style and functionality comes from [Jekyll](https://jekyllrb.com/). 
There are many different themes available, e.g., at [jekyllthemes.org](http://jekyllthemes.org/). I chose the [Hamilton theme](https://github.com/ngzhio/jekyll-theme-hamilton) as a basis and adjusted it a little (see below).
The theme features many tools like (SEO) Tags, Google Analytics, Disqus, and more. It also features [MathJax](https://www.mathjax.org/) for latex writing: 
$$\int_{-\infty}^\infty e^{-x^2/2} dx = \sqrt{2\pi}.$$

## Developing the website locally

### Installing prerequisites
To run the website locally on a laptop, one has to install a few things around the Ruby programming language: [see here for the instructions](https://jekyllrb.com/docs/). On my Ubuntu system, it took me while to make things work:
* A recent Ruby version seems necessary (e.g., 2.7.2)
* Things worked only when I installed Ruby with `rbenv`, [as explained here](https://www.techiediaries.com/install-ruby-2-7-rails-6-ubuntu-20-04/).
* The package `ruby-dev` seems necessary, which I installed with `sudo apt-get install ruby-dev` .

### Creating the Jekyll environment and starting the webserver
Having finished this technical stuff, one creates a new Jekyll environment in the repository that corresponds to the GitHub page by executing `jekyll new .`  in a terminal.
Now `bundle exec jekyll serve` starts a webserver at `http://localhost:4000/`. Browsing to this address should show a basic website.

### Choosing a theme
In the root folder, there are two basic configuration files: `_config.yml` and `Gemfile`. For instance, to choose a theme different from the Jekyll default one `Minima`:
* one adds the line `gem 'jekyll-theme-mytheme'` to the `Gemfile`,
* then one installs the theme by executing `bundle` in a terminal;
* then to use the theme on the website one adds the line `theme: jekyll-theme-minimal` to the `_config.yml` file.

However, for the Hamilton theme I choose, [things are a little different](https://github.com/ngzhio/jekyll-theme-hamilton#installation).
In a similar way one installs and applies other Jekyll plugins.

### Adding content and publishing
One can add content in form of [posts](https://jekyllrb.com/docs/posts/) (see [here](https://raw.githubusercontent.com/zoowirt/zoowirt.github.io/master/_posts/2021-03-04-tutorial-how-to-setup-a-python-project.md) for an example) or [pages](https://jekyllrb.com/docs/pages/) (see [here](https://raw.githubusercontent.com/zoowirt/zoowirt.github.io/master/tutorials.md) for an example) to the website. 
Each post or page is based on a file (`.md`, `.html`), having the following type of header:
```
---
layout: post
title:  "This is a title"
tags: tag1 tag2
---
```
How to use the features of the chosen theme is usually explained in the theme's documentation, as it is [here](https://github.com/ngzhio/jekyll-theme-hamilton) for the Hamilton theme. For instance, [here](https://github.com/ngzhio/jekyll-theme-hamilton#navigation) is it explained how to add a navigation bar on the top right.

Having a running webserver, changes in the code are immediately visible after reloading in a browser. Changes in `config.yml` require to stop the webserver (usually with `ctrl-c`) and to execute `bundle exec jekyll serve` again.

Pushing to the repository publishes changes after a short while on the GitHub Page.

## Adjusting a Jekyll theme
To adjust a theme, one simply overrides the corresponding files. The works as follows. 

Say we want to adjust the footer of the Hamilton theme. We find the generating file `footer.html` in the theme's repository in the folder `_includes` ([see here](https://github.com/ngzhio/jekyll-theme-hamilton/tree/master/_includes)).
To adjust the footer, we create the folder `_includes` and a file `footer.html` therein, and copy the content of the `footer.html` in the theme's repository there. 

Now as this file exists in our repository, Jekyll uses the content of our file instead of the theme's original one. Of course, in this way we only overwrite the footer, the other theme files are still taken from the theme and are unchanged.
In this way we can adjust the style, layout, css, etc., as we like. Sometimes one has to look around a little bit to find the file containing the content one is searching for. 

We see that the content of `footer.html` is just some HTML, together with some dynamic code from the programming language Liquid - the code in `{}` brackets. Liquid seems to be quite similar to Jinja in the context of Flask webapps. For instance, one can access the variables in the `_config.yml` file by, e.g., `site.author` in double `{}` brackets.

The code is quite easy to adjust by copy and pasting around and a little trial and error. [See here](https://github.com/zoowirt/zoowirt.github.io/blob/master/_includes/footer.html) for the code that results in the footer of this website.
As another example, I adjusted the sidebar of the original Hamilton theme, and added a link to my company ([see here](https://github.com/zoowirt/zoowirt.github.io/blob/master/_includes/sidebar.html)).

