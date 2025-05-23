# Vivaldi Auto-Hide Bookmark Bar CSS

This custom CSS for the Vivaldi browser enhances the bookmark bar by making it automatically hide, only appearing when needed, and staying visible for a short duration before smoothly disappearing.

## Description

The primary goal of this stylesheet is to provide a cleaner, less cluttered Browse interface. The bookmark bar remains hidden until the user hovers over specific trigger areas: the browser's main header (typically containing the address bar), the tab strip area (if visible above the header), or the bookmark bar itself. Once triggered, the bar slides into view and, importantly, stays visible for a configurable period even after the mouse moves away, before smoothly retracting.

## Features

* **Auto-Hide Functionality:** The bookmark bar is hidden by default, maximizing screen real estate.
* **Hover to Reveal:** Becomes visible when the mouse cursor is moved over:
    * The browser's header area (Vivaldi's `#header`, usually containing the address bar).
    * The tab strip area (Vivaldi's `.tab-strip`), often located above the header.
    * The bookmark bar itself (to prevent it from hiding if the mouse is still over it).
* **Configurable Delayed Hide:** After the mouse leaves a trigger area, the bookmark bar remains visible for a user-defined duration (default is 2 seconds) before starting its hiding animation. This prevents accidental hiding if the mouse briefly strays.
* **Smooth Animations:** Utilizes CSS transitions for fluid slide-in and slide-out effects, with configurable animation speed.
* **Full Width Display:** When visible, the bookmark bar spans the entire width of the browser window.
* **No Page Content Shift:** The bookmark bar is absolutely positioned, ensuring that web page content does not reflow or "jump" when the bar appears or disappears.
* **Theme-Friendly Background:** Attempts to use Vivaldi's native background color (`var(--colorBg)`) for better theme consistency, with a fallback to white.

## Customization

The CSS includes the following variables at the top of the file, allowing you to easily tailor its behavior and appearance:

* `--vivaldi-bookmark-bar-height`: Defines the height of the bookmark bar itself (e.g., `30px`).
* `--vivaldi-header-height`: Specifies the height of the Vivaldi header area that sits directly *above* where the bookmark bar will appear (e.g., the row containing the address bar, typically around `34px`). Accurate adjustment of this variable is crucial for the correct vertical positioning of the bookmark bar.
* `--bookmark-bar-hide-delay`: Controls how long (in seconds or milliseconds) the bookmark bar stays visible after the mouse leaves a trigger area before it starts to hide (e.g., `2s` for 2 seconds, `500ms` for half a second).
* `--bookmark-bar-animation-duration`: Defines the speed of the slide-in and slide-out animations (e.g., `0.2s`).

## How It Works

The CSS leverages `position: absolute !important` to take the bookmark bar out of the normal document flow and overlay it. Initially, it's hidden by being translated upwards (`transform: translateY(-100%)`) and having its `opacity` set to `0` and `visibility` to `hidden`.

When the user hovers over the designated UI elements (`#browser #header`, `#browser .tab-strip`, or the `.bookmark-bar` itself), the `opacity`, `visibility`, and `transform` properties are transitioned to bring the bar smoothly into view (`transform: translateY(0)`).

Upon the mouse leaving these areas, the hiding process doesn't begin immediately. Instead, a `transition-delay` (controlled by `--bookmark-bar-hide-delay`) is applied to the `opacity` and `transform` properties. After this delay, these properties transition back to their hidden states over the duration specified by `--bookmark-bar-animation-duration`. The `visibility` property is changed to `hidden` only after both the delay and the hiding animation have completed, ensuring the bar remains interactive during the delay and animation.
