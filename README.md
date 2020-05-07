# primo-data

### `database_seqs.csv.gz`

Format: gzipped comma-separated text

Layout:

| ImageID                                         | Sequence                                                                         |
| ----------------------------------------------- | -------------------------------------------------------------------------------- |
| The OpenImagesV4 ID associated with this image. | The full DNA sequence (5' to 3') associated with this image, sent for synthesis. |


### `query_seqs.csv`

Format: comma-separated text

Layout:

| ImageID                                         | Sequence                                                                         |
| ----------------------------------------------- | -------------------------------------------------------------------------------- |
| The name of this image in the `query_images` directory  | The full DNA sequence (5' to 3', including modifications) associated with this image, sent for synthesis. |


### `query_images`

Format: directory of JPG images.

Layout: filenames correspond to those referenced in `query_seqs.csv`


### `sequencing/reads`

Format: directory of gzipped FASTQ files.

Layout: Each file contains the reads from a single experiment where the
database was filtered by a query (given by the filename).


### `sequencing/decoded`

Format: directory of gzipped comma-separated text. Each file contains the number
of reads observed for each image in the database after filtering by a query
(given by the filename).

Layout:

| ImageID | Count |
| ------- | ----- |
| The OpenImagesV4 ID | The number of times the barcode for this image was observed in the sequencing reads associated with this query. |

**Note**: due to contamination from an unrelated experiment using the same barcode, the count for the first image (`e39871fd9fd74f55`) is abnormally high.
We set it to zero during analysis for each query. There was no impact on the conclusions drawn from the analysis.


### `analysis/distances`

Format: directory of gzipped comma-separated text, with one file per query.

Layout:

| ImageID | Euclidean Distance |
| ------- | ------------------ |
| The OpenImagesV4 ID | The Euclidean distance between the feature vector of the query (indicated by the filename) and the feature vector of this image. |


### `analysis/thresholds`

Format: directory of comma-separated text files, with one file per query.

Layout:

Each row represents the statistics for a set of images with read counts at or
above the threshold.

| Threshold | Number Retrieved | 100-Nearest-Neighbor Recall |
| --------- | ---------------- | --------------------------- |
| Images in this set had at least this read count | The total number of images in this set | The number of the 100 nearest neighbors to the query in this set |

### `analysis/benchmarks.csv`

Format: comma-separated text. Each row represents a search through the database
using a particular algorithm and query, with varying parameters.

Layout:
| Algorithm | Query ID | Number Retrieved | Database Size | # of Nearest Neighbors | Nearest Neighbor Recall | Algorithm Parameters |
| --------- | -------- | ---------------- | ------------- | ---------------------- | ----------------------- | -------------------- |
| The search algorithm used. | The query image used to conduct the search. | The number of images in the database. | The desired number of nearest neighbors to be retrieved. | The number of nearest neighbors retrieved by the search. | The parameters used for constructing the index and/or performing the search. |

**Note 1**: The rows labeled with the `primo` algorithm contain the same data as the `analysis/thresholds` directory.
**Note 2**: Most of the *in silico* benchmarks were conducted with a slightly larger database. The results presented in the paper are normalized to the database size.
