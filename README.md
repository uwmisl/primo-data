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


