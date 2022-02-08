![GitHub Classroom Workflow](../../workflows/GitHub%20Classroom%20Workflow/badge.svg?branch=main)
<img alt="points bar" align="right" height="36" src="../../blob/badges/.github/badges/points-bar.svg" />

# COMP0061 -- Privacy Enhancing Technologies -- Lab 04

This lab will cover Zero Knowledge Proofs.

### Structure of Labs
The structure of all the labs will be similar: two Python files will be provided. 

- The first is named `lab0X.py` and contains the structure of the code you need to complete. 
- The second is named `lab0X_test.py` and contains unit tests (written for the Pytest library) that you may execute to 
partially check your answers.

Note that the tests passing is a necessary but not sufficient condition to fulfill each task.
There are programs that would make the tests pass that would still be invalid (or blatantly insecure) implementations.

The only dependency your Python code should have, besides Pytest and the standard library, is the Petlib library, 
which was specifically developed for this course (and also for our own use!). 

The petlib documentation is [available on-line here](http://petlib.readthedocs.org/en/latest/index.html).

### Checking out code

Check out the code by using your preferred git client (e.g., git command line client, Github Desktop, Sourcetree).
**Alternatively**, if you are using Visual Studio Code, click the `Open in Visual Studio Code` button above to automatically check
out and open the repository. Visual Studio Code also allows the use of 
[development containers](https://code.visualstudio.com/docs/remote/containers).

### Setup
The intended environment for this lab is the Linux operating system with Python 3 installed.

#### Local virtual environment

We provide a `setup.sh` file that creates a local virtual environment, installs the dependencies needed for the lab,
and activates the virtual environment. To run the setup file, type `source setup.sh` into the terminal. The virtual
environment is needed to run the unit tests locally. 

#### Visual Studio Code development containers

As an alternive to a local virtual environment, we provide the setup files for VSCode 
[development containers](https://code.visualstudio.com/docs/remote/containers)
which use [Docker](https://docs.docker.com/get-docker/) to create a separate development environment for each 
repository and install the required libraries. You don't need to know how to use Docker to use development containers.

#### Github tests

The tests are the same as the ones that run as part of the Github Classroom automated marking system, 
so you can also run the tests by simply committing and pushing your changes to Github, without the need for a local 
setup or even having Python 3 installed.

### Working with unit tests
Unit tests are run from the command line by executing the command:

```sh
$ pytest -v
```

Note the `-v` flag toggles a more verbose output.
If you wish to inspect the output of the full tests run you may pipe this command to the `less` utility 
(execute `man less` for a full manual of the less utility):

```sh
$ pytest -v | less
```

You can also run a selection of tests associated with each task by adding the Pytest marker for each task to the Pytest
command:

```sh
$ pytest -v -m task1
```
The markers are defined in the test file and listed in `pytest.ini`.

You may also select tests to run based on their name using the `-k` flag.
Have a look at the test file to find out the function names of each test.
For example the following command executes the very first test of Lab 1:

```sh
$ pytest -v -k test_provekey_correct
```

The full documentation of pytest is [available here](http://pytest.org/latest/).


### What you will have to submit
The deadline for all labs is at the end of term but labs will be progressively released throughout the term, as new
concepts are introduced. 
We encourage you to attempt labs as soon as they are made available and to use the dedicated lab time to bring up any
queries with the TAs.

Labs will be checked using Github Classroom, and the tests will be run each
time you push any changes to the `main` branch of your Github repository.
The latest score from automarking should be shown in the Readme file.
To see the test runs, look at the Actions tab in your Github repository. 

Make sure the submitted `lab01.py` file at least satisfies the tests, without the need for any external dependency 
except the Python standard libraries and the Petlib library. 
Only submissions prior to the Github Classroom deadline will be marked, so make sure you push your code in time.


To re-iterate, the tests passing is a necessary but not sufficient condition to fulfill each task.
All submissions will be checked by TAs for correctness and your final marks are based on their assessment of your work.  
For full marks, make sure you have fully filled in any sections marked with `TODO` comments, including answering any
questions in the comments of the `lab01.py`.


## General Hints:

- The `setup` returns a set of parameters including the group `G`, its order `o`, a generator `g`, and an array of 
generators `hs`, shared by all functions in this exercise.
- The `to_challenge` function takes a number of group elements (EC points in this case), hashes them, and returns a Bn
appropriate to be used as a challenge.
- As usual modify the code file in the specified location. (marked by `# TODO: YOUR CODE HERE:`)
- Study the unit tests `lab04_test.py` to understand how to pass them, as well as how the functions you complete are 
meant to be used.

## TASK 01 -- Prove knowledge of a DH public key's secret. \[1 point\]

- You will need to implement the Schnorr protocol in its non-interactive form to prove knowledge of a private key of a
particular public key.
- The output of `provekey` is a pair `(c, r)`, a `Bn` challenge and a `Bn` response.
- Study the `verifyKey` function to ensure it may verify the proof you generate.

## TASK 02 -- Prove knowledge of a Discrete Log representation. \[1 point\]

- You will have to use the extended Schnorr protocol to prove knowledge of all secrets and opening of a commitment.
- Study the function `commit` to understand the structure of the commitment. Ensure you understand the role of the
opening value `r`.
- Study the function `verifyCommitement` to ensure your proof can be verified correctly.
- The `proveCommitment` function is passed the commitment and the secrets (including the opening).
It should return a proof consisting of the challenge and responses (multiple ones). 

## TASK 03 -- Prove Equality of discrete logarithms. \[1 point\]

- In this task you need to implement `verifyDLEquality` the verification algorithm of the proof of equality of discrete
logarithms of K and L.
- Study carefully `proveDLEquality` to ensure your verification algorithm verifies only correct proofs.

## TASK 4 -- Prove correct encryption and knowledge of a plaintext. \[1 point\]

- In this task you need to implement both the zero knowledge proof and verification of validity of a ciphertext under
public key pub and knowledge of the encrypted message `m`.
- In this proof you will need to combine proof of equality (for `k`) as well as proofs of multiple elements (`a` and `b`).

## TASK 5 -- Prove a linear relation \[1 point\]

- Study `relation` and understand how it returns a commitment to values `x0` and `x1` with a relation between them 
(`x0 = 10 x1 + 20`).
- You need to implement a function that proves knowledge of `x0`, `x1` and `r`, as well as prove that the linear 
relation between the secrets holds.
- You also need to implement the verification function for knowledge of the commitment's secrets and the linear relation.

## TASK 6 -- (OPTIONAL) Prove that a ciphertext is either 0 or 1 \[0 point\]

- You have to implement both proof and verification that an encrypted message under `pub` is either `0` or `1` without 
revealing which.

## TASK Q1 and Q2 -- Answer the two questions \[1 point\]

- Answer the questions in a comment block
- In Q2 you are given a snippet of code, and a test for it. Do not forget to study both before answering the question.