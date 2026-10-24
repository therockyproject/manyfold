# Manyfold: multi-model AI chat landing page

A single-file landing page for an AI chat interface that lets people talk to many models (GPT, Claude, Gemini, Llama, DeepSeek and more) in one place. The visual style follows jimo.ai/product/ai: dark, minimal, with a product window as the hero. It uses a light touch of liquidglass for the glass effects.

# What's included
manyfold-landing.html: the whole page (HTML, CSS and JS in one file, no build step)
# Features
Live chat demo. Type a message and get a streamed reply. Switching models in the glass bar adds a "context kept" note to the thread.
Liquid glass. The model switcher and a draggable orb use WebGL glass refraction. If the library fails to load, the page falls back to a CSS frosted-glass style.
Motion. Staggered headline entrance, drifting background glow, scrolling model marquee, scroll-triggered feature animations, count-up stats and an animated FAQ.
Responsive and accessible. Works down to mobile widths, shows keyboard focus, and respects prefers-reduced-motion.
Email signup form. Front-end only. It shows a confirmation and does not send or store the address.
#Browser support

Current Chrome, Edge, Firefox and Safari. The glass effect needs WebGL; other features need no special support.

# Run it locally

No install needed. Open manyfold-landing.html in a browser.

The glass effect loads from a CDN, so you need an internet connection for it. Without one, the page still works with the CSS fallback.

If you host it yourself, serve it over HTTPS. The page uses Google Fonts (Inter) and this module:

https://cdn.jsdelivr.net/npm/@ybouane/liquidglass@1.0.3/dist/index.js

# Customize
What	Where
Product name	Search for Manyfold (nav logo, title, footer)
Colors	CSS variables at the top of <style> (--bg, --fg, --mut, --acc)
Headline and copy	The .hero, #features, #faq and #cta sections
Models in the demo	The M object in the main script (name, dot color, canned reply)
Marquee names	The <span> items inside #mq
Stats	data-to attributes on .stat elements
Glass look	The data-config JSON set in the type="module" script at the bottom

# Glass settings

Each glass element is configured with the library's options. The current values:

Switcher bar: cornerRadius: 28, refraction: 0.55, blurAmount: 0.12, specular: 0.15
Draggable orb: floating: true, bevelMode: 1, refraction: 0.9, chromAberration: 0.12

See the liquidglass docs for every option.

Library rules to keep in mind when editing:

Glass elements must be direct children of the root (#stage).
The root's own background is not captured. Put backgrounds in a child element (the .bg div does this).
Webfonts must be loaded before the library starts, so keep the Google Fonts link in the <head>.

# Connect real models

The demo replies are scripted. To use real models:

Send the user's message from the f.onsubmit handler to your backend. Don't put provider API keys in the page.
Pass the selected model (cur) and the full message history so context carries across model switches.
Replace the say(M[cur].t) call with a function that streams your backend's response into the message bubble.

# Add the signup backend

The form handler at the bottom of the main script only swaps in a thank-you message. Post the email to your own endpoint or a form service inside $('#j').onsubmit.

