---
title: Using the :target pseudo-class in selectors
short-title: Using :target
slug: Web/CSS/CSS_selectors/Using_the_:target_pseudo-class_in_selectors
page-type: guide
sidebar: cssref
---

When a URL points at a specific piece of a document using a [URL fragment identifier](/en-US/docs/Web/URI/Reference/Fragment#fragment), it can be difficult for the user to notice. This guide discusses using CSS to draw attention to the target of a URL to improve user experience.

## Picking a Target

The [pseudo-class](/en-US/docs/Web/CSS/Pseudo-classes) {{cssxref(":target")}} is used to style the target element of the document identified using the URL fragment identifier. For example, the URL `https://developer.mozilla.org/en-US/docs/Web/CSS#reference` contains the fragment identifier `#reference`. In HTML, identifiers are found as the values of either `id` or `name` attributes, since the two share the same namespace. Thus, the example URL would point to the element that has the id `reference` in that document.

To style any `h2` element that is the target of a URL, while not effecting any other kind of element to get a target style, use the `:target` pseudo-class with the [type selector](/en-US/docs/Web/CSS/Type_selectors):

```css
h2:target {
  outline: 2px solid;
}
```

It's also possible to create styles that are specific to a particular fragment of the document. This is done using the same identifying value that is found in the URI. Thus, to add a background color to the `#reference` fragment, we would write:

```css
#reference:target {
  background-color: yellow;
}
```

## Targeting all elements

If the intent is to create a "blanket" style that will apply to all targeted elements, then the universal selector comes in handy:

```css
:target {
  color: red;
}
```

## Example

In the following example, there are five links that point to elements in the same document. Selecting the "First" link, for example, will cause `<h1 id="one">` to become the target element. Note that the document may jump to a new scroll position, since target elements are placed on the top of the browser window if possible.

```html
<h4 id="one">…</h4>
<p id="two">…</p>
<div id="three">…</div>
<a id="four">…</a> <em id="five">…</em>

<a href="#one">First</a>
<a href="#two">Second</a>
<a href="#three">Third</a>
<a href="#four">Fourth</a>
<a href="#five">Fifth</a>
```

## Conclusion

In cases where a fragment identifier points to a portion of the document, readers may become confused about which part of the document they're supposed to be reading. By styling the target of a URI, reader confusion can be reduced or eliminated.

## See also

- {{cssxref(":target")}}
