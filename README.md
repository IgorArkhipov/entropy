# PR #277 UI screenshots

Native macOS About device page from Entropy PR #277, source head d9b0d3004d241fd9f12cb2f6d745c4633b80a536.

The preview uses simulated Phenom data with native RMK/Rynk firmware 0.3.0 and illustrative release metadata. No keyboard was connected, queried, reset, or flashed.

The preview calls the production About device renderer with the production fonts and theme, using the inert application constructor. A temporary entry point requests eframe framebuffer PNG captures after layout settles. Temporary source changes were restored afterward.

- phenom-about-en.png: English
- phenom-about-ru.png: Russian

These images verify presentation only, not device communication or live release discovery.
