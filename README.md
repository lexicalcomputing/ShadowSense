# ShadowSense

This is a repository containing ShadowSense, a word sense annotated dataset for Czech and English.

For a detailed description, please read the [paper](https://aclanthology.org/2024.lrec-main.1286.pdf).

## Data Files

The `data/` directory contains the annotated test sets.

 - `English.tsv.zst` contains the full English dataset compressed using zstd.
 - `Czech.tsv.zst` contains the full Czech dataset compressed using zstd.
 - `English_sample.tsv` contains the first 1000 rows of the English dataset.
 - `Czech_sample.tsv` contains the first 1000 rows of the Czech dataset.

Note that the compressed files are stored using [Git LFS](https://git-lfs.com/), which you might need to install to be able to access them from a local copy of the repository.

The files are encoded as UTF-8 and use columnar format separated by TAB characters. No quoting is used and the first line describes the names of the columns. All the files have the same structure.

 - Column `head` represents the headword.
 - Columns starting with `sense` represent the "gold" annotations, one column per annotator. Value ending with an `x` means that the annotator has not marked this line in any way.
 - Column `text` contains the the sentence, within which the specific occurrence appears.
 - Columns `rel` and `col` are the word sketch relations used for extracting the instances from the corpus.
 - Column `pos` shows the token number in the underlying corpus.
   - English dataset uses the [enTenTen08 corpus](http://hdl.handle.net/11858/00-097C-0000-0001-CCDF-8).
   - Czech dataset uses the [csTenTen17 corpus](http://hdl.handle.net/11234/1-4835).
  
## The Scorer Program
To obtain a good performance, is written in `Rust`, the source code is in the `scorer/` directory, a prebuilt static binary for x86_64 Linux is present in the `bin/` directory.

### Usage
Annotate the test set using your own WSI system and add the result as another column in the file. Only the sense and head columns need to be kept.

Run the scorer and observe the output:

    ./bin/scorer ANNOTATED_FILE ANNOTATEDCOLUMN_NAME

### Compilation
To build the program yourself, install Rust using [https://rustup.rs/](https://rustup.rs/) and then run `cargo build --release` from the `scorer/` directory.

## Licensing

Shield: [![CC BY-NC-SA 4.0][cc-by-nc-sa-shield]][cc-by-nc-sa]

This work is licensed under a [Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License][cc-by-nc-sa].

[![CC BY-NC-SA 4.0][cc-by-nc-sa-image]][cc-by-nc-sa]

[cc-by-nc-sa]: http://creativecommons.org/licenses/by-nc-sa/4.0/
[cc-by-nc-sa-image]: https://licensebuttons.net/l/by-nc-sa/4.0/88x31.png
[cc-by-nc-sa-shield]: https://img.shields.io/badge/License-CC%20BY--NC--SA%204.0-lightgrey.svg

## Citing

If you use this repository in your work, please cite it! A ready made BibTex citation record is available in the [CITATION.bib](./CITATION.bib) file.

Your citation helps acknowledge the effort put into developing this resource and assists others in locating and using it effectively. Thank you!
