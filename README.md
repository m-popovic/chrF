# chrF
 a tool for calcualting character n-gram F score

By: Maja Popovic <maja.popovic.166@gmail.com>,  June 2017


chrF++ is a tool for automatic evaluation of machine translation output based on character n-gram precision and recall enhanced with word n-grams. 
The tool calculates the  F-score averaged on all character and word n-grams, where the default character n-gram order is 6 and word n-gram order is 2.  The arithmetic mean is used for n-gram averaging.

Recent experiments have shown that adding word 1-grams and 2-grams to the standard character 6-grams improves the Pearson correlation with direct human assessments. If you want to use only character n-grams, just set the word n-gram order to 0.

It is written in Python, so you have to install Python 2 or Python 3.
The option -h, --help outputs a description of the available command line options.


Required inputs:
++++++++++++++++

- translation reference and hypothesis

The required format of all inputs is raw text containing one sentence per line. Tokenisation is not necessary. 

In the case of multiple references, all available reference sentences must be separated by *#


Optional inputs:
~~~~~~~~~~~~~~~~

-nc, --ncorder
  character n-gram order (default value is 6)

-nw, --nworder
  word n-gram order (default value is 2)

-b, --beta
  beta parameter to balance precision and recall (default value is 2)


Default outputs:
++++++++++++++++
- start time
- overall document level F-score
- overal macro-averaged document level F-score (arithmetic average of the sentence level scores)
- end time

Optional outputs:
~~~~~~~~~~~~~~~~~

-s, --sent
    sentence level scores


Examples for testing:
-------------------------------------- 

You can try the tool on the given examples containing distinct languages: English (en), Czech (cs), Russian (ru) and Chinese (zh). 
For each language, example.ref.land represents a reference and example.hyp.lang represents a hypothesis.

You can try various calls and compare the results:

1) a simple call:

English:

chrF++.py -R example.ref.en -H example.hyp.en

start_time:	1497437792
c6+w2-F2	54.9482
c6+w2-avgF2	52.1829
end_time:	1497437792

Russian:

chrF++.py -R example.ref.ru -H example.hyp.ru

start_time:	1497437973
c6+w2-F2	42.2905
c6+w2-avgF2	42.6974
end_time:	1497437973



2) changing default n-gram orders:

a) chrF++.py -R example.ref.en -H example.hyp.en -nc 8 -nw 1 

start_time:	1497438072
c8+w1-F2	52.7801
c8+w1-avgF2	49.7979
end_time:	1497438072


b) chrF++.py -R example.ref.en -H example.hyp.en nw 0 (uses only character n-grams -- recommended for Chinese and similar languages)

start_time:	1497438113
c6+w0-F2	58.0911
c6+w0-avgF2	55.1081
end_time:	1497438113


Chinese:

chrF++.py -R example.ref.zh -H example.hyp.zh -nw 0

start_time:	1497438131
c6+w0-F2	32.6986
c6+w0-avgF2	33.5167
end_time:	1497438131



3) changing beta parameter:

a) chrF++.py -R example.ref.en -H example.hyp.en -b 1 (equal contribution of precision and recall)

start_time:	1497438189
c6+w2-F1	53.9267
c6+w2-avgF1	50.9922
end_time:	1497438189


b) chrF++.py -R example.ref.en -H example.hyp.en -b 0.4 (more weight on precision)

start_time:	1497438211
c6+w2-F0	52.7434
c6+w2-avgF0	50.0280
end_time:	1497438211



4) sentence level scores:

chrF+.py -R example.ref.en -H example.hyp.en -s

start_time:	1497438336
1::c6+w2-F2	64.0368
2::c6+w2-F2	70.8799
3::c6+w2-F2	21.5461
4::c6+w2-F2	31.9252
5::c6+w2-F2	44.5054
6::c6+w2-F2	45.0953
7::c6+w2-F2	45.6882
8::c6+w2-F2	54.8102
9::c6+w2-F2	81.0330
10::c6+w2-F2	62.3084
c6+w2-F2	54.9482
c6+w2-avgF2	52.1829
end_time:	1497438336

