
# autoBIGS.Galaxy

A program that allows quickly batched requests for obtaining MLST profiles on multiple FASTA sequences and exporting it as a convenient CSV. Capable of querying a variety of MLST databases from both Institut Pasteur and PubMLST. autoBIGS.galaxy is the galaxy frontend implementation of autoBIGS.cli and autoBIGS.engine.

This Galaxy tool implements [autoBIGS.engine](https://pypi.org/project/autoBIGS.engine) via wrapping the official [autoBIGS.cli](https://github.com/Syph-and-VPD-Lab/autoBIGS.cli) wrapper.

## Features

This CLI is capable of exactly what [autoBIGS.engine](https://pypi.org/project/autoBIGS.engine) is capable of:
- Import multiple whole genome FASTA files
- Fetch the available BIGSdb databases that is currently live and available
- Fetch the available BIGSdb database schemas for a given MLST database
- Retrieve exact/non-exact MLST allele variant IDs based off a sequence
- Retrieve MLST sequence type IDs based off a sequence
- Inexact matches are annotated with an asterisk (\*)
- Output all results to a single CSV
