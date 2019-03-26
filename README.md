# A birthday type attack to Naccache Stern Knapsack (NSK) cryptosystem

We provide an improved and parallel implementation of a previous attack ([1]) to Naccache-Stern knapsack (NSK) cryptosystem.
The cryptosystem is described in [2]. 

[1] M. Anastasiadis, N. Chatzis and K. A. Draziotis, Birthday type attacks to the Naccache-Stern Knapsack cryptosystem, 
Information Proc.Letters (Elsevier) Vol. 138, October 2018, Pages 39-43. 

[2] D. Naccache and J. Stern, A New Public Key Cryptosystem Based on Higher Residues, Proceedings of the 5th ACM Conference on Computer and Communications Security. CCS '98. ACM. pp. 59–66. doi:10.1145/288090.288106.

For reporting bugs, please refer to the original [repository](https://github.com/vamartid/NSK-birthday-attack). 

## Authors

* **Vasileios Martidis**

## License

This project is licensed under the GPLv3 License - see the [LICENSE.md](LICENSE.md) file for details.

## Getting Started

First, you need to install the following programs.

* [GMP](https://gmplib.org/) - Arithmetic without limitations
* [args](https://github.com/Taywee/args) - Argument parsing library
* [OpenSSL](https://www.openssl.org/) - Used for the md5-hashes

and for the parallel version (optional)
* [Openmp](https://www.openmp.org/) - API specification for parallel programming

Tested succesfully with g++ ver.4.9.2-10

To build the project,
```
$git clone https://github.com/drazioti/NSK-birthday-attack.git
$cd NSK-birthday-attack/procedural/
$make all2
```
To build the parallel version,
```
$cd NSK-birthday-attack/parallel/
$make all2par
```

This make argument, builds the project and we get multy.out which is the excecutable.

### Running the attack

You can view how to use the arguments of the excecutable like this. 
```
$./multy.out --help
```

After reading the help output. We can run for example an attack to a message with hamming 7 and p of 2048-bits and b=n/2-3  like this.
```
$./multy.out -p 3 --ham 7 --sb 3
```

For instance 
```
$./multy.out -p 1 --ham 7 --sb 0
---------Generating keys...
number bits of prime p: 600
message   : 19342886918842423195996160
Hamming weight of msg: 7
Bound of the attack : 42
---------Starting ...
Round : 1
h1 4
h2 3
time : 4.568272s
Round : 2
h1 4
h2 3
time : 4.586754s
Round : 3
h1 4
h2 3
msg = 19342886918842423195996160
time : 4.605926s
Overall time : 13.760952s
```

## Parallelism
After experiments we calculated that the cost of the computation to construct the
sets Ui,hi , is the most intensive part of the algorithm.
In this implementation we parallelized the creation of the elements of the sets Ui,hi, so that each thread will have to calculate one element and add it to the Ui,hi set.

Also we use the [libstdc++ parallel mode](https://gcc.gnu.org/onlinedocs/libstdc++/manual/parallel_mode_using.html) for the functions sort,intersection and find_if.


## Acknowledgments

* [First version of this attack written in Sagemath](https://github.com/drazioti/python_scripts/tree/master/paper_ns)
