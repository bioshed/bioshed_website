---
title: BioShed Documentation
layout: page.njk
---

### Installation ###

Make sure pip (https://pypi.org/project/pip/) is installed on your system and type:

**`$ pip install bioshed`**

Depending on your system, you may need to use pip3 (BioShed uses Python 3), and you may need to install it as a user:

**`$ pip3 install --user bioshed`**

### Initialization and Setup ###

Once installed, initialize your BioShed environment by typing:

**`$ bioshed init`**

You will be prompted for your BioShed username and password. If you don't have a BioShed account, you can sign up for a free account <a href="https://bioshed.io/signup">here</a>.

To unlock the full power of BioShed, we highly recommend you setup a cloud environment. BioShed currently integrates with AWS cloud services. If you don't already have an AWS account, get a free account <a href="https://aws.amazon.com/free/" rel="noopener" target="_blank" title="AWS">here.</a>

To setup and integrate BioShed into your existing AWS environment, type:

**`$ bioshed setup aws`**

You will be prompted for your AWS credentials.  For help with AWS user credentials, see <a href="https://www.youtube.com/watch?v=qmtDRmplMG4">here</a>.

You will also be prompted for a public security key, which is used to access AWS resources. Generate a public key by typing:

**`$ ssh-keygen`**

and following the instructions to generate two files: <KEY_FILE> (private key) and <KEY_FILE>.pub (public key). Copy the contents of <KEY_FILE>.pub when prompted during BioShed setup.

BioShed has been verified to work on Linux and Mac OS X systems. If you are having trouble installing or setting up BioShed, please contact us at <a href="mailto:support@bioshed.io">support@bioshed.io</a>.

================================================================================
### BioShed OS ###

BioShed OS is a cloud operating system that allows you to run bioinformatics applications in the cloud, without the need to manually install software or setup infrastructure.

We currently have over 50 pre-built applications you can run, including:

- &dash; fastqc
- &dash; bowtie2
- &dash; bwa
- &dash; STAR (RNA-STAR)
- &dash; deseq2
- &dash; varscan2

You can also easily build and integrate your own applications into the BioShed environment, and even share your applications with the BioShed community.

To get started, make sure you have a cloud account (we currently support AWS) and you have properly initialized and setup your BioShed environment.

IMPORTANT: You need to first deploy the core BioShed OS infrastructure to your cloud environment. To do this, type:

`$ bioshed deploy core`

To run an application, you simply prefix with **bioshed run** and run as you would on the command line. For example:

`$ bioshed run fastqc s3://myfastqs/my-R1.fastq.gz`

Will run FastQC in your cloud environment and output the results back to the same folder as the input FASTQ file. When you run a BioShed application, we recommend you specify a remote output path by providing **out::** as the last argument, like so:

`$ bioshed run fastqc s3://myfastqs/my-R1.fastq.gz out::s3://fastqcout/`

For help with any application module, make sure you have <a href="https://docs.docker.com/get-docker/">Docker</a> installed and configured on your system, and just type:

`$ bioshed run --local <MODULE_NAME> --help`

For Admins: To uninstall and tear down your BioShed infrastructure, type the following:

`$ bioshed teardown aws`

`$ pip uninstall bioshed`

For more help, please contact us at <a href="mailto:support@bioshed.io">support@bioshed.io</a>

================================================================================
### BioShed Atlas ###

BioShed Atlas is an easy-to-use command-line tool for downloading public datasets from common genomic repositories such as NCBI, ENCODE, TCGA, etc.

Our beta product currently integrates with ENCODE (https://encodeproject.org).

#### ENCODE ####

To get started, simply type:

`$ bioshed search encode`

You will get complete information on all existing datasets within ENCODE and the appropriate search categories, from which you can perform relevant searches.

To do a general search for datasets on ENCODE, simply type your search terms:

`$ bioshed search encode <SEARCH_TERMS>`

For example, to search for breast cancer RNA-Seq datasets, type:

`$ bioshed search encode breast cancer rna-seq`

You can also do a refined search using search categories:

`$ bioshed search encode --tissue breast cancer --assay rna-seq`

Once you perform a search, relevant search results are output to a file **search_encode.txt**. This results file contains all relevant biosamples or experiments from your search, one per row.

This search results file is used to download relevant files with the following command:

`$ bioshed download encode`

NOTE: You MUST first run **bioshed search** before you can run **bioshed download**.

You can filter which files you want to download by adding search terms:

`$ bioshed download encode --filetype fastq`

By default, this will download to the current folder. You can specify a relative path to download with the --output parameter. The output path can be local or cloud storage.

`$ bioshed download encode --output /my/local/dir`
`$ bioshed download encode --output s3://my/s3/folder`

NOTE: Again, you MUST have a bioshed_encode.txt search results file before you can run bioshed download.

If you only want to download new files (i.e., don't overwrite existing files), type:

`$ bioshed download encode --update`

For help with anything else, including a full list of search categories and valid command-line arguments, type:

`$ bioshed search encode --help`

`$ bioshed download encode --help`

================================================================================
### BioShed Shuttle ###

We currently have a beta application you can install on a Linux machine to transfer sequencing files from a sequencer or local server to your cloud environment.

If interested, please contact us at support@bioshed.io and we will provide a download link.


================================================================================
### BioShed Portal ###

We currently have a working prototype for a web-based portal from which you can access, upload and download your sequencing files and data.

If you are interested in a demo, please contact us at support@bioshed.io.
