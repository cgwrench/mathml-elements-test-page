---
layout: base.njk
title: MathML Core elements test page
description: Examples of the elements of MathML Core.
date: 2023-06-15
---
# MathML Core elements test page { #mathml-core-elements-test-page }

This page includes examples of most of
[the elements of MathML Core](https://www.w3.org/TR/mathml-core/#mathml-elements-and-attributes).

Many of the samples and descriptions included here are adapted from the
[MathML Core specification](https://www.w3.org/TR/mathml-core/).

This page was last updated on {{ page.date | date }}.

If you've got any questions or comments about this page, or if you've found a
mistake, please [get in touch](mailto:{{ site.author.email }}).

<style>
[hidden] {
    display: none !important;
}
</style>
<p id="browser-support-message" hidden>
    <strong>Note</strong>: MathML Core is <strong>not supported</strong> in
    your web browser. The examples on this page might not look right.
</p>
<script>
  var element = document.getElementById("browser-support-message");
  if (!mathMLSupported()) {
      element.hidden = false;
  }
  // Detect support for MathML, based on
  // https://github.com/mathjax/MathJax/issues/182
  function mathMLSupported() {
      const div = document.createElement("div");
      div.style.position = "absolute";
      div.style.visibility = "hidden";
      div.innerHTML = "<math><mfrac><mi>xx</mi><mi>yy</mi></mfrac></math>";
      document.body.appendChild(div);
      const isMathMLSupported = div.offsetHeight > div.offsetWidth;
      div.parentNode.removeChild(div);
      return isMathMLSupported;
  }
</script>

<!-- TODO write blog article on fallback for MathML

    - https://developer.mozilla.org/en-US/docs/Web/MathML/Authoring#fallback_for_browsers_without_mathml_support
    - https://masasakano.github.io/mathml_mathjax_js/#background
    - https://fred-wang.github.io/mathml.css/mathml.css
    - https://www.w3.org/TR/mathml-core/#user-agent-stylesheet

 -->

<!-- TODO fallback content, use MathJax, CSS?
        Only if there is actually a MathML element on the page, e.g.:
        const namespaceURI = "http://www.w3.org/1998/Math/MathML";
        if (document.body.getElementsByTagNameNS(namespaceURI, "math")[0]) {
            if (!mathMLSupported()) {
                const script = document.createElement("script");
                // TODO self-host this.
                script.src = "https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=MML_HTMLorMML";
                document.head.appendChild(script);
            }
        }
 -->
<!-- https://github.com/fred-wang/mathml-warning.js/blob/gh-pages/mpadded.js -->
<!-- TODO See https://fred-wang.github.io/mathml-warning.js/ -->
<!-- TODO See CSS in https://w3c.github.io/mathml-core/#the-top-level-math-element -->


[[toc]]


## The top-level `math` element

[math]: https://www.w3.org/TR/mathml-core/#dfn-math

The [`math`][math] element represents the root of each instance of MathML
markup within a <abbr title="HyperText Markup Language">HTML</abbr> document.
All the other elements of MathML must be descendants of this element.

Each of the examples below is contained within a `math` element.


## Token elements

[mtext]: https://www.w3.org/TR/mathml-core/#dfn-mtext
[mi]: https://www.w3.org/TR/mathml-core/#dfn-mi
[mn]: https://www.w3.org/TR/mathml-core/#dfn-mn
[mo]: https://www.w3.org/TR/mathml-core/#dfn-mo
[mspace]: https://www.w3.org/TR/mathml-core/#dfn-mspace
[ms]: https://www.w3.org/TR/mathml-core/#dfn-ms

### Text

The [`mtext`][mtext] element represents arbitrary text that should be rendered
as itself. This element is intended to denote commentary text.

In the following example, the `mtext` element is used to put conditional words
in a definition.

<math>
  <mi>y</mi>
  <mo>=</mo>
  <mrow>
    <msup>
      <mi>x</mi>
      <mn>2</mn>
    </msup>
    <mtext>&nbsp;if&nbsp;</mtext>
    <mrow>
      <mi>x</mi>
      <mo>≥</mo>
      <mn>1</mn>
    </mrow>
    <mtext>&nbsp;and&nbsp;</mtext>
    <mn>2</mn>
    <mtext>&nbsp;otherwise.</mtext>
  </mrow>
</math>

### Identifiers

The [`mi`][mi] element represents a symbolic name or arbitrary text that should
be rendered as an identifier. Identifiers can include variables, function
names, and symbolic constants.

In the following example, the `mi` element is used to render variables and
function names.

<math>
  <mi>cos</mi>
  <mo>,</mo>
  <mi>c</mi>
  <mo>,</mo>
  <mi mathvariant="normal">c</mi>
</math>

### Numbers

The [`mn`][mn] element represents a numeric literal or other data that should
be rendered as a numeric literal. 

In the following example, the `mn` element is used to write the mathematical
constant [π](https://en.wikipedia.org/wiki/Pi).

<math>
  <mn>3.141592653589793</mn>
</math>

### Operators

The [`mo`][mo] element represents an operator or other data, such as fences,
separators and accents, that should be rendered as an operator.

In the following example, the `mo` element is used to represent the summation
symbol.

<math>
  <mrow displaystyle="true">
  <munder>
    <mo>∑</mo>
    <mn>5</mn>
  </munder>
  <munder>
    <mo largeop="false">∑</mo>
    <mn>6</mn>
  </munder>
  </mrow>
  <mrow>
    <munder>
      <mo>∑</mo>
      <mn>5</mn>
    </munder>
    <munder>
      <mo movablelimits="false">∑</mo>
      <mn>7</mn>
    </munder>
  </mrow>
</math>

### Space

The [`mspace`][mspace] element represents a blank space.

In the following example, the `mspace` element is used to force spacing within
the formula (a 1px blue border is added to visualize the space).

<math>
  <mn>1</mn>
  <mspace width="1em" style="border-top: 1px solid blue"/> 
  <mfrac>
    <mrow>
      <mn>2</mn>
      <mspace depth="1em" style="border-left: 1px solid blue"/>
    </mrow>
    <mrow>
      <mn>3</mn>
      <mspace height="2em" style="border-left: 1px solid blue"/>
    </mrow>
  </mfrac>
</math>

### String literals

The [`ms`][ms] element represents string literals in expressions meant to be
interpreted by computer algebra systems or other systems containing programming
languages.

In the following example, the `ms` element is used to write a literal string of
characters.

<math>
  <mi>s</mi>
  <mo>=</mo>
  <ms>"hello world"</ms>
</math>


## Layout elements

[mrow]: https://www.w3.org/TR/mathml-core/#dfn-mrow
[mfrac]: https://www.w3.org/TR/mathml-core/#dfn-mfrac
[msqrt]: https://www.w3.org/TR/mathml-core/#dfn-msqrt
[mroot]: https://www.w3.org/TR/mathml-core/#dfn-mroot
[mstyle]: https://www.w3.org/TR/mathml-core/#dfn-mstyle
[merror]: https://www.w3.org/TR/mathml-core/#dfn-merror
[mpadded]: https://www.w3.org/TR/mathml-core/#dfn-mpadded
[mphantom]: https://www.w3.org/TR/mathml-core/#dfn-mphantom

### Group sub-expressions

The [`mrow`][mrow] element represents a group of sub-expressions.

In the following example, the `mrow` element is used to group a sum "1 + 2/3"
as a fraction numerator and to construct a fenced expression that is raised to
the power of 5.

<math>
  <msup>
    <mrow>
      <mo>(</mo>
      <mfrac>
        <mrow>
          <mn>1</mn>
          <mo>+</mo>
          <mfrac>
            <mn>2</mn>
            <mn>3</mn>
          </mfrac>
        </mrow>
        <mn>4</mn>
      </mfrac>
      <mo>)</mo>
    </mrow>
    <mn>5</mn>
  </msup>
</math>

### Fractions

The [`mfrac`][mfrac] element represents a fraction.

In the following example, the `mfrac` element is used to layout four fractions.

<math>
  <mn>0</mn>
  <mo>+</mo>
  <mfrac displaystyle="true">
    <mn>1</mn>
    <mn>2</mn>
  </mfrac>
  <mo>−</mo>
  <mfrac>
    <mn>1</mn>
    <mn>2</mn>
  </mfrac>
  <mo>+</mo>
  <mfrac linethickness="200%">
    <mn>1</mn>
    <mn>234</mn>
  </mfrac>
  <mo>−</mo>
  <mrow>
    <mo>(</mo>
    <mfrac linethickness="0">
      <mn>123</mn>
      <mn>4</mn>
    </mfrac>
    <mo>)</mo>
  </mrow>
</math>

### Radicals

The [`mroot`][mroot] element represents the
[*nth root*](https://en.wikipedia.org/wiki/Nth_root). The [`msqrt`][mroot]
element represents the
[*square root*](https://en.wikipedia.org/wiki/Square_root).

In the following example, the `mroot` element is used to layout a cube root,
amd the `msqrt` element is used to layout a square root.

<math>
  <mroot>
    <msqrt>
      <mfrac>
        <mn>1</mn>
        <mn>2</mn>
      </mfrac>
      <mo>+</mo>
      <mn>4</mn>
    </msqrt>
    <mn>3</mn>
  </mroot>
  <mo>+</mo>
  <mn>0</mn>
</math>

### Style change

The [`mstyle`][mstyle] element represents a change in style.

The <cite>MathML Core specification</cite> notes that:

> `<mstyle>` is implemented for compatibility with full MathML. Authors whose
> only target is MathML Core are encouraged to use CSS for styling.

<!-- No example yet -->

### Error message

The [`merror`][merror] element represents an error message.

In the following example, the `merror` element is used to indicate a parsing
error for some LaTeX-like input.

<math>
  <mfrac>
    <merror>
      <mtext>Syntax error: \frac{1}</mtext>
    </merror>
    <mn>3</mn>
  </mfrac>
</math>

### Adjust space around content

The [`mpadded`][mpadded] element represents space around it's content.

In the following example, the `mpadded` element is used to adjust spacing
around a fraction (a blue border is used to visualize the space). 

<math>
  <mrow>
    <mn>1</mn>
    <mpadded style="border: 1px solid blue;">
      <mfrac>
        <mn>23456</mn>
        <mn>78</mn>
      </mfrac>
    </mpadded>
    <mn>9</mn>
  </mrow>
  <mo>+</mo>
  <mrow>
    <mn>1</mn>
    <mpadded lspace="2em" voffset="-1em" height="1em" depth="3em" width="7em"
      style="border: 1px solid blue;">
      <mfrac>
        <mn>23456</mn>
        <mn>78</mn>
      </mfrac>
    </mpadded>
    <mn>9</mn>
  </mrow>
</math>

### Making sub-expressions invisible

The [`mphantom`][mphantom] element represents content that is invisible, but
which still affects layout.

The <cite>MathML Core specification</cite> notes that:

> `<mphantom>` is implemented for compatibility with full MathML. Authors whose
> only target is MathML Core are encouraged to use CSS for styling.

<!-- No example yet -->


## Scripts and limits

### Subscripts and superscripts

[msub]: https://www.w3.org/TR/mathml-core/#dfn-msub
[msubsup]: https://www.w3.org/TR/mathml-core/#dfn-msubsup
[msup]: https://www.w3.org/TR/mathml-core/#dfn-msup

The [`msub`][msub] and [`msup`][msup] elements represent subscripts and
superscripts respectively. The [`msubsup`][msubsup] element is used to layout
both a subscript and superscript.

In the following example, the `msub`, `msubsup` and `msup` elements are used to
layout subscripts and superscripts.

<math>
  <msub>
    <mn>1</mn>
    <mn>2</mn>
  </msub>
  <mo>+</mo>
  <msup>
    <mn>3</mn>
    <mn>4</mn>
  </msup>
  <mo>+</mo>
  <msubsup>
    <mn>5</mn>
    <mn>6</mn>
    <mn>7</mn>
  </msubsup>
</math>

### Underscripts and overscripts

[mover]: https://www.w3.org/TR/mathml-core/#dfn-mover
[munder]: https://www.w3.org/TR/mathml-core/#dfn-munder
[munderover]: https://www.w3.org/TR/mathml-core/#dfn-munderover

The [`mover`][mover] and [`munder`][munder] elements represent accents or
limits placed under and over a MathML expression respectively. 

The [`munderover`][msubsup] element is used to layout an accent or
limit place both under and over a MathML expression.

In the following example, the `mover`, `munder` and `munderover` elements are used
to layout under and over scripts.

<math>
  <munder>
    <mn>1</mn>
    <mn>2</mn>
  </munder>
  <mo>+</mo>
  <mover>
    <mn>3</mn>
    <mn>4</mn>
  </mover>
  <mo>+</mo>
  <munderover>
    <mn>5</mn>
    <mn>6</mn>
    <mn>7</mn>
  </munderover>
  <mo>+</mo>
  <munderover accent="true">
    <mn>8</mn>
    <mn>9</mn>
    <mn>10</mn>
  </munderover>
  <mo>+</mo>
  <munderover accentunder="true">
    <mn>11</mn>
    <mn>12</mn>
    <mn>13</mn>
  </munderover>
</math>

### Prescripts and tensor indices

[mmultiscripts]: https://www.w3.org/TR/mathml-core/#dfn-mmultiscripts
[mprescripts]: https://www.w3.org/TR/mathml-core/#dfn-mprescripts
[none]: https://www.w3.org/TR/mathml-core/#dfn-none

The [`mmultiscripts`][mmultiscripts] element represents presubscripts and
tensor notations, with hints represented by the [`mprescripts`][mprescripts]
and [`none`][none] elements. `none` represents an empty script.

In the following example, shows basic use of prescripts and postscripts, 
In the following example, the `mmultiscripts`, `mprescripts`, and `none`
elements are used to layout prescripts and postscripts.

<math>
  <mmultiscripts>
    <mn>1</mn>
    <mn>2</mn>
    <mn>3</mn>
    <none/>
    <mn>5</mn>
    <mprescripts/>
    <mn>6</mn>
    <none/>
    <mn>8</mn>
    <mn>9</mn>
  </mmultiscripts>
</math>


## Tabular math elements

[mtable]: https://www.w3.org/TR/mathml-core/#dfn-mtable
[mtr]: https://www.w3.org/TR/mathml-core/#dfn-mtr
[mtd]: https://www.w3.org/TR/mathml-core/#dfn-mtd

The [`mtable`][mtable] represents matrices, arrays and other table-like
mathematical notation. Rows in the table or matrix are represented by the
[`mtr`][mtr] element, and entries in the table or matrix are represented by the
[`mtd`][mtd] element.

This example uses the `mtable`, `mtr`, and `mtd` elements to layout a matrix.

<math>
  <mfrac>
    <mi>A</mi>
    <mn>2</mn>
  </mfrac>
  <mo>=</mo>
  <mrow>
    <mo>(</mo>
    <mtable>
      <mtr>
        <mtd><mn>1</mn></mtd>
        <mtd><mn>2</mn></mtd>
        <mtd><mn>3</mn></mtd>
      </mtr>
      <mtr>
        <mtd><mn>4</mn></mtd>
        <mtd><mn>5</mn></mtd>
        <mtd><mn>6</mn></mtd>
      </mtr>
      <mtr>
        <mtd><mn>7</mn></mtd>
        <mtd><mn>8</mn></mtd>
        <mtd><mn>9</mn></mtd>
      </mtr>
    </mtable>
    <mo>)</mo>
  </mrow>
</math>


## Enlivening expressions

[maction]: https://www.w3.org/TR/mathml-core/#dfn-maction

The [`maction`][maction] element provides a mechanism for binding actions to
expressions.

The <cite>MathML Core specification</cite> notes that:

> `<maction>` is implemented for compatibility with full MathML. Authors whose
> only target is MathML Core are encouraged to use other HTML, CSS and
> JavaScript mechanisms to implement custom actions.

<!-- No example yet -->


## Semantics and presentation

[semantics]: https://www.w3.org/TR/mathml-core/#semantics-and-presentation
[annotation]: https://www.w3.org/TR/mathml-core/#dfn-annotation
[annotation-xml]: https://www.w3.org/TR/mathml-core/#dfn-annotation-xml

The [`semantics`][semantics] element is a container element that associates
annotations, represented by the [`annotation`][annotation] and
[`annotation-xml`][annotation-xml] elements, with a MathML expression.

In the following example, the fraction "one half" is annotated with both a
textual (LaTeX) annotation and an XML annotation (content MathML). These
annotations are not rendered.

<math>
  <semantics>
    <mfrac>
      <mn>1</mn>
      <mn>2</mn>
    </mfrac>
    <annotation encoding="application/x-tex">\frac{1}{2}</annotation>
    <annotation-xml encoding="application/mathml-content+xml">
      <apply>
        <divide/>
        <cn>1</cn>
        <cn>2</cn>
      </apply>
    </annotation-xml>
  </semantics>
</math>
