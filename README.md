# AccordDaTools
Collection of ACCORD DA tools. So far we have jbdiagnose and associated plotting. 

Desirables:
- diacov
- festat
- TuneBR
- obstat
- Other ...

## Installation
```
cd AccordDaTools
mkdir build
cd build
cmake .. -DCMAKE_INSTALL_PREFIX=/path/to/da_tools 
make 
ctest
make install
```
Add DA Tools to your PATH:
```
export PATH=/path/to/da_tools:$PATH
```

## Tools
### Structure functions
#### Jb diagnose
Full documentation is available [here](doc/tools/jbdiagnose.md).

Help/usage:
```
jbdiagnose -h
```

Example:
```
jbdiagnose -b jb_data/stabfiltn_IRELAND75L65_jbconv.bal -c jb_data/stabfiltn_IRELAND75L65_jbconv.cv -g 15000 -l harmL65 -e IRELAND75L65
```

#### plotjbbal
Help/usage:
```
plotjbbal -h
```

Example:
```
plotjbbal -t stdv -p QQ -r ./ -e IRELAND75L65
```

#### plotjbdiag
Help/usage:
```
plotjbdiag -h
```

Example:
```
plotjbdiag -l 50 -t vercor -p QQ -r ./ -e IRELAND75L65 
```
### VarBC
#### VARBC.cycle data extraction
Help/usage:
```
varbcdiagnose -h
```

Example:
```
varbcdiagnose -i /path/to/directory/with/varbc_files/ -o varbc_diag_out
```

#### VarBC predictor time-series plotting
Help/usage:
```
plotvarbcpred -h
```

Example:
```
plotvarbcpred -i varbc_diag_out/VARBC_3_16_3309_210000 -b
```

### DFS
#### DFS computation
The dfscomp tool reads the (ASCII) data from an unperturbed CCMA and a perturbed CCMA.

Help/usage:
```
dfscomp -h
```

Example:
```
dfscomp -p CCMA_2022050112.dat -u CCMA_2022050112_unpert.dat -o dfs2022050112.dat
```

### DIACOV
First, you should have Festat output and the DIACOV binary compiled by Harmonie stored somewhere.
Then, create the new directory, copy the DIACOV binary and Jb files there. Example:
```
mkdir DiacovTest
cd DiacovTest
cp /path/to/DIACOV .
mkdir dataTest
cp /path/to/Jb/data dataTest/.
```
#### Run Diacov
Use rundiacov script to initiate the processing of the Jb files.
Help/usage:
```
rundiacov -h
```

Example:
```
rundiacov -i dataTest -c METCOOP25D_65_2021100300-2021111006_412 -l 65 -g 2.5 -m 539 -n 1080 -d DIACOV
```

#### Produce diagonal stats
When you get DIACOV output, use diag_diacov script to produce stats in ASCII format, which are suitable for further plotting.
Help/usage:
```
diag_diacov -h
```

Example:
```
diag_diacov -i dataTest -o stats
```

#### Produce plots
Use plotdiacov script to produce the plots from ACSII files.
Help/usage:
```
plotdiacov -h
```

You can either produce the plots for all of the available stat files, or to choose specific ones. Examples:
```
plotdiacov -d ./stats (the plots will be saved to the same directory as stat files)
plotdiacov -i ./stats/corqu65.dat -o ./stats/corqu65.png (if the output file name is not specified, the plot is saved to the pwd with the default name "output.png")
```
