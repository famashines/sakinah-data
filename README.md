# sakinah-data

Data files for the Sakinah prayer app. The app downloads them on demand through jsDelivr,
pinned to a tag, so a file under a tag never changes. A data fix is a new tag.

```
https://cdn.jsdelivr.net/gh/famashines/sakinah-data@hadith-v1/hadith/<book>/<chapter>.json
```

## hadith/

One directory per book (`bukhari`, `muslim`, `abudawud`, `tirmidhi`, `nasai`, `ibnmajah`),
one JSON file per chapter, named by the sunnah.com section number. A file is an array of
rows:

```
[number, "arabic", "english", "urdu", "grades"]
```

`number` is the sunnah.com hadith number. `grades` is empty for Bukhari and Muslim and
`"Grader: Grade | Grader: Grade"` for the four Sunan. An empty translation means the source
has none for that row.

The files are written by `scripts/build-hadith.js` in the app repository, from the
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
