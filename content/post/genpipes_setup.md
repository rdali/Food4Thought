---
layout:     post 
title:      "Setting up GenPipes on Compute Canada Servers"
subtitle:   "Accessing C3G/GenPipes resources"
description: "GenPipes is a Workflow Management System/Framework that I help develop at C3G. It eases the analysis of genomics data. This piece goes over how to set up GenPipes on the Compute Canada servers."
date:       2018-08-26
author:     "Rola Dali"
URL: "/2018/genpipes_setup/index.html"
tags:
    - Genomics
    - RNASeq
    - C3G
    - GenPipes
    - Compute Canada
categories: [ Genomic Analysis ]
image:      ""
---



# Overview:

In this practical, we will set up **_GenPipes_**, to be able to access its installed **modules**, **pipelines** and **genomes**.


<br/>

# Setting up GenPipes:

To set up _GenPipes_, you will need to add some lines of code in your **bash_profile** file on the server you will be using. The bash_profile is a hidden file in your home directory that sets up your environment every time you log in. Alternatively, you can also use your **bashrc** file.  


> A Note on hidden files:

<details>
  <summary>
**Hidden Files** (click here)
  </summary>

Hidden files start with a `.` at the beginning of their names. For example: `.bash_profile` or `.bashrc`. To be able to see hidden files, you need to use:

`ls -a`

</details>


Let's start:


**1- Connect to the server:**

Open a terminal window and log into the server:


```bash
#<my_cc_account> is your CC user name
ssh <my_cc_account>@mp2.ccs.usherbrooke.ca
```  



**2- Add Code to your bash_profile:**

```bash
## open bash_profile:
nano $HOME/.bash_profile
```


Copy/Paste the following text into your .bash_profile *after* modifying the last 2 lines with your information:

```bash
## GenPipes/MUGQIC genomes and modules
export MUGQIC_INSTALL_HOME=/cvmfs/soft.mugqic/CentOS6
module use $MUGQIC_INSTALL_HOME/modulefiles
module load mugqic/python/2.7.13
module load mugqic/genpipes

## Modify text below within <> to add you own email and CC_account ID:
export JOB_MAIL=<my.name@my.email.ca>
export RAP_ID=<cc_account> 

```

**Note:** The RAP_ID is usually in the form of `def-<account>` or `rrg-<account>`.


Exit nano (control/Ctrl + X).



**3- Source your bash_profile:**

After making changes to your bash_profile file, you will either need to source it, using:

`source $HOME/.bash_profile`

**OR** you need to log out and then log in again.


**Now you are ready to use GenPipes!**

To test whether everything worked, type in the following command:

`rnaseq.py`


You have succeeded, if you get something that looks like this:

**usage: rnaseq.py [-h] [--help] [-c CONFIG [CONFIG ...]] ...**


If you get **bash: rnaseq.py: command not found**, then something is not right. Let us know.

<br/>

# GenPipes Modules:

GenPipes gives you access to hundreds of bioinformatics [tools/modules](http://www.computationalgenomics.ca/cvmfs-modules/) pre-installed by our team. To explore the available tools, you can type:

`module avail mugqic/`


This will allow you to use bioinformatics tools like Samtools, Homer, MACS2, without installing them yourself.

You can load them as follows:

```bash
# module add mugqic/<tool>/<version>
module add mugqic/samtools/1.4.1
# Now samtools 1.4.1 is available to use. To check:
samtools
```


  
> What are Modules and Why do we need them?

<details>
  <summary>
**More about Modules** (click here)
  </summary>

"Modules" are a way to load software or tools when we need them.

Every time a computer runs a command (example "ls"), it needs to find the instructions to do so. It looks for the instructions in places listed in a variable called the **"$PATH"**. Every time you install a new tool, you need to add its location to your $PATH. Every time you issue a command (like ls), the computer will search through all the places listed in the $PATH to find the instructions on what to do.

Imagine, for servers that have thousands of users, each in need of several software, how long the PATH can get and how much that can slow down the system!

To avoid this, installed software is packaged in "modules" that you can be loaded when needed. The software is installed on the computer but the computer is not aware of it until you "load"" the module, which adds the software location to the $PATH.

To see what is in your $PATH, use:

`echo $PATH`

To see where the instructions of a command are stored, you can use `which`.
`which ls`

For ls, the instruction are usually stored in: /bin/ls


</details>




> What are the Modules that are available with GenPipes?

<details>
  <summary>
**GenPipes Modules:** (click here)
  </summary>

Command: 

`module avail mugqic/`

**OR** check out this [page](http://www.computationalgenomics.ca/cvmfs-modules/).

</details>

 <br/>

# GenPipes Pipelines:

GenPipes comes with [12 Pipelines](https://bitbucket.org/mugqic/genpipes/src/ec3183ff39ed8371446fc243d41971efd0d092ac/pipelines/?at=master) for various genomics analyses, named `<pipeline>.py`.

To use the pipeline, you just need to type its name:

```bash

## for rnaseq, the pipeline is rnaseq.py. Try typing:

rnaseq.py
```

The pipelines are found in:

`ls -ltrh $MUGQIC_PIPELINES_HOME/pipelines/`

<br/>

# GenPipes Genomes:

GenPipes also gives you access to pre-installed [genomes](http://www.computationalgenomics.ca/cvmfs-genomes/) available in `$MUGQIC_INSTALL_HOME/genomes/species/`.

To check all the available species, type:

`ls $MUGQIC_INSTALL_HOME/genomes/species`


All genome-related files, including indices for different aligners and annotation files can be found in:

```bash
# $MUGQIC_INSTALL_HOME/genomes/species/<species_scientific_name>.<assembly>/

## so for Homo Sapiens hg19 assembly, that would be:
ls $MUGQIC_INSTALL_HOME/genomes/species/Homo_sapiens.hg19/
```



> What are the Genomes that are available with GenPipes?

<details>
  <summary>
**GenPipes Genomes:** (click here)
  </summary>

Command: 

`ls $MUGQIC_INSTALL_HOME/genomes/species`

**OR** check this [page](http://www.computationalgenomics.ca/cvmfs-genomes/).


</details>

<br/>

# Extra:

> GenPipes Test Data:

<details>
  <summary>
**GenPipes Test Data** (click here)
  </summary>

To test GenPipes, some small test datasets can be downloaded from this [page](http://www.computationalgenomics.ca/test-dataset/). 

</details>



> A note about CVFMS:

<details>
  <summary>
**More about CVMFS** (click here)
  </summary>

GenPipes is currenlty installed on many servers (Abacus, Guillimin, Mammouth, Cedar, Graham...). To avoid discrepancy between compute sites, GenPipes setup has been centralized to one location which is then distributed on a real-time shared file system: the CERN Virtual Machine File System (CVMFS). This helps us make sure that all the components of GenPipes are the same across servers. 

</details>

<br/>
<br/>
<br/>
<br/>


