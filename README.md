## compiling and running KAT generation and the test program

Generating the KAT values is as simple as navigating to the desired implementation in a subdirectory of 
the "Reference_Implementation" or "Optimized_Implementation" direcory and running the

"make KAT" 

command. This compiles the implementation and runs the compiled program, which outputs the KAT request,
response and intermediateValues files.

The test program is compiled with the "make test" command.

## enabling message recovery mode 

Message recovery mode is disabled by default. To enable it, simply uncomment the statement 

"// #define MESSAGE_RECOVERY"

in the "parameters.h" file.

## Using the python script for making parameter choices 

At the top of the script the parameters OMEGA, MAXDEPTH can be modified. 

Then, the chooseParams function is called at the bottom of the script with 3 parameters
1 - The size of the finite field to be used
2 - The log_2 of the number classical gates that an attack should costs
3 - The log_2 of the number quantum gates that an attack should costs. 
    If not specified, this is equal to the number of classical gates.

The function prints the chosen parameters, lower bounds to the complexities of the known attacks,
and the size of the keys and the signatures

## The contents of the LUOV submission

* README 	- This file.


* KAT/			- A directory containing KAT values for the various parametrizations of the LUOV scheme. This directory contains one subdirectory for each parametrization, each subdirectory contains 3 files
    * luov-r-m-v/	- A subdirectory containing KAT values for a parametrization of the LUOV scheme with message recovery disabled
    	* PQCsignKAT_*.req       	- The KAT request file, generated with PQCgenKAT_sign
        * PQCsignKAT_*.rsp      	- The KAT response file, generated with PQCgenKAT_sign
        * intermediateValues.txt 	- Contains intermediate values, generated by running PQCgenKAT_sign with the DKAT compiler flag.
    * luov-r-m-v-mr/	- A subdirectory containing KAT values for a parametrization of the LUOV scheme with message recovery enabled
        * PQCsignKAT_*.req       	- The KAT request file, generated with PQCgenKAT_sign
        * PQCsignKAT_*.rsp      	- The KAT response file, generated with PQCgenKAT_sign
        * intermediateValues.txt 	- Contains intermediate values, generated by running PQCgenKAT_sign with the DKAT compiler flag
* Reference_Implementation/ 	- Contains the reference implementation of the LUOV signature scheme. This directory contains a subdirectory for each parametrization of the LUOV scheme. Each subdirectory contains the exact same files, except for the "parameters.h" file, which contains the parameters of the scheme and is thus different for each parametrization
    * luov-r-m-v-PRNG/		- A subdirectory containing the source code for a parametrization of the LUOV scheme
        * api.h 			- Defines the size of sk, pk and s and declares the functions of the LUOV scheme
        * Buffer.{c,h}		        - Implements reader and writer objects that are used for reading from and writing to unsigned char arrays while keeping track of how many bits have been used
        * Column.{c,h}			- Implements lists of bits that support xoring and other simple functionalities
        * FrField.{c,h} 		- Implements finite field arithmetic and other operations over a finite field. The fields GF(8),GF(16),GF(32),GF(48),GF(64) and GF(80) are implemented, each in their separate files
        * intermediateValues.{c,h}	- Defines functions for printing intermediate values
        * LinearAlgebra.{c,h}		- Defines matrices and implements solving linear systems described by an augmented matrix
        * LUOV.{c,h} 			- Defines SecretKey, PublicKey and Signature objects as well as functions for serializing and deserializing these objects. Also implements the key generation, signing and verification algorithms, 
        * Makefile 			- Makefile for generating the kat values and for compilimg the test program
        * parameters.h	       	        - Contains the parameters of this LUOV parametrization
        * PQCgenKAT_sign.c		- Code provided by NIST for generating the KAT values
        * prng.{c,h}			- Defines functions for sampling objects from a PRNG
        * rng.{c,h}			- Code provided by NIST for generating pseudorandom bytes
        * test.c			- A test program generating keys, signing random messages and verifying the signatures. Reports the sizes of the keys and signed messages and time consumed by the different algorithms 

* Optimized_Implementation/ 	- Contains the optimized implementation of the LUOV signature scheme.

* AVX2_Optimized_Implementation/ 	- Contains the AVX2 optimized implementation of the LUOV signature scheme.

* Supporting_Documentation/	- Contains supporting documentation for the submission
    * LUOV.pdf			- The main design document
    * ChoiceOfParameters.py 	- A python script that helps to make secure parameter choices
