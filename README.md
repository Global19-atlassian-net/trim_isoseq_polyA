# trim_isoseq_polyA
This is a program to trim the polyA tails of DNA sequences in a Fasta format, using HMM. 

It is primarily developped to process the "FLNC" file of PacBio Iso-Seq output, with the HMM
model trained with that data. However, with an `-G` option, it will process other sequence
as well.

## Prerequisite
- C++11
- Boost
- Zlib 
- BZib2
- pthread

## Install
```bash
mkdir build && cd build && cmake ../ -DBOOST_ROOT=PATH_TO_YOUR_BOOST_ROOT_DIR -DCMAKE_BUILD_TYPE=Release && make 
```

    Executables will be saved in directory trim_isoseq_polyA/bin.
    Please replace PATH_TO_YOUR_BOOST_ROOT_DIR with your own boost root directory.
    e.g., -DBOOST_ROOT=~/mylib/boost/boost_1_60_0/

## Build with unit tests
```bash
mkdir buildwtest && cd buildwtest && cmake ../ -DBOOST_ROOT=PATH_TO_YOUR_BOOST_ROOT_DIR -DTrimIsoseqPolyA_build_tests=ON && make && make test
```

## Usage
To process Iso-Seq
```bash
trim_isoseq_poly -i isoseq.flnc.fa -t 8 > isoseq.flnc.atrim.fa 2> isoseq.flnc.atrim.log
```

To process generic fasta files
```bash
trim_isoseq_poly -i input.fa -t 8 -G > input.atrim.fa 2> input.atrim.log
```
`.atrim.fa` file contain the fasta entries with polyA trimmed, based on a default HMM model trained with PacBio data. 

`.atrim.fa` is a tab file with length of polyA been trimmed.

To visualize polyA
```bash
trim_isoseq_poly -i isoseq.flnc.fa -t 8 -c 2>/dev/null
```