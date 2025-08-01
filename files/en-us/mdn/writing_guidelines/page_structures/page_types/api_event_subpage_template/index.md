---
title: API event subpage template
slug: MDN/Writing_guidelines/Page_structures/Page_types/API_event_subpage_template
page-type: mdn-writing-guide
sidebar: mdnsidebar
---

> [!NOTE]
> _Remove this whole explanatory note before publishing._
>
> ---
>
> **Page front matter:**
>
> The front matter at the top of the page is used to define "page metadata".
> The values should be updated appropriately for the particular event.
>
> ```md
> ---
> title: "NameOfTheParentInterface: NameOfTheEvent event"
> slug: Web/API/NameOfTheParentInterface/NameOfTheEvent_event
> page-type: web-api-event
> status:
>   - deprecated
>   - experimental
>   - non-standard
> browser-compat: path.to.feature.NameOfTheEvent_event
> ---
> ```
>
> - **title**
>   - : Title heading displayed at the top of the page.
>     Format as "_NameOfTheParentInterface_**:** _NameOfTheEvent_ **event**".
>     For example, the [animationcancel](/en-US/docs/Web/API/Element/animationcancel_event) event of the [Window](/en-US/docs/Web/API/Window) interface has a _title_ of `Window: animationcancel event`.
> - **slug**
>   - : The end of the URL path after `https://developer.mozilla.org/en-US/docs/`.
>     This will be formatted like `Web/API/NameOfTheParentInterface/NameOfTheEvent_event`.
> - **page-type**
>   - : The `page-type` key for Web/API events is always `web-api-event`.
> - **status**
>   - : Flags describing the status of this feature. An array which may contain one or more of the following: `experimental`, `deprecated`, `non-standard`. This key should not be set manually: it is set automatically based on values in the browser compatibility data for the feature. See [How feature statuses are added or updated](/en-US/docs/MDN/Writing_guidelines/Page_structures/Feature_status#how_feature_statuses_are_added_or_updated).
> - **browser-compat**
>   - : Replace the placeholder value `path.to.feature.NameOfTheEvent_event` with the query string for the event in the [Browser compat data repo](https://github.com/mdn/browser-compat-data).
>     The toolchain automatically uses the key to populate the compatibility and specification sections (replacing the `\{{Compat}}` and `\{{Specifications}}` macros).
>
>     Note that you may first need to create/update an entry for the event in our [Browser compat data repo](https://github.com/mdn/browser-compat-data), and this entry will need to include specification information.
>     See our [guide on how to do this](/en-US/docs/MDN/Writing_guidelines/Page_structures/Compatibility_tables).
>
> ---
>
> **Top-of-page macros**
>
> A number of macro calls appear at the top of the content section (immediately below the page frontmatter).
>
> These macros are automatically added by the toolchain (there is no need to add/remove):
>
> - `\{{SeeCompatTable}}` — this generates a **This is an experimental technology** banner that indicates the technology is [experimental](/en-US/docs/MDN/Writing_guidelines/Experimental_deprecated_obsolete#experimental).
>   If it is experimental, and the technology is hidden behind a pref in Firefox, you should also fill in an entry for it in the [Experimental features in Firefox](/en-US/docs/Mozilla/Firefox/Experimental_features) page.
> - `\{{Deprecated_Header}}` — this generates a **Deprecated** banner that indicates that use of the technology is [discouraged](/en-US/docs/MDN/Writing_guidelines/Experimental_deprecated_obsolete#deprecated).
> - `\{{Non-standard_Header}}` — this generates a **Non-standard** banner that indicates that the feature is not part of any specification.
>
> You should update or delete the following macros according to the advice below:
>
> - `\{{SecureContext_Header}}` — this generates a **Secure context** banner that indicates the technology is only available in a [secure context](/en-US/docs/Web/Security/Secure_Contexts).
>   If it isn't, then you can remove the macro call.
>   If it is, then you should also fill in an entry for it in the [Features restricted to secure contexts](/en-US/docs/Web/Security/Secure_Contexts/features_restricted_to_secure_contexts) page.
> - `\{{AvailableInWorkers}}` — this generates a **Available In Workers** note that indicates that the technology is available in [worker context](/en-US/docs/Web/API/Web_Workers_API).
>   If it is only available in window context, then you can remove the macro call.
>   If it is also available or only available in worker context, then you may also need to passing an parameter to it due to its availability (see [\\{{AvailableInWorkers}} macros source code](https://github.com/mdn/rari/blob/main/crates/rari-doc/src/templ/templs/banners.rs) for all available values), you may also need to fill in an entry for it in the [Web APIs available in workers](/en-US/docs/Web/API/Web_Workers_API/Functions_and_classes_available_to_workers#web_apis_available_in_workers) page.
> - `\{{APIRef("GroupDataName")}}` — this generates the left-hand reference sidebar showing quick reference links related to the current page.
>   For example, every page in the [WebVR API](/en-US/docs/Web/API/WebVR_API) has the same sidebar, which points to the other pages in the API.
>   To generate the correct sidebar for your API, you need to add a `GroupData` entry to our GitHub repo, and include the entry's name inside the macro call in place of _GroupDataName_.
>   See our [API reference sidebars](/en-US/docs/MDN/Writing_guidelines/Howto/Write_an_api_reference/Sidebars) guide for information on how to do this.
>
> Do not provide status header macros manually. Refer to the section ["How feature statuses are added or updated"](/en-US/docs/MDN/Writing_guidelines/Page_structures/Feature_status#how_feature_statuses_are_added_or_updated) to add these statuses to the page.
>
> Samples of the **Secure context**, **Available in workers**, **Experimental**, **Deprecated**, and **Non-standard** banners are shown right after this note block.
>
> ---
>
> **Parent object link**
>
> Add a link to this new page from its parent object's _Events_ section.
> For example, [Element: wheel event](/en-US/docs/Web/API/Element/wheel_event) is linked from [`Element` Events](/en-US/docs/Web/API/Element#events).
>
> If the parent object does not have an _Events_ section, then add one.
> If this is a new "class" of event, then you should add a link to this section of the parent from the [DOM events](/en-US/docs/Web/API/Document_Object_Model/Events#event_index) guide.
>
> _Remember to remove this whole explanatory note before publishing._

{{SecureContext_Header}}{{AvailableInWorkers}}{{SeeCompatTable}}{{Deprecated_Header}}{{Non-standard_Header}}

Begin the content on the page with an introductory paragraph — start by naming the event, saying what interface it is part of, and saying what it does.
This should ideally be one or two short sentences.
You could copy most of this from the property's summary on the corresponding API reference page.

## Syntax

Use the event name in methods like {{domxref("EventTarget.addEventListener", "addEventListener()")}}, or set an event handler property.

```js-nolint
addEventListener("NameOfTheEvent", (event) => { })

onNameOfTheEvent = (event) => { }
```

## Event type

If the event has a special type, mention it along with its inheritance. If not, indicate that it is a generic event:

_A generic {{domxref("Event")}}._

Or, for example:

_An {{domxref("XRSessionEvent")}}. Inherits from {{domxref("Event")}}._

{{InheritanceDiagram("XRSessionEvent")}}

## Event properties

If the event is not just a generic {{domxref("Event")}}, list the additional properties the event has.

_In addition to the properties listed below, properties from the parent interface, {{domxref("Event")}}, are available._

- {{domxref("XRSessionEvent.session", "session")}} {{ReadOnlyInline}}
  - : The {{domxref("XRSession")}} to which the event refers.

## Description

If you want to provide additional text (too long for the summary), add a Description section.
It may contain the headings

### Trigger

and

### Use cases

which can provide more information.

## Examples

Note that we use the plural "Examples" even if the page only contains one example.

### A descriptive heading

Each example must have an H3 heading (`###`) naming the example. The heading should be descriptive of what the example is doing. For example, "A simple example" does not say anything about the example and therefore, not a good heading. The heading should be concise. For a longer description, use the paragraph after the heading.

See our guide on how to add [code examples](/en-US/docs/MDN/Writing_guidelines/Page_structures/Code_examples) for more information.

> [!NOTE]
> Sometimes you will want to link to examples given on another page.
>
> **Scenario 1:** If you have some examples on this page and some more examples on another page:
>
> Include an H3 heading (`###`) for each example on this page and then a final H3 heading (`###`) with the text "More examples", under which you can link to the examples on other pages. For example:
>
> ```md
> ## Examples
>
> ### Using the fetch API
>
> Example of Fetch
>
> ### More examples
>
> Links to more examples on other pages
> ```
>
> **Scenario 2:** If you _only_ have examples on another page and none on this page:
>
> Don't add any H3 headings; just add the links directly under the H2 heading "Examples". For example:
>
> ```md
> ## Examples
>
> For examples of this API, see [the page on fetch()](https://example.org/).
> ```

## Specifications

`\{{Specifications}}`

_To use this macro, remove the backticks and backslash in the markdown file._

## Browser compatibility

`\{{Compat}}`

_To use this macro, remove the backticks and backslash in the markdown file._

## See also

Include links to reference pages and guides related to the current API. For more guidelines, see the [See also section](/en-US/docs/MDN/Writing_guidelines/Writing_style_guide#see_also_section) in the _Writing style guide_.

- link1
- link2
- external_link (year)
