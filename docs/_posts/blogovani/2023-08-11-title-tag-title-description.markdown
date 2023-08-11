---
layout: post
title:  "Title = title | description???"
date:   2023-08-11 07:30:00 +0200
last_modified_at: 2023-08-11 07:30:00 +0200
category: Blogování
read_time: 1 min 48 s
description: Všimli jste si, že se na záložce v prohlížeči vedle titulku domovské stránky zobrazuje i její popis? Čtěte dál, pokud se chcete dozvědět, jak to upravit.
excerpt: Návod, jak upravit meta tag title na domovské stránce. 
permalink: blogovani/title-tag-title-description
---

[Předchozí [Jak jsem vytvořila rozcestník]]({% post_url blogovani/2023-07-20-jak-jsem-vytvorila-rozcestnik %})

Doufám, že dnešní titulek nezní až příliš španělsky. Zkusím situaci nejdřív trochu rozvést, než vám ukážu řešení.

Každá stránka má k dispozici ve svém zdrojovém souboru, HTML, tzv. meta tagy. To jsou tagy, které obsahují informace o stránce, a patří mezi ně i tag "title" a metatag "description". U blogových příspěvků si je definujeme ve front matter (to, co píšeme na začátek dokumentu mezi ty pomlčky), pro domovskou stránku jsou dané v souboru _config.yml. Prohlédnout si obsah těchto tagů můžete např. tak, že si na požadované stránce pravým tlačítkem vyjedete menu, kde zvolíte "View Page Source" (v AJ ve Firefoxu; může se u jednotlivých prohlížečů a jazykových variant lišit). Celkem nahoře, uvnitř tagu "head" byste měli najít tagy title a description.

![Screenshot menu pro zobrazení zdrojáku stránky](/assets/images/view_page_source.png)

![Screenshot zdrojáku stránky, zvýrazněn title a description](/assets/images/meta_title_description.png)

U hlavní, domovské stránky se title skládá z titulu a description (oboje definováno v _config.yml), u příspěvků pak z titulku příspěvku a titulku blogu. Title příspěvků je OK, co mě ale vadilo bylo, že se v titulu domovské stránky zobrazuje celá (ca 150 znaků dlouhá) description, neboli popis blogu. Title se zobrazuje i na záložce, kartě prohlížeče, a tam fakt nevypadá dobře, když tam máte text přes několik řádků.

Tyto tagy se píšou uvnitř tagu "head", který se píše celkem na začátku HTML souboru (před vlastním, zobrazovaným obsahem). To, jak je stránka koncipovaná, nám v první řadě udávají layouty. Pro připomenutí, takhle se dostanete k layoutům od Minimy:

```console
bundle info --path minima
```

A tady jsem začala hledat. Nejdříve jsem ve složce "_layouts" mrkla na soubor "home.html". Ten se odkazoval na "default.html", ve kterém bylo pomocí include odkázáno na "head.html", který se nachází ve složce "_includes". A jaké mě čekalo překvapení, když jsem tam nenašla jedinou zmínku o tagu title. Co ještě mohlo skrývat nějaké další informace je tag "seo" a to už jsem sáhla po Googlu. A tak jsem se dostala k [manuálu od jekyll seo tagu](https://github.com/jekyll/jekyll-seo-tag/blob/master/docs/usage.md).

Dokumentace je psaná v angličtině (již jsem na začátku poukazovala na to, že to je běžný postup, aby byly informace dostupné většímu publiku). Ale ve zkratce u "description" stojí, že je součástí "title" tagu, pokud není definován titul stránky (page.title) nebo tagline celého webu (site.tagline). A to je případ domovské stránky, kde je definován jen site.title a site.description. Nabízí se tedy jednoduché řešení - přidat do _config.yml "tagline", neboli krátký popisek, který bude použit jako součást title tagu.

Upravit, uložit, znovu spustit web (pro připomenutí *bundle exec jekyll serve*) - tradá! Funguje to.

## Kam dál?

*\-TBD\-*
