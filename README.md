### Integration with qBitTorrent

```sh
/usr/bin/filebot -script fn:amc \
    --output "$HOME/Media" \
    --action 'move' \
    --conflict 'skip' \
    -non-strict \
    --log-file 'amc.log' \
    --def excludeList=amc.excludes
    --def unsorted=y \
    --def subtitles=en \
    --def clean=y \
    --def "ut_dir=%F"
    --def "ut_kind=multi" \
    --def "ut_title=%N" \
    --def "ut_label=%L" \
    --def "seriesFormat={home}/Media/TV Shows/{n}/{'Season '+s}/{n} - {s00e00} - {t}" \
    --def "movieFormat={home}/Media/Movies/{info.SpokenLanguages.displayLanguage[0]}/{n} {[y, genre, rating]} / {n} ({y}) [{fn.findMatch('scr|hq') ? 'Scr, ' : {fn.findMatch('TV') ? 'TV, ' : null} }{vf}, {vc}]"
```

#### Copy friendly format

```sh
/usr/bin/filebot -script fn:amc --action 'move' --conflict 'skip' -non-strict --log-file 'amc.log' --def excludeList=amc.excludes unsorted=y clean=y "ut_dir=%F" "ut_kind=multi" "ut_title=%N" "ut_label=%L" "seriesFormat={home}/Media/TV Shows/{n}/{'Season '+s}/{n} - {s00e00} - {t}" "movieFormat={home}/Media/Movies/{info.SpokenLanguages.displayLanguage[0]}/{n} {[y, genre, rating]}/ {n} ({y}) [{fn.findMatch('scr|hq') ? 'Scr, ' : {fn.findMatch('TV') ? 'TV, ' : null} }{vf}, {vc}]"
```

### Format expressions

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
