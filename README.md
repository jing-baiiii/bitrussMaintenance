# Bitruss Maintenance on Dynamic Bipartite Graphs

This repository provides the runnable implementations of BM, SA, SAP, and SAP+, experiment drivers, and Bai et al.'s PI*/PR* baseline source with build and runtime configurations. The unmodified upstream snapshot and the measurement source are kept in separate directories; see [Bai baseline documentation](baselines/bai/README.md).

## Data Archive

The experiment data are distributed separately because `data.zip` is approximately 248 MiB, above GitHub's standard 100 MiB per-file limit. The public data record is [available on Zenodo](https://zenodo.org/records/24081250), DOI [10.5281/zenodo.24081250](https://doi.org/10.5281/zenodo.24081250). Download [data.zip directly](https://zenodo.org/records/24081250/files/data.zip?download=1). A mirror is also available from [Baidu Netdisk](https://pan.baidu.com/s/1P_Rwh-coqBwlR4wvtvJtbg?pwd=ytex) (access code: `ytex`). The SHA-256 checksum is `011ef7926c3a506a055ba39f5a89c86aa1755bc020c4752dcebe14d10039ee70`.

Extract the archive in this repository's root directory. It contains a top-level `data/` directory with the nine main graphs, scalability graphs, ordered event workloads, per-event timing and work records, candidate-detection records, result tables, and provenance files. See [dataset details](docs/datasets.md) and [the release inventory](docs/release_inventory.md).

## Build and Run

Requirements: Linux, Bash, g++ with C++17 and OpenMP support, and Python 3 standard library.

```bash
bash experiments/scripts/build_drivers.sh
build/experiments/verify_oracle
python3 experiments/scripts/run_paper.py --dry-run
```

The commands build the experiment drivers, run the small-graph correctness validator, and check the full timing/count campaign configuration. After extracting `data.zip`, run the full campaign with:

```bash
python3 experiments/scripts/run_paper.py --output build/paper_results
```

The campaign includes 52 main timing/count configurations. Supplementary memory, allocation-capacity, accumulating-index, and fixed-vertex experiments have dedicated drivers; instructions are in [the reproduction guide](docs/reproduction.md). Result files and their mapping to manuscript tables are indexed in [table results](docs/table_results.md).

## Repository Contents

- `src/`: BM, SA, SAP, SAP+, and shared dependencies.
- `experiments/`: experiment drivers, scripts, and preprocessing sources.
- `baselines/bai/upstream/`: unmodified source snapshot from Bai et al.'s public repository.
- `baselines/bai/measured/`: baseline measurement source and its build provenance.
- `docs/`: algorithms, datasets, reproduction instructions, result tables, and release inventory.
- `MANIFEST.sha256`: SHA-256 checksums for files in this code repository.

All manuscript datasets remain attributed to their original sources. Bai et al.'s source attribution and license information are documented with the baseline files.
