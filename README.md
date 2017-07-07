# Overview

The file is taken from http://norvig.com/ngrams/, which is just the cleaned version of 1-gram data set http://norvig.com/ngrams/count_1w100k.txt

If anyone has a more recent version please let me know. Stuff like "instagram" doesn't appear in this data set.

## Download

    wget -O google_100k.txt https://github.com/gjthompson1/google_100k/blob/master/google_100k.txt?raw=true

## Use

Obviously there are many but I personally use it to augment spell checking using http://pythonhosted.org/pyenchant/

    pip install enchant

Then spell checking.

    import re
    from enchant import DictWithPWL
    from enchant.checker import SpellChecker

    def spell_check(blob):
        d2 = DictWithPWL("en_US","google_100k.txt")
        chkr = SpellChecker(d2)
        chkr.set_text(blob)
        for err in chkr:
            err.replace('')
        blob = chkr.get_text().lower()
        blob = re.sub(' +',' ',blob).strip()
        return blob
    
So

     In [1]:  blob = 'hey whats up dawg how you doin, you should use pyenchant with this data set from google, and have you heard of this new company instagram'

     In [2]: spell_check(blob)
     Out[2]: 'hey whats up dawg how you doin, you should use with this data set from google, and have you heard of this new company'
    
    
