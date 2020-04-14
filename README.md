# Syllabifier for Luxembourgish

Based on the syllabifier from the [Penn Phonetics Toolkit](https://sourceforge.net/projects/p2tk/), 
this is an adaption for Luxembourgish. 

The Python script `syllabifer.py` takes IPA-transcribed words of Luxembourgish as input and 
returns the segments grouped as syllables. The phonetic segments in the input have to be 
separated by spaces, e.g. `æ p ə l t ɛːɐ t ɐ ɕ ɐ` (*Äppeltäertercher*).

The script applies the `Maximum Onset Principle` to assign as many consonants to a potential 
syllable onset as long as this onset is permitted in the language. These allowed onsets are 
specified in `luxembourgish.cfg` (and also in the scripts itself) as `onsets`; permitted 
`consonants` and `nuclei` are specified in the configuration as well.

## Usage
The Python notebook `Syllabifier` provides a simple example.

```
import syllabifier
language = syllabifier.Luxembourgish
syllables = syllabifier.syllabify(language, "ɑ p ʀ o v i z i̯ o n ɜɪ ə ʀ ə n")
for stress, onset, nucleus, coda in syllables :
   print(" ".join(onset), " ".join(nucleus), " ".join(coda))

 ɑ 
p ʀ o 
v i 
z i̯ o 
n ɜɪ 
 ə 
ʀ ə n
```

When run from a terminal:

```
python syllabifier.py luxembourgish.cfg < lux_ipa.txt > lux_ipa_syllabified.txt
```
