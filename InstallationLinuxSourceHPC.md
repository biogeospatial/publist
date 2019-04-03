These instructions apply to version 2.99_001 and later.

They are based on development on Centos 6.3, but have not been tested line by line when written.  Please report any errors or suggestions.  

They also assume you are using a standard user account, and are accessing Biodiverse through the git repository.


**Table of contents:**
* [Installation](#installation)
* [Running it](#running-it)
* [Troubleshooting](#troubleshooting)


# Installation #

  * Install PerlBrew, including its optional cpanm client.  Instructions are at http://perlbrew.pl/
    * There are other othertanites like plenv, but I have not tested them.  Regardless, **you should not use the system perl**.  The operating system assumes specific versions of files are in the system perl.  Perlbrew is recommended, and is used for Biodiverse development, and is assumed below.  

  * Make sure you are using the perlbrew perl, you need to make sure it is the one you call in subsequent steps.  This could involve adding a line to your .bashrc (or equivalent) file to ensure it is loaded each time you login.  
  
  *  These instructions assume you are not installing the GUI components.  It is possible to do, and details can be added if needed.  


```bash

  ##  if you are using perlbrew and forgot to install the cpanm client:
  perlbrew install-cpanm

  ## Now install the rest of the dependencies
  ## Note that new deps might be added as 
  ## part of the development process
  cpanm Task::Biodiverse::NoGUI

  ## some libs to make Biodiverse go faster
  ## Panda::Lib does not install on Windows, so is not in the generic dep list
  cpanm Panda::Lib
  ##  Biodiverse::Utils is not yet on cpan
  cpanm http://www.biodiverse.unsw.edu.au/downloads/Biodiverse-Utils-1.06.tar.gz
  
  #  Alien::gdal is a big dependency.
  #  Note that, if you have GDAL version 2.1 or higher already 
  #  installed on your system then this will use that version instead of building its own.
  #  If you have loaded a system GDAL using ```module load``` or similar then you need to ensure
  #  it is loaded each time you run Biodiverse or it will fail to run.  
  cpanm Alien::sqlite
  cpanm Alien::proj
  cpanm Alien::gdal
  
  ##  Geo::GDAL::FFI also depends on PDL, for which installation will take a little while
  cpanm Geo::GDAL::FFI


```



# Running it #

  * Run your scripts as you would any other perl script, e.g.
```bash
perl ~/biodiverse/bin/run_randomisation.pl
```



# Troubleshooting #
  * If you are keeping up with the git development then you will occassionally need to install extra dependencies.  
    If perl complains that you are missing a module called Blort::Bork then you can run ```cpanm Blort::Bork``` 
    at the command line to install it and its dependencies.  
  * Please report any issues using the [project issue tracker](https://github.com/shawnlaffan/biodiverse/issues/)