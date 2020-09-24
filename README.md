# Monochromic
A custom theme for Jellyfin mediaserver created using CSS overrides. Note that I maintain this theme to be compatible with whatever version of Jellyfin I am currently using. Which is usually the latest stable release. You can therefore assume that using the theme on older versions won't work, but also that if a new release breaks something, that I will fix it. If you encounter unthemed elements or something broken, open an issue.

To use the theme copy paste the line below into "Dashboard>General>Custom CSS" and click save, it will apply immediately server-wide to all users on top of any theme they may be using. To remove the theme, clear the "Custom CSS" field and then click save. **NOTE: Theme may not work when using reverse proxy**, check the bottom section of this readme for more info.


```css
@import url('https://ctalvio.github.io/Monochromic/default_style.css');
```

![six](screenshots/6.png)
![five](screenshots/5.png)

## Features
- Themes **EVERYTHING**
- Dark, Transparent, Minimalistic
- Uses the same font as the JF logo everywhere
- Add-ons for an easy personal touch
- Customizable accent color
- Blurred backdrops
- Squared aesthetic with rounded corners (optionally corners so sharp you might get an eye poked out)
- Two options for progress bars
- Works well on mobile
- More compact
- Smaller and squared cast info

## Add-ons

This theme has some additional options, they can allow the use of a custom accent color, and more. These are added immediately after the default import line.

### No rounded corners 

In fact, squares off  every rounded corner JF ever had.

```css
@import url('https://ctalvio.github.io/Monochromic/sharp_style.css');
```

### Accent color presets 

Blue restores some of the default jellyfin blue accenting, while purple uses... Well, purple, in a Jellyfin shade of course.

```css
@import url('https://ctalvio.github.io/Monochromic/jfblue_style.css');

@import url('https://ctalvio.github.io/Monochromic/jfpurple_style.css');
```

### Restore bottom bar style episode progress

```css
@import url('https://ctalvio.github.io/Monochromic/bottom-progress_style.css');
```

### Define your own accent color

**UPDATED**: This now uses a single RGB value in a variable. This lets me use the color at various transparencies in the css. Use any RGB color picker to find the value for any given color and enter it. **This import line should always be last**.
```css
@import url('https://ctalvio.github.io/Monochromic/customcolor_style.css');
:root {--accent: R, G, B;}
```

## Screenshots

![one](screenshots/1.png)
![two](screenshots/2.png)
![four](screenshots/4.png)
![seven](screenshots/7.png)
![three](screenshots/3.png)


## Using with reverse proxy

When using the Nginx Reverse proxy config from the [Jellyfin docs](https://jellyfin.org/docs/general/networking/nginx.html) the theme will not work by default. (If you are using the subpath config, you can ignore all this.)

Because the config includes Content-Security-Policy which reduces risk of XSS, you need to add the URL from this repo and the fonts to the list of allowed external sources.

In the nginx config you should change the
```
add_header Content-Security-Policy ....
```
to:
```
add_header Content-Security-Policy "default-src https: data: blob:; style-src 'self' 'unsafe-inline' 
https://ctalvio.github.io/Monochromic/default_style.css 
https://ctalvio.github.io/Monochromic/sharp_style.css 
https://ctalvio.github.io/Monochromic/jfblue_style.css 
https://ctalvio.github.io/Monochromic/jfpurple_style.css 
https://ctalvio.github.io/Monochromic/bottom-progress_style.css.css 
https://ctalvio.github.io/Monochromic/customcolor_style.css 
https://ctalvio.github.io/Monochromic/customcolor-advanced_style.css 
https://fonts.googleapis.com/css2; 
script-src 'self' 'unsafe-inline' 
https://www.gstatic.com/cv/js/sender/v1/cast_sender.js 
https://www.youtube.com/iframe_api https://s.ytimg.com 
https://ctalvio.github.io/Monochromic/default_style.css 
https://ctalvio.github.io/Monochromic/sharp_style.css 
https://ctalvio.github.io/Monochromic/jfblue_style.css 
https://ctalvio.github.io/Monochromic/jfpurple_style.css 
https://ctalvio.github.io/Monochromic/bottom-progress_style.css
https://ctalvio.github.io/Monochromic/customcolor-advanced_style.css 
https://ctalvio.github.io/Monochromic/customcolor_style.css;
worker-src 'self' blob:; connect-src 'self'; object-src 'none'; frame-ancestors 'self'";
```

If you don't do this the theme will simply not load (reverts back to default theme) and the browser console will spit out an error. Even if you paste in all the CSS, the font will still not load since it is loaded from an external source.

Thanks to [LickABrick](https://github.com/LickABrick) for discovering this, and submitting instructions on how to fix.
