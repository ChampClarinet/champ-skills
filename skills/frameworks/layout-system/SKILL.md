---
name: layout-system
description: Champ's Grid/Flex-first web layout, spacing hierarchy, responsive-width, container-aware, and intentional positioning policy. Use when creating or modifying page/component layout, responsive behavior, or reference-UI spacing.
---

# Layout System

Build layout from explicit structural relationships, not accumulated spacing corrections.

Repository-local explicit layout conventions override these personal defaults.

## Hard invariants

- Use CSS Grid or Flexbox as the primary mechanism for page, section, and component layout.
- Use `gap` for repeated spacing between children inside Grid or Flex containers.
- Parent containers should own the flow, alignment, distribution, and repeated spacing of their children.
- Do not simulate ordinary structural layout with accumulated margins, positional offsets, transforms, or arbitrary spacing when Grid or Flexbox can express the relationship directly.
- Use padding for internal inset. Use margin for genuine local or external separation, not to compensate for an incorrect parent layout.
- Intentional overlapping or anchored elements may use positioned layout. Absolute positioning is not a substitute for ordinary sibling flow.
- Horizontal scrolling is acceptable only for intentionally scrollable regions such as tables, code, timelines, or carousels. It is not a fallback for broken ordinary page layout.

## Spacing hierarchy

Spacing communicates containment and grouping.

For nested structures, normally preserve:

`page > section > group/card > inline`

Higher-level separation should normally be larger than spacing among tightly related descendants.

Do not copy one gap token indiscriminately across every nesting level. A nested gap larger than its surrounding structural separation requires an explicit design reason.

Responsive compression should preserve this hierarchy rather than flatten every level to the same spacing.

If a layout accumulates many one-off spacing corrections, re-evaluate the layout model before adding another correction.

## Positioning

Do not use relative/absolute positioning, transforms, negative margins, or positional offsets to compensate for ordinary document-flow layout that should be expressed with Grid or Flexbox.

Absolute positioning is appropriate when elements intentionally overlap or are anchored within a positioned container.

Typical valid uses include overlays, badges, floating controls, decorative layers, and controls intentionally placed over another element.

The positioned parent owns the coordinate system. Do not use absolute positioning to reconstruct ordinary sibling flow or compensate for incorrect spacing or alignment.

## Responsive width policy

Unless the product explicitly defines another minimum:

- `320px` is the minimum width for full layout quality.
- `280px–319px` requires graceful degradation.
- below `280px`, preserve access where practical without a default full-quality guarantee.

Do not set a global `min-width: 320px` merely to hide overflow.

Recommended verification widths:

```text
280px   graceful-degradation smoke check
320px   minimum fully supported phone width
360px   common narrow Android width
375px   common phone width
390px   common modern phone width
768px   tablet / compact layout transition
1024px  compact desktop / tablet landscape
1280px  standard desktop
1440px  wide desktop
```

Also inspect intermediate widths between these checkpoints. Passing only the listed snapshots is not sufficient.

Graceful degradation means content remains reachable, controls usable, and text free from destructive overlap or clipping. Exact composition and spacing parity are not required below the full-quality minimum.

When space becomes constrained, reduce outer and high-level spacing before compressing tightly related controls or text. Preserve the spacing hierarchy while compressing.

Allow Grid and Flex items to wrap, stack, shrink, or change column count according to available space.

Long text, localization, browser text zoom, increased system text size, and dynamic content must not create destructive overlap or inaccessible content.

## Container-aware components

Viewport width and component width are not interchangeable.

When a reusable component can become narrow independently of the viewport—such as inside a sidebar, dashboard column, dialog, drawer, split pane, or nested card—base component-level responsive decisions on its available container width when appropriate.

Prefer container queries when the layout decision belongs to the component's containing region rather than the page viewport.

Establish the container boundary at the meaningful feature or module owner instead of scattering container declarations through descendants.

Do not rely only on viewport breakpoints when a component can become narrow while the viewport remains wide.

Do not add container-query complexity when the layout genuinely depends only on page-level viewport composition.

Verify reusable components at relevant parent widths independently of viewport width.

## Arbitrary spacing and offsets

Prefer the project's standard spacing tokens.

An arbitrary value is acceptable when it represents a concrete design requirement that the project's spacing or layout system cannot express cleanly.

It is not acceptable when it compensates for a broken layout model.

When arbitrary spacing values begin accumulating, trace the underlying structural relationship before adding more.

## Reference UI work

When reproducing a reference UI, treat visible spacing as evidence of an underlying layout model.

Infer rows, columns, alignment groups, container boundaries, repeated gaps, and spacing hierarchy before tuning individual values.

Establish Grid/Flex structure first, then tune the smallest necessary local values.

Do not chase screenshot fidelity by accumulating margins, transforms, positional offsets, or arbitrary spacing corrections.

Infer responsive behavior beyond the captured reference width instead of treating the screenshot as a fixed canvas.

## Cross-browser safety

For affected layout behavior, verify compatibility with Chromium, Firefox, desktop Safari, and iOS Safari when practical.

Avoid layout assumptions that depend unnecessarily on unstable font metrics, intrinsic-content quirks, viewport-unit behavior, browser rounding, or browser-specific layout behavior.

## Verification

For touched in-scope layout, verify:

- Grid or Flex owns structural layout where applicable
- the parent owns repeated child spacing and alignment
- spacing preserves meaningful hierarchy
- arbitrary spacing and offsets are requirements rather than structural compensation
- positioned layout is used for intentional overlap or anchoring rather than ordinary sibling flow
- full layout quality holds at `320px` unless the product defines another minimum
- `280px–319px` remains usable without destructive clipping or overlap
- intermediate widths do not reveal broken transitions
- reusable components account for container width when it can differ materially from viewport width
- long or dynamic text and text zoom do not break accessibility or layout
- ordinary page content has no unintended horizontal overflow
- affected browser-specific layout behavior is checked where relevant

A discovered in-scope structural layout defect is required correction before completion. Do not expand scope into unrelated untouched layout solely to enforce this policy.
