---
title: CSS colors
slug: Web/CSS/CSS_colors
page-type: css-module
spec-urls:
  - https://drafts.csswg.org/css-color/
  - https://drafts.csswg.org/css-color-5/
sidebar: cssref
---

The **CSS colors** module defines colors, color types, color blending, opacity, and how you can apply these colors and effects to HTML content.

While this module has only two CSS properties, {{cssxref("color")}} and {{cssxref("opacity")}}, over 20 CSS and SVG properties, CSS images, at-rules, and @media rules depend on these two properties.

### Colors in action

The color syntax converter below shows the values of the currently selected color in [red-green-blue](/en-US/docs/Web/CSS/color_value/rgb) (RGB), [hexadecimal](/en-US/docs/Web/CSS/hex-color) (HEX), [hue, saturation, and lightness](/en-US/docs/Web/CSS/color_value/hsl) (HSL), and [hue, whiteness, and blackness](/en-US/docs/Web/CSS/color_value/hwb) (HWB) CSS color formats. All the RGB, HEX, HSL, and HWB color values here, while written differently, represent the same color value.

{{EmbedGHLiveSample("css-examples/modules/colors.html", '100%', 450)}}

Selecting a color via the [color picker](/en-US/docs/Web/HTML/Reference/Elements/input/color) and an opacity via the [slider](/en-US/docs/Web/HTML/Reference/Elements/input/range) updates the RGB, HEX, HSL, and HWB values. When you choose a new color or opacity value, the color of the background and the slider update via the CSS properties {{cssxref("background-color")}} and {{cssxref("accent-color")}}, respectively.

To see the code for this color syntax converter, [view the source on GitHub](https://github.com/mdn/css-examples/blob/main/modules/colors.html).

## Reference

### Properties

- {{cssxref("color")}}
- {{cssxref("opacity")}}

### At-rules and descriptors

> [!NOTE]
> The CSS color module introduces the {{cssxref("@color-profile")}} at-rule, along with its `components`, `rendering-intent` and `src` descriptors. These features have not yet been implemented in any browser.

### Functions

- Color functions:
  - [`rgb()`](/en-US/docs/Web/CSS/color_value/rgb)
  - [`hsl()`](/en-US/docs/Web/CSS/color_value/hsl)
  - [`hwb()`](/en-US/docs/Web/CSS/color_value/hwb)
  - [`lab()`](/en-US/docs/Web/CSS/color_value/lab)
  - [`lch()`](/en-US/docs/Web/CSS/color_value/lch)
  - [`oklab()`](/en-US/docs/Web/CSS/color_value/oklab)
  - [`oklch()`](/en-US/docs/Web/CSS/color_value/oklch)
  - [`color()`](/en-US/docs/Web/CSS/color_value/color)
- [`color-mix()`](/en-US/docs/Web/CSS/color_value/color-mix)
- [`contrast-color()`](/en-US/docs/Web/CSS/color_value/contrast-color)
- {{CSSXref("color_value/light-dark", "light-dark()")}}

> [!NOTE]
> The CSS color module introduces the {{CSSXref("color_value/device-cmyk", "device-cmyk()")}} and `contrast-color()` functions, which have not yet been implemented in any browser.

### Data types

- {{cssxref("&lt;color&gt;")}}
- [`<color-function>`](#functions)
- {{cssxref("hex-color")}}
- {{cssxref("named-color")}}
- {{cssxref("alpha-value")}}
- {{cssxref("hue")}}
- {{cssxref("system-color")}}
- [`<colorspace-params>`](/en-US/docs/Web/CSS/color_value/color#using_predefined_color_spaces_with_color)

### Glossary terms and keywords

- {{glossary("color space")}}
- [`currentcolor`](/en-US/docs/Web/CSS/color_value#currentcolor_keyword)
- {{glossary("interpolation")}}
- {{glossary("RGB")}}
- [`transparent`](/en-US/docs/Web/CSS/named-color#transparent)

### Interfaces

> [!NOTE]
> The CSS color module introduces the `CSSColorProfileRule` interface, which has not been implemented in any browser.

## Guides

- [Applying color to HTML elements using CSS](/en-US/docs/Web/CSS/CSS_colors/Applying_color)
  - : A guide to using CSS to apply color to a variety of types of content, including all CSS properties that accept `<color>` as a value.
- [CSS color values](/en-US/docs/Web/CSS/CSS_colors/Color_values)
  - : An overview of color spaces and the different `<color>` functional notations available in CSS.
- [Using color wisely](/en-US/docs/Web/CSS/CSS_colors/Using_color_wisely)
  - : Color theory and resources, including finding the right colors to create an accessible color palette, contrast, and printing in color.
- [Using relative colors](/en-US/docs/Web/CSS/CSS_colors/Relative_colors)
  - : This article explains relative CSS color syntax, shows what the different options are, and looks at some illustrative examples.
- [Color picker tool](/en-US/docs/Web/CSS/CSS_colors/Color_picker_tool)
  - : A tool that lets you pick a color in the sRGB color space and converts it between various CSS color formats, helping you understand the syntax of the different color notations.
- [Understanding color and luminance](/en-US/docs/Web/Accessibility/Guides/Colors_and_Luminance)
  - : Color perception and using colors with color insensitive (color blind) users, reduced vision users and users with vestibular disorders or other neurological disorders in mind.
- [WCAG 1.4.1: Color contrast](/en-US/docs/Web/Accessibility/Guides/Understanding_WCAG/Perceivable/Color_contrast)
  - : Explanation of contrast requirements between background and foreground content to ensure legibility.

## Related concepts

- CSS properties that are part of other specifications:
  - {{cssxref("accent-color")}}
  - {{cssxref("background-color")}}
  - {{cssxref("background-image")}}
  - {{cssxref("border-color")}}
  - {{cssxref("box-shadow")}}
  - {{cssxref("caret-color")}}
  - {{cssxref("color")}}
  - {{cssxref("color-scheme")}}
  - {{cssxref("column-rule-color")}}
  - {{cssxref("outline-color")}}
  - {{cssxref("scrollbar-color")}}
  - {{cssxref("text-decoration-color")}}
  - {{cssxref("text-emphasis-color")}}
  - {{cssxref("text-shadow")}}
  - {{cssxref("-webkit-tap-highlight-color")}}
- SVG color properties that are part of other specifications:
  - [`fill`](/en-US/docs/Web/SVG/Reference/Attribute/fill)
  - [`flood-color`](/en-US/docs/Web/SVG/Reference/Attribute/flood-color)
  - [`lighting-color`](/en-US/docs/Web/SVG/Reference/Attribute/lighting-color)
  - [`stop-color`](/en-US/docs/Web/SVG/Reference/Attribute/stop-color)
  - [`stroke`](/en-US/docs/Web/SVG/Reference/Attribute/stroke)
- SVG [`color`](/en-US/docs/Web/SVG/Reference/Attribute/color) attribute
- {{glossary("Color wheel")}} glossary term
- {{glossary("Interpolation")}} glossary term
- The [`@font-palette-values`](/en-US/docs/Web/CSS/@font-palette-values) at-rule [`override-colors`](/en-US/docs/Web/CSS/@font-palette-values/override-colors) descriptor
- The [`@color-profile`](/en-US/docs/Web/CSS/@color-profile) at-rule
- The [`color-gamut`](/en-US/docs/Web/CSS/@media/color-gamut) @media feature
- The [`forced-colors`](/en-US/docs/Web/CSS/@media/forced-colors) @media feature

## Specifications

{{Specifications}}

## See also

- [CSS color adjustment](/en-US/docs/Web/CSS/CSS_color_adjustment) module and the {{cssxref("print-color-adjust")}} property.
- [CSS images](/en-US/docs/Web/CSS/CSS_images) module, which is where CSS [`<gradient>`](/en-US/docs/Web/CSS/gradient) images are defined.
- The [`VideoColorSpace`](/en-US/docs/Web/API/VideoColorSpace) interface
- The SVG [`<feColorMatrix>`](/en-US/docs/Web/SVG/Reference/Element/feColorMatrix) element
- [Canvas API: applying styles and colors](/en-US/docs/Web/API/Canvas_API/Tutorial/Applying_styles_and_colors#colors)
