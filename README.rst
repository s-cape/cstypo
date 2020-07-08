cstypo
======

Balíček pro zkrášlení českých textů aplikováním základních typografických
pravidel. Nesnaží se o pokrytí veškerých českých pravidel, spíše o aplikaci
základních a to hlavně těch, které jsou na webu nejvíce vidět.

.. image:: https://travis-ci.org/yetty/cstypo.png?branch=master
    :target: https://travis-ci.org/yetty/cstypo
.. image:: https://coveralls.io/repos/yetty/cstypo/badge.png?branch=master
    :target: https://coveralls.io/r/yetty/cstypo?branch=master
.. image:: https://pypip.in/v/cstypo/badge.png
    :target: https://crate.io/packages/cstypo/
.. image:: https://pypip.in/d/cstypo/badge.png
    :target: https://crate.io/packages/cstypo/

**Pozor!** Aplikování typografických pravidel na delší texty je poměrně výpočetně
náročná operace. Zvažte kešování těchto textů.

Instalace
---------

::

    pip install cstypo



API
-------

- ``cstypo.parser.TxtParser``

  Výchozí třída pro zpracování textu. Použití:

  ::

        parser = cstypo.parser.TxtParser(text)
        print parser.parse()       # zformátovaný text


  Je možné využít samostatně jednotlivé metody aplikující určitá pravidla:

  - ``cstypo.parser.TxtParser.parse_ellipsis``
  - ``cstypo.parser.TxtParser.parse_en_dash``
  - ``cstypo.parser.TxtParser.parse_em_dash``
  - ``cstypo.parser.TxtParser.parse_dates``
  - ``cstypo.parser.TxtParser.parse_arrows``
  - ``cstypo.parser.TxtParser.parse_plusminus``
  - ``cstypo.parser.TxtParser.parse_dimension``
  - ``cstypo.parser.TxtParser.parse_quotes``
  - ``cstypo.parser.TxtParser.parse_prepositions``
  - ``cstypo.parser.TxtParser.parse_last_short_word``
  - ``cstype.parser.TxtParser.parse_hyphen``

-   ``cstypo.parser.HtmlParser``

    Potomek třídy ``TxtParser``, který nejdříve escapuje veškeré HTML tagy,
    aplikuje typografická pravidla na získaný text a vratí tagy zpět.


Django
-------

Pro použití ve frameworku Django je připraven filtr typify v souboru ``cstags``.

Nejdříve je potřeba ``cstypo`` přidat do ``INSTALLED_APPS``

::

    INSTALLED_APPS = (
        ...
        'cstypo',
    )

Poté je možné začít v šablonách používat filtr.

::

    {% load cstags %}

    {{ text|typify }}                # zpracování obyčejného textu (výchozí)
    {{ text|typify:'txt' }}          # ...

    {{ text|typify:'html' }}         # zpracování html
    {{ text|typify:'html'|safe }}    # pro povolení vypsání je potřeba filter safe

    {% filter typify:'html' %}       # zpracování bloku
    <h1>{{ title }}</h1>
    <p>{{ text }}</p>
    {% endfilter %}


CLI
----

::

    cstypo

    Usage:
        cstypo [--type (txt|html)] <input>
        cstypo -h | --help
        cstypo -v | --version

    Options:
        -h --help               show this screen.
        -v --version            show version.
        --type                  type of parsed file (txt default).

Python 3
--------

Oproti `originální verzi <https://github.com/yetty/cstypo>`_ by balíček měl fungovat v Pythonu 3.
Z řetězců a regulárních výrazů je odstraněn prefix ``u`` resp. ``ur``.
