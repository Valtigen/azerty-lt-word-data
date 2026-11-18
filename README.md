# ĄŽERTY – Lithuanian word data

The word data bundled with **ĄŽERTY klaviatūra**, a free (pro bono) iOS keyboard for the Lithuanian Standard LST 1582 layout, published by Valtigen MB. The keyboard uses it for completions, diacritic fixes, typo corrections, autocorrection and next-word predictions, entirely on the device.

The data is licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) (see `LICENSE`). It is adapted from the two sources below, which are also licensed under CC BY. When you reuse it, credit both sources and this adaptation.

| File | Size | Contents |
|---|---|---|
| `lt.lex` | 9.2 MB | 300,000 most frequent Lithuanian word forms with frequency scores, plus an index by the word without diacritics |
| `lt.next` | 1.3 MB | For about 131,000 words, the up to four words that most often follow them, with their shares |

## Sources and changes

**Word forms and frequencies (`lt.lex`)**
CCLL Lemmatised Frequency Lists (2025), file `3-LT_alpha_wordform_freq_list.txt`. Corpus of Contemporary Lithuanian Language, SITTI, Vytautas Magnus University; CLARIN-LT. https://hdl.handle.net/20.500.11821/77. Licence: CC BY 4.0.
Changes: capitalised forms merged into lowercase, all-caps abbreviations dropped, limited to the 300,000 most frequent word forms, frequencies turned into 0–255 scores on a log scale, converted to the binary format below.

**Next words (`lt.next`)**
Leipzig Corpora Collection, `lit_news_2020_1M` and `lit-lt_web_2015_1M` (neighbour co-occurrences). © Universität Leipzig / Sächsische Akademie der Wissenschaften / InfAI. https://wortschatz.uni-leipzig.de/en/download/lit. Licence: CC BY, per https://wortschatz.uni-leipzig.de/en/usage.
Changes: co-occurrence counts from both corpora merged (case merged), limited to words in `lt.lex`, the four most frequent followers kept per word (pairs seen fewer than 3 times dropped), converted to the binary format below.

## Suggested credit

> Lithuanian word data from ĄŽERTY (Valtigen MB), CC BY 4.0, adapted from the CCLL Lemmatised Frequency Lists 2025 (SITTI, Vytautas Magnus University, CC BY 4.0) and the Leipzig Corpora Collection (© Universität Leipzig / SAW / InfAI, CC BY).

## File formats

Both files are little-endian and designed to be memory-mapped.

`lt.lex`:
```
"LTLX", UInt32 version (2), UInt32 word count N
Words:   UInt32 × (N + 1) offsets, UInt8 × N scores, UTF-8 blob (sorted by bytes)
Folded:  UInt32 × (N + 1) offsets, UInt32 × N word index, ASCII blob (sorted by folded bytes,
         equal folded forms by score, highest first)
```
"Folded" is the word with Lithuanian diacritics removed (ą→a, č→c, ę→e, ė→e, į→i, š→s, ų→u, ū→u, ž→z).

`lt.next`:
```
"LTNX", UInt32 version (1), UInt32 context count C, UInt32 follower count F
UInt32 × C        context word (index into lt.lex), ascending
UInt32 × (C + 1)  start of each context's followers
UInt32 × F        follower word (index into lt.lex), most likely first
UInt8 × F         share of the context's occurrences, 0–255
```

## Checksums (SHA-256)

```
24cb76bb159f69ad41980627afb821a4b7879e9ca1b19f379bb3aede7c6da8d8  lt.lex
def56f7e51512f2a8246a93760aff53c262f6924bd9c7a420881735c4bc93940  lt.next
```

## Contact

Valtigen MB, Girulių g. 10, LT-12112 Vilnius, Lithuania · info@valtigen.com
