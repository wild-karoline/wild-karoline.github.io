---
layout: post
title:  "Příspěvek se nezobrazuje?"
date:   2023-07-18 08:00:00 +0200
last_modified_at: 2023-07-18 08:00:00 +0200
category: Blogování
description: Úvod do blogování s Jekyllem. Možné řešení problému s příspěvkem, který se nezobrazuje na blogu.
---

[Předchozí]({% post_url blogovani/2023-06-29-jak-zverejnit-blog %})

Nedávno jsem narazila na následující problém. Sepsala a vytvořila jsem příspěvek, vše nahrála na GitHub, počkala až se stránka aktualizuje... a nic. Příspěvek na blogu nebyl! Kontrola repository (místa, kde na GitHubu mám kód k blogu), vše v pořádku. *bundle exec jekyl serve*, taky nic. Tak pokud se někdy setkáte se stejným problém, zde několik možných důvodů pro nezobrazující se příspěvek:

- příspěvek se nenachází ve složce *_posts*
- soubor příspěvku má nesprávný název - každý soubor s příspěvkem by měl mít název ve formátu *ROK-MĚSÍC-DEN-nadpis-příspěvku.MARKUP* (přičemž MARKUP bývá *.md* nebo *.markdown*)
- datum příspěvku je v budoucnosti
  - to se stalo mně - datum nebylo v budoucnosti, ale u tagu *date* jsem nezohlednila časové zóny, proto nebyl publikován ihned, přestože se vše zdálo v pořádku
    - nyní mám u každého data kromě rrrr-mm-dd hh:mm:ss i časovou zónu (v mém případě *+0200*) a vše funguje jak má
  
Důvodů pro nezobrazení příspěvků může být i vícero. Pokud se někdy setkáte s nějakým neobvyklejším, budu ráda, když mi o tom dáte echo třeba na [Discordu](https://discord.gg/hB8UYAgwUE).

## Kam dál?

*\-TBD\-*

**Pozor, jsem na dovolené. Nedokážu tedy zatím říct, co bude následovat, ani kdy to bude zveřejněné.**
