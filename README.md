Lensingbiases
==

Computation of N0 and N1 biases in the context of CMB weak lensing (flat-sky approximation).
Derivatives of N1 biases with respect to the lensing potential power-spectrum available.

**Modified version:** only the N1 computation was modified and checked. In this new version we have allowed to pass the observed angular power spectra as a parameter. Now, the ini file is not needed and the noise power spectra is not calculated internally. All the information is passed via the arguments of the python function LensingBiases.compute_n1_py(...), which computes the unnormalized N1 bias. We did not integrate the N0 computation accordingly in this modified version, so it is probably that it does not work.

License: GNU License (see the LICENSE file for details) covers all files
in the lensingbiases repository unless stated otherwise.

### Before starting
The Python code has the following dependencies:
* numpy, pylab, argparse
* f2py (make sure is f2py3 if you are using python3)

In most machines, those packages are automatically installed.
Make sure you update your PYTHONPATH to use the code.
Just add in your bashrc:
```bash
BIASPATH=/path/to/the/package
export PYTHONPATH=$PYTHONPATH:$BIASPATH
```

### Compilation of Fortran
The package is written in python, but internal operations are
done in Fortran. Therefore you need to compile it before using
the routines. We provide a setup file. Just run:
```bash
python setup.py build_ext --inplace [--fcompiler=gfortran]
```
Depending on system, you may need to specify a different fortran compiler.
For the purist, we also provide a Makefile for a direct compilation.
For extended multipole ranges, computation can be long.
So make sure that you are using several processors by adding in your bashrc:
```bash
export OMP_NUM_THREADS=n
```
Check in python that the OPENMP paralization is working properly:

```python3
>> import LensingBiases
>> LensingBiases.checkproc_py()
You are using n processors
```



### Usage
User has to provide the range of multipole, beam width, noise level, etc.
In order to ease the start, we provide both a test script and a launcher:
* LensingBiases.py (see the main)
* launch.sh

For usage on clusters, we also provide a batch (SLURM).
