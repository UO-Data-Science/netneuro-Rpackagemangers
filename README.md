# netneuro: R Package Managers Conda

Package managers in R help when working on different projects that may require packages with different versions or have dependencies that may conflict with each other. There are a few options that work with R for example

* [renv](https://rstudio.github.io/renv/articles/renv.html) - This is a package that works within R to create project folders that have metadata to recreate and share the environment. Its main drawback is that it does not easily let you handle different versions of R itself, and it can be tricky (speaking for Jake) to get working in RStudio. 

* [conda](https://docs.anaconda.com/working-with-conda/packages/using-r-language/) - this is a very popular package manger used for python, however, also it has support for R packages. It can be used to track different versions of R, but requires a little more work on the command line.

For this powerup we'll use conda.

# Conda for R

An **Enviroment** contains all the software packages you need for a project each enviroment has a name, and you will need to install all the packages you need once for each enviroment. Enviroments are normally created, activated, and deactivated on the command line. 

## Creating an Environment

1) Download and install https://docs.anaconda.com/anaconda/install/

2) Create a Conda environment on the command line

To create a Conda environment for R, you can use the following command on the command line:
```
conda create -n myenv 
```
This will create a new Conda environment named "myenv". You can replace "myenv" with your preferred environment name.

3) Activate
To activate the environment, use the following command:

```
conda activate myenv
```
4) Install packages

One an enviroment is activated you can install software into it. Install r and r-studio with

```
conda install conda-forge::r-base
conda install rstudio
```

to launch `rstudio` run 

```
rstudio 
```

rstudio should now be using the most recent version of R. 

## Creating an enviroment with an older version of R

Lets create another environment with R version 3.6.1

1) Deactivate your previous environment

```conda deactivate```

2) Create a new environment

```
conda create -n r3_6 
conda activate r3_6


conda install conda-forge::r-base==3.6.1
conda install rstudio
```


this is normal conda syntax for installing a package with a different version.
``` conda installl package==version ```

your rstudio should now be running with R version 3.6.1

# Installing Packages

To install R packages into a Conda environment, you can use the `install.packages()` function as usual. However, you need to make sure that the Conda environment is activated before installing the packages.

Here are the steps to install packages into a Conda environment:

1. Activate the Conda environment:
    ```
    conda activate myenv
    ```

2. Launch R from the command line:
    ```
    R
    ```
or with rstudio
    ```
    rstudio
    ```

3. In the R console, install the desired packages using `install.packages()`. For example:
    ```
    install.packages("tidyverse")
    ```


# Troubleshooting

* Enviroments rely on software being isolated from software in other enviroments in R this is done by setting the .libpath to make sure this works try running R in the terminal

```R
R
```
```
R version 3.6.1 (2019-07-05) -- "Action of the Toes"
Copyright (C) 2019 The R Foundation for Statistical Computing
Platform: x86_64-apple-darwin13.4.0 (64-bit)

R is free software and comes with ABSOLUTELY NO WARRANTY.
You are welcome to redistribute it under certain conditions.
Type 'license()' or 'licence()' for distribution details.

  Natural language support but running in an English locale

R is a collaborative project with many contributors.
Type 'contributors()' for more information and
'citation()' on how to cite R or R packages in publications.

Type 'demo()' for some demos, 'help()' for on-line help, or
'help.start()' for an HTML browser interface to help.
Type 'q()' to quit R.

```


```
.libPaths()
"/opt/anaconda3/envs/r3_6/lib/R/library"
```

if your libpath has more than one directory, or does not point to  ```.../<enviroment_name>/lib/R/libarary``` you may be setting the variable somewhere else, this might happen if you've used renv in the past or are setting it in a .Rprofile file in your directory. You'll need to remove those to get conda working.
