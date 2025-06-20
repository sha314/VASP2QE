# VASP2QE
A simple code to convert a VASP POSCAR to a Quantum ESPRESSO (QE) input file.
The code was used in a project testing the time-reversal symmtery feature of LOBSTER as reported in this publication:
http://dx.doi.org/10.1002/jcc.26353

Installing the requirements in Ubuntu
```
sudo apt-get install libboost-all-dev
sudo apt-get install libeigen3-dev
```


The code needs the boost library and can be compiled by the following command:

```
g++ -I/usr/include/eigen3 -o vasp2qe.x vasp2qe.cpp -lboost_filesystem -lboost_system
```

you'll see the 


Once the binary is generated, you need to put the binary in your bin directory. To run the program simply use the following command:
```
vasp2qe.x \<path-to-poscar-or-contcar\>/POSCAR
```
OR 
```
vasp2qe.x \<path-to-poscar-or-contcar\>/POSCAR DENSITY
```

where DENSITY is an integer number representing the kpoint density (in the unit of kpoints x atoms) to generate the number of kpoints for three directions.
Note that, unlike the previous version, this version always requires user to specify POSCAR.

The result will be output to the stdout. Once the QE input file is produced, you still need to set the values for the variables ecutwfc and nbnd, the pseudo-potential filenames in order for the input file to be useable for a QE calculation.

UPDATE:
The program can now take an int argument to specify a kpoint density for automatic setup of the number of k-mesh.
An example can be found in the directory "example". The output (mp-720.scf.in) was produced with the following command:

```
vasp2qe.x POSCAR_mp-720 8000 > mp-720.scf.in
```