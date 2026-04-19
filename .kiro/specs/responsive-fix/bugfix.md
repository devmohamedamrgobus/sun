# Bugfix Requirements Document

## Introduction

The Sunsnow travel website (Arabic RTL, 4 pages: index.html, about.html, packages.html, package-details.html) has widespread responsive layout issues. Components use fixed widths, grids lack tablet breakpoints, the navbar has no mobile menu, and many elements overflow or fail to adapt across the defined breakpoints (mobile < 768px, tablet 768–1023px, desktop ≥ 1024px). These issues make the site unusable or visually broken on mobile and tablet devices.

## Bug Analysis

### Current Behavior (Defect)

1.1 WHEN the viewport is less than 768px THEN the navbar links are hidden with no hamburger menu or alternative navigation, leaving mobile users unable to navigate the site

1.2 WHEN the viewport is less than 768px THEN the navbar logo image remains at a fixed width of 170px (set via HTML attribute), causing it to overflow or appear disproportionately large on small screens

1.3 WHEN the viewport is less than 768px THEN the search bar avatar (positioned at `left: -44px`) overflows outside the viewport boundary, even though it is hidden via `display: none` only in some CSS files, creating inconsistent behavior

1.4 WHEN the viewport is less than 768px THEN the search bar fields do not stack vertically in a usable manner due to conflicting styles between main.css and responsive.css

1.5 WHEN the viewport is between 768px and 1023px THEN the why-us grid (4 columns on desktop) has no tablet-specific breakpoint in the component CSS files (css/components/why-us.css), relying only on main.css fallback rules

1.6 WHEN the viewport is between 768px and 1023px THEN the testimonials grid (3 columns main row, 4 columns small row) has no tablet breakpoint, causing cards to be too narrow or overflow

1.7 WHEN the viewport is between 768px and 1023px THEN the gallery grid (4 columns) has no tablet breakpoint in the component CSS (css/components/gallery.css), causing images to be too small

1.8 WHEN the viewport is between 768px and 1023px THEN the contact form (2-column grid) has no tablet breakpoint, remaining in 2 columns when space is insufficient

1.9 WHEN the viewport is between 768px and 1023px THEN the footer grid has no consistent tablet breakpoint across page-specific CSS files (packages.css, package-details.css, about.css)

1.10 WHEN the viewport is less than 768px THEN the destinations grid (`.cards-grid`) only collapses to 1 column via main.css, while the component CSS (css/components/destinations.css) has no media queries at all

1.11 WHEN the viewport is less than 768px THEN the package detail thumbnail images remain at fixed `width: 130px; height: 82px` with only a partial mobile override (90px × 58px), and have no tablet breakpoint

1.12 WHEN the viewport is less than 768px THEN the footer logo image uses a fixed `width="120"` HTML attribute with no responsive scaling

1.13 WHEN the viewport is less than 768px THEN the hero section title font size is only reduced to 1.5–1.6rem (depending on which CSS file takes precedence), and the subtitle has no responsive font sizing at all

1.14 WHEN the viewport is less than 768px THEN buttons and interactive elements (inputs, links) do not meet the minimum 44px touch target size recommended for mobile usability

1.15 WHEN the viewport is between 768px and 1023px THEN the packages grid (`.pkg-grid`) transitions from 3 columns to 2 columns but has no further adaptation, and the about page testimonials 4-column grid (`.test-grid--4col`) only drops to 2 columns

1.16 WHEN any viewport width is used THEN conflicting/duplicate responsive rules exist between main.css (inline media queries) and responsive.css, and component CSS files have no media queries, causing unpredictable cascade behavior

1.17 WHEN the viewport is less than 768px THEN there are no padding/margin adjustments for section spacing, and no body font-size scaling for improved mobile readability

### Expected Behavior (Correct)

2.1 WHEN the viewport is less than 768px THEN the system SHALL provide a hamburger menu button that toggles visibility of the navigation links, ensuring mobile users can access all pages

2.2 WHEN the viewport is less than 768px THEN the system SHALL scale the navbar logo image responsively (using CSS `max-width` instead of a fixed HTML width attribute) so it fits within the mobile navbar without overflow

2.3 WHEN the viewport is less than 768px THEN the system SHALL consistently hide the search bar avatar across all CSS files and ensure no overflow from its absolute positioning

2.4 WHEN the viewport is less than 768px THEN the system SHALL stack the search bar fields vertically in a single consistent rule set, with full-width fields and adequate spacing

2.5 WHEN the viewport is between 768px and 1023px THEN the system SHALL display the why-us grid in 2 columns with consistent rules across all CSS files

2.6 WHEN the viewport is between 768px and 1023px THEN the system SHALL display the testimonials main grid in 2 columns and the small grid in 2 columns, preventing cards from being too narrow

2.7 WHEN the viewport is between 768px and 1023px THEN the system SHALL display the gallery grid in 2 columns

2.8 WHEN the viewport is between 768px and 1023px THEN the system SHALL collapse the contact form to a single-column layout

2.9 WHEN the viewport is between 768px and 1023px THEN the system SHALL display the footer in a consistent 2-column or 1-column layout across all pages

2.10 WHEN the viewport is less than 768px THEN the system SHALL collapse the destinations grid to 1 column with consistent rules in the component CSS file

2.11 WHEN the viewport is less than 768px THEN the system SHALL scale package detail thumbnail images to fit the available width, and provide a tablet breakpoint for intermediate sizing

2.12 WHEN the viewport is less than 768px THEN the system SHALL scale the footer logo image responsively using CSS rather than a fixed HTML width attribute

2.13 WHEN the viewport is less than 768px THEN the system SHALL reduce the hero title to a readable mobile size (around 1.4–1.5rem) and apply responsive font sizing to the subtitle text

2.14 WHEN the viewport is less than 768px THEN the system SHALL ensure all interactive elements (buttons, inputs, links) have a minimum touch target size of 44px

2.15 WHEN the viewport is between 768px and 1023px THEN the system SHALL display the packages grid in 2 columns and the about page testimonials 4-column grid in 2 columns (hiding the peek card)

2.16 WHEN any viewport width is used THEN the system SHALL consolidate responsive rules into a single authoritative location (responsive.css or component files) to eliminate conflicting cascade behavior

2.17 WHEN the viewport is less than 768px THEN the system SHALL apply reduced section padding/margins and slightly smaller body font size for improved mobile readability and spacing

### Unchanged Behavior (Regression Prevention)

3.1 WHEN the viewport is 1024px or wider THEN the system SHALL CONTINUE TO display the full desktop layout with navbar links visible, 3-column destination grid, 4-column why-us grid, 4-column gallery grid, 3-column testimonials grid, 2-column contact form, and 3-column footer

3.2 WHEN the viewport is 1024px or wider THEN the system SHALL CONTINUE TO display the search bar avatar positioned to the side of the search box

3.3 WHEN the viewport is 1024px or wider THEN the system SHALL CONTINUE TO display the hero section with the current font sizes (2.2–2.5rem title) and layout

3.4 WHEN the viewport is 1024px or wider THEN the system SHALL CONTINUE TO display the packages grid in 3 columns with the current card styling

3.5 WHEN the viewport is 1024px or wider THEN the system SHALL CONTINUE TO display the package details page with the hero image at 420px height and thumbnails at their current size

3.6 WHEN any viewport width is used THEN the system SHALL CONTINUE TO maintain RTL (right-to-left) text direction and Arabic font rendering across all pages

3.7 WHEN any viewport width is used THEN the system SHALL CONTINUE TO use the existing CSS variable system (colors, typography, spacing) defined in variables.css

3.8 WHEN any viewport width is used THEN the system SHALL CONTINUE TO preserve all hover effects, transitions, and interactive states on cards, buttons, and links
