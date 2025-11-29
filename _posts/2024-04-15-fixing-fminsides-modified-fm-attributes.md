---
layout: post
title: "Bringing Back Familiarity: Fixing FMInside.net's Modified FM Attributes"
author: Amar0302
tags:
  - Gaming
  - Javascript
---

If you're a Football Manager enthusiast like me, you might have visited FMInside.net regularly to check out player stats and attributes. Unfortunately, a copyright issue between FMInside.net and SEGA forced the site to change its attribute formats. The site was previously displaying stats in a way that perfectly mirrored Football Manager's in-game attributes, but due to the legal constraints, they had to normalise the data, which made it less readable for those familiar with the game's usual format.

While this change was necessary for FMInside.net to avoid further issues with SEGA, it left many of us frustrated, as it made browsing through player stats more difficult and less intuitive. That's when I decided to take matters into my own hands and develop a script that converts these normalised stats back into the familiar FM format that we all know and love.

<!--more-->

## The Problem with Normalised Stats

In Football Manager, player attributes are displayed on a 1-20 scale, which is both simple and effective. FMInside.net's new format, however, presented attributes on a 5-100 scale, which required extra mental effort to translate into the original FM format. This became a major inconvenience for regular users like myself who are used to the 1-20 scale. To resolve this, I wrote a script that automatically converts the attributes back into the 1-20 scale whenever I visit the site.

Here is an example of a player profile before the use of my script: ![Player Profile Before](/images/MbappeBefore.png) Here is the player profile after the use of my script: ![Player Profile After](/images/MbappeAfter.png)
## The Script That Saves the Day

The script I wrote works by injecting JavaScript into the FMInside.net website. Here's how it functions:

1. **Conversion Function**: The script includes a function that converts the normalised 5-100 scale back to the familiar 1-20 scale used in Football Manager. The formula scales down the 5-100 value to fit within the 1-20 range, ensuring the stats are displayed in the format we're used to.

2. **Stat Conversion**: Once the page loads, the script scans all the stat elements on the page, checks if the values fall within the 5-100 range, and then converts them to the 1-20 scale.

3. **Reordering Attributes**: The script also reorganises the attributes based on categories like "Technical," "Mental," "Physical," and "Goalkeeping" to make it easier to locate specific stats. This reordering mirrors how stats are displayed in the actual Football Manager game, bringing a sense of familiarity and ease of use to the FMInside.net site.

Here’s a snippet of the core conversion function:

```javascript
function convertToFMStats(value) {
  return Math.floor((value - 5) / 94 * 19) + 1;
}

function convertStats() {
  const statsElements = document.querySelectorAll('.stat');
  statsElements.forEach((element) => {
    const originalValue = parseInt(element.textContent, 10);
    if (!isNaN(originalValue) && originalValue >= 5 && originalValue <= 100) {
      const convertedValue = convertToFMStats(originalValue);
      element.textContent = convertedValue;
    }
  });
}
```

This script runs in the background and seamlessly converts and reorders the stats, making FMInside.net usable again. No more mental gymnastics to convert the values yourself!

When I first created this script, it was just for personal use, but as I shared it with fellow Football Manager enthusiasts, more people started using it. Today, 15 users are benefiting from the script, enjoying the convenience of having FMInside.net display stats the way they expect them to be.

The feedback has been overwhelmingly positive, and it's been rewarding to see the community rally around this small but impactful tool. If you're someone who misses the old FMInside.net and wants a smoother experience browsing player attributes, feel free to download it from the following link:

[Download the script from the Chrome Web Store](https://chromewebstore.google.com/detail/hhpoobclfkpojlnfploipjfanndmpech)

Thanks


