---
layout: post
title:  "Smyčky a podmínky v C"
date:   2023-08-12 08:50:00 +0200
last_modified_at: 2023-08-12 08:50:00 +0200
category: Programovací jazyk C
read_time: 6 min 11 s
description: Dnešní díl vám představí smyčky a podmínky, větvení v C. Ukážeme si if a if-else struktury, while, do-while a for smyčky.
permalink: programovaci-jazyk-c/smycky-a-podminky
---

[Předchozí [Opakování - datové typy, operátory, ASCII]]({% post_url c/2023-08-09-opakovani-datove-typy-operatory-ascii %})

Smyčky a podmínky nebo větvení patří v programování mezi tzv. řídící struktury, v AJ control flow statements. Nabízí nám možnost alternativních či opakujících se cest v řámci našeho programu.

## Podmínky

Větvení programu můžeme docílit za pomocí tzv. if podmínek. V takové if podmínce neděláme nic jiného, než že klademe ano/ne otázky a podle toho se rozhodujeme, kam náš program bude dále pokračovat.

{% include image.html url="/assets/images/c/if.png" description="Jedna z mnoha možností větvení programu za pomocí if podmínky" %}

Obrázek výše znázorňuje jednu takovou možnost rozvětvit chod programu za pomocí if podmínky. V programu se můžeme rozhodnout jít 2 různými cestami na základě toho, jestli je nějaká proměnná větší nebo menší než 0 (if podmínky vždy vyhodnocují pravdivostní, logické výrazy). Pokud bude číslo skryté za proměnnou x větší než 0, bude program pokračovat výrazem B, jinak výrazem A. Nikdy neprovede oba kroky najednou.

{% include image.html url="/assets/images/c/if2.png" description="Jedna z mnoha možností větvení programu za pomocí if podmínky" %}

Toto představuje zase jinou možnost. Program vybočí ze své sekvence jenom v případě, že bude podmínka v if-u pravdivá. Pokud ne, nic neobvyklého se nestane, program bude pokračovat hned za if-blokem.

{% include image.html url="/assets/images/c/if3.png" description="Jedna z mnoha možností větvení programu za pomocí if podmínky" %}

If-blocky a podmínky je také možné vkládat do sebe a dostávat se tak k dalším if otázkám jen tehdy, pokud už ty předtím byly nějak vyhodnoceny. Podívejte se na obrázek výše. Pokud by první podmínka byla vyhodnocena jako nepravdivá, bude program pokračovat bloky A a C. Bude-li však první podmínka vyhodnocena jako pravdivá a stejně tak druhá, program nikdy k blokům A a B nedojde a rovnou bude pokračovat blokem C. Pokud by byla první podmínka pravdivá a druhá nepravdivá, půjde program přes bloky B a C (a vynechá tedy A).

Větvení pomocí if-podmínek může mít formu samotného if, if v kombinaci s else, případně if v kombinaci s else if zakončeným samotným else.

Pokud by za if následoval jenom jeden jediný příkaz, není potřeba ho psát do bloku (tzn. do složených závorek). Pokud by následovalo vícero příkazů, je vždy nutné je uzavřít do složených závorek, bloku, aby bylo programu jasné, co všechno má provést v případě, že by byla splněna podmínka v if.

I kdybyste závorky nepotřebovali, vždy myslete na odsazení! Úplně na začátku jsem zmiňovala, že je potřeba psát kód tak, aby ho mohli číst i jiní. (Na odsazení myslete i kdykoliv jindy, i když budete psát hezky závorky a do bloku.)

### Ternární operátor

Některé programovací jazyky nabízejí tzv. ternární operátor. Již o něm byla zmínka v předminulé kapitole, kde jsme si řekli, že je to operátor, který ke svému fungování vyžaduje 3 operandy. Teď, u if-podmínek, si jeho fungování můžeme vysvětlit blíže.

Ternární operátor se skládá z op1 ? op2 : op3 (přičemž op je operand, neboli člen, který se účastní operace). Výsledek odečítáme nějak takto: pokud je pravda op1, pak mi dej op2, jinak op3. Nezní vám to povědomě? Ano, je to to samé, jako byste udělali if-podmínku na op1, která by zastřešovala blok op2 a která by měla else-větev, která by zastřešovala op3.

Použití by mohlo vypadat následovně:

{% highlight c %}
#include <stdio.h>

int main(void) 
{
    int cislo = 5;

    printf("Cislo je sude: %s\n", (cislo % 2 == 0) ? "ANO" : "NE");

    return 0;
} {% endhighlight %}

Výsledek by byl stejný jako za použití if-else konstruktu:

{% highlight c %}
#include <stdio.h>

int main(void) 
{
    int cislo = 5;

    if (cislo % 2 == 0)
    {
        printf("Cislo je sude: ANO\n");
    } else 
    {
        printf("Cislo je sude: NE\n");
    }

    return 0;
} {% endhighlight %}

### Switch case

Switch nabízí další možnost zápisu na bázi if-podmínek. 

Představte si následující situaci: Uživatel dostane na výběr ze 4 světových stran a vy pak na základě jeho volby budete nějak v programu pokračovat. Toto můžete buď vyřešit formou 4 samostatných if, případně složeného if-else výrazu. Anebo switch konstrukcí. Ale asi nejjednodušší bude si to ukázat na příkladu.

Za pomocí námi známých if-else podmínek by program mohl vypadat následovně:

{% highlight c %}
#include <stdio.h>

int main(void)
{
    // Ahoj uzivateli! Prosim zvol si jednu z nasledujicich moznosti:
    //   1: Rovne
    //   2: Leva
    //   3: Prava
    //   4: Zpet

    int volba = 3;

    if (volba == 1) 
    {
        printf("Pokracujes dal? OK!\n");
    } else if (volba == 2)
    {
        printf("Hura doleva!\n");
    } else if (volba == 3) 
    {
        printf("Prava je ta prava...\n");
    } else if (volba == 4)
    {
        printf("Jak jen to bylo... 1 krok dopredu a 2 dozadu?\n");
    } else 
    {
        printf("Nepodvadime! Vyber si jednu z nabizenych moznosti, jina neni.\n");
    }

    return 0;
} {% endhighlight %}

A takhle, když použijeme switch:

{% highlight c %}
#include <stdio.h>

int main(void)
{
    // Ahoj uzivateli! Prosim zvol si jednu z nasledujicich moznosti:
    //   1: Rovne
    //   2: Leva
    //   3: Prava
    //   4: Zpet

    int volba = 3;

    switch (volba)
    {
        case 1: 
            printf("Pokracujes dal? OK!\n");
            break;
        case 2:
            printf("Hura doleva!\n");
            break;
        case 3:
            printf("Prava je ta prava...\n");
            break;
        case 4: 
            printf("Jak jen to bylo... 1 krok dopredu a 2 dozadu?\n");
            break;
        default:
            printf("Nepodvadime! Vyber si jednu z nabizenych moznosti, jina neni.\n");
    }

    return 0;
} {% endhighlight %}

Do závorky za klíčové slovo *switch* jde proměnná, jejíž hodnota se bude posuzovat. Následují případy, neboli *case*. Pokud nastane případ, kdy proměnná *volba* bude rovna 1, pak nám program na konzoli vydá "Pokracujes dal? OK!", atd. Klíčové slovo *break* opouští switch. Schválně si zkuste smazat *break*, který je součástí třetího case-u a program znovu zkompilujte a spusťte. Vidíte rozdíl? Bez *break* program propadne do další větve, mluvíme o propadávacím switch case konstruktu. No a nakonec případ *default* - ten je jako poslední else větev o program výše. Nenastane-li žádný z uvedených případů, pak se provede jakýkoli příkaz, který je udaný v defaultním případu. Pokud by chyběl, nestalo by se v rámci switch větvení nic (pokud by zároveň nenastal žádný z uvedených případů). 

### Příklady

<!-- Example 1 -->
Napište program, který uživateli na základě věku vyhodnotí, kterého řidičského oprávnění by již mohl dosáhnout. Potřebné údaje můžete získat např. [zde (§ 83)](https://www.zakonyprolidi.cz/cs/2000-361). Ještě jsme si neukázali, jak získat vstupy od uživatele, proto si věk uložte do nějaké proměnné. Důležité je, že pak za pomocí if podmínek na konzoli uvidíte odpovídající výstup.

Takto by např. mohl vypadat výstup pro věk 19 let:

{% highlight console %}
Vek: 19 let
Splnujes vekovou hranici pro ridicske opravneni skupiny A2, B, B+E, C1 a C1+E. {% endhighlight %}

<!-- Example 1 solution -->

<details>
  <summary><u>Možné řešení: </u></summary>
<br />
{% highlight c %}
#include <stdio.h>

int main(void)
{
    int vek = 10;

    printf("Vek: %d\n", vek);

    if (vek >= 24)
    {
        printf("Splnujes vekovou hranici pro ridicske opravneni skupiny AM, A1, B1 a T, A2, B, B+E, C1 a C1+E, C, C+E, D1, D1+E, A, D, D+E.\n");
    } else if (vek >= 21)
    {
        printf("Splnujes vekovou hranici pro ridicske opravneni skupiny AM, A1, B1 a T, A2, B, B+E, C1 a C1+E, C, C+E, D1, D1+E.\n");
    } else if (vek >= 18)
    {
        printf("Splnujes vekovou hranici pro ridicske opravneni skupiny AM, A1, B1 a T, A2, B, B+E, C1 a C1+E.\n");
    } else if (vek >= 17)
    {
        printf("Splnujes vekovou hranici pro ridicske opravneni skupiny AM, A1, B1 a T.\n");
    } else if (vek >= 16)
    {
        printf("Splnujes vekovou hranici pro ridicske opravneni skupiny AM, A1.\n");
    } else if (vek >= 15)
    {
        printf("Splnujes vekovou hranici pro ridicske opravneni skupiny AM.\n");
    } else {
        printf("Nesplnujes vek pro zadne ridicske opravneni!\n");
    }

    return 0;
} {% endhighlight %}

Víte, co se stane, když program postavíte na samotných if? Tedy bez else? A co se stane, když vynecháte složené závorky mezi if-else? Do toho, vyzkoušejte si to, pokud si nejste jistí! 🙃
</details>
<br />

<!-- Example 2 -->

Podívejte se na následující program. Víte, jak by bylo možné ho přepsat, aby neobsahoval dvě if-podmínky vložené do sebe?
{% highlight c %}
#include <stdio.h>

int main(void)
{
    int cislo = 5;

    if (cislo >= 0)
    {
        if (cislo <= 10)
        {
            printf("Zadane cislo %d je v intervalu 0-10!\n", cislo);
        }
    }

    return 0;
} {% endhighlight %}

<!-- Example 2 solution -->

  <details>
    <summary><u>Řešení: </u></summary>
<br />
{% highlight c %}
#include <stdio.h>

int main(void)
{
    int cislo = 11;

    if (cislo >= 0 && cislo <= 10) {
        printf("Zadane cislo %d je v intervalu 0-10!\n", cislo);
    }

    return 0;
} {% endhighlight %}

Oba příklady nedělají nic jiného, než že nejdříve zkontrolují, zda je číslo větší nebo rovno 0 a potom, zda je menší nebo rovno 10. To lze udělat buď za pomocí dvou if-podmínek, nebo spojením logickým AND operátorem (&&).
  </details>
<br />

<!-- Example 3 -->

Poznáte, co je tady špatně?

{% highlight c %}
#include <stdio.h>

int main(void)
{
    int cislo = -1;

    if (cislo >= 0)
        printf("Cislo je vetsi nebo rovno 0!\n");
        if (cislo <= 10)
            printf("Cislo se nachazi v intervalu 0-10!\n");

    return 0;
} {% endhighlight %}

<!-- Example 3 solution -->

  <details>
    <summary><u>Řešení: </u></summary>
<br />
Hmm, výstup není takový, jaký se na první pohled zdá být. Tohle je příklad toho, jak se nemá používat odsazení a že je vhodné používat závorky na ohraničení bloků.

Správně odsazený program by mohl vypaddat následovně (nehleďte přitom na to, že je nyní krásně vidět, že nedělá to, co by měl):

<br />
<br />
{% highlight c %}
#include <stdio.h>

int main(void)
{
    int cislo = -1;

    if (cislo >= 0)
        printf("Cislo je vetsi nebo rovno 0!\n");

    if (cislo <= 10)
        printf("Cislo se nachazi v intervalu 0-10!\n");

    return 0;
} {% endhighlight %}

Program s použitím závorek na ohraničení bloku, bez vhodného odsazení:

<br />
<br />
{% highlight c %}
#include <stdio.h>

int main(void)
{
    int cislo = -1;

    if (cislo >= 0) 
    {
        printf("Cislo je vetsi nebo rovno 0!\n");
    }
       
        if (cislo <= 10)
        {
            printf("Cislo se nachazi v intervalu 0-10!\n");
        }

    return 0;
} {% endhighlight %}

Použití vhodného odsazení a složených závorek na ohraničení bloku, který náleží k if-podmínce:

<br />
<br />
{% highlight c %}
#include <stdio.h>

int main(void)
{
    int cislo = -1;
     
    if (cislo >= 0) 
    {
        printf("Cislo je vetsi nebo rovno 0!\n");
    }
        
    if (cislo <= 10)
    {
        printf("Cislo se nachazi v intervalu 0-10!\n");
    }

    return 0;
} {% endhighlight %}

Sami posuďte, které řešení se vám zdá nejčitelnější a na první pohled srozumitelné.


  </details>
<br />

<!-- Example 4 -->

Napadá vás, jak byste napsali program, který vám řekne, které ze dvou čísel je větší?

<!-- Example 4 solution -->

  <details>
    <summary><u>Řešení: </u></summary>
<br />
{% highlight c %}
#include <stdio.h>

int main(void)
{
    int x = 10;
    int y = 15;

    printf("Posuzovana cisla: %d a %d\n", x, y);
    printf("Max je: %d\n", x > y ? x : y);

    return 0;
} {% endhighlight %}

  </details>
<br />

## Smyčky

*\-TBD\-*
