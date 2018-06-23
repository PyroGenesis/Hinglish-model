Hinglish acoustic model
========================  
This repo contains the resources used for creating a Hinglish (Hindi + English) acoustic model (for CMUSphinx).

Though woefully lackluster in terms of the amount and length of data, these resources may help someone kickstart developing a similar kind of acoustic model.

Currently this model only uses the English phoneme set to represent all words. Hindi sounds are approximated using English phonemes (or their combinations).

## Contents
- A dictionary consisting of ~6300 words
- An LM made using SRILM that contains 50% training data phrases and 50% common hindi phrases
- A training transcription made of ~2600 sentences / phrases
- Almost all of the segmented .wav files used to build the model (divided according to speaker)
- CMUSphinx model options

## How to use
#### Building / Training the model
1. Set up CMUSphinx on your preferred Linux distro.
    - Download Sphinxbase, Sphinxtrain and Pocketsphinx from [here](https://cmusphinx.github.io/wiki/download/).
    - Extract to common directory and follow the READMEs within.
1. Download/Clone this repository to the same parent directory.
1. Open a terminal in the `enghin/` directory and execute command `sphinxtrain run`
    - You may need to complete configuration first by exporting these paths:  
      `export PATH=/usr/local/bin:$PATH`  
      `export LD_LIBRARY_PATH=/usr/local/lib`  
      `export PKG_CONFIG_PATH=/usr/local/lib/pkgconfig`  
1. The model will be built using parameters in `sphinx_train.cfg`.
1. If no test data is present, the terminal might give you an error at the end but you can ignore that.

That's all you need to do if you just want to build a CMUSphinx acoustic model.

#### Testing / Decoding using model
1. Add test .wav files to the `wav/` directory (they should be speaker-separated).
1. Create the files `enghin_test.fileids` and `enghin_test.transcription` in the `etc/` directory containing the test file locations and transcriptions respectively.
    - You can use the `enghin_train.fileids` and `enghin_train.transcription` files as a reference.
1. If you want to build the model again and test, run:  
`sphinxtrain run`  
else, if you want to just test, run:  
`sphinxtrain -s decode run`  
