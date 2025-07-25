---
title: Basic HTML syntax
slug: Learn_web_development/Core/Structuring_content/Basic_HTML_syntax
page-type: tutorial-chapter
sidebar: learnsidebar
---

{{NextMenu("Learn_web_development/Core/Structuring_content/Webpage_metadata", "Learn_web_development/Core/Structuring_content")}}

In this article, we cover the absolute basics of HTML. To get you started, this article defines elements, attributes, and all the other important terms you may have heard. It also explains where these fit into HTML. You will learn how HTML elements are structured, how a typical HTML page is structured, and other important basic language features. Along the way, there will be an opportunity to play with HTML too!

<table>
  <tbody>
    <tr>
      <th scope="row">Prerequisites:</th>
      <td>
        <a href="/en-US/docs/Learn_web_development/Getting_started/Environment_setup/Installing_software">Basic software installed</a>, and basic knowledge of <a href="/en-US/docs/Learn_web_development/Getting_started/Environment_setup/Dealing_with_files">working with files</a>.
      </td>
    </tr>
    <tr>
      <th scope="row">Learning outcomes:</th>
      <td>
        <ul>
          <li>The anatomy of an HTML element — element, opening tag, content, closing tag, attributes.</li>
          <li>The HTML body and its purpose as a container for the page content.</li>
          <li>What <a href="/en-US/docs/Glossary/Void_element">void elements</a> (also known as empty elements) are, and how they differ from other elements.</li>
          <li>The need for a doctype at the top of HTML documents. Its original intended purpose, and the fact that now it is somewhat of a historical artifact.</li>
          <li>Understanding that HTML needs to be correctly nested.</li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>

## What is HTML?

{{glossary("HTML")}} (HyperText Markup Language) is a _markup language_ that tells web browsers how to structure the web pages you visit. It can be as complicated or as simple as the web developer wants it to be. HTML consists of a series of {{glossary("Element", "elements")}}, which you use to enclose, wrap, or _mark up_ different parts of content to make it appear or act in a certain way. The enclosing {{glossary("Tag", "tags")}} can make content into a hyperlink to connect to another page, italicize words, and so on. For example, consider the following line of text:

```plain
My cat is very grumpy
```

If we wanted the text to stand by itself, we could specify that it is a paragraph by enclosing it in a paragraph ({{htmlelement("p")}}) element:

```html
<p>My cat is very grumpy</p>
```

HTML lives inside text files called **HTML documents**, or just **documents**, with a `.html` file extension. Where previously we've talked about web pages, an HTML document contains the web page's content and specifies its structure.

The most common HTML file you'll encounter is `index.html`, which is generally used to contain a website's home page content. It's also common to see subfolders with their own `index.html`, so a website can have multiple index files in different places.

> [!NOTE]
> Tags in HTML are not case-sensitive. This means they can be written in uppercase or lowercase. For example, a {{htmlelement("title")}} tag could be written as `<title>`, `<TITLE>`, `<Title>`, `<TiTlE>`, etc., and it will work. However, it is best practice to write all tags in lowercase for consistency and readability.

## Anatomy of an HTML element

Let's further explore our paragraph element from the previous section:

![A sample code snippet demonstrating the structure of an html element.<p> My cat is very grumpy </p>.](grumpy-cat-small.png)

The anatomy of our element is:

- **The opening tag:** This consists of the name of the element (in this example, _p_ for paragraph), wrapped in opening and closing angle brackets. This opening tag marks where the element begins or starts to take effect. In this example, it precedes the start of the paragraph text.
- **The content:** This is the content of the element. In this example, it is the paragraph text.
- **The closing tag:** This is the same as the opening tag, except that it includes a forward slash before the element name. This marks where the element ends. Failing to include a closing tag is a common beginner error that can produce peculiar results.

The element is the opening tag, followed by content, followed by the closing tag.

> [!NOTE]
> Head on over to our learning partner Scrimba's [HTML tags](https://scrimba.com/learn-html-and-css-c0p/~02?via=mdn) <sup>[_MDN learning partner_](/en-US/docs/MDN/Writing_guidelines/Learning_content#partner_links_and_embeds)</sup> scrim for an interactive explanation of HTML tags.

### Creating your first HTML element

Let's give you some practice at writing your own HTML elements:

1. Click **"Play"** in the code block below to edit the example in the MDN Playground.
2. Wrap the line of text with the tags `<em>` and `</em>`. To _open the element_, put the opening tag `<em>` at the start of the line. To _close the element_, put the closing tag `</em>` at the end of the line. Doing this should give the rendered text in the output panel italic text formatting.
3. If you are feeling adventurous, try looking up some more HTML elements and applying them to the text example.

If you make a mistake, you can clear your work using the _Reset_ button in the MDN Playground. If you get really stuck, you can view the solution below the code block.

```html live-sample___basic_html_1
This is my text.
```

{{ EmbedLiveSample('basic_html_1', "100%", 60) }}

<details>
<summary>Click here to show the solution</summary>

Your finished line of HTML should look like this:

```html
<em>This is my text.</em>
```

</details>

### Nesting elements

Elements can be placed within other elements. This is called _nesting_. If we wanted to state that our cat is **very** grumpy, we could wrap the word _very_ in a {{htmlelement("strong")}} element, which means that the word is to have strong(er) text formatting:

```html
<p>My cat is <strong>very</strong> grumpy.</p>
```

There is a right and wrong way to do nesting. In the example above, we opened the `p` element first, then opened the `strong` element. For proper nesting, we should close the `strong` element first, before closing the `p`.

The following is an example of the _wrong_ way to do nesting:

```html-nolint example-bad
<p>My cat is <strong>very grumpy.</p></strong>
```

The **tags have to open and close in a way that they are inside or outside one another**. With the kind of overlap in the example above, the browser has to guess at your intent. This kind of guessing can result in unexpected results.

### Void elements

Not all elements follow the pattern of an opening tag, content, and a closing tag. Some elements consist of a single tag, which is typically used to insert/embed something in the document. Such elements are called {{glossary("void element", "void elements")}}. For example, the {{htmlelement("img")}} element embeds an image file onto a page:

```html
<img
  src="https://raw.githubusercontent.com/mdn/beginner-html-site/gh-pages/images/firefox-icon.png"
  alt="Firefox icon" />
```

This would output the following:

{{ EmbedLiveSample('Void_elements', 700, 300, "", "") }}

> [!NOTE]
> In HTML, there is no requirement to add a `/` at the end of a void element's tag, for example: `<img src="images/cat.jpg" alt="cat" />`. However, it is also a valid syntax, and you may do this when you want your HTML to be valid XML.

## Attributes

Elements can also have attributes. Attributes look like this:

![paragraph tag with 'class="editor-note"' attribute emphasized](grumpy-cat-attribute-small.png)

Attributes contain extra information about the element that won't appear in the content. In this example, the **`class`** attribute is an identifying name used to target the element with style information.

An attribute should have:

- A space between it and the element name. (For an element with more than one attribute, the attributes should be separated by spaces too.)
- The attribute name, followed by an equal sign.
- An attribute value, wrapped with opening and closing quote marks.

### Adding attributes to an element

Now it's your turn again. In this section we are going to get you to add attributes to an `<img>` element to get an image displaying on the page. The `<img>` element can take several attributes, including:

- `src`: A **required** attribute that specifies the location of the image. For example: `src="https://raw.githubusercontent.com/mdn/beginner-html-site/gh-pages/images/firefox-icon.png"`.
- `alt`: A text description of the image. For example: `alt="The Firefox icon"`.
- `width`: The width of the image in pixels. For example: `width="300"`.
- `height`: The height of the image in pixels. For example: `height="300"`.

Follow the steps below to complete the task:

1. Click **"Play"** in the code block below to edit the example in the MDN Playground.
2. Find your favorite image online, right click it, and press _Copy Image Link/Address_.
3. Back in the MDN Playground, add the `src` attribute to the `<img>` element and set its value to the link from Step 2.
4. Set the `alt` attribute to a suitable description of the image.
5. Set the `width` attribute to a value of say `300` so you can see the image a bit better inside the output panel. Adjust it if needed.

If you make a mistake, you can clear your work using the _Reset_ button in the MDN Playground. If you get really stuck, you can view the solution below the code block.

```html live-sample___basic_html_2
<img />
```

{{ EmbedLiveSample('basic_html_2', "100%", 60) }}

<details>
<summary>Click here to show the solution</summary>

Your finished HTML element should look like this:

```html
<img src="<URL-OF-IMAGE>" alt="A description of the image" width="300" />
```

</details>

### Boolean attributes

Sometimes you will see attributes written without values. This is entirely acceptable. These are called [Boolean attributes](/en-US/docs/Glossary/Boolean/HTML). When a boolean attribute is written without a value, or with any value, even like `"false"`, the boolean attribute is always set to true. Otherwise, if the attribute is not written in an HTML tag, the attribute is set to false. The spec requires the attribute's value to either be the empty string (including when the attribute has no value explicitly specified) or the same as the attribute's name, but other values work the same. For example, consider the [`disabled`](/en-US/docs/Web/HTML/Reference/Elements/input#disabled) attribute, which you can assign to form input elements. (You use this to _disable_ the form input elements so the user can't make entries. The disabled elements typically have a grayed-out appearance.) For example:

```html
<input type="text" disabled="disabled" />
```

As shorthand, it is acceptable to write this as follows:

```html
<!-- using the disabled attribute prevents the end user from entering text into the input box -->
<input type="text" disabled />

<!-- text input is allowed, as it doesn't contain the disabled attribute -->
<input type="text" />
```

For reference, the example above also includes a non-disabled form input element. The HTML from the example above produces this result:

{{ EmbedLiveSample('Boolean_attributes', 700, 100, "", "") }}

### Omitting quotes around attribute values

If you look at code for a lot of other sites, you might come across a number of strange markup styles, including attribute values without quotes. This is permitted in certain circumstances, but it can also break your markup in other circumstances. The element in the code snippet below, `<a>`, is called an anchor. Anchors enclose text and turn them into links. The `href` attribute specifies the web address the link points to. You can write this basic version below with _only_ the `href` attribute, like this:

```html
<a href=https://www.mozilla.org/>favorite website</a>
```

Anchors can also have a `title` attribute, a description of the linked page. However, as soon as we add the `title` in the same fashion as the `href` attribute there are problems:

```html-nolint example-bad
<a href=https://www.mozilla.org/ title=The Mozilla homepage>favorite website</a>
```

As written above, the browser misinterprets the markup, mistaking the `title` attribute for three attributes: a title attribute with the value `The`, and two Boolean attributes, `Mozilla` and `homepage`. Obviously, this is not intended! It will cause errors or unexpected behavior, as you can see in the live example below. Try hovering over the link to view the title text!

{{ EmbedLiveSample('Omitting_quotes_around_attribute_values', 700, 100, "", "") }}

Always include the attribute quotes. It avoids such problems, and results in more readable code.

### Single or double quotes?

In this article, you will also notice that the attributes are wrapped in double quotes. However, you might see single quotes in some HTML code. This is a matter of style. You can feel free to choose which one you prefer. Both of these lines are equivalent:

```html-nolint
<a href='https://www.example.com'>A link to my example.</a>

<a href="https://www.example.com">A link to my example.</a>
```

Make sure you don't mix single quotes and double quotes. This example (below) shows a kind of mixing of quotes that will go wrong:

```html-nolint example-bad
<a href="https://www.example.com'>A link to my example.</a>
```

However, if you use one type of quote, you can include the other type of quote _inside_ your attribute values:

```html
<a href="https://www.example.com" title="Isn't this fun?">
  A link to my example.
</a>
```

To use quote marks inside other quote marks of the same type (single quote or double quote), use {{glossary("character reference", "character references")}}.
For example, this will break:

```html-nolint example-bad
<a href="https://www.example.com" title="An "interesting" reference">A link to my example.</a>
```

Instead, you need to do this:

```html-nolint
<a href="https://www.example.com" title="An &quot;interesting&quot; reference">A link to my example.</a>
```

## Anatomy of an HTML document

Individual HTML elements aren't very useful on their own. Next, let's examine how individual elements combine to form an entire HTML page:

```html
<!doctype html>
<html lang="en-US">
  <head>
    <meta charset="utf-8" />
    <title>My test page</title>
  </head>
  <body>
    <p>This is my page</p>
  </body>
</html>
```

Here we have:

1. `<!doctype html>`: The doctype. When HTML was young (1991-1992), doctypes were meant to act as links to a set of rules that the HTML page had to follow to be considered good HTML. Doctypes used to look something like this:

   ```html
   <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
   ```

   More recently, the doctype is a historical artifact that needs to be included for everything else to work right. `<!doctype html>` is the shortest string of characters that counts as a valid doctype. That is all you need to know!

2. `<html></html>`: The {{htmlelement("html")}} element. This element wraps all the content on the page. It is sometimes known as the root element.
3. `<head></head>`: The {{htmlelement("head")}} element. This element acts as a container for everything you want to include on the HTML page, **that isn't the content** the page will show to viewers. This includes keywords and a page description that would appear in search results, CSS to style content, character set declarations, and more. You will learn more about this in the next article of the series.
4. `<meta charset="utf-8">`: The {{htmlelement("meta")}} element. This element represents metadata that cannot be represented by other HTML meta-related elements, like {{htmlelement("base")}}, {{htmlelement("link")}}, {{htmlelement("script")}}, {{htmlelement("style")}} or {{htmlelement("title")}}. The [`charset`](/en-US/docs/Web/HTML/Reference/Elements/meta#charset) attribute specifies the character encoding for your document as UTF-8, which includes most characters from the vast majority of human written languages. With this setting, the page can now handle any textual content it might contain. There is no reason not to set this, and it can help avoid some problems later.
5. `<title></title>`: The {{htmlelement("title")}} element. This sets the title of the page, which is the title that appears in the browser tab the page is loaded in. The page title is also used to describe the page when it is bookmarked.
6. `<body></body>`: The {{htmlelement("body")}} element. This contains _all_ the content that displays on the page, including text, images, videos, games, playable audio tracks, or whatever else.

### Adding some features to an HTML document

At this point, we want you to practice writing some slightly more substantial HTML content. To do this, you've got a couple of options — you can create the HTML on your local computer, or use the MDN Playground like in the previous examples.

- To do it on your local machine:
  1. Copy the HTML page example listed in the previous section and paste it into a new file in your code editor.
  2. Make the changes to the page outlined in the instructions below.
  3. Save the file as `index.html` then load it in a new browser tab to see the results.

  > [!NOTE]
  > You can also find this [basic HTML template](https://github.com/mdn/learning-area/blob/main/html/introduction-to-html/getting-started/index.html) on our GitHub repo. You can make a copy of this file instead of creating it yourself.

- To do it in the MDN Playground, click **"Play"** in the output panel below to edit the example, then follow the below instructions. If you make a mistake, you can clear your work using the _Reset_ button in the MDN Playground.

```html hidden live-sample___basic_html_3
<!doctype html>
<html lang="en-US">
  <head>
    <meta charset="utf-8" />
    <title>My test page</title>
  </head>
  <body>
    <p>This is my page</p>
  </body>
</html>
```

{{ EmbedLiveSample('basic_html_3', "100%", 60) }}

Here are the instructions to follow:

1. Just below the opening tag of the {{htmlelement("body")}} element, add a main title for the document. This should be wrapped inside an `<h1>` opening tag and `</h1>` closing tag.
2. Edit the paragraph content to include text about a topic that you find interesting.
3. Make important words stand out in bold by wrapping them inside a {{htmlelement("strong")}} element.
4. Add two links to your paragraph. This is achieved using the {{htmlelement("a")}} element.
5. Add an image to your document, as [explained earlier in the article](#adding_attributes_to_an_element). Place it below the paragraph. If it is too big to see, add a `width` attribute to it, to shrink it down.

If you get really stuck, you can view the solution here:

<details>
<summary>Click here to show the solution</summary>

The contents of your finished HTML element body should look something like this:

```html
<h1>Some music</h1>
<p>
  I really enjoy <strong>playing the drums</strong>. One of my favorite drummers
  is Neal Peart, who used to play in the band
  <a href="https://en.wikipedia.org/wiki/Rush_%28band%29">Rush</a>. My favorite
  Rush album is currently
  <a href="https://www.deezer.com/album/942295">Moving Pictures</a>.
</p>
<img
  src="https://www.cygnus-x1.net/links/rush/images/albums/sectors/sector2-movingpictures-cover-s.jpg"
  alt="Rush Moving Pictures album cover"
  width="300" />
```

</details>

### Whitespace in HTML

In the examples above, you may have noticed that a lot of whitespace is included in the code. This is optional. These two code snippets are equivalent:

```html-nolint
<p id="noWhitespace">Dogs are silly.</p>

<p id="whitespace">Dogs
    are
        silly.</p>
```

No matter how much whitespace you use inside HTML element content (which can include one or more space characters, but also line breaks), the HTML parser reduces each sequence of whitespace to a single space when rendering the code. So why use so much whitespace? The answer is readability.

It can be easier to understand what is going on in your code if you have it nicely formatted. In our HTML we've got each nested element indented by two spaces more than the one it is sitting inside. It is up to you to choose the style of formatting (how many spaces for each level of indentation, for example), but you should consider formatting it.

Let's have a look at how the browser renders the two paragraphs above with and without whitespace:

{{ EmbedLiveSample('Whitespace_in_HTML', 700, 100) }}

> [!NOTE]
> Accessing the [innerHTML](/en-US/docs/Web/API/Element/innerHTML) of elements from JavaScript will keep all the whitespace intact.
> This may return unexpected results if the whitespace is trimmed by the browser.

```js
const noWhitespace = document.getElementById("noWhitespace").innerHTML;
console.log(noWhitespace);
// "Dogs are silly."

const whitespace = document.getElementById("whitespace").innerHTML;
console.log(whitespace);
// "Dogs
//    are
//        silly."
```

## Character references: including special characters in HTML

In HTML, the characters `<`, `>`, `"`, `'`, and `&` are special characters. They are parts of the HTML syntax itself. So how do you include one of these special characters in your text? For example, if you want to use an ampersand or less-than sign, and not have it interpreted as code.

You do this with {{glossary("character reference", "character references")}}. These are special codes that represent characters, to be used in these exact circumstances. Each character reference starts with an ampersand (&), and ends with a semicolon (;).

| Literal character | Character reference equivalent |
| ----------------- | ------------------------------ |
| <                 | `&lt;`                         |
| >                 | `&gt;`                         |
| "                 | `&quot;`                       |
| '                 | `&apos;`                       |
| &                 | `&amp;`                        |

The character reference equivalent could be easily remembered because the text it uses can be seen as less than for `&lt;`, quotation for `&quot;` and similarly for others. To find more about entity references, see [List of XML and HTML character entity references](https://en.wikipedia.org/wiki/List_of_XML_and_HTML_character_entity_references) (Wikipedia).

In the example below, there are two paragraphs:

```html-nolint
<p>In HTML, you define a paragraph using the <p> element.</p>

<p>In HTML, you define a paragraph using the &lt;p&gt; element.</p>
```

In the live output below, you can see that the first paragraph has gone wrong. The browser interprets the second instance of `<p>` as starting a new paragraph. The second paragraph looks fine because it has angle brackets with character references.

{{ EmbedLiveSample('Entity_references_Including_special_characters_in_HTML', 700, 200, "", "") }}

> [!NOTE]
> You don't need to use entity references for any other symbols, as modern browsers will handle the actual symbols just fine as long as your HTML's [character encoding is set to UTF-8](/en-US/docs/Learn_web_development/Core/Structuring_content/Webpage_metadata#specifying_your_documents_character_encoding).

## HTML comments

HTML has a mechanism to write comments in the code. Browsers ignore comments, effectively making comments invisible to the user. The purpose of comments is to allow you to include notes in the code to explain your logic or coding. This is very useful if you return to a code base after being away for long enough that you don't completely remember it. Likewise, comments are invaluable as different people are making changes and updates.

To write an HTML comment, wrap it in the special markers `<!--` and `-->`. For example:

```html
<p>I'm not inside a comment</p>

<!-- <p>I am!</p> -->
```

As you can see below, only the first paragraph is displayed in the live output.

{{ EmbedLiveSample('HTML_comments', 700, 100, "", "") }}

## Summary

You made it to the end of the article! We hope you enjoyed your tour of the basics of HTML.

At this point, you should understand what HTML looks like, and how it works at a basic level. You should also be able to write a few elements and attributes. The subsequent articles of this module go further on some of the topics introduced here, as well as presenting other concepts of the language.

- As you start to learn more about HTML, consider learning the basics of CSS (Cascading Style Sheets). [CSS](/en-US/docs/Learn_web_development/Core/Styling_basics) is the language used to style web pages, such as changing fonts or colors or altering the page layout. HTML and CSS work well together, as you will soon discover.

## See also

- [Applying color to HTML elements using CSS](/en-US/docs/Web/CSS/CSS_colors/Applying_color)

{{NextMenu("Learn_web_development/Core/Structuring_content/Webpage_metadata", "Learn_web_development/Core/Structuring_content")}}
