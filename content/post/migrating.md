+++
title = "Migrating my website to Hugo + Academic + ox-hugo"
author = ["Qingyuan Zhao"]
date = 2020-06-13
tags = ["Workflow"]
draft = false
+++

Being stuck at home during the pandemic, as miserable as it is, actually
helps me to redesign my working environment. One of the many outcomes
is this new personal website powered by the [Academic theme](https://sourcethemes.com/academic/) for [Hugo](https://gohugo.io/). I
hope you will agree with me that it just looks awesome!

For the rest of this blog post, I will explain the workflow to
generate this website. I hope you may find it useful when designing
your own website.

{{% toc %}}


## The Hugo framework {#the-hugo-framework}

I admire the front-end web developers who still hand write HTML and
CSS, but those are simply too much for me. If you are like me who just
wants a personal website that can keep track of one's work, chances
are you would like to use some [static site generator](https://en.wikipedia.org/wiki/Web%5Ftemplate%5Fsystem#Static%5Fsite%5Fgenerators). When I was young
and had my first encounter with the internet, [Microsoft Frontpage](https://en.wikipedia.org/wiki/Microsoft%5FFrontPage) and
[Dreamweater](https://en.wikipedia.org/wiki/Adobe%5FDreamweaver) were the most popular website generator.


### Static site generators {#static-site-generators}

But we are well past that time and there are many much better choices
today. One great framework is the _Markdown_, a lightweight markup
language that is used in [GitHub readme pages](https://guides.github.com/features/mastering-markdown/) and deeply integrated
with statistical computing with the [R Markdown](https://rmarkdown.rstudio.com/). Many static site
generators (including [Jekyll](https://jekyllrb.com/) and [Hugo](https://gohugo.io/)) are able to automatically
generate HTML codes from Markdown. This is a giant life-saver because
Markdown is so much more readable.

After some brief research I decided to use Hugo. Based on my reading,
Hugo is renowned as "the world's fastest framework for building
websites" and many developers were extremely happy about it. But for
me, the killer was two extensions to Hugo: the Academic theme that
implements many use features for academic researchers, and the
[ox-hugo](https://ox-hugo.scripter.co/) backend that exports `.org` files straight to Hugo-compatible
Markdown files. As an academic who already uses Emacs for most of the
day-to-day work, these features are extremely convenient for me.

Installing Hugo in Mac OS X is straightforward with [homebrew](https://brew.sh/). Simply
run

```sh
brew install hugo
```


### Content management in Hugo {#content-management-in-hugo}

Let's first take a look at how Hugo works. The most useful thing to
know is Hugo's [organization of content source](https://gohugo.io/content-management/organization/). In particular, the most
important is the `content` folder, which contains all the Markdown
files needed to generate the website. Here is a sample structure for
the `content` folder from Hugo's official documentation (the base URL
for this site is <https://example.com/>):

```text
.
└── content
    └── about
    |   └── index.md  // <- https://example.com/about/
    ├── posts
    |   ├── firstpost.md   // <- https://example.com/posts/firstpost/
    |   ├── happy
    |   |   └── ness.md  // <- https://example.com/posts/happy/ness/
    |   └── secondpost.md  // <- https://example.com/posts/secondpost/
    └── quote
        ├── first.md       // <- https://example.com/quote/first/
        └── second.md      // <- https://example.com/quote/second/
```

As you can see, each Markdown file in a directory under `content`
generates a webpage. Notice that `_index.md` has a special role in
Hugo---it allows you to add front matter and content to the list
pages. See [here](https://gohugo.io/content-management/organization/#:~:text=%5Findex.md%20has%20a%20special,in%20%5Findex.md%20using%20the%20) for more detail.


### Front matter in Hugo {#front-matter-in-hugo}

Another important concept is the _front matter_ of a Markdown file
that contains metadata and options for the content. Some popular
formats are TOML and YAML, which are much more human friendly than
JSON. The following block contains the first few lines of this blog
post. The front matter is the lines between `+++` (which means it is in TOML):

```nil
+++
title = "Migrating website to Hugo + Academic + ox-hugo"
author = ["Qingyuan Zhao"]
date = 2020-06-13
tags = ["Workflow"]
draft = false
+++

Being stuck at home during the pandemic, as miserable as it is, actually
helps me to redesign my working environment....
```

Apart from `draft` which is a option for the Academic theme, all other
fields are standard for Hugo Markdown files.


### Hugo themes {#hugo-themes}

There are many [cool themes](https://themes.gohugo.io/) for Hugo that you can immediately use. As
far as I know, they are useful in two ways. First, all the page
styles are already pre-defined and many of them look awesome! Second,
they also provide convenient templates for the front matter. As an
example, I was initially considering to use the [Jane theme](https://themes.gohugo.io/hugo-theme-jane/) for this
website. Similar to most other Hugo themes, it is really easy to
install and get started; an example site can be found in its [GitHub
repository](https://github.com/xianmin/hugo-theme-jane/tree/master/exampleSite), which generates this [demo page](https://themes.gohugo.io/theme/hugo-theme-jane/). One thing I especially
like about this theme is how it allows the reader to focus on the
website content. Eventually I did not choose it because it is not
powerful enough for all the different functions I needed, but I would
highly recommend it if you just want to write blogs.


### From Markdown to HTML {#from-markdown-to-html}

After creating all the Markdown content and selecting a theme, you can
preview the website by running

```sh
hugo server
```

from the website directory. This builds the website and creates a
local web server to
host it. It generates a link (the default is <http://localhost:1313/>)
which can be pasted into a web browser. In the background, the hugo
server also detects any change to the content and updates the website
automatically.

To public the website, first execute `hugo` from the website
directory. This builds all the website pages in the `public/` folder
within seconds. You can then upload that folder to an FTP server. For
me, this amounts to

```sh
rsync -avz --delete public/ qz280@ssh.maths.cam.ac.uk:~/public_html
```

See [here](https://gohugo.io/hosting-and-deployment/) for other options to host and deploy your website.


## The Academic theme {#the-academic-theme}

[Academic](https://sourcethemes.com/academic/) is a Hugo theme designed for academic researchers. To me, it
is a website builder with just the right balance of complexity and
flexibility. There are [many ways](https://sourcethemes.com/academic/docs/install-locally/) to install the Academic theme. I
prefer the Git option by forking and cloning the [Academic Kickstart
GitHub repository](https://github.com/sourcethemes/academic-kickstart). You can then modify the content of the startup
website and customize its styles.


### Content management in Academic {#content-management-in-academic}

Academic has a convenient content management system that is inherited
from Hugo. This is currently how my website directory looks like:

```text
├── assets
│   ├── images
│   └── scss
├── config
│   └── _default
├── content
│   ├── authors
│   ├── home
│   ├── news
│   ├── post
│   ├── project
│   ├── publication
│   ├── talk
│   └── teaching
├── content-org
├── data
│   ├── fonts
│   └── themes
├── resources
│   └── _gen
├── scripts
├── static
│   ├── admin
│   ├── files
│   └── img
└── themes
    └── academic
```

Unsurprisingly, the `content` folder contains all the Markdown files
for website content. Most of its sub-directories correspond to a
section of the webpage; in particular, `home` corresponds to the
homepage of your website. Another unique folder is the `authors`,
which contains basic information about the website owner and all other
authors (not needed for a personal website). The `content-org`
contains the org-mode files that generate some or all of the Markdown
files in `content`. I will go through this later on in the post, but
it is of course not needed if you don't use org-mode. The `config`
folder contains all the important website settings offered by the
Academic theme. See [its documentation](https://sourcethemes.com/academic/docs/get-started/) for more information.


### Organizing your work {#organizing-your-work}

A nice feature of the Academic framework is the templates for
publications, talks, projects, and many other academic-related
objects. For example, I recently arXived a paper on the
[selection bias in COVID-19 studies](https://arxiv.org/abs/2004.07743). To add this new publication to my
webpage, I can execute the following command

```sh
hugo new --kind publication publication/covid-19-bets
```

This generates a Markdown file `publication/covid-19-bets/index.md`
with YAML front matter from the publication template. I can then
add all the relevant information about this publication to the
Markdown file. This is how the beginning of this file looks like
right now:

```text
---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "BETS: The dangers of selection bias in early analyses of the coronavirus disease (COVID-19) pandemic"
authors: ["admin", "Phyllis Ju", "Sergio Bacallado", "Rajen Shah"]
date: 2020-04-16
doi: ""

# Schedule page publish date (NOT publication's date).
publishDate: 2020-06-13T21:28:45Z

# Publication type.
# Legend: 0 = Uncategorized; 1 = Conference paper; 2 = Journal article;
# 3 = Preprint / Working Paper; 4 = Report; 5 = Book; 6 = Book section;
# 7 = Thesis; 8 = Patent
publication_types: ["3"]
---
```

As you can see, the YAML fields record important metadata about the
publication, which are used by Academic to automatically generate this
nice [webpage](/~qz280/publication/covid-19-bets/). This same workflow apples to talks, projects, and other
[content types](https://sourcethemes.com/academic/docs/managing-content/) provided by Academic.


### Widget pages {#widget-pages}

An important feature of Academic is its [widget pages](https://sourcethemes.com/academic/docs/page-builder/). They are
essentially custom page blocks that summarizes the information in the
other pages. By default, the homepage is a widget page with many
built-in widgets:

```sh
> ls content/home
```

```text
about.md           demo.md            hero.md            projects.md        tags.md
accomplishments.md experience.md      index.md           skills.md          teaching.md
contact.md         featured.md        people.md          slider.md          welcome.md
```

Personally, I prefer a clean homepage and would use separate section
pages to organize the website. So [my homepage](/) only contains two
widgets. Additionally, I created a custom widget page called [news](/news/) to
make announcements and display new content.


### Customization in Academic {#customization-in-academic}

The are several important files to modify when building your own
website:

-   `config/default/config.toml` General configuration for Hugo.
-   `config/default/params.toml` Parameters for Academic.
-   `config/default/menus.toml` Configuration for the menu bar.
-   `content/authors/admin/_index.md` Information about the website
    owner.

Advanced customization can be found [here](https://sourcethemes.com/academic/docs/customization/).


## The ox-hugo exporter {#the-ox-hugo-exporter}

Finally, I use `ox-hugo`, an Org mode to Hugo exporter, to generate blog
posts and other text-rich content in this website. Since the beginning
of my PhD, I have gradually become an heavy user of the extremely
extensible text editor [Emacs](https://www.gnu.org/software/emacs/). Previously I was mostly just using Emacs
for writing _R_ and \\(\LaTeX\\) with the amazing [ESS](https://ess.r-project.org/) and [AUCTeX](https://www.gnu.org/software/auctex/) modes. I
saw great reviews of the [Org mode](https://orgmode.org/) before and started
to appreciate it as my duties pile up after becoming an independent
investigator. Org mode, as its name suggests, is a great way to keep
oneself organized. Besides keeping notes and managing TODO lists,
Org mode is also great for writing documents. It has powerful backends
that can export `.org` files to LaTeX, HTML, Markdown, and other
formats.

A picture is worth a thousand words. This is the `.org` files that generates the blog
post you are currently viewing.

{{< figure src="/~qz280/img/ox-hugo-example.png" >}}

I followed the "one post per Org subtree" format [recommended](https://ox-hugo.scripter.co/) by the
`ox-hugo` author. So my `content-org/` folder has only one `.org`
file:

```sh
> ls content-org/
```

```text
all-posts.org
```

Each website section corresponds to a level-1
heading (one \*), and each blog post is contained under a level-2
heading in Post. Each heading has some properties (and inherit the
properties of its ancestors) that are exported to TOML or YAML front
matter. If the `EXPORT_FILE_NAME` is specified, content under that
heading is then exported to the corresponding section in the `content`
folder:

```sh
> ls content/post/
```

```text
_index.md      migrating.md   mr-software.md
```

To export all subtrees to Hugo Markdown, simply press `C-c C-e H A` in
Emacs. The local Hugo server then picks up the content change and
updates the website. More information about `ox-hugo` (including
many advanced features that I am still learning) can be found in its
[online documentation](https://ox-hugo.scripter.co/).

So that's it for now! Feel free to leave a comment below. I will
update this post if I make any major modification to this workflow in
the future.
