---
layout: post
title: Clojure Macros Examples
date: 2019-06-27
categories: blog
tags: clojure 
description: brief
---

  <div tabindex="-1" id="notebook" class="border-box-sizing">
    <div class="container" id="notebook-container">

<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h1 id="Clojure-Macro-examples">Clojure Macro examples<a class="anchor-link" href="#Clojure-Macro-examples">&#182;</a></h1>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="'-quote">' quote<a class="anchor-link" href="#'-quote">&#182;</a></h3>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[1]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-clojure"><pre><span></span><span class="p">(</span><span class="nf">clojure.repl/doc</span> <span class="nv">quote</span><span class="p">)</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

    <div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>-------------------------
quote
  (quote form)
Special Form
  Yields the unevaluated form.

  Please see http://clojure.org/special_forms#quote
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[2]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-clojure"><pre><span></span><span class="p">(</span><span class="nb">= </span><span class="ss">&#39;a</span> <span class="p">(</span><span class="k">quote </span><span class="nv">a</span><span class="p">))</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

    <div class="prompt output_prompt">Out[2]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>true</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[3]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-clojure"><pre><span></span><span class="o">&#39;</span><span class="p">(</span><span class="nb">+ </span><span class="nv">q</span> <span class="p">(</span><span class="nf">w</span><span class="p">)</span> <span class="nv">e</span><span class="p">)</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

    <div class="prompt output_prompt">Out[3]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>(+ q (w) e)</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[4]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-clojure"><pre><span></span><span class="p">(</span><span class="k">quote </span><span class="p">(</span><span class="nb">println </span><span class="s">&quot;foo&quot;</span><span class="p">))</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

    <div class="prompt output_prompt">Out[4]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>(println &#34;foo&#34;)</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[5]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-clojure"><pre><span></span><span class="p">(</span><span class="nf">clojure.repl/source</span> <span class="nv">quote</span><span class="p">)</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

    <div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>Source not found
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[6]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-clojure"><pre><span></span><span class="p">(</span><span class="nb">macroexpand </span><span class="o">&#39;&#39;</span><span class="p">(</span><span class="mi">1</span> <span class="mi">2</span> <span class="mi">3</span><span class="p">))</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

    <div class="prompt output_prompt">Out[6]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>(quote (1 2 3))</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="`-syntax-quote">` syntax quote<a class="anchor-link" href="#`-syntax-quote">&#182;</a></h3><p>quoting with</p>
<ul>
<li>namespace resolution</li>
<li>possibility to unquote</li>
</ul>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[7]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-clojure"><pre><span></span><span class="o">`</span><span class="nv">x</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

    <div class="prompt output_prompt">Out[7]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>user/x</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[8]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-clojure"><pre><span></span><span class="p">(</span><span class="nb">= </span><span class="o">`</span><span class="nv">x</span> <span class="p">(</span><span class="k">quote </span><span class="nv">x</span><span class="p">))</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

    <div class="prompt output_prompt">Out[8]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>false</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[9]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-clojure"><pre><span></span><span class="o">&#39;</span><span class="p">(</span><span class="nf">foo</span> <span class="nv">bar</span><span class="p">)</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

    <div class="prompt output_prompt">Out[9]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>(foo bar)</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[10]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-clojure"><pre><span></span><span class="o">`</span><span class="p">(</span><span class="nf">foo</span> <span class="nv">bar</span><span class="p">)</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

    <div class="prompt output_prompt">Out[10]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>(user/foo user/bar)</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="~-unquote">~ unquote<a class="anchor-link" href="#~-unquote">&#182;</a></h3><p>"evaluate this item in syntax quoted expression"</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[11]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-clojure"><pre><span></span><span class="p">(</span><span class="k">let </span><span class="p">[</span><span class="nv">x</span> <span class="mi">2</span><span class="p">]</span>
  <span class="o">`</span><span class="p">(</span><span class="mi">1</span> <span class="p">(</span><span class="nb">inc </span><span class="nv">x</span><span class="p">)</span> <span class="mi">3</span><span class="p">))</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

    <div class="prompt output_prompt">Out[11]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>(1 (clojure.core/inc user/x) 3)</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[12]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-clojure"><pre><span></span><span class="p">(</span><span class="k">let </span><span class="p">[</span><span class="nv">x</span> <span class="mi">2</span><span class="p">]</span>
  <span class="o">`</span><span class="p">(</span><span class="mi">1</span> <span class="o">~</span><span class="p">(</span><span class="nb">inc </span><span class="nv">x</span><span class="p">)</span> <span class="mi">3</span><span class="p">))</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

    <div class="prompt output_prompt">Out[12]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>(1 3 3)</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[13]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-clojure"><pre><span></span><span class="p">(</span><span class="k">let </span><span class="p">[</span><span class="nv">x</span> <span class="mi">2</span><span class="p">]</span>
  <span class="o">`</span><span class="p">(</span><span class="mi">1</span> <span class="p">(</span><span class="nb">inc </span><span class="o">~</span><span class="nv">x</span><span class="p">)</span> <span class="mi">3</span><span class="p">))</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

    <div class="prompt output_prompt">Out[13]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>(1 (clojure.core/inc 2) 3)</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[14]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-clojure"><pre><span></span><span class="o">`</span><span class="p">(</span><span class="nf">this</span> <span class="o">~</span><span class="p">(</span><span class="nb">symbol </span><span class="p">(</span><span class="nb">str </span><span class="s">&quot;i&quot;</span> <span class="s">&quot;s&quot;</span> <span class="sc">\-</span> <span class="s">&quot;cool&quot;</span><span class="p">)))</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

    <div class="prompt output_prompt">Out[14]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>(user/this is-cool)</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="~-and-unquote-not-the-same">~ and unquote not the same<a class="anchor-link" href="#~-and-unquote-not-the-same">&#182;</a></h3>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[15]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-clojure"><pre><span></span><span class="p">(</span><span class="nf">clojure.repl/source</span> <span class="nv">unquote</span><span class="p">)</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

    <div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>(def unquote)
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[16]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-clojure"><pre><span></span><span class="p">(</span><span class="nf">clojure.repl/doc</span> <span class="nv">unquote</span><span class="p">)</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

    <div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>-------------------------
clojure.core/unquote
  nil
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[17]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-clojure"><pre><span></span><span class="nv">unquote</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

    <div class="prompt output_prompt">Out[17]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>#object[clojure.lang.Var$Unbound 0x8d934d7 &#34;Unbound: #&#39;clojure.core/unquote&#34;]</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="~-works-simple-in-syntax-quoted-expression">~ works simple in syntax quoted expression<a class="anchor-link" href="#~-works-simple-in-syntax-quoted-expression">&#182;</a></h3>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[18]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-clojure"><pre><span></span><span class="o">`</span><span class="p">(</span><span class="nb">+ </span><span class="mi">1</span> <span class="p">(</span><span class="nf">unquote</span> <span class="ss">&#39;x</span><span class="p">))</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

    <div class="prompt output_prompt">Out[18]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>(clojure.core/+ 1 (clojure.core/unquote (quote user/x)))</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>!!! we want just evaluate 'x form ('x -&gt; x)</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[19]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-clojure"><pre><span></span><span class="o">`</span><span class="p">(</span><span class="nb">+ </span><span class="mi">1</span> <span class="o">~</span><span class="ss">&#39;x</span><span class="p">)</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

    <div class="prompt output_prompt">Out[19]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>(clojure.core/+ 1 x)</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="~@-unquote-splicing">~@ unquote-splicing<a class="anchor-link" href="#~@-unquote-splicing">&#182;</a></h3>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[20]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-clojure"><pre><span></span><span class="p">(</span><span class="k">let </span><span class="p">[</span><span class="nv">x</span> <span class="o">`</span><span class="p">(</span><span class="mi">2</span> <span class="mi">3</span><span class="p">)]</span> 
  <span class="o">`</span><span class="p">(</span><span class="mi">1</span> <span class="o">~</span><span class="nv">x</span><span class="p">))</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

    <div class="prompt output_prompt">Out[20]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>(1 (2 3))</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[21]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-clojure"><pre><span></span><span class="p">(</span><span class="k">let </span><span class="p">[</span><span class="nv">x</span> <span class="o">`</span><span class="p">(</span><span class="mi">2</span> <span class="mi">3</span><span class="p">)]</span> 
  <span class="o">`</span><span class="p">(</span><span class="mi">1</span> <span class="o">~@</span><span class="nv">x</span><span class="p">))</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

    <div class="prompt output_prompt">Out[21]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>(1 2 3)</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[22]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-clojure"><pre><span></span><span class="o">`</span><span class="p">(</span><span class="mi">1</span> <span class="mi">2</span> <span class="o">~</span><span class="p">(</span><span class="nb">list </span><span class="mi">3</span> <span class="mi">4</span><span class="p">))</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

    <div class="prompt output_prompt">Out[22]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>(1 2 (3 4))</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[23]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-clojure"><pre><span></span><span class="o">`</span><span class="p">(</span><span class="mi">1</span> <span class="mi">2</span> <span class="o">~@</span><span class="p">(</span><span class="nb">list </span><span class="mi">3</span> <span class="mi">4</span><span class="p">))</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

    <div class="prompt output_prompt">Out[23]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>(1 2 3 4)</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="Gensym">Gensym<a class="anchor-link" href="#Gensym">&#182;</a></h3><p>get cool name for var</p>
<ul>
<li>gensym function</li>
<li>var# inside syntax quote</li>
</ul>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[24]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-clojure"><pre><span></span><span class="o">`</span><span class="p">(</span><span class="k">let </span><span class="p">[</span><span class="nv">foo#</span> <span class="mi">1</span><span class="p">]</span> <span class="p">(</span><span class="nb">+ </span><span class="nv">foo#</span> <span class="mi">2</span><span class="p">))</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

    <div class="prompt output_prompt">Out[24]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>(clojure.core/let [foo__5377__auto__ 1] (clojure.core/+ foo__5377__auto__ 2))</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[25]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-clojure"><pre><span></span><span class="o">`</span><span class="nv">foo#</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

    <div class="prompt output_prompt">Out[25]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>foo__5381__auto__</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[26]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-clojure"><pre><span></span><span class="p">(</span><span class="nb">gensym </span><span class="s">&quot;foo&quot;</span><span class="p">)</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

    <div class="prompt output_prompt">Out[26]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>foo5386</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="Composition">Composition<a class="anchor-link" href="#Composition">&#182;</a></h3>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[27]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-clojure"><pre><span></span><span class="o">`</span><span class="p">[</span><span class="ss">:a</span> <span class="o">~</span><span class="p">(</span><span class="nb">+ </span><span class="mi">1</span> <span class="mi">1</span><span class="p">)</span> <span class="nv">c</span><span class="p">]</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

    <div class="prompt output_prompt">Out[27]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>[:a 2 user/c]</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[28]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-clojure"><pre><span></span><span class="o">`</span><span class="p">[</span><span class="ss">:a</span> <span class="o">~</span><span class="p">(</span><span class="nb">+ </span><span class="mi">1</span> <span class="mi">1</span><span class="p">)</span> <span class="o">~</span><span class="ss">&#39;c</span><span class="p">]</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

    <div class="prompt output_prompt">Out[28]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>[:a 2 c]</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[29]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-clojure"><pre><span></span><span class="o">`</span><span class="p">[</span><span class="ss">:a</span> <span class="o">~</span><span class="p">(</span><span class="nb">+ </span><span class="mi">1</span> <span class="mi">1</span><span class="p">)</span> <span class="o">~`</span><span class="nv">c</span><span class="p">]</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

    <div class="prompt output_prompt">Out[29]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>[:a 2 user/c]</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[30]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-clojure"><pre><span></span><span class="o">`</span><span class="p">{</span><span class="ss">:a</span> <span class="mi">1</span> <span class="ss">:b</span> <span class="o">&#39;~</span><span class="p">(</span><span class="nb">+ </span><span class="mi">1</span> <span class="mi">2</span><span class="p">)}</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

    <div class="prompt output_prompt">Out[30]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>{:b (quote 3), :a 1}</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[31]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-clojure"><pre><span></span><span class="o">`</span><span class="p">[</span><span class="ss">:a</span> <span class="o">~</span><span class="p">(</span><span class="nb">+ </span><span class="mi">1</span> <span class="mi">1</span><span class="p">)</span> <span class="o">&#39;~</span><span class="ss">&#39;c</span><span class="p">]</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

    <div class="prompt output_prompt">Out[31]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>[:a 2 (quote c)]</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[32]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-clojure"><pre><span></span><span class="o">`</span><span class="p">{</span><span class="ss">:a</span> <span class="mi">1</span> <span class="ss">:b</span> <span class="o">&#39;~@</span><span class="p">(</span><span class="nb">list </span><span class="mi">1</span> <span class="mi">2</span><span class="p">)}</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

    <div class="prompt output_prompt">Out[32]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>{:b (quote 1 2), :a 1}</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[33]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-clojure"><pre><span></span><span class="o">`</span><span class="p">(</span><span class="mi">1</span> <span class="o">`</span><span class="p">(</span><span class="mi">2</span> <span class="mi">3</span><span class="p">)</span> <span class="mi">4</span><span class="p">)</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

    <div class="prompt output_prompt">Out[33]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>(1 (clojure.core/seq (clojure.core/concat (clojure.core/list 2) (clojure.core/list 3))) 4)</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[34]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-clojure"><pre><span></span><span class="o">`</span><span class="p">(</span><span class="nb">list </span><span class="mi">1</span> <span class="o">`</span><span class="p">(</span><span class="mi">2</span> <span class="o">~</span><span class="p">(</span><span class="nb">- </span><span class="mi">9</span> <span class="mi">6</span><span class="p">))</span> <span class="mi">4</span><span class="p">)</span> <span class="c1">; twice syntax quoted and unquote</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

    <div class="prompt output_prompt">Out[34]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>(clojure.core/list 1 (clojure.core/seq (clojure.core/concat (clojure.core/list 2) (clojure.core/list (clojure.core/- 9 6)))) 4)</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[35]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-clojure"><pre><span></span><span class="o">`</span><span class="p">(</span><span class="nb">list </span><span class="mi">1</span> <span class="o">`</span><span class="p">(</span><span class="mi">2</span> <span class="o">~~</span><span class="p">(</span><span class="nb">- </span><span class="mi">9</span> <span class="mi">6</span><span class="p">))</span> <span class="mi">4</span><span class="p">)</span> <span class="c1">; twice syntax quoted and twice unquoted</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

    <div class="prompt output_prompt">Out[35]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>(clojure.core/list 1 (clojure.core/seq (clojure.core/concat (clojure.core/list 2) (clojure.core/list 3))) 4)</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[36]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-clojure"><pre><span></span><span class="p">(</span><span class="nb">eval </span><span class="o">`</span><span class="p">(</span><span class="nb">list </span><span class="mi">1</span> <span class="o">`</span><span class="p">(</span><span class="mi">2</span> <span class="o">~~</span><span class="p">(</span><span class="nb">- </span><span class="mi">9</span> <span class="mi">6</span><span class="p">))</span> <span class="mi">4</span><span class="p">))</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

    <div class="prompt output_prompt">Out[36]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>(1 (2 3) 4)</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[37]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-clojure"><pre><span></span><span class="p">(</span><span class="nb">= </span><span class="o">`&#39;~</span><span class="p">(</span><span class="nb">+ </span><span class="mi">2</span> <span class="mi">3</span><span class="p">)</span> <span class="o">`</span><span class="p">(</span><span class="k">quote </span><span class="o">~</span><span class="p">(</span><span class="nb">+ </span><span class="mi">2</span> <span class="mi">3</span><span class="p">))</span> <span class="p">(</span><span class="nb">list </span><span class="ss">&#39;quote</span> <span class="mi">5</span><span class="p">)</span> <span class="o">&#39;</span><span class="p">(</span><span class="k">quote </span><span class="mi">5</span><span class="p">))</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

    <div class="prompt output_prompt">Out[37]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>true</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="Macros-and-functions">Macros and functions<a class="anchor-link" href="#Macros-and-functions">&#182;</a></h2>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="Macros-not-evaluate-arguments">Macros not evaluate arguments<a class="anchor-link" href="#Macros-not-evaluate-arguments">&#182;</a></h3>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[38]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-clojure"><pre><span></span><span class="p">(</span><span class="kd">defmacro </span><span class="nv">simple-macro</span> <span class="p">[</span><span class="nv">a</span><span class="p">]</span> <span class="p">(</span><span class="k">do </span><span class="p">(</span><span class="nb">println </span><span class="s">&quot;arg: &quot;</span> <span class="nv">a</span><span class="p">)</span> <span class="nv">a</span><span class="p">))</span>
<span class="p">(</span><span class="kd">defn </span><span class="nv">simple-fun</span> <span class="p">[</span><span class="nv">a</span><span class="p">]</span> <span class="p">(</span><span class="k">do </span><span class="p">(</span><span class="nb">println </span><span class="s">&quot;arg: &quot;</span><span class="nv">a</span><span class="p">)</span> <span class="nv">a</span><span class="p">))</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

    <div class="prompt output_prompt">Out[38]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>#&#39;user/simple-fun</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[39]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-clojure"><pre><span></span><span class="p">(</span><span class="nf">simple-macro</span> <span class="s">&quot;test&quot;</span><span class="p">)</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

    <div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>arg:  test
</pre>
</div>
</div>

<div class="output_area">

    <div class="prompt output_prompt">Out[39]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>&#34;test&#34;</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[40]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-clojure"><pre><span></span><span class="p">(</span><span class="nf">simple-fun</span> <span class="s">&quot;test&quot;</span><span class="p">)</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

    <div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>arg:  test
</pre>
</div>
</div>

<div class="output_area">

    <div class="prompt output_prompt">Out[40]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>&#34;test&#34;</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="But">But<a class="anchor-link" href="#But">&#182;</a></h3>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[41]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-clojure"><pre><span></span><span class="p">(</span><span class="nf">simple-macro</span> <span class="p">(</span><span class="nb">+ </span><span class="mi">1</span> <span class="mi">2</span><span class="p">))</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

    <div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>arg:  (+ 1 2)
</pre>
</div>
</div>

<div class="output_area">

    <div class="prompt output_prompt">Out[41]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>3</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[42]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-clojure"><pre><span></span><span class="p">(</span><span class="nf">simple-fun</span> <span class="p">(</span><span class="nb">+ </span><span class="mi">1</span> <span class="mi">2</span><span class="p">))</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

    <div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>arg:  3
</pre>
</div>
</div>

<div class="output_area">

    <div class="prompt output_prompt">Out[42]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>3</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="Functions-evaluate-arguments-first-and-can't-see-(+-1-2)">Functions evaluate arguments first and can't see <em>(+ 1 2)</em><a class="anchor-link" href="#Functions-evaluate-arguments-first-and-can't-see-(+-1-2)">&#182;</a></h3><ul>
<li>Functions evaluate arguments <del>result</del></li>
<li>Macros   evaluate <del>arguments</del> result</li>
</ul>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">

<pre><code>(= (macroexpand-1 '(foo-m arg1 arg2 ...))
   (foo-f 'arg1 'arg2 '...))

(= (foo-m arg1 arg2 ...)
   (eval (foo-f 'arg1 'arg2 '...)))</code></pre>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[43]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-clojure"><pre><span></span><span class="p">(</span><span class="kd">defmacro </span><span class="nv">m-dec2</span> <span class="p">[</span><span class="nv">x</span><span class="p">]</span>
    <span class="o">`</span><span class="p">(</span><span class="nb">- </span><span class="o">~</span><span class="nv">x</span> <span class="mi">2</span><span class="p">))</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

    <div class="prompt output_prompt">Out[43]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>#&#39;user/m-dec2</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[44]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-clojure"><pre><span></span><span class="p">(</span><span class="nf">m-dec2</span> <span class="mi">5</span><span class="p">)</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

    <div class="prompt output_prompt">Out[44]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>3</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[45]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-clojure"><pre><span></span><span class="p">(</span><span class="nb">macroexpand-1 </span><span class="o">&#39;</span><span class="p">(</span><span class="nf">m-dec2</span> <span class="mi">5</span><span class="p">))</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

    <div class="prompt output_prompt">Out[45]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>(clojure.core/- 5 2)</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[46]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-clojure"><pre><span></span><span class="p">(</span><span class="kd">defn </span><span class="nv">f-dec2</span> <span class="p">[</span><span class="nv">x</span><span class="p">]</span> <span class="p">(</span><span class="nb">- </span><span class="nv">x</span> <span class="mi">2</span><span class="p">))</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

    <div class="prompt output_prompt">Out[46]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>#&#39;user/f-dec2</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[47]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-clojure"><pre><span></span><span class="p">(</span><span class="nf">f-dec2</span> <span class="mi">5</span><span class="p">)</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

    <div class="prompt output_prompt">Out[47]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>3</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[48]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-clojure"><pre><span></span><span class="p">(</span><span class="k">let </span><span class="p">[</span><span class="nv">y</span> <span class="mi">7</span><span class="p">]</span>
  <span class="p">(</span><span class="nb">= </span><span class="p">(</span><span class="nb">+ </span><span class="p">(</span><span class="nf">m-dec2</span> <span class="nv">y</span><span class="p">)</span> <span class="mi">6</span><span class="p">)</span>
     <span class="p">(</span><span class="nb">+ </span><span class="p">(</span><span class="nf">f-dec2</span> <span class="nv">y</span><span class="p">)</span> <span class="mi">6</span><span class="p">)))</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

    <div class="prompt output_prompt">Out[48]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>true</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[49]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-clojure"><pre><span></span><span class="p">(</span><span class="kd">defmacro </span><span class="nv">represent1</span> <span class="p">[</span><span class="nv">x</span><span class="p">]</span> <span class="o">`&#39;~</span><span class="nv">x</span><span class="p">)</span>
<span class="p">(</span><span class="nf">represent1</span> <span class="p">(</span><span class="nb">+ </span><span class="mi">3</span> <span class="mi">54</span><span class="p">))</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

    <div class="prompt output_prompt">Out[49]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>(+ 3 54)</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[50]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-clojure"><pre><span></span><span class="p">(</span><span class="kd">defmacro </span><span class="nv">represent2</span> <span class="p">[</span><span class="nv">x</span><span class="p">]</span> <span class="o">`</span><span class="p">(</span><span class="k">quote </span><span class="o">~</span><span class="nv">x</span><span class="p">))</span>
<span class="p">(</span><span class="nf">represent2</span> <span class="p">(</span><span class="nb">+ </span><span class="mi">3</span> <span class="mi">54</span><span class="p">))</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

    <div class="prompt output_prompt">Out[50]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>(+ 3 54)</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[51]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-clojure"><pre><span></span><span class="p">(</span><span class="kd">defmacro </span><span class="nv">represent-and-eval</span> <span class="p">[</span><span class="nv">x</span><span class="p">]</span> <span class="o">`</span><span class="p">(</span><span class="nb">str </span><span class="o">&#39;~</span><span class="nv">x</span> <span class="s">&quot; &gt;&gt; &quot;</span> <span class="o">~</span><span class="nv">x</span><span class="p">))</span>
<span class="p">(</span><span class="nf">represent-and-eval</span> <span class="p">(</span><span class="nb">+ </span><span class="mi">3</span> <span class="mi">54</span><span class="p">))</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

    <div class="prompt output_prompt">Out[51]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>&#34;(+ 3 54) &gt;&gt; 57&#34;</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="Inside-defmacro">Inside defmacro<a class="anchor-link" href="#Inside-defmacro">&#182;</a></h3><p><strong>&amp;form</strong>,
<strong>&amp;env</strong></p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[52]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-clojure"><pre><span></span><span class="p">(</span><span class="kd">defmacro </span><span class="nv">show-env</span> <span class="p">[]</span> <span class="p">(</span><span class="nb">println </span><span class="o">&amp;</span><span class="nv">env</span><span class="p">))</span>
<span class="p">(</span><span class="nf">show-env</span><span class="p">)</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

    <div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>nil
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[53]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-clojure"><pre><span></span><span class="p">(</span><span class="k">let </span><span class="p">[</span><span class="nv">band</span> <span class="s">&quot;zeppelin&quot;</span> <span class="nv">city</span> <span class="s">&quot;london&quot;</span><span class="p">]</span> <span class="p">(</span><span class="nf">show-env</span><span class="p">))</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

    <div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>{band #object[clojure.lang.Compiler$LocalBinding 0x5fb96ae6 clojure.lang.Compiler$LocalBinding@5fb96ae6], city #object[clojure.lang.Compiler$LocalBinding 0x74b88275 clojure.lang.Compiler$LocalBinding@74b88275]}
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[54]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-clojure"><pre><span></span><span class="p">(</span><span class="kd">defmacro </span><span class="nv">show-env-info</span> <span class="p">[]</span>
    <span class="p">(</span><span class="nb">println </span><span class="p">(</span><span class="nb">keys </span><span class="o">&amp;</span><span class="nv">env</span><span class="p">))</span> <span class="c1">; symbols</span>
    <span class="p">(</span><span class="nb">println </span><span class="p">(</span><span class="nb">map class </span><span class="p">(</span><span class="nb">keys </span><span class="o">&amp;</span><span class="nv">env</span><span class="p">)))</span>
    <span class="p">(</span><span class="nb">println </span><span class="p">(</span><span class="nb">map namespace </span><span class="p">(</span><span class="nb">keys </span><span class="o">&amp;</span><span class="nv">env</span><span class="p">)))</span>  <span class="c1">; don&#39;t have namespace</span>
    <span class="o">`</span><span class="p">(</span><span class="nb">println </span><span class="o">~@</span><span class="p">(</span><span class="nb">keys </span><span class="o">&amp;</span><span class="nv">env</span><span class="p">)))</span> <span class="c1">; have values</span>
<span class="p">(</span><span class="k">let </span><span class="p">[</span><span class="nv">band</span> <span class="s">&quot;zeppelin&quot;</span> <span class="nv">city</span> <span class="s">&quot;london&quot;</span><span class="p">]</span> <span class="p">(</span><span class="nf">show-env-info</span><span class="p">))</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

    <div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>(band city)
(clojure.lang.Symbol clojure.lang.Symbol)
(nil nil)
zeppelin london
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[55]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-clojure"><pre><span></span><span class="p">(</span><span class="kd">defmacro </span><span class="nv">show-form</span> <span class="p">[</span><span class="nv">a</span> <span class="nv">b</span><span class="p">]</span> <span class="p">(</span><span class="nb">println </span><span class="o">&amp;</span><span class="nv">form</span><span class="p">))</span> 
<span class="p">(</span><span class="nf">show-form</span> <span class="mi">50</span> <span class="nv">undefined-var</span><span class="p">)</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

    <div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>(show-form 50 undefined-var)
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[56]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-clojure"><pre><span></span><span class="p">(</span><span class="kd">defmacro </span><span class="nv">show-classes</span> <span class="p">[</span><span class="nv">a</span> <span class="nv">b</span><span class="p">]</span> <span class="p">(</span><span class="nb">println </span><span class="p">(</span><span class="nb">map </span><span class="p">(</span><span class="nf">juxt</span> <span class="nb">identity </span><span class="nv">class</span><span class="p">)</span> <span class="o">&amp;</span><span class="nv">form</span><span class="p">)))</span>
<span class="p">(</span><span class="nf">show-classes</span> <span class="mi">10</span> <span class="s">&quot;10&quot;</span><span class="p">)</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

    <div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>([show-classes clojure.lang.Symbol] [10 java.lang.Long] [10 java.lang.String])
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[57]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-clojure"><pre><span></span><span class="p">(</span><span class="kd">defmacro </span><span class="nv">show-meta</span> <span class="p">[</span><span class="nv">a</span> <span class="nv">b</span><span class="p">]</span> <span class="p">(</span><span class="nb">println </span><span class="p">(</span><span class="nb">meta </span><span class="o">&amp;</span><span class="nv">form</span><span class="p">)))</span>
<span class="p">(</span><span class="nf">show-meta</span> <span class="mi">10</span> <span class="s">&quot;10&quot;</span><span class="p">)</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

    <div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>{:line 2, :column 1}
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[58]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-clojure"><pre><span></span><span class="p">(</span><span class="nb">meta </span><span class="p">(</span><span class="nf">show-meta</span> <span class="mi">10</span> <span class="s">&quot;10&quot;</span><span class="p">))</span>
<span class="p">(</span><span class="nb">meta </span>
 <span class="p">(</span><span class="nf">show-meta</span> <span class="mi">10</span> <span class="s">&quot;10&quot;</span><span class="p">))</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

    <div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>{:line 1, :column 7}
{:line 3, :column 2}
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p><strong>Links</strong></p>
<ul>
<li><a href="https://clojuredocs.org/">https://clojuredocs.org/</a></li>
<li><a href="https://8thlight.com/blog/colin-jones/2012/05/22/quoting-without-confusion.html">https://8thlight.com/blog/colin-jones/2012/05/22/quoting-without-confusion.html</a></li>
<li><a href="https://blog.klipse.tech/clojure/2016/05/01/macro-tutorial-1.html">https://blog.klipse.tech/clojure/2016/05/01/macro-tutorial-1.html</a></li>
<li><a href="https://clojure.org/reference/reader">https://clojure.org/reference/reader</a></li>
<li><a href="https://clojure.org/reference/macros">https://clojure.org/reference/macros</a></li>
<li><a href="http://blog.jayfields.com/2011/02/clojure-and.html">http://blog.jayfields.com/2011/02/clojure-and.html</a></li>
</ul>

</div>
</div>
</div>
    </div>
  </div>