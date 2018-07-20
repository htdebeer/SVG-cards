SVG-cards
=========

A set of playing cards in SVG, now also with a rendering in PNG and
installable via NPM.

*   Version: 4.0.0
*   License: LGPL-2.1
*   Install via NPM: `npm install --save svg-cards` or just download the
[SVG](https://raw.githubusercontent.com/htdebeer/SVG-cards/master/svg-cards.svg)
file.

![Example use of SVG
Cards](https://raw.githubusercontent.com/htdebeer/SVG-cards/master/example_use.png)

This is a fork of [SVG-cards 2.0.1](http://svg-cards.sourceforge.net/), which
was created by [David Bellot](http://david.bellot.free.fr/). He writes in the
README of the original package:

> This is a set of playing cards made in pure SVG with all kings, queens,
> jacks, numbers, jokers and backs of cards. This set of SVG files is intended
> to be used in games, figures, illustrations, web sites as long as you
> provide the code source and the LGPL license (see the COPYING file).
> Although this is a free software, the license is the LGPL so you can use
> this set of cards even in a non-free software.
>
> The kings, queens and jacks are based on the French representation, because
> I find them beautiful. You can access to each either by rendering the file
> into a pixmap and clipping each card or by using their name with a DOM
> interface.

I agree with David that these cards are beautiful! I am grateful for his work
and that he published them under an open source license. However, while playing
around with the SVG file containing the cards, I found that using the cards in
SVG was not as straightforward as I would have liked. For example, I expected
the following line,

    <use xlink:href="svg-cards.svg#red_joker" x="40" y="12"/>

to put the red joker card with its top-left corner at (40, 12). It does not,
as it takes into account the place of the red joker in the SVG file: the card
top-left corner shows up at (207.575, 750.55).

In this fork I translated all cards to set their top-left corner at the origin
(0,0). After this change, the above USE element works as expected: it places
the red joker card's top-left corner at (40, 12).

For transforming the cards after using them, it is good to know that the
cards have the following natural dimensions:

- width: 169.075
- height: 244.64
- center: (+98.0375, +122.320)

Furthermore, to enable to create different stocks of cards, I set the color on
the back card to `inherit` instead of `#0062ff`. The color of the back card can
be changed by setting the fill on the USE-element. For example:

    <use xlink:href="svg-cards-indented.svg#back" x="150" y="10" fill="red"/>

The use of the cards is demonstrated in the
[`example_use.svg`](https://raw.githubusercontent.com/htdebeer/SVG-cards/master/example_use.svg) file.

The naming of the cards is *not* kept as in the original (because of SVG standard compliance):

Names are the following:

- joker_black and joker_red
- back
- {club,diamond,heart,spade}_{king,queen,jack}
- {club,diamond,heart,spade}_{1,2,3,4,5,6,7,8,9,10}

Examples:
- the ace of club is `club_1`
- the queen of diamond is `diamond_queen`

and so on…

When developing applications with these cards, I had also need of the card
circumference and the four suits. To that end I introduced the following
shapes you can USE:

- *card-base*, with the same dimensions as a card
- *suit-club*
- *suit-heart*
- *suit-diamond*
- *suit-spade*

The suits have the following dimensions:

- width: 15.42
- height: 15.88
- center: (7.71, 7.94)

A while later I also discovered that the back card is too complex to be
rendered swiftly in my web browsers. When rendering a deck of 52 cards facing
down, it took almost 2 seconds to render about 50,000 elements in the DOM. To
overcome these issues, I created an alternative back by removing all the
frills from the original
one. You can USE it via:

- *alternate-back*

I have also added a nicely formatted SVG file, `svg-cards-indented.svg`, which
makes the SVG file easier to inspect using a text editor. Converting from
indented to unindented version goes via
[xmllint](http://xmlsoft.org/xmllint.html): `xmllint --noblanks
svg-cards-indented.svg > svg-cards.svg`

To automatically convert these SVG files to PNG I developed a separate
project: [svg-cards-to-png](https://github.com/htdebeer/svg-cards-to-png). For
convenience, PNG files are included in this repository in the `png`
subdirectory. There are two directories, `png/1x` and `png/2x`, with PNG
files of the SVG cards with, respectively, their natural dimensions and twice
their natural dimensions. Furthermore, 16 different colored back cards are
included as well.

[desphilboy](https://github.com/desphilboy) has made this project into an
[NPM](https://www.npmjs.com/) package to make it easier for web developers to
use it in their projects. Now it can be installed and used like other
dependencies: `npm install --save svg-cards`.

In July 2018, [Thomas Linard](https://github.com/thlinard) improved the SVG
files by making them compliant with the [SVG
specification](https://www.w3.org/TR/SVG/).
