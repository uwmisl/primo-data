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
| The OpenImagesV4 ID | The number of times the barcode for this image was observed in the
sequencing reads associated with this query. |

