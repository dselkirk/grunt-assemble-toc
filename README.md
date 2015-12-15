# Table of Contents jQuery Plugin - jquery.toc

A minimal, tiny jQuery plugin that will generate a table of contents, drawing from headings on the
page.

The generated TOCs are semantic, nested lists (`ul` or `ol`) with hash-link anchors to the headings.

## Usage

You can [download the latest release](http://ndabas.github.com/toc/assets/jquery.toc.zip), or
install with Twitter's [Bower](http://twitter.github.com/bower): `bower install jquery.toc`.

Include jQuery (>= 1.6) and jquery.toc.js/jquery.toc.min.js on your page. The plugin can then be
used either via HTML5 data attributes, or via the programmatic API. See below for the available
options.

### Via data attributes

Minimal example:

    <ul data-toc></ul>

With options:

    <ol data-toc="div.container" data-toc-headings="h2,h3,h4"></ol>

### Via the JavaScript programmatic API

Minimal example:

    <ul id="toc"></ul>
    ...
    <script type="text/javascript">
        $("#toc").toc();
    </script>

With options:

    <ul id="toc"></ul>
    ...
    <script type="text/javascript">
        $("#toc").toc({content: "div.container", headings: "h2,h3,h4"});
    </script>

### Options

    <ul data-toc="content" data-toc-headings="headings"></ul>

    $(...).toc({content: "body", headings: "h1,h2,h3"});

The plugin has two options:

* `content` is a selector where the plugin will look for headings to build up the TOC. The default
  value is `"body"`.
* `headings` is a string with a comma-separated list of selectors to be used as headings, in the
  order which defines their relative hierarchy level. The default value of `"h1,h2,h3"` will select
  all `h1`, `h2`, and `h3` elements to build the TOC, with `h1` being a level 1, `h2` a level 2, and
  so on. You can use any valid list of jQuery selectors; for example, if you just want `h1` tags
  with a specific class, and no `h3` tags, you could use `"h1.title,h2"` for this parameter.

In addition, the plugin will create nested lists of the same type (`ul` or `ol`) as the element that
it is called on.

### Automatic ID generation

The plugin generates hash-links to the headings on the page, to allow users to jump to the heading
by clicking in the generated table of contents. This feature requires that the headings have IDs
assigned; if they do not, the plugin will generate and assign IDs automatically.

The generated IDs are based on the text inside the headings, and uses two simple rules:

* The ID must begin with a letter; so any non-letter (`[^A-Za-z]`) characters are discarded from the
  beginning of the string.
* For the rest of the ID, only letters and numbers are used from the heading text; all other
  characters (`[^A-Za-z0-9]`) are converted to underscores.

For example, a heading like `<h2>Heading 2.1</h2>` will get the ID `Heading_2_1`.