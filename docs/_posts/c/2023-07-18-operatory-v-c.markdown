---
layout: post
title:  "Operátory v C"
date:   2023-07-18 08:30:00 +0200
last_modified_at: 2023-07-18 08:30:00 +0200
category: Programovací jazyk C
description: Aritmetické a logické operátory v programovacím jazyce C.
---

[Předchozí]({% post_url c/2023-07-07-prvni-program-datove-typy-a-printf %})

Již jsme si pověděli, že proměnné jsou místa v paměti, která uchovávají jistou hodnotu. S touto hodnotou je pak možné dále pracovat, přičemž nám k tomu C nabízí různé tzv. operátory, které pracují na jedné nebo více proměnných.

## Aritmetické operátory

Aritmetické operátory v C zahrnují ze školy známé sčítání (+), odečítání (-), násobení (*) a dělení(/). Navíc tu máme modulo-operátor (%), inkrement (++) a dekrement (--). Modulo nám dá jako výsledek zbytek celočíselného dělení (např. 5 % 3 = 2), inkrement a dekrement pracují pouze s jednou proměnnou a zvětší/zmenší její hodnotu o 1.

Pozor, typ operandu určuje typ výsledku (operand je vstupní hodnota matematické operace, výše tedy 5 a 3)! Zkuste si zkopírovat následující řádky do nové main-funkce, program zkompilujte a spusťte. U celočíselného dělení se vše za desetinnou čárkou prostě zahodí. Je tedy třeba na toto myslet, protože kompilátor zde nenahlásí chybu, ale výsledek se může lišit od očekávaného.

{% highlight c %}
int operand = 1;
float result = operand / 2;
printf("%f\n", result);
{% endhighlight %}

Řešení přestavuje použití desetinného čísla na místě alespoň jednoho operandu. Následující úprava kódu ze shora ještě jednou zobrazí nesprávný výsledek a následně již výsledek takový, jaký bychom při dělení očekávali:

{% highlight c %}
int operand = 1;
float result = a / 2;
printf("%f\n", result);
result = operand / 2.0;
printf("%f\n", result);
{% endhighlight %}

Rovněž se zahodí vše za desetinnou čárkou, pokud byste takové číslo chtěli uložit do proměnné s celočíselným typem.

{% highlight c %}
int sum = 1 + 0.5;
printf("%d\n", sum);
int sum = 1 - 0.5;
printf("%d\n", sum);
{% endhighlight %}

### Závorky

Používejte závorky při programování a používání vícero operátorů najednou. Poslouží nejenom k tomu, že výsledek bude opravdu takový, jaký chcete, ale dopomůžou také k větší přehlednosti (myslete na již zmiňovanou čitelnost kódu). Závorky můžete i škatulkovat do sebe a pokud byste náhodou někde nějakou zapomněli, měla by vás na to upozornit buď IDE, nebo nejpozději compiler.

Příklad na použití závorek a počítání s desetinnou čárkou:

{% highlight c %}
int a = 2;
int b = 3;
float average = a + b / 2.0;
printf("%f\n", average);
average = (a + b) / 2.0;
printf("%f\n", average);
average = (a + b) / 2;
printf("%f\n", average);
{% endhighlight %}

### Inkrement a dekrement

Jak jsem již zmínila, C nabízí i tzv. unární operátory inkrementu a dekrementu. Tyto operátory nelze ovlivnit závorkami. Používají se jako prefix nebo postfix.

Jedná se vlastně o zkrácenou variantu přičítání +1:

{% highlight c %}
counter++;
{% endhighlight %}

Je to samé jako:

{% highlight c %}
counter = counter + 1;
{% endhighlight %}

Použití post- a prefixu ovlivňuje okamžik, kdy bude hodnota uložená v proměnné inkrementována, příp. dekrementována. Následující příklad má za úkol problematiku trochu přiblížit (zdá se mi jednodušší se na věc hned podívat takto, než to komplikovaně popisovat):

{% highlight c %}
#include <stdio.h>

int result = 0;
int number = 2;

int main(void)
{
  result = number++;
  printf("Post increment:	%d, %d \n", result, number);
  result = ++number;
  printf("Pre increment:	%d, %d \n", result, number);
  result = number--;
  printf("Post decrement:	%d, %d \n", result, number);
  result = --number;
  printf("Pre decrement:	%d, %d \n", result, number);
  return 0;
}
{% endhighlight %}

### Další zkratky

Programátoři jsou občas líní tvorové a co můžou zkrátit, to zkrátí. C proto nabízí i další zkratky (vedle inkrementu a dekrementu):
- +=, -=, *=, /=

{% highlight c %}
int number = 2;
number *= 3;
{% endhighlight %}

Je to samé jako:

{% highlight c %}
int number = 2;
number = number * 3;
{% endhighlight %}

Celé se to samozřejmě dá i kombinovat, např.:

{% highlight c %}
int a = 3;
int b = 4;
b *= --a;
{% endhighlight %}

## Porovnávací a logické operátory

### Operátory porovnání

Výsledkem použití logických operátorů je pravdivostní hodnota. V [minulém díle]({% post_url c/2023-07-07-prvni-program-datove-typy-a-printf %}#pravdivostní-hodnoty) jsme si již ukázali, že pravdivostní hodnota 0 představuje nepravdu, jakékoli jiné číslo pak pravdu. Srovnání, logické operace, dodají jako výsledek buď 0, nebo 1.

Ke srovnání dvou hodnot používáme následující operátory:
- ==
- !=
- &gt;
- <
- &gt;=
- <=

Častou chybou bývá záměna = (přiřazení) a == (rovnost)!

### Logické operátory

Mezi logické operátory řadíme:
- ! (NOT, výsledkem je hodnota opačná té, která je uložena v proměnné, na kterou aplikujeme NOT)
- && (AND, výsledkem je pravda, pokud všechny proměnné jsou pravdivé, nepravda v opačném případě)
- &#124;&#124; (OR, výsledkem je pravda, pokud alespoň jedna z proměnných je pravdivá)

## Kam dál?

*\-TBD\-*

**Pozor, jsem na dovolené. Nedokážu tedy zatím říct, co bude následovat, ani kdy to bude zveřejněné.**