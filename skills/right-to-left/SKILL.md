---
name: right-to-left
description: Instructions for how to make interactivity and Tailwind styling work with right-to-left (rtl) languages.
---

## Styling

If not already present, add the following to the Tailwind config CSS file:

```css
@custom-variant rtl (&:dir(rtl));
```

The Tailwind `@custom-variant` called `rtl` can be used to apply styles when the page is in rtl mode. Usage looks like `rtl:<class-name>`. This is used to mirror styles for CSS properties that don't natively support direction changes, such as `translateX`.

Logical inset utilities (ex. `inset-s-<value>`) require Tailwind v4.2.0 or higher.

The following table shows a mapping of Tailwind classes that have been converted to support rtl languages. 

| Old class name                   | Converted class name                           | Notes                                                     |
| -------------------------------- | ---------------------------------------------- | --------------------------------------------------------- |
| `left-<value>`                   | `inset-s-<value>`                              | Positions from the start edge (left in LTR, right in RTL) |
| `right-<value>`                  | `inset-e-<value>`                              | Positions from the end edge (right in LTR, left in RTL)   |
| `ml-<value>`                     | `ms-<value>`                                   | Margin on start side                                      |
| `mr-<value>`                     | `me-<value>`                                   | Margin on end side                                        |
| `pl-<value>`                     | `ps-<value>`                                   | Padding on start side                                     |
| `pr-<value>`                     | `pe-<value>`                                   | Padding on end side                                       |
| `rounded-r-<value>`              | `rounded-e-<value>`                            | Rounded corner on end side                                |
| `rounded-l-<value>`              | `rounded-s-<value>`                            | Rounded corner on start side                              |
| `border-l-<value>`               | `border-s-<value>`                             | Border on start side                                      |
| `border-r-<value>`               | `border-e-<value>`                             | Border on end side                                        |
| `origin-left`                    | `origin-left rtl:origin-right`                 | Transform origin at start                                 |
| `translate-x-<value>` (with `-`) | `translate-x-<value> rtl:-translate-x-<value>` | Invert translateX for RTL using rtl: modifier             |
| `bg-linear-to-tr`                | `bg-linear-to-tr rtl:bg-linear-to-tl`          | Mirror any gradients for RTL                              |

## Directionality

Any navigational arrows on the page such as forward/back buttons or carousel controls should be flipped for rtl languages. This should happen automatically if grid/flexbox are being used to layout the buttons. The arrow icons need to be mirrored too, consider using `rtl:rotate-180` to fix the visual direction of the arrow.

## Interactivity

- Any arrow key handlers that use `ArrowLeft` or `ArrowRight` should use `isForwardArrow` and `isBackwardArrow` utility functions to invert the behavior for rtl languages.
- Horizontal carousels should flip the direction of their x-axis animations for rtl languages.
- Horizontal animations like underline hover effects or infinitely scrolling marquees should flip their direction for rtl languages.
