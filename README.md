# EImpact CSS Utilities

A CSS utility and integration stylesheet for maintaining consistent spacing, responsive sizing, shadows, icons, buttons, and cards across EImpact sites.

The file contains two kinds of styles:

- Reusable design tokens, fluid sizing, and utility classes.
- Opinionated integrations for Blocksy, Kadence Blocks, Swiper, and Strong Testimonials.

## Usage

Load `utilities.css` after the relevant theme and plugin styles so its integration rules can override their defaults.

```php
add_action( 'wp_enqueue_scripts', function () {
	wp_enqueue_style( 'parent-style', get_template_directory_uri() . '/style.css' );
	wp_enqueue_style( 'child-style', get_stylesheet_directory_uri() . '/style.css', ['parent-style', 'utilities-style'] );
	wp_enqueue_style( 'utilities-style', 'https://cdn.jsdelivr.net/gh/joseph-eimpact/eimpact-css-utilities@v1.0.9/utilities.css', [] );
});
```

The stylesheet uses cascade layers for its configuration, tokens, utilities, and fluid calculator. Integration rules outside those layers participate in the normal author cascade.

## Configuration

Override configuration properties after loading `utilities.css`. Site-wide values usually belong on `:root`:

```css
:root {
    --config-fluid-screen-width-min: 768px;
    --config-fluid-screen-width-max: 1440px;
    --config-button-icon-size: 20px;
    --config-button-gap: 8px;
}
```

### Fluid sizing

| Property | Default | Purpose |
| --- | --- | --- |
| `--config-fluid-screen-width-min` | `1000px` | Viewport width where fluid scaling starts. |
| `--config-fluid-screen-width-max` | Blocksy's normal container width plus `60px`, or `1500px` | Viewport width where fluid scaling ends. |

### Menu and dropdowns

| Property | Default | Purpose |
| --- | --- | --- |
| `--config-menu-dropdown-icon` | Embedded chevron SVG | Mask used for desktop dropdown indicators. |
| `--config-menu-dropdown-icon-size` | `12px` | Available icon-size setting. |
| `--config-menu-dropdown-icon-color` | `--theme-palette-color-1` | Dropdown indicator color. |
| `--config-menu-dropdown-icon-color--hover` | `--theme-palette-color-2` | Active dropdown indicator color. |
| `--config-submenu-bg-color--hover` | 5% theme palette color mixed with the inherited color | Submenu item hover background. |

### Navigation controls

These properties style Swiper and Strong Testimonials navigation buttons.

| Property | Default |
| --- | --- |
| `--config-nav-icon` | Embedded arrow SVG |
| `--config-nav-icon-size` | `18px` |
| `--config-nav-icon-color` | `--theme-palette-color-8`, falling back to `black` |
| `--config-nav-icon-color--hover` | `inherit` |
| `--config-nav-button-size` | `40px` |
| `--config-nav-button-border` | `none` |
| `--config-nav-button-border--hover` | Current navigation border |
| `--config-nav-button-radius` | `0px` |
| `--config-nav-button-color` | `--theme-palette-color-1`, falling back to `transparent` |
| `--config-nav-button-color--hover` | `--theme-palette-color-2`, falling back to the current background |
| `--config-nav-button-shadow` | `none` |
| `--config-nav-button-shadow--hover` | Current navigation shadow |

### Strong Testimonials

The Strong Testimonials integration lays out testimonial content, styles the slide card, and positions side navigation.

| Property | Default | Purpose |
| --- | --- | --- |
| `--config-testimonial-platform-size` | `48px` | Platform image width. |
| `--config-testimonial-slide-padding-x` | `48px` | Added to the slide's block padding. |
| `--config-testimonial-slide-padding-y` | `32px` | Added to the slide's inline padding. |
| `--config-testimonial-bg-color` | `white` | Card background. |
| `--config-testimonial-box-shadow` | `none` | Card shadow. |
| `--config-testimonial-border-color` | `unset` | Card border color. |
| `--config-testimonial-border-width` | `0` | Card border width. |
| `--config-testimonial-border-style` | `solid` | Card border style. |
| `--config-testimonial-border-radius` | `unset` | Card corner radius. |
| `--config-testimonial-platform-order` | `0` | Platform item flex order. |
| `--config-testimonial-rating-order` | `1` | Rating flex order. |
| `--config-testimonial-content-order` | `2` | Content flex order. |
| `--config-testimonial-name-order` | `3` | Name flex order. |
| `--config-testimonial-navigation-top-offset` | Vertically centered | Navigation position from the top. |
| `--config-testimonial-navigation-sides-offset` | `0px` | Additional navigation offset from the sides. |

Add `.slider-stretch` to a wrapper when the Strong Testimonials slider content should use a flex layout.

### Button icons and card layout

| Property | Default | Purpose |
| --- | --- | --- |
| `--config-button-icon` | Embedded right-arrow SVG | Icon appended to supported buttons. |
| `--config-button-icon-size` | `24px` | Button icon width and height. |
| `--config-button-gap` | `10px` | Space before the icon. |
| `--config-button-icon-slide-amount` | `10px` | Distance the icon moves on hover. |
| `--config-card-buttons-align-bottom` | `1` | Flex-grow value used to push Kadence card buttons to the bottom. Set to `0` to disable. |

Button arrows are automatically applied to Blocksy buttons, Kadence buttons, entry-card links, and links targeted with `.ei-button-icon`.

```html
<a class="ei-button-icon" href="/contact">Contact us</a>
```

## Design tokens

The following public tokens are defined on `:root` in the `tokens` layer:

| Token | Default | Purpose |
| --- | --- | --- |
| `--ei-transition` | `all 350ms ease-in-out` | Shared transition shorthand. |
| `--ei-container-margin` | Calculated from the viewport and normal container width, with a `0px` minimum | Aligns content with the main site container. |
| `--ei-container-margin-15` | Same calculation, with a `15px` minimum | Container alignment with a minimum gutter. |
| `--ei-narrow-max` | `--theme-narrow-container-max-width`, or `800px` | Maximum width for narrow content. |
| `--ei-box-shadow-1` | `0 2px 4px rgba(0, 0, 0, 0.24)` | Lower-elevation shadow. |
| `--ei-box-shadow-2` | `0 4px 8px rgba(0, 0, 0, 0.32)` | Higher-elevation shadow. |

The container calculations use Blocksy's `--theme-normal-container-max-width` when available. Without it, they fall back to the configured maximum fluid width.

## Utility classes

### Width and shadows

| Class | Effect |
| --- | --- |
| `.ei-narrow-max` | Applies the narrow maximum width and centers the element. |
| `.ei-shadow-1` | Applies shadow level 1 to every direct child. |
| `.ei-shadow-2` | Applies shadow level 2 to every direct child. |
| `.ei-shadow-1--hover-2` | Applies shadow level 1 to direct children and transitions to level 2 when each child is hovered. |

The shadow classes target direct children, not the element carrying the class:

```html
<div class="ei-shadow-1--hover-2">
    <article>...</article>
</div>
```

### Container-aligned margins

| Class | Effect |
| --- | --- |
| `.ei-container-margin-inline` | Container-aligned left and right margins. |
| `.ei-container-margin-left` | Container-aligned left margin. |
| `.ei-container-margin-right` | Container-aligned right margin. |
| `.ei-container-margin-inline-15` | Left and right margins with a minimum `15px` gutter. |
| `.ei-container-margin-left-15` | Left margin with a minimum `15px` gutter. |
| `.ei-container-margin-right-15` | Right margin with a minimum `15px` gutter. |
| `.ei-container-margin-left--inside` | Applies the left margin to direct `div` children. |
| `.ei-container-margin-right--inside` | Applies the right margin to direct `div` children. |
| `.ei-container-margin-left--inside-15` | Applies the left margin with a minimum `15px` gutter to direct `div` children. |
| `.ei-container-margin-right--inside-15` | Applies the right margin with a minimum `15px` gutter to direct `div` children. |

Width and container-margin utilities use `!important` so they can reliably override page-builder styles.

## Fluid value calculator

`--ei-fluid` produces a value that scales linearly from `--ei-min` to `--ei-max` as the viewport moves between the configured minimum and maximum widths. Outside that range, the result is clamped to the nearest endpoint.

Set `--ei-min` and `--ei-max` on the element that consumes `--ei-fluid`:

```css
.hero-title {
    --ei-min: 32px;
    --ei-max: 64px;
    font-size: var(--ei-fluid);
}

.section {
    --ei-min: 40px;
    --ei-max: 96px;
    padding-block: var(--ei-fluid);
}
```

Both endpoints should be compatible length values, and the minimum should not exceed the maximum.

### Blocksy header shortcuts

The stylesheet configures fluid values automatically for several Blocksy desktop-header elements:

- **Menu gap:** set `--ei-gap-min` and `--ei-gap-max` on the menu or an ancestor. Both default to `--menu-items-gap`.
- **Menu and contact-link font size:** set `--ei-font-size-min` and `--ei-font-size-max`. Both default to `--theme-font-size`, and the result cannot exceed that theme value.
- **Header button font size:** uses the same font-size properties, defaulting to `--theme-button-font-size` and capped at that value.
- **Logo height:** set `--ei-logo-height-min` and optionally `--ei-logo-height-max`. The maximum defaults to and is capped by `--logo-max-height`; no default minimum is provided.

```css
header#header {
    --ei-gap-min: 10px;
    --ei-gap-max: 30px;
    --ei-font-size-min: 14px;
    --ei-font-size-max: 18px;
    --ei-logo-height-min: 40px;
    --ei-logo-height-max: 72px;
}
```

Header buttons also support `--ei-theme-button-padding-block` and `--ei-theme-button-padding-inline`. Their defaults are `16em` and `24em`, converted relative to Blocksy's configured button font size.

## Compatibility

This stylesheet uses modern CSS features including cascade layers, native nesting, `color-mix()`, `:has()`, CSS masks, and trigonometric functions (`tan()` and `atan2()`). Test against the browser versions required by the project before deploying to older-browser audiences.

Theme and plugin integrations only take effect when their expected markup and custom properties are present. The reusable tokens, utility classes, and fluid calculator do not require those plugins, although container defaults are designed to integrate with Blocksy.
