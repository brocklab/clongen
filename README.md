# Clongen: ClonMapper Reference Generator

<p align='center'>
<img src='https://raw.githubusercontent.com/brocklab/clongen/main/assets/help.svg' width =800>
</p>

## Installation

```sh
pipx install clongen 
python3 <(curl -fsSL viv.dayl.in/viv.py) shim clongen
```

For one-time use consider using `viv run` to use an ephemeral venv, see below for an example.

*NOTE*: make sure to separate `viv` and `clongen` flags with `--`

```sh
python3 <(curl -fsSL viv.dayl.in/viv.py) run \
  clongen -- --lineages ./lineages.csv
```

## Usage

To generate a clonmapper-compatible reference genome we
first need to produce a `fasta` and `gtf` file of our expected lineages.
This is where `clongen` comes in.
The only input is a single `csv` that can come in one of two forms.

```csv
id,lineage
lineage1,ATGATCATGGTACCATAAGG
...
```

You may also provide a simpler version with only lineage sequences:

```csv
ATGATCATGGTACCATAAGG
...
```

The header is optional, however we will only attempt to match with `id,lineage` or `lineage`.
Any other header will likely not be removed and assumed to be a lineage and id.

If the input list contains id's these will be used as the `gene_name`.
Otherwise we will use the full lineage sequence proceeded by the prefix designated by prefix flag, by default "lin-".

Then we can generate `clonmapper.gtf` and `clonmapper.fa` by default in `./references`:

```sh
clongen --lineages ./lineages.csv
```

<!--TODO: add instructions for generating reference genome with cellranger mkref and included script-->
