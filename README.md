# musicbrainz-bookmarklets

**[Bookmarklets](https://en.wikipedia.org/wiki/Bookmarklet) and other JavaScript snippets for MusicBrainz.org**

In order to use one of the snippets under [`src/`](src/) as a bookmarklet you can save the compressed code snippets from the sections below as bookmarks or convert them yourself.

Running `node bookmarkletify.js snippet.js` outputs a minified version of `snippet.js` in the form of a `javascript:` URI that can be copied.

Before you run the above script you have to make sure that you have setup *Node.js* and have installed the dependencies of the script via `npm install`.

## [Expand collapsed mediums](src/expandCollapsedMediums.js)

```js
javascript:void $('.expand-disc').trigger('click');
```

Expands all collapsed mediums in the release editor, useful for large releases.

## [Guess Unicode punctuation](src/guessUnicodePunctuation.js)

```js
javascript:(()=>{var g,e;function a(g,d){$(g).css('background-color',''),$(g).each((g,e)=>{let a=e.value;a&&(d.forEach(([g,$])=>{a=a.replace(g,$)}),a!=e.value&&$(e).val(a).trigger('change').css('background-color','yellow'))})}e=[[/'''/g,'<b>'],[/''/g,'<i>'],...g=[[/(?<=\W|^)"(.+?)"(?=\W|$)/g,'\u201c$1\u201d'],[/(?<=\W|^)'(.+?)'(?=\W|$)/g,'\u2018$1\u2019'],[/(\d+)"/g,'$1\u2033'],[/(\d+)'(\d+)/g,'$1\u2032$2'],[/'/g,'\u2019'],[/(?<!\.)\.{3}(?!\.)/g,'\u2026'],[/ - /g,' \u2013 '],[/(\d{4})-(\d{2})-(\d{2})(?=\W|$)/g,'$1\u2010$2\u2010$3'],[/(\d{4})-(\d{2})(?=\W|$)/g,'$1\u2010$2'],[/(\d+)-(\d+)/g,'$1\u2013$2'],[/-/g,'\u2010']],[/<b>/g,"'''"],[/<i>/g,"''"]],a(['input#name','input.track-name','#id-edit-recording\\.name','#id-edit-work\\.name'].join(),g),a('textarea',e)})();
```

- Searches and replaces ASCII punctuation symbols for all title input fields by their preferred Unicode counterparts.
- Works for release title and track titles (in the release editor), recording and work title (on their respective edit pages).
- Experimental support for annotations and edit notes. Preserves apostrophe-based markup (bold, italic) but might break URLs if they contain punctuation symbols.
