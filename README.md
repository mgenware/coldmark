# ColdMark
The Markdown language we use at coldfunction.com

The language is based on the [CommonMark](http://commonmark.org/) standard with following additions.

## No inline HTML
Allowing inline HTML enforces parser to sanitize HTML to block malicious code. It also looks pretty ugly.

## Line breaks
We discourage the use of [hard line breaks](http://spec.commonmark.org/0.12/#hard-line-breaks) in CommonMark spec. We believed that markdown should be rendered the same as what you wrote.


In ColdMark:
* **One Carriage return** renders to `<br />`.
* **Two consecutive Carriage returns** will start a new paragraph, that is, a `<p>` element.

For example, this:
```
a
b

c
```

Renders to:
```html
<p>a<br />b</p>
<p>c</p>
```

## Fenced code blocks

### Support for languages and `language-` CSS class
````markdown
```javascript
```
````

Renders to:
```html
<pre><code class="language-javascript"></code></pre>
```

Language name defaults to `none`:
````markdown
```
```
````

Renders to:
```
<pre><code class="language-none"></code></pre>
```


### Support for custom styles
````markdown
```javascript happy
let value = 1 / 0;
```
````

Renders to:
```html
<pre><code class="language-javascript coldmark-happy">let value = 1 / 0;</code></pre>
```

A fenced code block can contain one language name and unlimited number of custom classes (see "System styles" for an exception). For example:
````markdown
```none info bold dark-theme
Hi
```
````

Renders to:
```html
<pre><code class="language-javascript coldmark-info coldmark-bold coldmark-dark-theme">Hi</code></pre>
```

#### System styles
Belows are ColdMark's system styles
```
info, success, error, warning
```

Unlike custom styles, a system style remains as a style even they appears like a language name. For example:
````
```info
```
````

Renders to:
````
```
<pre><code class="coldmark-info"></code></pre>
```
````

### Support for language shortcuts
````markdown
```js
```
````

Renders to:
```html
<pre><code class="language-javascript"></code></pre>
```

List of supported shortcuts:
* `c#`: `csharp`.
* `f#`: `fsharp`.
* `js`: `javascript`.
* `py`: `python`.
* `ts`: `typescript`.


### Use longer fences to escape shorter fences
**Note that this feature is supported by [CommonMark](http://spec.commonmark.org/0.27/#example-92)**. I just want to emphasize it in case you may not know.

`````markdown
````markdown
```markdown
# this is a markdown title
```
````
`````

Renders to:
````html
<pre><code class="language-markdown">```markdown
# this is a markdown title
```</code></pre>
````

## Links
## Autolinks
Unlike CommonMark, which requires autolinks to be surrounded by `<` and `>`, ColdMark will convert all URL-like text to links.
