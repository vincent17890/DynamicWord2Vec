# DynamicWord2Vec
## Introduction
This fork makes the codes self-contained by completing the pmi matrix computation, which is missing from the original codes, changes the codes to be compatible with python3, and explains some of the variables in the codes. 

## Inputs
In order to run the code, prepare the following files:
1. .txt files for each corpora. Each corpus must be in a separate file. The file names must follow the format [filestem]_[id].txt, where all the id's are consecutive integers, e.g. corpus_2018.txt, corpus_2019.txt, corpus_2020.txt, etc.
2. a pre-trained word2vec or glove word vectors of dimension DIM (referred to as static embedding inside the codes) trained on the entire corpus, with each line following the format below:
    - word[SPACE]coordinate1[SPACE]coordinate2[SPACE]...coordinateN[SPACE][NEWLINE]
    - in other words, each line start with the word followed by its embedding vector, delimited by space

## Usage
1. Run `python util_wordvec.py -dc /path/to/corpora/directory -fc filestemOfCorpora -ds /path/to/static/embedding -fs filestemOfEmbedding -s startnumber -e endnumber [-m mincount] [-l windowlength]`
      - `mincount` and `windowlength` are optional, with default values `100` and `5` respectively
      - Suppose your corpora are in the directory `/home/user/corpora/` , with file names `my_corpus_10.txt`, `my_corpus_11.txt`, ..., `my_corpus_19.txt`, and your static embedding has the abosolute path `/home/user/embedding/static_emb.txt`, then you should run `python util_wordvec.py -dc /home/user/corpora/ -fc my_corpus -ds /home/user/embedding/ -fs static_emb -s 10 -e 19`
  This will generate the pmi matrices `wordPairPMI_[id].csv` for each corpus; `w2id_[filestem]_[startnumber]-[endnumber]_minc_[mincount].json` and `id2w_[filestem]_[startnumber]-[endnumber]_minc_[mincount].json`, which identify the words with thier corresponeding row number in the pmi matrices (the same ordering is also used in the final embedding); and `emb_static_d[DIM]_[startnumber]-[endnumber].mat`, which is the static embedding converted from .txt to .mat to be compatible with the main program.

2. 