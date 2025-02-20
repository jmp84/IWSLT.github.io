---
permalink: /2021/offline
title: "Offline Speech Translation"
---

## Description


<!-- the task, the languages, and the type of data -->

Recent advances in deep learning are giving the possibility to address traditional NLP tasks in a new and completely different manner. One of these tasks is spoken language translation (SLT). For years, SLT has been addressed by cascading an automatic speech recognition (ASR) and a machine translation (MT) system. Recent trends rely on using a single neural network to directly translate the input audio signal in one language into a text in a different language without intermediate symbolic representations, e.g., transcriptions.  

The goal of the **Offline Speech Translation Task** is to examine automatic methods for translating audio speech in one language into text in the target language. This has to be done either by exploiting cascaded solutions or end-to-end approaches. Last year's results of IWSLT 2020 have shown that the performance of end-to-end models is approaching and even overtaking the results of cascade solutions. Hence, the question we want to answer this year is: **is the cascaded solution still the dominant technology in spoken language translation?**

In continuity with last year, the task addresses the translation of TED talks from English into German. **One test set will be released containing the same talks, respectively with and without audio segmentation.**

The system's performance will be evaluated with respect to their capability to produce translations similar to the target-language references. Such similarity will be measured in terms of multiple automatic metrics: BLEU, TER, BEER and characTER. The submitted runs will be ranked based on the BLEU calculated on the test set by using automatic resegmentation of the hypothesis based on the reference translation by [mwerSegmenter](https://www-i6.informatik.rwth-aachen.de/web/Software/mwerSegmenter.tar.gz). The detailed evaluation script can be found in the [SLT.KIT](https://github.com/isl-mt/SLT.KIT/blob/master/scripts/evaluate/Eval.sh).


## Evaluation Conditions

Both cascade and end-to-end models will be evaluated. We kindly ask each participant to specify at submission time if a cascade or an end-to-end model has been used.

In this task, we use the following definition of end-to-end model:
  * No intermediated discrete representations (source language like in cascade or target languages like in rover)
  * All parameters/parts that are used during decoding need to be trained on the end2end task (may also be trained on other tasks -> multitasking ok, LM rescoring is not ok)


## Test Data

This year one versions of the same TED talks is released. It contains the audio files and the information to convert them into sentence-like segmentation using automatic tools. Systems using the given or another segmentation will be evaluated in a single ranking without distinction between given or own segmentation.

To measure the progress in the ST field, each participant is required to translate also the 2020 test set that is still blind. Similar to this year test set, the 2021 test set will be made available with and without automatic segmentation.

### Test sets:

2020:
  -   [Unsegmented](http://i13pc106.ira.uka.de/~jniehues/IWSLT-SLT/data/eval/en-de/unsegmented/IWSLT-SLT.unsegmented.tst2020.en-de.tgz)
  -   [Segmented](http://i13pc106.ira.uka.de/~jniehues/IWSLT-SLT/data/eval/en-de/segmented/IWSLT-SLT.segmented.tst2020.en-de.tgz)

2021:


## Past Editions Development Data

The development data is not segmented using the reference transcript. The archives contain segmentation into sentence-like segmentation using automatic tools. But the participants might also use a different segmentation. The data provided as an archive with the following files ($set e.g. IWSLT.TED.dev2010):
  * $set.en-de.en.xml: Reference transcript (will not be provided for evaluation data)
  * $set.en-de.en.xml: Reference translation (will not be provided for evaluation data)
  * CTM_LIST: Ordered file list containing the ASR Output CTM Files (will not be provided for evaluation data) (Generated by ASR systems that use more data)
  * FILE_ORDER: Ordered file list containing the wav files
  * $set.yaml: This file contains the time steps for sentence-like segments. It is generated by the LIUM Speaker Diarization tool.
  * $set.h5: This file contains the 40-dimensional Filterbank features for each sentence-like segment of the test data created by XNMT.
  * The last two files are created by the following command:
python -m xnmt.xnmt_run_experiments /opt/SLT.KIT/scripts/xnmt/config.las-pyramidal-preproc.yaml

Development data:

(Please note that system generated the provided ASR scripts use more training data than allowed for this year's evaluations)
  * [dev2010](http://i13pc106.ira.uka.de/~jniehues/IWSLT-SLT/data/eval/en-de/preprocessed/IWSLT-SLT.dev2010.en-de.tgz)
  * [tst2010](http://i13pc106.ira.uka.de/~jniehues/IWSLT-SLT/data/eval/en-de/preprocessed/IWSLT-SLT.tst2010.en-de.tgz)
  * [tst2013](http://i13pc106.ira.uka.de/~jniehues/IWSLT-SLT/data/eval/en-de/preprocessed/IWSLT-SLT.tst2013.en-de.tgz)
  * [tst2014](http://i13pc106.ira.uka.de/~jniehues/IWSLT-SLT/data/eval/en-de/preprocessed/IWSLT-SLT.tst2014.en-de.tgz)
  * [tst2015](http://i13pc106.ira.uka.de/~jniehues/IWSLT-SLT/data/eval/en-de/preprocessed/IWSLT-SLT.tst2015.en-de.tgz)
  * [tst2018](http://i13pc106.ira.uka.de/~jniehues/IWSLT-SLT/data/eval/en-de/IWSLT-SLT.tst2018.en-de.tgz)


## Allowed Training Data

<!--### IMPORTANT: new En-De training data will be made avaialble soon! Stay tuned! -->



**"NEW TRAINING DATA!!"** 

In addition to the resources listed below, this year a new version of the En-De training data is released. It is part of the MuST-C V2 that will be made available in the next months. It includes training, dev, and test (Test Common), in the same structure of MuST-C V1.

Differences with MuST-C v1:
  * More talks that result in 20k more audio/text segments;  
  * Improved cleaning strategies able to better discard low-quality triplets (audio, transcript, translation), in particular, when the text is not well-aligned with the audio and the audio is shorter than 50 millisecs;  
  * TED talks of MuST-C v2 were downloaded from the [YouTube TED channel](https://www.youtube.com/c/TED/videos), where higher quality audio/videos are available with respect to the TED website used for the previous version of MuST-C. The downloading was performed by means of [youtube-dl](https://youtube-dl.org/), the well-known open-source download manager, specifying the "-f bestaudio option". The audios were finally converted from two (stereo) to one (mono) channel and downsampled from 48 to 16 kHz, using [FFmpeg](https://ffmpeg.org/). 
By inspecting the spectrograms of the same talks in the two versions of MuST-C clearly emerges that the upper limit band in the audios used in MuST-C V1 is 5 kHz, while it is at 8 kHz in the latest version, coherently with the 16 kHz sample rate. **This difference does not guarantee the fully compatibility between V1 and V2 of MuST-C.**  
  
The dataset is available [here](https://ict.fbk.eu/must-c/). Press the bottom "click here to download the corpus", and select version V2. 

IMPORTANT NOTE: the 2021 test set will be processed using the same pipeline of the MuST-C V2 training data. For this reason, we recommend the use of the new MuST-C training data. 

These datasets can be used to train your model:
  * [MuST-C corpus v1](https://ict.fbk.eu/must-c/) The MuST-C V1 is still available to favor the reuse of past trained models.
  * [CoVoST](https://github.com/facebookresearch/covost)
  * [TED corpus](https://wit3.fbk.eu/2017-01-c)
  * [Speech-Translation TED corpus](http://i13pc106.ira.uka.de/~mmueller/iwslt-corpus.zip) (for this corpus, we provided 40-dimension Filterbank features from the audio, extracted by XNMT)
  * [How2 Corpus](https://github.com/srvk/how2-dataset) (only English - Portuguese) 
  * [LibriVoxDeEn](https://heidata.uni-heidelberg.de/dataset.xhtml?persistentId=doi:10.11588/data/TMEDTX) (only German - English)
  * [Europarl-ST](https://www.mllp.upv.es/europarl-st/)
  * TED LIUM corpus [v2](https://lium.univ-lemans.fr/en/ted-lium2/), [v3](https://lium.univ-lemans.fr/en/ted-lium3/) 
      * The official test set is not part of this corpus, but if you want to use the development data you need to make sure that it is not part of the data
  * Data provided by WMT [2019](http://www.statmt.org/wmt19/) and [2020](http://www.statmt.org/wmt20/)
  * [OpenSubtitles2018](http://opus.nlpl.eu/OpenSubtitles2018.php)
  * [Augmented LibriSpeech](https://github.com/alicank/Translation-Augmented-LibriSpeech-Corpus) (only English - French)
  * [Mozilla Common Voice](https://voice.mozilla.org/en/datasets) for English use version en_2179h_2020-12-11
  * [LibriSpeech ASR corpus](http://www.openslr.org/12/)


## Submission Guidelines

  * Multiple run submissions are allowed, but participants must explicitly indicate one PRIMARY run for each track. All other run submissions are treated as CONTRASTIVE runs. In the case that none of the runs is marked as PRIMARY, the latest submission (according to the file time-stamp) for the respective track will be used as the PRIMARY run.
  * Submissions have to be submitted as a gzipped TAR archive (see format below) and sent as an email attachment to  <iwslt_offline_task_submission@fbk.eu>.
  * The TAR archive should include in the file name the type of system (cascade/end-to-end) used to generate the submission
  * Each run has to be stored in a plain text file with one sentence per line
  * Scoring will be case-sensitive and including the punctuation. Submissions have to be in UTF-8. Tags such as applause, laughing etc are not considered during the evaluation.

TAR archive file structure:  
< UserID >/< Set >.< Task >.< UserID >.primary.txt  
&emsp;&emsp;  /< Set >.< Task >.< UserID >.contrastive1.txt
&emsp;&emsp;  /< Set >.< Task >.< UserID >.contrastive2.txt  
&emsp;&emsp;  /...  
where:  
< UserID > = user ID of participant used to download data files  
< Set > = IWSLT18.SLT.tst2018  
< Task > =  < fromLID >-< toLID >  
< fromLID >, < toLID > = Language identifiers (LIDs) as given by ISO 639-1 codes; see for example the WIT3 webpage   

All the submissions should be sent to this address: <iwslt_offline_task_submission@fbk.eu>

The email should include the following information:
  * Institute:
  * Contact Person:
  * Email:
  * Data condition: Constraint/Unconstraint 
  * Segmentation: Own/Given
  * Brief abstract about the system:
  * Do you want to make your submissions freely available for research purposes? (yes/no)


## Contacts 

Chair: Marco Turchi (FBK, Italy). 

Discussion: <iwslt-evaluation-campaign@googlegroups.com>


## Organizers

Sebastian Stüker (KIT, Germany)  
Jan Niehues (Maastricht University, Netherlands)  
Matteo Negri (FBK, Italy)  
Roldano Cattoni (FBK, Italy) 







<!-- list of names and affiliations -->


<!-- Markdown notes: comments can be formed as above; bulleted lines start with a - ; if you want to have a line break either put a blank line in between the text or leave two spaces at the end of the line -->
