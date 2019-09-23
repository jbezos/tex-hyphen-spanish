# tex-hyphen-spanish

TeX hyphenation patterns for Spanish, v 5.0, development releases. They
are based on rules, with the help of a diccionary of about 700 000
words, created over 20 years and still expanding,. This project is
related to tex-hyphen, the collection of hyphenation patterns for TeX
and other systems based on the same algorithm (Mozilla, Kindle, FOP,
etc.):

https://github.com/hyphenation/tex-hyphen

Patrones de división de palabras en español para TeX y otros sistemas
basados en el mismo algoritmo.

**2019-08-30.** tools/eshyph-test.tex rewritten.

**2019-09-01.** La RAE cambió la norma tradicional sobre las haches,
  y la actual básicamente consiste en que no se divide casi nunca ante
  ella (es decir, «chihuahua» o «menhir» son palabras indivisibles).
  Comienzo la adaptación a la nueva norma (por inconveniente
  que pueda resultar). 

**2019-09-04.** Comienzo a flexibilizar las particiones, ya que ahora,
  en cierto número de casos, se pueden encontrar series de 6 caracteres
  o más sin división («postureo» o «postillar», por ejemplo), lo que no
  parece razonable desde el punto de vista práctico. Véase la
  explicación más abajo sobre los principios de la división.

### Contenido

* `tex/eshyphexh.tex` provides exceptions for traditional rules with adh,
  exh, and a few more.
* `doc/division.pdf` is a draft of an article (in Spanish) explaining
  the rules to be applied and how they are being translated into TeX in
  a unified set of patterns (somewhat outdated).
* `tools/eshyph-make.lua` generates the patterns, with `eshyph.src` for
  prefixes and special cases.
* `tools/eshyph-test.tex` makes a comparison of two hyphenation rules.
  Use `hyphen-es-base.tex` for more or less strict syllabic rules. It
  requires a file `spanish-words.txt` with a list of words (a sample
  with about 56 000 entries is supplied), one per line. You can
  (should) filter the words. Requires luatex 1.10.

The sources for the word list include
[ispell](https://www.cs.hmc.edu/~geoff/ispell.html),
[DRAE-DLE](https://dle.rae.es/), Moliner,
[Fundéu](https://www.fundeu.es/) and personal tools for web crawling,
with manual selection of terms.

### Principios básicos de la división

Uno de los principios básicos es el de dividir siempre correctamente,
aunque no incluya todas las posibles divisiones. Al menos en TeX, esta
estrategia es más segura que la de permitir divisiones inválidas.

No obstante, aunque siempre será mejor «porta-aeronave» (que es como, de
hecho, se divide) que «portaae-ronave» (que es el criterio puramente
«silábico»), este último no es de por sí incorrecto. Lo mismo se puede
decir, por ejemplo, de «ex-enemigo» frente a «exe-nemigo». (Aunque de
momento no hay nada implementado al respecto, es interesante señalar
que con luatex es posible asignar diferentes penalizaciones o pesos en
casos así.)

### Generación de los patrones

Los patrones se han creado mediante reglas y se han comprobado con un
diccionario de unas 700 000 palabras. La generación de patrones no se
hace con `patgen` porque este programa está pensado para ortografías
morfológicas. En particular, con `patgen` se da por hecho que los
sufijos y los interfijos son grupos para la división, lo cual no se
ajusta al español (solo los prefijos productivos y opcionalmente).

Por otra parte, necesita un diccionario con un elevado número de
palabras ya divididas: pensemos que el inglés, que no tiene
conjugaciones verbales, empleó 150 000 en sus primeras fases; para el
checo se llegó a tomar como punto de partida ¡5 000 000!, aunque
posteriormente se filtró con ciertas reglas para reducirlo a algo menos
de 400 000. Tengo mis serias dudas de que se pueda conseguir nada con
`patgen` que sea mínimamente aceptable con menos 200 000 palabras, y
diccionarios así no existen en español, salvo algunos que se han
generado automáticamente con reglas, por lo que su utilidad es escasa.

En este momento, el archivo cuenta con unos 4600 patrones. Es posible
que haya algunas redundancias, pero no tienen que ser muchas, y en
cualquier caso una redundancia correcta no debe ser un problema. Como
comparación, el ruso tiene unos 7200, y el francés unos 1400.

No es el propósito de estos patrones el purismo. Por ello, la lista de
palabras incluye cierto número de extranjerismos de uso común (e
incluso algún que otro error frecuente, como «paraolímpico»), para
tenerlos en cuenta.

See also:
* https://github.com/sbosio/rla-es/tree/master/separacion
* https://ctan.org/pkg/mkpattern