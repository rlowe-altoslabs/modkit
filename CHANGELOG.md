# Changelog
All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [v0.2.8-rc1]
### Fixes
- [dmr] Don't crash when using matched samples, but not all samples have modification counts at a position. Fixes #165.
- [update-tags] Correctly handle implicit tags when there are no probs, i.e. `C+h` -> `C+h.`., fixes #160.

## [v0.2.7]
### Fixes
- [dmr] Header was incorrect with multiple samples
- [pileup] Improve performance when using `--include-bed`, only process contigs in the BED file.
- [dmr, single-site] When using multiple samples, don't fail a position when one or more samples doesn't have a modification call at that position.
- [extract] Expose queue size to reduce memory usage with long reads.
- [validate] Report number of calls filtered out with thresholds.


## [v0.2.6]
### Fixes
- [dmr, single-site] Don't require that there are equal numbers of samples for single site DMR with multiple samples. Fixes #140.
- [dmr, pairwise, region] Protect when zero bedmethyl records are found for a region, fixes #146.
### Adds
- [validate] Adds on-the-fly filtering of reads by alignment identity and/or alignment length.


## [v0.2.5]
### Fixes
- [extract] Only emit mapped reads when `--region` is provided, but still emit unmapped bases in those reads unless `--mapped-only` is passed.
- [extract] Performance improvement due to better tracking of interval boundaries.
- [repair] Updates the `MN` tag on repaired records.
### Adds
- [dmr, single-site] Refactor `dmr pair` without regions (i.e. single site analysis) to increase performance.
- [dmr, single-site] Add estimated MAP-based p-value to output.
- [all] Allows BED3 input for all options that use `--include-bed`. Strand will be assumed to be BOTH (equivalent to '.').
- [extract] Increases the kmer size limit to 50.


## [v0.2.5-rc2]
### Fixes
- [all] Reads with entirely implicit canonical calls are no longer skipped for "modbase info empty" or similar.
### Adds
- adds the `--no-implicit-calls` flag to `modkit update-tags` so when changing from the "probability of modification" modes (".", and "") to explicit mode (`?`) implicit cannonical calls can be skipped. This is important, for example, if the modification calling model did not have the `?` mode available.


## [v0.2.5-rc1]
### Adds
- `modkit validate` sub-command for rigorous testing of modified base calling models when ground truth labels are known.
### Fixes
- [all] Improve performance when using commands on transcriptome reference (or any reference with many sequences less than ~100kb).

## [v0.2.4]
### Adds
- [extract, adjust-mods, update-tags, call-mods] Parse MN tag in order to use secondary and supplementary alignments.
### Fixes
- [all] Improve performance slightly when using short and frequent motifs with `--motif` option.


## [v0.2.3]
### Adds
- [dmr, multi] Allow site-level scoring by omitting the `--regions` argument. Sites will be collected from the input bedMethyl files.
- [dmr] Friendlier handling of missing files and when regions aren't found in the bedMethyl input files.
- [dmr] allow filtering on valid coverage without changing input
- [extract] output "read calls" extract table, a TSV with the base modification calls for every modified position in every read using the same thresholding algorithm as pileup
- [extract] allow filtering of calls by reference motif (like in pileup) as well as BED regions (and exclude regions)
### Fixes
- [extract] Improve performance, especially on longer reads.
- [extract] Improve performance with long reads (actually a bug fix)
- [extract] num_soft_clipped_start and num_soft_clipped_end were incorrect on some reverse-mapped reads


## [v0.2.3-rc1]
### Adds
- [dmr, pair] Allow site-level scoring by omitting the `--regions` argument. Sites will be collected from the input bedMethyl files.
- [dmr] Friendlier handling of missing files and when regions aren't found in the bedMethyl input files.
### Fixes
- [extract] Improve performance, especially on longer reads.
### Changes


## [v0.2.2]
### Adds
- [all] Allow ChEBI codes and more flexible single-character modification codes. E.g. now you can use `c` for carboxy cytosine or `z` for something exotic.
- [extract] Adds `--kmer-length` option to modulate the kmer length on the command line.
### Fixes
- [dmr] Automatically select the correct bedMethyl rows when using multiple modified bases (e.g. C-mods and A-mods). Removes assert and replaces it with a warning.
### Deprecated
- In the next version `pileup` output will only have tab delimiters and the `--only-tabs` flag will be removed.

## [v0.2.2-rc1]
### Fixes
- [logging] Changes log level from error to debug when a record doesn't have any base modification probabilities.

## [v0.2.1]
### Adds
- [adjust-mods, summary, pileup, call-mods] Allows asymmetric edge filter (i.e. filter out base modification calls X bases from the start of the reads and Y bases from the ends). Previously, only one parameter was allowed and filtering was symmetric.
### Fixes
- [summary, sample-probs] Fixes bug where inferred canonical bases were not being accounted.
- [dmr] Fail when cannot parse _any_ bedMethyl lines from input, log when there are failures to parse lines, fixes #60
- [dmr] Automatically make directory if it doesn't already exist, fixes #61

## [v0.2.0]
### Adds
- [dmr] Adds `modkit dmr` command suite for differential methylation exploratory data analysis.
- [pileup-hemi] Adds `modkit pileup-hemi` for tabulating double-stranded methylation patterns.
### Fixes
- [repair] Fixes potential stack overflow when donor and/or acceptor BAMs aren't sorted correctly.

## [v0.1.13]
### Fixes
- [extract, mod_bam] Potential stack overflow when many reads are skipped.
- [extract] Output inferred canonical calls when the `.` MM tag is used.
- [adjust-mods] change MM flag to `?` and add inferred canonical calls when `--edge-filter` is applied.

### Adds
- [pileup] performs pileup in batches to decrease peak memory usage, configurable with `--chunk_size`.
- [pileup] Allow users to narrow output to any number of specified motifs (instead of only CpG dinucleotides) with `--motif` option

### Changes
- [extract] adds `inferred` column


## [v0.1.13-rc1]
## Fixes
- [extract, mod_bam] Potential stack overflow when many reads are skipped.

## [v0.1.12]
## Fixes
- [extract] no longer requires an index to use `--num-reads`, it will just take the first `--num-reads` reads if no index is found.
## Adds
- New command `modkit repair` allows projecting base modifiction calls from one modBAM onto another where the reads have beem trimmed or clipped.
- `adjust-mods`, `update-tags`, `sample-probs`, `summary`, `call-mods` and `extract` can now be used with standard input/output streams. 

## [v0.1.11]
### Fixes
- [extract] Correctly handles duplex modBAMs when using `--include-bed`
- Refactors handling of CRAM when sampling records. Fixes #35. Suggests to use BAM.
### Adds
- [extract] Output contains `ref_mod_strand` and `modified_primary_base`
- [pileup] New option `--max-depth` allows increasing depth beyond default in hts-lib and sets the default to 8,000 in case it changes in hts-lib.


## [v0.1.11-rc1]
### Fixes
- [extract] Correctly handles duplex modBAMs when using `--include-bed`


## [v0.1.10]
### Fixes
- Don't log message whilst aggregating base modification probabilities (exposed with duplex reads as input).
### Changes
- [pileup] Fail fast when bam index doesn't contain any mapped reads.


## [v0.1.9]
### Changes
- [pileup] When estimating the pass-threshold only use base modification probabilities if the read base is aligned to the reference (don't use soft-clipped and inserts). Use `--include-unmapped` to use all base modification probabilities.
- [adjust-mods] requires `--ignore`, `--convert`, or `--edge-filter`.
### Adds
- [pileup, extract, sample-probs, summary] Allow narrowing of analysis to specific sites with `--include-bed`. 
- [summary, sample-probs] Add `--only-mapped` flag that will only report on base modification probabilities if they are mapped to the reference.
- [pileup] Allow partitioning counts to separate bedMethyl files based on SAM tags with `--partition-tag` option.
### Fixes
- [adjust-mods, update-tags, call-mods] Panic when failure to parse SAM header, fixes #29.


## [v0.1.8]
### Changes
- [call-mods] Emit 0 ML value when a mod code is not called, previously the call was omitted (only the called mod was emitted).
### Adds
- [adjust-mods, call-mods, pileup, sample-probs, summary, extract] Allow `--edge-filter` that will remove base modification probabilities at the ends of reads.
### Fixes
- [call-mods] `--no-filtering` flag properly handled. 
### Deprecated
- [adjust-mods] In order to allow `--edge-filter` without also performing an ignore or convert, in the next release `--ignore` will require an explicit argument (`h` is no longer the default). In this release, when no edge filter, conversion, or ignore is provided, `h` will be used for ignore, but this behavior will be removed in the next release.

## [v0.1.7]
### Changes
### Adds
    - `modkit extract` sub-command that produces a table of per-read base modification probabilities.
    - Allow suppression of progress bar with `--suppress-progress`
### Fixes
    - Don't count skipped reads towards total when sampling.

## [v0.1.6]
### Changes
- When ignoring a base modification in pileup, calculate pass thresholds on the probabilities after ignoring the specified probability.

### Adds
- [pileup] API to specify pass thresholds per base modification (or canonical) with `--mod-threshold` option.
- New modBAM->modBAM subcommand, `call-mods` that will apply pass thresholds and clamp base modification probabilities to zero (canonical) or 1.0 for base modifications
- [sample-probs, summary] Allow `--ignore` to remove a base modification class from the analysis.

## [v0.1.5]
### Changes
- Table output is default in `modkit summary`, columns are all_counts/frac and pass_counts/frac instead of counts/frac and filt_counts/frac. See help for details.

### Fixes
- The `modkit summary` command will not use all of the reads in the input modBAM when the `--no-filtering` flag is used. To disable sampling (and use all of the reads) use `--no-sampling`. See docs for details.

### Adds
- The `sample-probs` command will now output histograms of the base modification probabilities with the `--hist` option.
- "Book-style" docs.


## [v0.1.4]
### Changes
- Implicitly canonical mode `.` See [SAM tags](https://samtools.github.io/hts-specs/SAMtags.pdf) does not require `--force-allow-implicit`. However no mode at all still does.
- `modkit adjust-mods` will allow conversion of base modification codes that aren't in the [specification](https://samtools.github.io/hts-specs/SAMtags.pdf) (e.g. `Z`). In order to process these with `modkit pileup` you must first run `modkit adjust-mods in.bam out.bam --convert Z m` (for example). 
- Per-canonical base thresholds will be automatically inferred, e.g. different thresholds will be chosen for A mods and C mods. This is also true for `modkit summary` and `modkit sample-probs`.
- `modkit summary` will now allow specification of a `--region` when using an indexed BAM and will sample evenly over the aligned contigs when the region is omitted.
### Adds
- `modkit summary` has `--table` option that produces a human-readable table.
### Deprecated
- `modkit summary` tab-separated format will not be default in the next release. The table output (currently specified with the `--table` option will become the default).
### Fixes
- Restructuring of the code allows for more parallelism when estimating threshold values, speeding up this process at the start of `modkit pileup` or `modkit summary`.

## [v0.1.4-rc1]

### Changes
- Filter base modification calls that are < the threshold value instead of <= the threshold value.


## [v0.1.3]
### Adds
- `--mask` flag in `pileup` and `motif-bed`

### Fixes
- Default behavior will find CGs in masked regions of the reference.


## [v0.1.2]
### Adds
- First release.
    
### Fixes

