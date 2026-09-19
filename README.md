# sakinah-data

Data files for the Sakinah prayer app. The app downloads them on demand from the release
assets of this repository. A release is immutable once the app points at it; a data fix is
a new release.

```
https://github.com/famashines/sakinah-data/releases/download/hadith-v2/<book>.db
```

## Hadith databases

One SQLite file per book (`bukhari`, `muslim`, `abudawud`, `tirmidhi`, `nasai`,
`ibnmajah`), attached to the `hadith-v<version>` release. Each file holds:

```
meta(key, value)                       version, book, built
hadith(id, position, number, chapter, ordinal, arabic, english, urdu, grades)
search USING fts5(arabic, english, urdu, content='', tokenize='unicode61 remove_diacritics 2')
```

`number` is the sunnah.com hadith number. `position` is the reading order across the
book, `chapter` the sunnah.com section number, `ordinal` the row's place in that chapter.
`grades` is empty for Bukhari and Muslim and `"Grader: Grade | Grader: Grade"` for the four
Sunan. An empty translation means the source has none for that row. The `search` table is
a contentless FTS5 index; its `arabic` and `urdu` columns are folded (no harakat, alef,
yeh, heh, and kaf variants unified) and a query must be folded the same way.

The files are written by `scripts/build-hadith.py` in the app repository, from the
hadith-api dataset by Fawaz Ahmed (github.com/fawazahmed0/hadith-api), released into the
public domain under the Unlicense. The Arabic text is the received text of the collections
and is not under copyright.

The English translations are the ones the dataset carries: Muhsin Khan for Sahih
al-Bukhari, Abdul Hamid Siddiqui for Sahih Muslim, and the sunnah.com texts for Sunan Abu
Dawud, Jami at-Tirmidhi, Sunan an-Nasa'i, and Sunan Ibn Majah. The Urdu translations are
the ones the dataset carries; it does not name their translators. The grades of the four
Sunan are those of Al-Albani, Zubair Ali Zai, Shuaib Al-Arnaut, Abu Ghuddah, Ahmad Muhammad
Shakir, Bashar Awad Maarouf, Muhammad Fouad Abd al-Baqi, and Muhammad Muhyi Al-Din Abdul
Hamid, as the dataset took them from al-maktaba.org.

The dataset lists these references as the sites that made it possible, quoted from its
References.md:

- https://al-maktaba.org
- https://www.iium.edu.my/deed/hadith/
- https://github.com/alQuranBD/Bangla-Hadith-api
- https://www.hadithbd.com
- https://sunnah.com/
- https://www.urdupoint.com
- https://hamariweb.com/islam/hadith/
- https://www.al-hadees.com/hadees/
- https://muhammad.pk
- https://github.com/gadingnst/hadith-api
- http://forhuman.free.fr/hadith/muslim/
- https://www.rahmathpublications.com
- http://www.normalift.com/kitap
- https://zubairalizai.com/
- al-maktaba.org books 1755, 32832, 33759 (Abu Dawud: Al-Albani, Al-Arnaut, Abdul Hamid),
  783 and 33865 (Nasa'i: Al-Albani, Abu Ghuddah), 782, 33754, 33861 (Tirmidhi: Al-Albani,
  Shakir, Maarouf), 810 (Ibn Majah: Al-Albani)

## Licence

The files in this repository are released under the same terms as their source, the
Unlicense. See LICENSE.
