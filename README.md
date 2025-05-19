# Vivaldi Auto-Hide Bookmark Bar CSS

This custom CSS for the Vivaldi browser modifies the appearance of the bookmark bar, making it automatically hide and only appear when needed.

## Description

The primary goal of this stylesheet is to provide a cleaner Browse interface by keeping the bookmark bar out of sight until the user hovers over the header area of the browser. When triggered, the bookmark bar smoothly slides into view.

## Features

* **Auto-Hide Functionality:** The bookmark bar is hidden by default.
* **Hover to Reveal:** It becomes visible when the mouse cursor is moved over the browser's header area (containing the address bar and tabs) or over the bookmark bar itself.
* **Smooth Animations:** Uses CSS transitions for a fluid slide-in and slide-out effect.
* **Full Width Display:** When visible, the bookmark bar spans the entire width of the browser window.
* **No Page Content Shift:** The bookmark bar is absolutely positioned, ensuring that web page content does not reflow or "jump" when the bar appears or disappears.
* **Theme-Friendly Background:** Attempts to use Vivaldi's native background color for theme consistency.

## Customization

The CSS includes the following variables at the top of the file that you can adjust to match your Vivaldi setup:

* `--vivaldi-bookmark-bar-height`: Defines the height of the bookmark bar itself (e.g., `30px`).
* `--vivaldi-header-height`: Specifies the height of the area above the bookmark bar (e.g., address bar + tab bar if tabs are on top, typically around `34px`). Accurate adjustment of this variable is important for correct positioning.

## How It Works

The CSS uses `position: absolute` to take the bookmark bar out of the normal document flow. It's initially translated upwards (`transform: translateY(-100%)`) and set to `opacity: 0` and `visibility: hidden`. On hover of designated UI elements (like `#header`), these properties are transitioned to bring the bar into view.

      :root {
        --vivaldi-bookmark-bar-height: 30px;
        --vivaldi-header-height: 34px;
      }
      
      .bookmark-bar {
        position: absolute !important;
        top: var(--vivaldi-header-height) !important;
        left: 0 !important;
        right: 0 !important;
        width: 100% !important;
        z-index: 200 !important;
        background-color: var(--colorBg, #fff);
        box-shadow: 0 2px 5px rgba(0,0,0,0.15);
        max-height: var(--vivaldi-bookmark-bar-height);
        overflow: hidden;
        opacity: 0;
        visibility: hidden;
        transform: translateY(-100%);
        transition:
          opacity 0.2s ease-in-out,
          transform 0.2s ease-in-out,
          visibility 0s linear 0.2s !important;
      }
      
      #browser #header:hover ~ #main .bookmark-bar,
      #browser #header:hover + .bookmark-bar,
      .bookmark-bar:hover {
        opacity: 1;
        visibility: visible;
        transform: translateY(0);
        transition:
          opacity 0.2s ease-in-out,
          transform 0.2s ease-in-out,
          visibility 0s linear 0s !important;
      }
