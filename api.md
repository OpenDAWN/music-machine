## Classes
<dl>
<dt><a href="#GuidedMusicMachine">GuidedMusicMachine</a></dt>
<dd></dd>
<dt><a href="#MusicMachine">MusicMachine</a></dt>
<dd></dd>
</dl>
## Functions
<dl>
<dt><a href="#plusIntervalInKey">plusIntervalInKey(key, sciPitch, intervalSize)</a> ⇒ <code>String</code> | <code>function</code></dt>
<dd><p>helper function that finds the result of adding a generic interval to a given pitch
in the context of a key</p>
<p>Optionally, exclude the intervalSize parameter and get back a curried function
with the key and startPitch set as defaults.</p>
</dd>
</dl>
<a name="GuidedMusicMachine"></a>
## GuidedMusicMachine
**Kind**: global class  

* [GuidedMusicMachine](#GuidedMusicMachine)
  * [new GuidedMusicMachine(guide, [key], [initialScaleDegrees])](#new_GuidedMusicMachine_new)
  * [.construction()](#GuidedMusicMachine+construction) ⇒ <code>Array.&lt;string&gt;</code>
  * [.tonic()](#GuidedMusicMachine+tonic)
  * [.isComplete()](#GuidedMusicMachine+isComplete) ⇒ <code>boolean</code>

<a name="new_GuidedMusicMachine_new"></a>
### new GuidedMusicMachine(guide, [key], [initialScaleDegrees])
step-by-step construction of music from a predefined Music Machine


| Param | Type | Default | Description |
| --- | --- | --- | --- |
| guide | <code>GuidedDecisionGraph</code> |  | a Guided Decision Graph. See: [GuidedDecisionGraph]{https://github.com/jrleszcz/grammar-graph/blob/master/api.md#GuidedDecisionGraph} |
| [key] | <code>string</code> | <code>&quot;&#x27;C major&#x27;&quot;</code> | the key in which to apply the generic interval. Must be a valid pitch string and mode name seperated by whitespace such as 'Bb major'. |
| [initialScaleDegrees] | <code>Array.&lt;number&gt;</code> | <code>[1]</code> | the scale degree(s) which constructions can start on |

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
<a name="MusicMachine"></a>
## MusicMachine
**Kind**: global class  

* [MusicMachine](#MusicMachine)
  * [new MusicMachine(grammar, startSymbol, [initialScaleDegrees])](#new_MusicMachine_new)
  * [.vertices()](#MusicMachine+vertices) ⇒ <code>Array.&lt;string&gt;</code>
  * [.createGuide([key])](#MusicMachine+createGuide) ⇒ <code>[GuidedMusicMachine](#GuidedMusicMachine)</code>

<a name="new_MusicMachine_new"></a>
### new MusicMachine(grammar, startSymbol, [initialScaleDegrees])
creates a new MusicMachine which can generate Guides for music construction.


| Param | Type | Default | Description |
| --- | --- | --- | --- |
| grammar | <code>object</code> |  | an object representing a musical grammar. |
| startSymbol | <code>string</code> |  | the symbol at which to start constructions |
| [initialScaleDegrees] | <code>Array.&lt;number&gt;</code> | <code>[1]</code> | the scale degree(s) which constructions can start on |

<a name="MusicMachine+vertices"></a>
### musicMachine.vertices() ⇒ <code>Array.&lt;string&gt;</code>
get an array of vertex names in the graph

**Kind**: instance method of <code>[MusicMachine](#MusicMachine)</code>  
**Returns**: <code>Array.&lt;string&gt;</code> - the vertex names in this graph  
<a name="MusicMachine+createGuide"></a>
### musicMachine.createGuide([key]) ⇒ <code>[GuidedMusicMachine](#GuidedMusicMachine)</code>
get a new GuidedMusicMachine using this decision graph

**Kind**: instance method of <code>[MusicMachine](#MusicMachine)</code>  
**Returns**: <code>[GuidedMusicMachine](#GuidedMusicMachine)</code> - a new guide from the provided start point  
**See**: [GuidedMusicMachine](#GuidedMusicMachine) for the methods available on the Guide  

| Param | Type | Default | Description |
| --- | --- | --- | --- |
| [key] | <code>string</code> | <code>&quot;&#x27;C major&#x27;&quot;</code> | the key in which to apply the generic interval. Must be a valid pitch string and mode name seperated by whitespace such as 'Bb minor'. |

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

