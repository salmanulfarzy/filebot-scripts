Format expressions used with [filebot]

#### Movies

```
Movies/{info.SpokenLanguages.displayLanguage[0]}/{n} {[y, genre, rating]} / {n} ({y}) [{fn.findMatch('scr|hq') ? 'Scr, ' : {fn.findMatch('TV') ? 'TV, ' : null} }{vf}, {vc}]
```

Categorise movies based on language and tag folder with **year**, **primary genre** and **rating**. Tag files with **video format** and **video codec**. Lower quality files like `Scr`, `HQ` or `TVRip` will be specifically tagged, Standard formats like `DVDRip` or `BRRip` won't be affected.

Bit explanation on non-standard expressions used here.,

| Expression | Explanation |
|:----------|:----|
| `info.SpokenLanguages.displayLanguage[0]` | Primary language used in movie, Useful when you watch movies from multiple languages.|
| `[{fn.findMatch('scr\|hq') ? 'Scr, ' : {fn.findMatch('TV') ? 'TV, ' : null}` | Tag file if it's either `Scr`, `HQ` or `TVRip`. |

#### Series

```
TV Shows/{n}/{'Season '+s}/{n} - {s00e00} - {t}
```

Categorise based on series name and seasons.

#### Resources

- [Filebot format expressions][1]

[filebot]: https://www.filebot.net/
[1]: https://www.filebot.net/naming.html
