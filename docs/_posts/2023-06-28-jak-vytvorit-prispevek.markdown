---
layout: post
title:  "Jak  vytvořit příspěvek na blog"
date:   2023-06-28 11:38
categories: Blogování
---

[Předchozí]({% post_url 2023-06-26-zakladni-konfigurace-blogu %})

Základní kostru blogu a jeho konfiguraci jsme si vytvořili v minulých dílech. Nyní se pojďme podívat na to, jak se s Jekyllem vytváří nové příspěvky.

Příspěvky se v Jekyllu píšou ve značkovacím jazyku *Markdown*. Nelekejte se, není to žádná věda. Jekyll vám na začátku vygeneroval příklad příspěvku, jehož obsah můžete pro začátek zkopírovat a upravit.

## Název a umístění souboru s textem příspěvku

Důležité je zmínit, že váš text musí být psán v souboru s pevně daným názvem, aby ho Jekyll rozpoznal a přetvořil v příspěvek na blogu. Soubor pak musí být uložen ve složce *_posts*.

Název soubouru musí mít následující formát:

{% highlight console %}
ROK-MESIC-DEN-nazev-prispevku.markdown
{% endhighlight %}

- ROK ve formě 4 čísel, měsíc a den 2

Například:

{% highlight console %}
2023-06-28-jak-vytvorit-prispevek.markdown
2023-06-24-jak-zalozit-blog.markdown
{% endhighlight %}

## Front Matter 

Každý soubor s novým příspěvkem musí začínat tzv. *front matter*, kterým určujeme použité rozvržení (layout), případně další metadata. Samozřejmě může být i prázdný. První řádky souboru tedy můžou vypadat například následovně:

{% highlight yaml %}
---
layout: post
title:  "Jak  vytvořit příspěvek na blog"
categories: Blogování
---
{% endhighlight %}

- layout udává, jaké rozložení má být použito pro tento příspěvek
  - html soubor k tomu naleznete mezi soubory šablony, kterou používáte (viz minulý díl)
- title značí název příspěvku, který je Jekyllem přetvořen v h1 tag (hlavní nadpis stránky)
- categories umožňuje podobně jako tags shlukovat příspěvky do kategorií

Již jsme viděli, že na proměnné ze souboru _config.yml je možné odkazovat přes site.*nazev_promenne*. Podobně je tomu u proměnných definovaných na počátku příspěvku, s tím rozdílem, že se na ně odkazuje přes page (tzn. *page.nazev_promenne*). Pokud byste tedy potřebovali v layoutu odkázat na kategorie (např. ve smyčce, for loop), udělali byste to přes *page.categories*.

## Kam dál?

*\-TBD\-*
