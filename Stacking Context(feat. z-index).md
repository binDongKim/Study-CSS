# Stacking Context

- The **stacking context** is a three dimensional conceptualization of HTML elements along an imaginary z-axis relative to the user.
- A **stacking context** is formed by any element in the following scenarios:
  - Root element of document(HTML).
  - Element with a `position` value either "absolute" or "relative" and `z-index` value other than "auto".
  - Element with a `position` value "fixed" or "sitcky".
  - Element that is a child of a `flex` container, with `z-index` value other than "auto".
  - Element with a `opacity` value less than 1.
  - ~~Element with a `mix-blend-mode` value other than "normal".~~
  - Element with any of the following properties with value other than "none":
    - transform
    - filter
    - perspective
    - clip-path
    - mask / mask-image / mask-border
  - Element with a `isolation` value "isolate".
  - Element with a `-webkit-overflow-scrolling` value "touch".
  - Element with a `will-change` value specifying any property that would create a stacking context on non initial value.
- Elements that do not create their own stacking contexts are assimilated by the parent stacking context.
- Every stacking context has a single HTML element as its root element.
- When a new stacking context is formed on an element, that stacking context confined all of its child elements to a particular place in the stacking order, which means if an element is contained in a stacking context at the bottom of the stacking order, there is no way to get it to appear in front of another element in a different stacking context that is higher in the stacking order.





Example: 

<img src="https://developer.mozilla.org/@api/deki/files/913/=Understanding_zindex_04.png">

DOM structure: 

- Root
  - DIV #1
  - DIV #2
  - DIV #3
    - DIV #4
    - DIV #5
    - DIV #6
- It's important to note that DIV #4, DIV #5 and DIV #6 are children of DIV #3, so stacking of those elements is completely resolved within DIV #3.
- DIV #4 is rendered under DIV #1 because DIV #1's z-index(5) is valid within the stacking context of the root element, while DIV #4's z-index(6) is valid within the stacking context of DIV #3.
- DIV #3's z-index is 4, but this value is independent from z-index of DIV #4, DIV #5 and DIV #6 because it belongs to a different stacking context.



## Stacking without the z-index property

- When the `z-index` property is not specified on any element, elements are stacked in the following order(from bottom to top):
  - Root
  - Non-positioned blocks
  - Positioned elements



## Stacking with floated blocks

- Stacking order:
  - Root
  - Non-positioned blocks
  - **Floating blocks**
  - Non-positioned inline elements
  - Positioned elements



## Using z-index

- The `z-index` property can be specified with an integer value(positive, zero, or negative), which represents the position of the element along the z-axis. 
- When no `z-index` property is specified, elements are rendered on the default rendering layer 0.
- If several elements share the same `z-index` value(i.e., they are placed on the same layer), [stacking rules](#stacking-without-the-z-index-property) apply.
- `z-index` works ONLY on the *positioned* elements.



## Stacking Order Within the Same Stacking Context

From back to front:

- The stacking context's root element
- Positioned elements with negative z-index
- Non-positioned elements
- Positioned elements with a z-index value of `auto`(default)
- Positioned elements with positive z-index values



## References

- [The Stacking Context](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Positioning/Understanding_z_index/The_stacking_context)
- [What No One Told You About Z-Index](https://philipwalton.com/articles/what-no-one-told-you-about-z-index/)