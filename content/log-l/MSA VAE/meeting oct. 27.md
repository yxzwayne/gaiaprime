with Avik

[https://hivdb.stanford.edu/cgi-bin/InhibitorsMutations.cgi?Gene=PR](https://hivdb.stanford.edu/cgi-bin/InhibitorsMutations.cgi?Gene=PR)

list of mutation is inserted into "consensus sequence"

If we have nucleotide sequences, we can let three of each represent one acid and convert the long nucleotide sequence to full protein sequence first;

Then, use accession id and other ids to get the full sequences with respect to the mutation sequence id match first.

wild-type-sequence: used when we have mutations annotated in i.e. K7Q, meaning at position 7, K was changed to Q.
- for example, use consensus B amino acid sequences;

We obtain the sequence after mutation and exclusively use it as the single observation (data point). By modeling on top of these post-mutation sequences, it can be argued that we can learn evolutionary history of the genetic mutations and epistasis.

after that, reduce the 21 letter into entropy pairing, or cluster into 4 letters based on entropy; we have to do this lower-dimension letter mapping for each position, because otherwise our parameter space will be too large to process. (think 20 to the power of sequence length).
