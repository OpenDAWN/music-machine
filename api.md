## Classes
<dl>
<dt><a href="#GuidedMusicMachine">GuidedMusicMachine</a></dt>
<dd></dd>
<dt><a href="#TreeNode">TreeNode</a></dt>
<dd></dd>
<dt><a href="#MusicMachine">MusicMachine</a></dt>
<dd></dd>
</dl>
## Functions
<dl>
<dt><a href="#allowedIntervalQualities">allowedIntervalQualities(...quality)</a> ⇒ <code><a href="#filter">filter</a></code></dt>
<dd><p>filter generator that returns a filter which restricts the maximum
                            length of the construction</p>
</dd>
<dt><a href="#maxLength">maxLength(max)</a> ⇒ <code><a href="#filter">filter</a></code></dt>
<dd><p>filter generator that returns a filter which restricts the maximum
                            length of the construction</p>
</dd>
<dt><a href="#maxRange">maxRange(maxIntervalSize)</a> ⇒ <code><a href="#filter">filter</a></code></dt>
<dd><p>filter generator that returns a filter which restricts the maximum
                            range of the construction</p>
</dd>
<dt><a href="#filter">filter(choices, construction)</a> ⇒ <code>Array.&lt;string&gt;</code></dt>
<dd><p>a user defined function that <a href="#GuidedMusicMachine+choices">choices</a>
will be passed through, filtering out certain choices.</p>
</dd>
<dt><a href="#plusIntervalInKey">plusIntervalInKey(key, sciPitch, intervalSize)</a> ⇒ <code>String</code> | <code>function</code></dt>
<dd><p>helper function that finds the result of adding a generic interval to a given pitch
in the context of a key</p>
<p>Optionally, exclude the intervalSize parameter and get back a curried function
with the key and startPitch set as defaults.</p>
</dd>
<dt><a href="#sortPitches">sortPitches(pitches)</a> ⇒ <code>Array.&lt;string&gt;</code></dt>
<dd><p>helper function to sort an array of pitches from lowest to highest</p>
</dd>
</dl>
## Typedefs
<dl>
<dt><a href="#SymbolChain">SymbolChain</a> : <code>string</code></dt>
<dd><p>a string of one or more symbol names seperated by whitespace</p>
</dd>
<dt><a href="#MusicGrammar">MusicGrammar</a> : <code>Object</code></dt>
<dd><p>a user defined context-free grammar formatted as an object consisting of key-value pairs,
with each <a href="https://github.com/jrleszcz/grammar-graph#non-terminal-symbols">non-terminal symbol</a>
pointing to an array of one or more <a href="https://github.com/jrleszcz/grammar-graph#symbol-chains">symbol chains</a>
choices for this non-terminal. All <a href="https://github.com/jrleszcz/grammar-graph#terminal-symbols">terminals</a>
must be positive or negative numbers, representing musical intervals. Said another way, anything that is not
a number must have its own definition.</p>
</dd>
</dl>
<a name="GuidedMusicMachine"></a>
## GuidedMusicMachine
**Kind**: global class  

* [GuidedMusicMachine](#GuidedMusicMachine)
  * [new GuidedMusicMachine(guide, [key], [initialScaleDegrees])](#new_GuidedMusicMachine_new)
  * [.addFilter(filter)](#GuidedMusicMachine+addFilter)
  * [.construction()](#GuidedMusicMachine+construction) ⇒ <code>Array.&lt;string&gt;</code>
  * [.tonic()](#GuidedMusicMachine+tonic)
  * [.isComplete()](#GuidedMusicMachine+isComplete) ⇒ <code>boolean</code>
  * [.choose(pitchChoice)](#GuidedMusicMachine+choose)
  * [.pop()](#GuidedMusicMachine+pop) ⇒ <code>string</code>
  * [.choices([nDeep])](#GuidedMusicMachine+choices) ⇒ <code>Array.&lt;string&gt;</code>
  * [.constructs()](#GuidedMusicMachine+constructs) ⇒ <code>Array.&lt;string&gt;</code>

<a name="new_GuidedMusicMachine_new"></a>
### new GuidedMusicMachine(guide, [key], [initialScaleDegrees])
step-by-step construction of music from a predefined Music Machine


| Param | Type | Default | Description |
| --- | --- | --- | --- |
| guide | <code>GuidedDecisionGraph</code> |  | a Guided Decision Graph. See: [GuidedDecisionGraph](https://github.com/jrleszcz/grammar-graph/blob/master/api.md#GuidedDecisionGraph) |
| [key] | <code>Key</code> | <code>&#x27;C major&#x27;</code> | the key in which to apply the generic interval. See [Key](https://github.com/jrleszcz/nmusic/blob/master/api.md#Key) |
| [initialScaleDegrees] | <code>Array.&lt;number&gt;</code> | <code>[1]</code> | the scale degree(s) which constructions can start on |

<a name="GuidedMusicMachine+addFilter"></a>
### guidedMusicMachine.addFilter(filter)
add a filter to the guide that will filter chioces based on the construction

**Kind**: instance method of <code>[GuidedMusicMachine](#GuidedMusicMachine)</code>  

| Param | Type | Description |
| --- | --- | --- |
| filter | <code>[filter](#filter)</code> | a callback filter function that returns valid choices |

<a name="GuidedMusicMachine+construction"></a>
### guidedMusicMachine.construction() ⇒ <code>Array.&lt;string&gt;</code>
the current construction

**Kind**: instance method of <code>[GuidedMusicMachine](#GuidedMusicMachine)</code>  
**Returns**: <code>Array.&lt;string&gt;</code> - a terminal symbol chain  
<a name="GuidedMusicMachine+tonic"></a>
### guidedMusicMachine.tonic()
the tonic note of this key
@ returns {string} a pitch class string

**Kind**: instance method of <code>[GuidedMusicMachine](#GuidedMusicMachine)</code>  
<a name="GuidedMusicMachine+isComplete"></a>
### guidedMusicMachine.isComplete() ⇒ <code>boolean</code>
is the current construction a valid, complete construction from the starting
nonterminal? ie, does the construction end in epsilon?

**Kind**: instance method of <code>[GuidedMusicMachine](#GuidedMusicMachine)</code>  
**Returns**: <code>boolean</code> - is the construction complete  
<a name="GuidedMusicMachine+choose"></a>
### guidedMusicMachine.choose(pitchChoice)
adds the given pitch to the construction

**Kind**: instance method of <code>[GuidedMusicMachine](#GuidedMusicMachine)</code>  
**Throws**:

- throws an error if pitchChoice is not in the
     current set of [choices](#GuidedMusicMachine+choices)


| Param | Type | Description |
| --- | --- | --- |
| pitchChoice | <code>string</code> &#124; <code>Array.&lt;string&gt;</code> | a pitch string in the current set of next choices or an array of choices to be applied sequentially |

<a name="GuidedMusicMachine+pop"></a>
### guidedMusicMachine.pop() ⇒ <code>string</code>
pop the last choice off the construction

**Kind**: instance method of <code>[GuidedMusicMachine](#GuidedMusicMachine)</code>  
**Returns**: <code>string</code> - the last pitch string of the construction that was
submitted through [choose](#GuidedMusicMachine+choose)  
**Throws**:

- throws an error if called when construction is empty

<a name="GuidedMusicMachine+choices"></a>
### guidedMusicMachine.choices([nDeep]) ⇒ <code>Array.&lt;string&gt;</code>
returns an array of all possible next pitches, or an array of
nDeep [TreeNodes](#TreeNode).

**Kind**: instance method of <code>[GuidedMusicMachine](#GuidedMusicMachine)</code>  
**Returns**: <code>Array.&lt;string&gt;</code> - if nDeep=1, an array of pitch strings, else
an array of nDeep [TreeNodes](#TreeNode)  

| Param | Type | Default | Description |
| --- | --- | --- | --- |
| [nDeep] | <code>number</code> | <code>1</code> | will search for nDeep possible choices |

<a name="GuidedMusicMachine+constructs"></a>
### guidedMusicMachine.constructs() ⇒ <code>Array.&lt;string&gt;</code>
Peak inside the machine and get a list of possible constructions
at this point. Constructions are returned in the terms of the grammar,
not as notes.

**Kind**: instance method of <code>[GuidedMusicMachine](#GuidedMusicMachine)</code>  
**Returns**: <code>Array.&lt;string&gt;</code> - a list of possible constructions  
**Example**  
```js
guide.constructs()  => ['2 3 -2 JupiterTheme -5 InfinitePhrase']
```
<a name="TreeNode"></a>
## TreeNode
**Kind**: global class  
**See**: TreeNode returned from
[GuidedDecisionGraph.choices](GuidedDecisionGraph#choices)  
**Properties**

| Name | Type | Description |
| --- | --- | --- |
| val |  | any value |
| next | <code>[Array.&lt;TreeNode&gt;](#TreeNode)</code> | a list of TreeNodes this node links to |

<a name="new_TreeNode_new"></a>
### new TreeNode(dg)
Tree nodes to return decision trees from choices


| Param | Type | Description |
| --- | --- | --- |
| dg | <code>DecisionGraph</code> | a Decision Graph that defines a grammar |

<a name="MusicMachine"></a>
## MusicMachine
**Kind**: global class  

* [MusicMachine](#MusicMachine)
  * [new MusicMachine(grammar, startSymbol, [initialScaleDegrees])](#new_MusicMachine_new)
  * _instance_
    * [.vertices()](#MusicMachine+vertices) ⇒ <code>Array.&lt;string&gt;</code>
    * [.addFilter(filter)](#MusicMachine+addFilter)
    * [.createGuide([key])](#MusicMachine+createGuide) ⇒ <code>[GuidedMusicMachine](#GuidedMusicMachine)</code>
  * _static_
    * [.filter](#MusicMachine.filter)
      * [.maxRange](#MusicMachine.filter.maxRange) ⇒ <code>[filter](#filter)</code>
      * [.maxLength(max)](#MusicMachine.filter.maxLength) ⇒ <code>[filter](#filter)</code>
      * [.allowedIntervalQualities(...quality)](#MusicMachine.filter.allowedIntervalQualities) ⇒ <code>[filter](#filter)</code>

<a name="new_MusicMachine_new"></a>
### new MusicMachine(grammar, startSymbol, [initialScaleDegrees])
creates a new MusicMachine which can generate Guides for music construction.


| Param | Type | Default | Description |
| --- | --- | --- | --- |
| grammar | <code>[MusicGrammar](#MusicGrammar)</code> |  | an object representing a musical grammar. |
| startSymbol | <code>string</code> |  | the symbol at which to start constructions |
| [initialScaleDegrees] | <code>Array.&lt;number&gt;</code> | <code>[1]</code> | the scale degree(s) which constructions can start on |

<a name="MusicMachine+vertices"></a>
### musicMachine.vertices() ⇒ <code>Array.&lt;string&gt;</code>
get an array of vertex names in the graph

**Kind**: instance method of <code>[MusicMachine](#MusicMachine)</code>  
**Returns**: <code>Array.&lt;string&gt;</code> - the vertex names in this graph  
<a name="MusicMachine+addFilter"></a>
### musicMachine.addFilter(filter)
add a filter to the guide that will filter chioces based on the construction

**Kind**: instance method of <code>[MusicMachine](#MusicMachine)</code>  

| Param | Type | Description |
| --- | --- | --- |
| filter | <code>[filter](#filter)</code> | a callback filter function that returns valid choices |

<a name="MusicMachine+createGuide"></a>
### musicMachine.createGuide([key]) ⇒ <code>[GuidedMusicMachine](#GuidedMusicMachine)</code>
get a new GuidedMusicMachine using this decision graph

**Kind**: instance method of <code>[MusicMachine](#MusicMachine)</code>  
**Returns**: <code>[GuidedMusicMachine](#GuidedMusicMachine)</code> - a new guide from the provided start point  
**See**: [GuidedMusicMachine](#GuidedMusicMachine) for the methods available on the Guide  

| Param | Type | Default | Description |
| --- | --- | --- | --- |
| [key] | <code>string</code> | <code>&quot;&#x27;C major&#x27;&quot;</code> | the key in which to apply the generic interval. Must be a valid pitch string and mode name seperated by whitespace such as 'Bb minor'. |

<a name="MusicMachine.filter"></a>
### MusicMachine.filter
a collection of filter generators that generate filter callback functions
intended to be passed to [addFilter](#MusicMachine+addFilter) or [addFilter](#GuidedMusicMachine+addFilter)

**Kind**: static property of <code>[MusicMachine](#MusicMachine)</code>  

  * [.filter](#MusicMachine.filter)
    * [.maxRange](#MusicMachine.filter.maxRange) ⇒ <code>[filter](#filter)</code>
    * [.maxLength(max)](#MusicMachine.filter.maxLength) ⇒ <code>[filter](#filter)</code>
    * [.allowedIntervalQualities(...quality)](#MusicMachine.filter.allowedIntervalQualities) ⇒ <code>[filter](#filter)</code>

<a name="MusicMachine.filter.maxRange"></a>
#### filter.maxRange ⇒ <code>[filter](#filter)</code>
filter generator that returns a filter which restricts the maximum
                            range of the construction

**Kind**: static property of <code>[filter](#MusicMachine.filter)</code>  
**Returns**: <code>[filter](#filter)</code> - a filter that limits the range of the construction  
**See**: [maxRange](#maxRange)  

| Param | Type | Description |
| --- | --- | --- |
| maxIntervalSize | <code>number</code> | the maximum range (inclusive) of the                             desired construction |

<a name="MusicMachine.filter.maxLength"></a>
#### filter.maxLength(max) ⇒ <code>[filter](#filter)</code>
limit the length of a construction

**Kind**: static method of <code>[filter](#MusicMachine.filter)</code>  
**Returns**: <code>[filter](#filter)</code> - a filter that limits the length of the construction  
**See**: [maxLength](#maxLength)  

| Param | Type | Description |
| --- | --- | --- |
| max | <code>number</code> | the maximum length (inclusive) of the                             desired construction |

<a name="MusicMachine.filter.allowedIntervalQualities"></a>
#### filter.allowedIntervalQualities(...quality) ⇒ <code>[filter](#filter)</code>
only allow certain interval qualities

**Kind**: static method of <code>[filter](#MusicMachine.filter)</code>  
**Returns**: <code>[filter](#filter)</code> - a filter that only allows the specified intervals  
**See**: [allowedIntervalQualities](#allowedIntervalQualities)  

| Param | Type | Description |
| --- | --- | --- |
| ...quality | <code>char</code> | characters representing quality. 'm' = minor, 'M' = Major, 'P' = Perfect, 'd' = diminished, 'A' = augmented |

<a name="allowedIntervalQualities"></a>
## allowedIntervalQualities(...quality) ⇒ <code>[filter](#filter)</code>
filter generator that returns a filter which restricts the maximum
                            length of the construction

**Kind**: global function  
**Returns**: <code>[filter](#filter)</code> - a filter that limits the length of the construction  
**Throws**:

- Will throw an error if an argument is not a valid quality character


| Param | Type | Description |
| --- | --- | --- |
| ...quality | <code>char</code> | characters representing quality. 'm' = minor, 'M' = Major, 'P' = Perfect, 'd' = diminished, 'A' = augmented |

<a name="maxLength"></a>
## maxLength(max) ⇒ <code>[filter](#filter)</code>
filter generator that returns a filter which restricts the maximum
                            length of the construction

**Kind**: global function  
**Returns**: <code>[filter](#filter)</code> - a filter that limits the length of the construction  

| Param | Type | Description |
| --- | --- | --- |
| max | <code>number</code> | the maximum length (inclusive) of the                             desired construction |

<a name="maxRange"></a>
## maxRange(maxIntervalSize) ⇒ <code>[filter](#filter)</code>
filter generator that returns a filter which restricts the maximum
                            range of the construction

**Kind**: global function  
**Returns**: <code>[filter](#filter)</code> - a filter that limits the range of the construction  

| Param | Type | Description |
| --- | --- | --- |
| maxIntervalSize | <code>number</code> | the maximum range (inclusive) of the                             desired construction |

<a name="filter"></a>
## filter(choices, construction) ⇒ <code>Array.&lt;string&gt;</code>
a user defined function that [choices](#GuidedMusicMachine+choices)
will be passed through, filtering out certain choices.

**Kind**: global function  
**Returns**: <code>Array.&lt;string&gt;</code> - the choices with notes filtered out  

| Param | Type | Description |
| --- | --- | --- |
| choices | <code>Array.&lt;string&gt;</code> | the current choices as returned    by [choices](#GuidedMusicMachine+choices) |
| construction | <code>Array.&lt;string&gt;</code> | the curent constrution as returned    by [construction](#GuidedMusicMachine+construction) |

<a name="plusIntervalInKey"></a>
## plusIntervalInKey(key, sciPitch, intervalSize) ⇒ <code>String</code> &#124; <code>function</code>
helper function that finds the result of adding a generic interval to a given pitch
in the context of a key

Optionally, exclude the intervalSize parameter and get back a curried function
with the key and startPitch set as defaults.

**Kind**: global function  
**Returns**: <code>String</code> &#124; <code>function</code> - the resulting pitch string, or if given only one argument,
returns a function with the given argument set as a default.  

| Param | Type | Description |
| --- | --- | --- |
| key | <code>string</code> | the key in which to apply the generic interval. Must be a valid pitch string and mode name seperated by whitespace such as 'Bb major' or 'Db dorian' |
| sciPitch | <code>string</code> | a pitch in scientific pitch notation. |
| intervalSize | <code>number</code> | an interval string or number with or without quality. If quality is not provided, accidentals on given pitch will be ignored. |

<a name="sortPitches"></a>
## sortPitches(pitches) ⇒ <code>Array.&lt;string&gt;</code>
helper function to sort an array of pitches from lowest to highest

**Kind**: global function  
**Returns**: <code>Array.&lt;string&gt;</code> - a new clone of the provided pitch string
array sorted from low pitch to high pitch  

| Param | Type | Description |
| --- | --- | --- |
| pitches | <code>Array.&lt;string&gt;</code> | an array of pitch strings |

<a name="SymbolChain"></a>
## SymbolChain : <code>string</code>
a string of one or more symbol names seperated by whitespace

**Kind**: global typedef  
**See**: a SymbolChain is used as definitions in [MusicGrammar](#MusicGrammar)  
**Example**  
```js
'4'                          // just a single symbol, means to go up a fourth
'5  -3'                      // go up a fifth, then down a third
'JupiterTheme  4  -2'        // play the JupiterTheme (which will be defined in another definition),
                             // then go up a fourth, then down a second
```
<a name="MusicGrammar"></a>
## MusicGrammar : <code>Object</code>
a user defined context-free grammar formatted as an object consisting of key-value pairs,
with each [non-terminal symbol](https://github.com/jrleszcz/grammar-graph#non-terminal-symbols)
pointing to an array of one or more [symbol chains](https://github.com/jrleszcz/grammar-graph#symbol-chains)
choices for this non-terminal. All [terminals](https://github.com/jrleszcz/grammar-graph#terminal-symbols)
must be positive or negative numbers, representing musical intervals. Said another way, anything that is not
a number must have its own definition.

**Kind**: global typedef  
**Properties**

| Name | Type | Description |
| --- | --- | --- |
| symbol | <code>[Array.&lt;SymbolChain&gt;](#SymbolChain)</code> | each element of the array is a possible definition    for this symbol. |

**Example**  
```js
var jupiterGrammar = {
InfinitePhrase: [ 'JupiterTheme InfinitePhrase',      // InfinitePhrase has two possible definitions
                 'SecondMotive InfinitePhrase' ],
  JupiterTheme: [ '2  3  -2' ],                       // JupiterTheme has only one definition
  SecondMotive: [ '4  StepDown' ],
      StepDown: [ '-2', '-2  StepDown']
}
// non-terminals: InfinitePhrase, JupiterTheme, SecondMotive, StepDown
//     terminals: -2, 2, 3, 4
```
