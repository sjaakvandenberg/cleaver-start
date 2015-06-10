# Cleaver Start

To install, you'll need [Cleaver](https://github.com/jdan/cleaver) by [Jordan Scales](https://github.com/jdan).

| Command                 | Description                                              |
|-------------------------|----------------------------------------------------------|
| npm i -g cleaver        | Install Cleaver globally                                 |
| cleaver file.md         | Generate file-cleaver.html                               |
| cleaver watch file.md   | Watch file.md for changes and generate file-cleaver.html |
| cleaver --debug file.md | Display debug information while generating               |

## YAML Options

Each Markdown file can start out with YAML options specified.

```
title: Presentation Title
theme: dark
output: basic.html
controls: false
--

# Presentation Title
```

| Option          | Description           | Default  |
|-----------------|-----------------------|----------|
| title           | The title of the rendered document. | Untitled |
| author          | Several fields which, if included, populate a basic author "credits" slide at the end of your presentation. | |
| · name          | Your full name | |
| · url           | A url to your website | |
| · twitter       | Your twitter handle | |
| · weibo         | Your weibo handle | |
| · email         | Your email address | |
| theme           | An optional theme to load. A theme is a directory, URL, or a github repo in the form of *username/repo* that may contain stylesheets, javascript, or rewritten templates. Themes group together many of the other options listed in this article. For more information on themes, check out the [documentation](https://github.com/jdan/cleaver/blob/master/docs/themes.md#options). | |
| style           | An optional stylesheet to load. This can be either a URL, or an absolute/relative path to a file. Relative to the markdown document you are sending to cleaver. These styles will be appended to Cleaver's default style. For more fine-grained control, check out the docs on Theming. | |
| output          | The filename (or absolute/relative path to a file) you wish to save your output to. | FILENAME-cleaver.html |
| controls        | An option determining whether or not you want to render simple navigation buttons on your presentation. | true |
| progress        | Displays a small progress bar at the top of your document. | true |
| encoding        | Content encoding to use on the rendered document. | utf-8 |
| template        | URL or path to a mustache template used to render the slides. See [default.mustache](https://github.com/jdan/cleaver/blob/master/templates/default.mustache) for inspiration. | |
| layout          | URL or path to a mustache template used to render the entire slideshow. See [layout.mustache](https://github.com/jdan/cleaver/blob/master/templates/layout.mustache) for inspiration. | |

## Overriding Themes

By default, *style.css* and *script.js* will be **appended** to the default stylesheets and javascripts included in cleaver presentations. If you wish to completely override these defaults, you must include another file in your theme - options.json - corresponding to the following:

```json
{
  "override": true
}
```

Template files will automatically override the default templates.

## More Info

For more information on themes, check out [our documentation](https://github.com/jdan/cleaver/blob/master/docs/themes.md).

## Markup

Cleaver slides are rendered using the following template:

```
{{#slides}}
  <div class="slide{{#hidden}} hidden{{/hidden}} {{classList}}" id="slide-{{id}}">
    <section class="slide-content">{{{content}}}</section>
  </div>
{{/slides}}
```

And produce the following markup:

```
+-------------------------------+
| #slide-N                      |
|     +-------------------+     |
|     | .slide-content    |     |
|     |                   |     |
|     |                   |     |
|     |                   |     |
|     |                   |     |
|     +-------------------+     |
|                               |
|                               |
| (navigation)                  |
+-------------------------------+
```

**#slide-N** (for example, *#slide-3*) allows you to identify a particular full-bleed slide by its position in the slideshow. It extends to the bounds of the page.

**.slide-content** is a smaller window which holds the actual content of the slide.

## Class List

A class list can be placed after each "slice" (denoted `--`) to help you style individual slides without worrying about their index.

```
-- bg

This slide will have a class "bg" associated with it

-- bg blink

This one, too, but it will also have the class "blink"
```

## Slide Types

### Title slide

```
# Cleaver 101
## A first look at quick HTML presentations
```

**h1** and **h2** elements (prefaced with # and ## respectively), will automatically include padding to render a title slide.

## Other slides

### Two columns

To use two columns, place your content in div tags with a `left` or `right` class.

```
<div class="left">
![left image](http://placehold.it/1500x800)
</div>
<div class="right">
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec suscipit aliquam aliquam. Nulla ultricies nisi quis leo gravida, lacinia auctor nisl dignissim.
</div>
```

### Code

~~~
```ruby
# comment
class Dog
  def initialize(name, color, bark)
    # code
  end
end

skippy = Dog.new()
skippy.bark()
```
~~~

### A list of things

```
* Item 1
* Item B
* Item gamma

No need for multiple templates!
```

### A table of things

```
| Item      | Description        |
|-----------|--------------------|
| This      | This is nice       |
| That      | That's also nice   |
| The Other | Well, the other... |
```

### A blockquote

```
> Lorem ipsum dolor sit amet.
```

### Links

```
[Twitter](https://twitter.com)
```

### Images

```
![Alt tag](http://placehold.it/600)
```

Since slides are written in [Markdown](http://daringfireball.net/projects/markdown/), you can include things like lists, images, and arbitrary HTML.

**h3** tags (prefaced `###`) are automatically given a bottom border to represent a slide title.

## Navigation

Cleaver supports keyboard navigation for switching between slides. Alternatively, click the control buttons located below the presentation.

To navigate the slideshow:

**forward**: <kbd>K</kbd>, <kbd>L</kbd>, <kbd>&uarr;</kbd>, <kbd>&rarr;</kbd>, <kbd>PgDn</kbd>, and <kbd>Space</kbd>

**reverse**: <kbd>H</kbd>, <kbd>J</kbd>, <kbd>&darr;</kbd>, <kbd>&larr;</kbd>, <kbd>PgUp</kbd>, and <kbd>Backspace</kbd>

The toggle fullscreen mode, press <kbd>ENTER</kbd>.
