# Syllabifier for Luxembourgish

Based on the syllabifier from the [Penn Phonetics Toolkit](https://sourceforge.net/projects/p2tk/), 
this is an adaption for Luxembourgish. 

The Python script `syllabifer.py` takes IPA-transcribed words of Luxembourgish as input and 
returns the segments grouped as syllables. The phonetic segments in the input have to be 
separated by spaces, e.g. `æ p ə l t ɛːɐ t ɐ ɕ ɐ` (*Äppeltäertercher*).

The script applies the `Maximum Onset Principle` to assign as many consonants to a potential 
syllable onset as long as this onset is permitted in the language. These allowed onsets are 
specified in `luxembourgish.cfg` (and also in the script itself) as `onsets`; permitted 
`consonants` and `nuclei` are specified in the configuration as well.

The lists with IPA transcribed words comes from the training data for my [g2p system](http://engelmann.uni.lu/transcription/).

Although developed and tested for Luxembourgish, this system should also work in principle for IPA data for lots of other 
languages. It is only necessary to adapt the configuration for `onsets`, `nuclei` and `consonsants`.

## Usage
The Python notebook `Syllabifier` provides a simple example.

```python
import syllabifier
language = syllabifier.Luxembourgish

syllables = syllabifier.syllabify(language, "æ p ə l t ɛːɐ t ɐ ɕ ɐ")

# some test words
# æ p ə l t ɛːɐ t ɐ ɕ ɐ
# ɑ p ʀ o v i z i̯ o n ɜɪ ə ʀ ə n
# ʃ ɑ̃ː m b ɐ s p ʀ e z i d æ n t i n ə n
# k ɑ ʀ ɑ k t ə ʀ eː ʑ ə n ʃ ɑ f t ə n
# k ɑ ʀ i s m aː
# ʃ i m iː s p ʀ o f æ s oː ʀ i n ə n
# ɕ i ʀ u ʀ ʑ i n ə n
# k w ɑ f œː ʀ s s ɑ l ɑ̃ː
# d e k l ɑ ʀ ɑ ts i̯ əʊ n ə n
# d ʀ oː ɡ ə ʃ t ɑ t i s t i k

for stress, onset, nucleus, coda in syllables :
   print(" ".join(onset), " ".join(nucleus), " ".join(coda))

æ 
p ə l
t ɛːɐ 
t ɐ 
ɕ ɐ 
```

When run from a terminal:

```
python syllabifier.py luxembourgish.cfg < lux_ipa.txt > lux_ipa_syllabified.txt
```

## Limitations

- Compounds like `b l i n t d aː ʀ m o p e ʀ ɑ ts i̯ əʊ n` where the `m` is falsely attributed 
to the next syllable, because `m o` is of course a permitted onset. To solve this, a 
morphological pre-segmentation would be necessary.

- Intervocalic single consonants after short vowel are ambisyllabic and should thus be 
attributed to both syllables, which is not possible in this framework. In `ʃ t ʀ e k ə l` the
 `k` is in the second, while in `z ɑ ŋ ə n` the `ŋ` goes to the first syllable.
 
