---
title: "Hacked up Hugo theme"
description: "Modifying Hyde-X to suit my wants and needs"
tags: [ "hugo", "github", "theme", "writing", "customisation", "css" ]
date: "2016-06-17"
categories:
  - "customisation"
---

This site currently uses the [Hyde-X][3] theme with [some][4] modifcations. After dabbling with CSS here's a few changes I made to suit my wants and needs.

* Sidebar and content background same colour
* Custom colour scheme
* [highlightjs][5] [Gruvbox][6] colour scheme
* Categories and Tags navigation pages (with links in side bar)
* Round avatar
* Reduce hight of post listing on main page

All these changes were organic as I learnt more about Hugo and CSS but I wanted to save the theme from my own mistakes. I'm still learning how to github but thanks to the help from Thomas over at [pckls.io][7] I was able to to quickly create a forked branch with my changes.

{{< highlight shell >}}
git remote rm origin
git remote add origin https:/github.com/network2501/hyde-x
git checkout -b feature/2501
git add --all
git commit -m "CSS, layout changes"
git push origin feature/2501
{{< /highlight >}}

[3]: https://github.com/zyro/hyde-x
[4]: https://github.com/network2501/hyde-x/tree/feature/2501
[5]: https://highlightjs.org
[6]: https://github.com/morhetz/gruvbox
[7]: https://www.pckls.io/
