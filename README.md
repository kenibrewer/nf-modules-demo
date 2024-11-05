# kenibrewer/nf-modules-demo

Adapted from [nf-core/modules/README.md](https://github.com/nf-core/modules/blob/master/README.md)

[![Nextflow](https://img.shields.io/badge/nextflow%20DSL2-%E2%89%A521.10.3-23aa62.svg?labelColor=000000)](https://www.nextflow.io/)
[![run with conda](http://img.shields.io/badge/run%20with-conda-3EB049?labelColor=000000&logo=anaconda)](https://docs.conda.io/en/latest/)
[![run with docker](https://img.shields.io/badge/run%20with-docker-0db7ed?labelColor=000000&logo=docker)](https://www.docker.com/)
[![run with singularity](https://img.shields.io/badge/run%20with-singularity-1d355c.svg?labelColor=000000)](https://sylabs.io/docs/)

A demo nf-core style modules library generated using nf-core/modules-template.

## Table of contents

- [kenibrewer/nf-modules-demo](#kenibrewer/nf-modules-demo)
  - [Table of contents](#table-of-contents)
  - [Using existing modules](#using-existing-modules)
  - [Adding new modules](#adding-new-modules)
  - [Help](#help)
  - [Citation](#citation)

## Using existing modules

The module files hosted in this repository define a set of processes for software tools that allow you to share and add common functionality across multiple pipelines in a modular fashion.

We use a helper command in the `nf-core/tools` package that uses the GitHub API to obtain the relevant information for the module files present in the [`modules/`](modules/) directory of this repository. This includes using `git` commit hashes to track changes for reproducibility purposes, and to download and install all of the relevant module files.

1. Install the latest version of [`nf-core/tools`](https://github.com/nf-core/tools#installation) (`>=2.0`)
2. List the available modules:

   ```bash
   nf-core modules --git-remote https://github.com/kenibrewer/nf-modules-demo.git list remote
   ```

   ```console

                                ,--./,-.
        ___     __   __   __   ___     /,-._.--~\
   |\ | |__  __ /  ` /  \ |__) |__         }  {
   | \| |       \__, \__/ |  \ |___     \`-._,-`-,
                                `._,._,'

   nf-core/tools version 3.0.1 - https://nf-co.re

   INFO     Modules available from https://github.com/kenibrewer/nf-modules-demo.git (main):

   ┏━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
   ┃ Module Name                    ┃
   ┡━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┩
   │ examplemodule       │
   ..truncated..
   ```

3. Install the module in your pipeline directory:

   ```bash
   nf-core modules --git-remote https://github.com/kenibrewer/nf-modules-demo.git install examplemodule
   ```

   ```console

                                ,--./,-.
        ___     __   __   __   ___     /,-._.--~\
   |\ | |__  __ /  ` /  \ |__) |__         }  {
   | \| |       \__, \__/ |  \ |___     \`-._,-`-,
                                `._,._,'

   nf-core/tools version 3.0.1 - https://nf-co.re

   INFO     Installing 'examplemodule'
   INFO     Use the following statement to include this module:

      include { EXAMPLEMODULE } from '../modules/kbrewer/examplemodule/main'
   ```

4. Import the module in your Nextflow script:

   ```nextflow
   #!/usr/bin/env nextflow

   nextflow.enable.dsl = 2

   include { EXAMPLEMODULE } from '../modules/kbrewer/examplemodule/main'
   ```

5. Remove the module from the pipeline repository if required:

   ```bash
   nf-core modules --git-remote https://github.com/kenibrewer/nf-modules-demo.git remove examplemodule
   ```

   ```console

                                ,--./,-.
        ___     __   __   __   ___     /,-._.--~\
   |\ | |__  __ /  ` /  \ |__) |__         }  {
   | \| |       \__, \__/ |  \ |___     \`-._,-`-,
                                `._,._,'

   nf-core/tools version 3.0.1 - https://nf-co.re

   INFO     Removed files for 'examplemodule' and its dependencies 'examplemodule'.
   ```

6. Check that a locally installed nf-core module is up-to-date compared to the one hosted in this repo:

   ```bash
   nf-core modules --git-remote https://github.com/kenibrewer/nf-modules-demo.git lint examplemodule
   ```

   ```console

                                ,--./,-.
        ___     __   __   __   ___     /,-._.--~\
   |\ | |__  __ /  ` /  \ |__) |__         }  {
   | \| |       \__, \__/ |  \ |___     \`-._,-`-,
                                `._,._,'

      nf-core/tools version 3.0.1 - https://nf-co.re

      INFO     Linting pipeline: '.'
      INFO     Linting module: 'examplemodule'

      ╭─ [!] 6 Module Test Warnings ──────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────╮
      │              ╷                             ╷                                                                                                                                          │
      │ Module name  │ File path                   │ Test message                                                                                                                             │
      │╶─────────────┼─────────────────────────────┼─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────╴│
      │ examplemodule       │ modules/kbrewer/examplemodule/main.nf  │ Unable to connect to container registry, code:  403, url: <https://www.docker.com/kbrewercc/examplemodule-suite:2.0.9>                                │
      │ examplemodule       │ modules/kbrewer/examplemodule/main.nf  │ Container versions do not match                                                                                                          │                                                                  │
      │              ╵                             ╵                                                                                                                                          │
      ╰───────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────╯
      ╭───────────────────────╮
      │ LINT RESULTS SUMMARY  │
      ├───────────────────────┤
      │ [✔]  59 Tests Passed  │
      │ [!]   6 Test Warnings │
      │ [✗]   0 Tests Failed  │
   ```

## Citation

If you use the module files in this repository for your analysis please you can cite the `nf-core` publication as follows:

> **The nf-core framework for community-curated bioinformatics pipelines.**
>
> Philip Ewels, Alexander Peltzer, Sven Fillinger, Harshil Patel, Johannes Alneberg, Andreas Wilm, Maxime Ulysse Garcia, Paolo Di Tommaso & Sven Nahnsen.
>
> _Nat Biotechnol._ 2020 Feb 13. doi: [10.1038/s41587-020-0439-x](https://dx.doi.org/10.1038/s41587-020-0439-x).

## Template

This module library was create using [nf-core/modules-template](https://github.com/nf-core/modules-template).

You can fetch updates to the library template by running:

```bash
pipx install copier
copier update
```
