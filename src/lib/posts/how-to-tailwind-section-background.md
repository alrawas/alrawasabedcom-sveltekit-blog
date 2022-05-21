---
title: "How To Code A Section With A Background In TailwindCSS"
date: "2022-05-21"
updated: "2022-05-21"
categories: 
  - "TailwindCSS"
coverImage: "/images/how-to-tailwind-section-background.jpg"
coverWidth: 3
coverHeight: 2
excerpt: This post contains a snippet demonstrating how to code a section with a background using TailwindCSS. As well as playing with overlay and clipping.
---

## Final Result
This is a quick tutorial on how to achieve the following effect using TailwindCSS.

As a bonus, add a background clipping too!

<img href="/" alt="h" src="/images/tailwind-section-bg-clipped.jpg" />

## Minimal Working Snippet
To achieve the effect of a background image, put the `background-image` css property inside the style attribute. The `url('')` works for remotely hosted images as well as for local images.

In order to make the image show we have to specify a height. `h-[80vh]` is an example.

The `<h1>` element will show inside the section, in front of the image. To push the `<h1>` down, use padding. `pt-16` is an example.

```html
<section
  style = "background-image: url('https://picsum.photos/800');"
  class = "w-full h-[80vh] bg-cover bg-center">

  <h1 class = "text-center pt-16 text-xl">Hello World!</h1>
    
  <!-- more html -->
</section>
```

## Adding Background Clipping

At the time of writing this article. I could not find a clipping solutions built into TailwindCSS. I did not want to install a package just for that.

Luckily adding the clipping effect is a one liner.

I use [CSS clip-path maker](https://bennettfeely.com/clippy/) to visually draw my clipping paths. Then copy the one liner into my html.

Building on top of the previous snippet. I added the clipping code into the style attribute.
```html
<section
  style = "
  background-image: url('https://picsum.photos/800');
  clip-path: polygon(0% 0%, 100% 0, 100% 85%, 50% 100%, 0 85%);
  "
  class = "w-full h-[80vh] bg-cover bg-center">

  <h1 class = "text-center pt-16 text-xl">Hello World!</h1>
    
  <!-- more html -->
</section>
```
## TailwindCSS Full Code Snippet
The clipping leaves whitespace behind it. To have control on that whitespace color, wrap the section with a div having a background color of your choice. `<div class="bg-[#E4E4E4]">` is an example.

I added some blend overlay effects to further customize the background. Feel free to use these effects or remove them.

```html
<div class="bg-[#E4E4E4]">
  <section
    style="
    background-image: url('https://picsum.photos/800');
    clip-path: polygon(0% 0%, 100% 0, 100% 85%, 50% 100%, 0 85%);"

    class="
    bg-white bg-opacity-30 bg-blend-overlay
    w-full
    h-[80vh] md:h-[65vh]
    bg-cover bg-center
    "
  >
    <h1 class="text-center pt-16 text-xl">Hello World!</h1>
    
    <!-- more html -->
  </section>
</div>
```