# LGNI
Repository for paper "Geodemographic Network Immunization for Epidemic Control"

# Introduction

...

# Use Guide
## Environment Setup

...

## Data Preparation

Here we publish the LA and NYC datasets used in our paper.

Each dataset contains files of mobility network, cost of locations, initial distribution of agents and 3 attack strategies which are necessary for our proposed LGNI algorithm.



## Generating control strategy

Compile and run LGNI.cpp to generate the log file with necessary parameters listed below：

* Budget.

* IIS:  Number of initially infected spectators.

* NPI:  Number of locations to be controlled per iteration.

* Step:  Maximum number of steps an agent may take.

* pl:  Probability that an infected agent passes an unaffected location making it infectious.

* lp:  Probability that an infected location makes a passing uninfected agent infected.

* uaf:  A parameter to control the initial number of agents in each location.

  ​		Generally set to 1. If set to 2, it means that the number of initial agents of each location double.

* logfile:  Path to save the log file, in which the order of  locations to be controlled (control strategy) will be recorded.

* dataset:  Directory of dataset.

* LB:  bool, use LOWER BOUND or not.

* LS:  bool, use LIMITED SPREAD or not.

```
	cd ./Code/
	g++ -O3 -fopenmp LGNI.cpp -o LGNI.out   # compile
	./LGNI.out Budget IIS NPI Step pl lp logfile dataset LB LS uaf   # run with param
	./LGNI.out 1.0 500 500 3 0.02 0.02 ../log_LGNI.txt ../Data_LA/ 1 1 1    # example
```

Then generate the control strategy from the log file.

```
	cd ../
	grep "Adding" log_LGNI.txt > ./Data_LA/Baseline_Controls/LGNI.txt
	sed -i "s/Adding: //g" ./Data_LA/Baseline_Controls/LGNI.txt
```

The control strategy will be saved in file: Data_LA/Baseline_Controls/LGNI.txt



## Evaluating control strategy

Comple and run LGNI_Baseline.cpp to evaluate the control strategy generated by LGNI or other baseline methods under different attack strategies. The results will be recorded in a result file.

Some parameters are different to the LGNI.cpp :

* logfile:  Path to save the result of spread influence under the control strategy to be evaluated and the 4 different attack strategies.

* CS:  Filename of the control strategy to be evaluated.

```
    cd ./Code/
    g++ -O3 -fopenmp LGNI_Baseline.cpp -o LGNI_Baseline.out     # compile
    ./LGNI_Baseline.out Budget IIS NPI Step pl lp logfile dataset LB CS uaf    # run with param
    ./LGNI_Baseline.out 0.2 500 500 3 0.02 0.02 ../result_LGNI.txt ../Data_LA/ 1 LGNI.txt 1    # example
```

The result will be recorded in file result_LGNI.txt
