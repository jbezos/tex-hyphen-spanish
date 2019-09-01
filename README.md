# tex-hyphen-spanish

**2019-08-30.** tools/eshyph-test.tex rewritten.

**2019-09-01.** La RAE cambió la norma tradicioanal sobre las haches.
  Comienzo la adaptación a la nueva norma (por absurda y inconveniente
  que me resulte). Más adelante daré un archivo de excepciones con los
  casos más importantes de la norma tradicional, para quienes prefieran
  seguir esta.

TeX hyphenation patterns for Spanish, v 4.7.

Patrones de división de palabras en español para TeX y otros sistemas
basados en el mismo algoritmo.

Todavía estoy trabajando en la puesta en marcha de este repositorio,
pero el archivo principal `tex/hyph-es.tex` está actualizado.

Los patrones se han creado mediante reglas y se han comprobado con un
diccionario de unas 700 000 palabras. La generación de patrones no se
hace con `patgen` porque este programa está pensado para ortografías
morfológicas. En particular, con `patgen` se da por hecho que los
sufijos y los interfijos son grupos para la división, lo cual no se
ajusta al español (solo los prefijos productivos y opcionalmente).

Uno de los principios básicos es el de dividir siempre correctamente,
aunque no incluya todas las posibles divisiones. Al menos en TeX, esta
estrategia es más segura que la de permitir divisiones inválidas.

* `doc/division.pdf` is a draft of an article (in Spanish) explaining
  the rules to be applied and how they are being translated into TeX in
  a unified set of patterns (somewhat outdated).
* `tools/eshyph-make.lua` generates the patterns, with `eshyph.src` for
  prefixes and special cases.
* `tools/eshyph-test.tex` makes a comparison of two hyphenation rules.
  Use `hyphen-es-base.tex` for more or less strict syllabic rules. It
  requires a file `spanish-words.txt` (not supplied, just a sample)
  with a list of word, one per line. You can (should) filter the words.
  Requires luatex 1.10.

Related project:
* https://github.com/hyphenation/tex-hyphen

See also:
* https://github.com/sbosio/rla-es/tree/master/separacion
* https://ctan.org/pkg/mkpattern