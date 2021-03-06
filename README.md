# Binding site predictor

## Data

### DNA
DNA is ordered in a 4D-tensor with for each training range, a one-hot encoding (4 element
vector) of all nucleotides in that range (assumed to always be 200). If
a sequence is unknown ('N' in FASTA format), the entire corresponding
one-hot vector is zero. Then, for all nucleotides seperately, ranges are
combined into bits in a `uint8` array for compactness (see
[`numpy.unpackbits`](https://docs.scipy.org/doc/numpy-1.15.0/reference/generated/numpy.unpackbits.html#numpy.unpackbits)).
Eventually the data is pickled into `dna.pkl` with protocol 2.


### ChIP
ChIP-seq peak conservative calls are collected per range and per
protein-cell combination in a 3D-tensor. The data is then pickled into
`chip.conservative.pkl` with protocol 2.

For experiments with only one protein (currently the only experiment
supported) one can generate a protein-cell specific dataset by running
`python3 pick_chip.py --cell X --protein Y`, where X and Y are the
indices of both properties in the original tensor.


## Training
One can start training on a specific protein-cell pair by running
`python3 train.py --epochs E --chip-path chip-X-Y.conservative.pkl`.
Check `python3 train.py --help` for additional training options.