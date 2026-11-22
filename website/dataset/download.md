# Download

The data are hosted on Hugging Face at
[**zhang-lab/sMCC40M**](https://huggingface.co/datasets/zhang-lab/sMCC40M).
The complete versioned folder is about **1.29 TB** (images, masks, expression and
reproducibility assets), so most users start with one acquisition.

```bash
pip install huggingface_hub anndata pyarrow
export REPO=zhang-lab/sMCC40M
```

## One acquisition

The dataset ships a small helper that fetches a complete sample package:

```bash
hf download "$REPO" examples/download_sample.py --repo-type dataset --local-dir .

# Visium HD, mouse ovary
python examples/download_sample.py --repo "$REPO" --platform HD --sample HD-002
python smcc_data/HD/samples/HD-002/read_example.py

# Xenium
python examples/download_sample.py --repo "$REPO" --platform Xenium --sample HHDX011
python smcc_data/Xenium/samples/HHDX011/read_example.py
```

Each sample folder holds the expression matrix, image, segmentation mask, metadata,
mappings, eligibility table, sample-specific field evidence and checksums.

!!! tip "Expression only"
    `download_sample.py` also has an `--expression-only` mode for just the H5AD matrix,
    when you do not need images or masks. The
    [data card](https://huggingface.co/datasets/zhang-lab/sMCC40M) lists its options.

## Pick samples first

Download the 156-row sample index and choose acquisitions by platform, category,
species or context before fetching anything large:

```bash
hf download "$REPO" metadata/samples.parquet --repo-type dataset --local-dir .
```

The original release is also indexed in
[`data/sample_catalog.csv`](https://github.com/aicb-ZhangLabs/sMMC40M/blob/main/data/sample_catalog.csv).
[Tutorial 4](../tutorials/04_context_selection.ipynb) shows how to filter it.

## Everything

```bash
hf download "$REPO" --repo-type dataset --revision 7c0d215a4683e6f074177e708a192c416e2e2708 --local-dir sMCC40M-2026-11-21
```

The command pins the [November 21 public revision](https://huggingface.co/datasets/zhang-lab/sMCC40M/tree/7c0d215a4683e6f074177e708a192c416e2e2708). The [October 28 revision](https://huggingface.co/datasets/zhang-lab/sMCC40M/tree/0f6f6577b0da8e00d2624e834aa6efc1c651b1ad) remains available for reproducing the original release.
The benchmark assets alone (~2.9 GB of sampled fixtures plus plans and predictions) are under
[`benchmark/`](https://huggingface.co/datasets/zhang-lab/sMCC40M/tree/0f6f6577b0da8e00d2624e834aa6efc1c651b1ad/benchmark).

## Verify

The root release manifest SHA256 is

```text
756f9541c679371083008ba70eadfb5b23193fb2123ec4c2e6fe17241d2b4dcc
```

Nested manifests and `SHA256SUMS` cover every file. Never modify a release folder in place;
write outputs elsewhere.

## License and attribution

Follow the terms and attribution requirements for each source. The 19 new Zenodo acquisitions
declare CC BY 4.0. The 13 new GEO acquisitions have a documented NCBI repository-policy review
and no standalone license declaration. See the [license manifest](https://huggingface.co/datasets/zhang-lab/sMCC40M/blob/main/licensing/license_manifest.csv)
and [attribution notes](https://github.com/aicb-ZhangLabs/sMMC40M/blob/main/docs/attribution.md).
