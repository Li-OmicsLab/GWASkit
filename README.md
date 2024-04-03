# GWASkit

A tool designed to provide fast all-in-one preprocessing for GWAS summary data files.

- [GWASkit](#GWASkit)
- [features](#features)
- [simple usage](#simple-usage)
  - [rs](#rs)
  - [standardize](#standardize)

# features
0. Quickly perform rs ID conversion.
1. Supports various GWAS summary data formats.
2. Supports both Windows and CentOS/Ubuntu platforms.
3. ...

If you find a bug or have additional requirement for `GWASkit`, please file an issue:https://github.com/Li-OmicsLab/GWASkit/issues/new

# simple usage

This binary was compiled on Ubuntu, and tested on CentOS/Ubuntu.

```shell
$ ./GWASkit --help
usage: GWASkit [-h] {rs,standardize} ...

positional arguments:
  {rs,standardize}
    rs              Map CHR:POS:REF:ALT to rs ID
    standardize     Standardize GWAS data format

optional arguments:
  -h, --help        show this help message and exit
```

```shell
# dowanload the referece

# download the latest build
$ wget https://github.com/Li-OmicsLab/GWASkit/GWASkit
$ chmod a+x ./GWASkit

# or download specified version, i.e. GWASkit v1.0.0
$ wget https://github.com/Li-OmicsLab/GWASkit/GWASkit.1.0.0
$ mv GWASkit.1.0.0 GWASkit
$ chmod a+x ./GWASkit
```

## rs

```shell
$ ./GWASkit rs --help
usage: GWASkit rs [-h] --inputFile INPUTFILE --rsdb RSDB --outFile OUTFILE [--SEP {1,2,3}] --CHR CHR --POS POS --REF REF --ALT ALT [--verbose]

optional arguments:
  -h, --help            show this help message and exit
  --inputFile INPUTFILE, -I INPUTFILE
                        Inupt file (.csv/.csv.gz or .tsv/.tsv.gz), specifying GWAS summary data. Required.
  --rsdb RSDB, -R RSDB  Reference database for rs ID conversion. Required.
  --outFile OUTFILE, -O OUTFILE
                        Output file to store the results. Required.
  --SEP {1,2,3}         Delimiter used in the input file. '1' represents space, '2' represents tab, '3' represents comma. Default is tab, namely '2'. Required.
  --CHR CHR             Chromosome for SNPs in the format 1:22, X, Y or MT, required.
  --POS POS             Position for SNPs, required.
  --REF REF             Name of column with effect or reference allele, required.
  --ALT ALT             Name of column with non effect or alternative allele, required.
  --verbose             Enable verbose mode for more detailed output.
```

```shell
$ ./GWASkit rs \
-I /mnt/HDRIVE/EBI/GCST90043384_buildGRCh37.tsv.gz \
-O /mnt/GDRIVE/src.out/SNP/SNP \
--rsdb /mnt/GDRIVE/.data/rsdb/GRCh37 \
--CHR chromosome \
--POS base_pair_location \
--REF other_allele \
--ALT effect_allele \
--verbose
```

## standardize

```shell
$ ./GWASkit standardize --help
usage: GWASkit standardize [-h] --inputFile INPUTFILE --outFile OUTFILE [--SEP {1,2,3}] --CHR CHR --POS POS --REF REF --ALT ALT --RSID RSID --BETA BETA --EAF EAF --SE SE --PVALUE PVALUE --SS SS
                           --TYPE {hg19,hg38,GRCh37,GRCh38} [--verbose]

optional arguments:
  -h, --help            show this help message and exit
  --inputFile INPUTFILE, -I INPUTFILE
                        Inupt file (.csv/.csv.gz or .tsv/.tsv.gz), specifying GWAS summary data. Required.
  --outFile OUTFILE, -O OUTFILE
                        Output file to store the results. Required.
  --SEP {1,2,3}         Delimiter used in the input file. '1' represents space, '2' represents tab, '3' represents comma. Default is tab, namely '2'. Required.
  --CHR CHR             Chromosome for SNPs in the format 1:22, X, Y or MT, required.
  --POS POS             Position for SNPs, required.
  --REF REF             Name of column with effect or reference allele, required.
  --ALT ALT             Name of column with non effect or alternative allele, required.
  --RSID RSID           Name of column with SNP rs IDs, required.
  --BETA BETA           Alternative allele for SNPs, required.
  --EAF EAF             Name of column with effect allele frequency, required.
  --SE SE               Name of column with standard errors, required.
  --PVALUE PVALUE       Name of column with p-value, required.
  --SS SS               Column name for sample size or specify sample size (number, i.e. 10000) directly, required.
  --TYPE {hg19,hg38,GRCh37,GRCh38}
                        Specifies the genome assembly type. It should be one of the following choices: 'hg19', 'hg38', 'GRCh37', 'GRCh38'. Default is 'hg19'.
  --verbose             Enable verbose mode for more detailed output.
```

```shell
$ ./GWASkit standardize \
-I /mnt/HDRIVE/EBI/GCST001404_buildGRCh37.tsv.gz \
-O /mnt/GDRIVE/src.out/SNP/GCST001404_buildGRCh37.vcf.gz \
--TYPE GRCh37 \
--CHR chromosome \
--POS base_pair_location \
--REF other_allele \
--ALT effect_allele \
--RSID variant_id \
--BETA beta \
--EAF effect_allele_frequency \
--SE standard_error \
--PVALUE p_value \
--SS N \
--verbose
```

