# Network Configuration Detection Dataset

A cross-platform network configuration anomaly detection dataset covering six
vendors and nine anomaly types, with training/test splits, original annotations
and standard templates.

## Dataset organization

```text
dataset/
  train/
    abnormal/<vendor>/       # Configuration text grouped by anomaly type
    annotations/<vendor>/    # Per-type anomaly annotations
    metadata/                # Vendor manifests and split summary
  test/                      # Same layout as train/
templates/                   # Standard templates / normal references
file_manifest.csv            # Source-to-repository mapping and SHA-256
SHA256SUMS                   # Checksums for all dataset and template files
```

The training and test splits contain controlled perturbations grouped by anomaly
type. The source detection dataset does not provide separate normal-sample
files; `templates/` contains its standard, normal references. Angle-bracket
placeholders in configuration text are intentionally retained.

## Vendors

| Directory identifier | Vendor |
| --- | --- |
| `hw` | Huawei |
| `h3c` | H3C |
| `cisco` | Cisco |
| `zte` | ZTE |
| `ruijie` | Ruijie |
| `fiber` | FiberHome |

## Anomaly labels

The canonical nine labels are `MISSING_STATEMENT`, `REDUNDANT_STATEMENT`,
`ORDER_ERROR`, `PARAM_TYPE_MISMATCH`, `SYNTAX_ERROR`, `DEPENDENCY_MISSING`,
`RESOURCE_CONFLICT`, `SEMANTIC_INCONSISTENCY`, and `POLICY_CONFLICT`.
Some original filenames and annotation fields use `ORDER_DEPENDENCY_ERROR`,
the legacy alias of `ORDER_ERROR`.

## Integrity and reproducibility

Dataset and template file contents are preserved byte-for-byte. The published
`dataset/train/` and `dataset/test/` directories originate from the project's
`train_dataset2/` and `test_dataset_2/`, respectively. Internal dataset identifiers
in original annotations and metadata retain those source names for traceability.
The published dataset is named `dataset`.

`file_manifest.csv` lists each source path, published path, file size and SHA-256.
`SHA256SUMS` can be used to verify every dataset and template file. JSON files
were checked for valid UTF-8 JSON. Original summary and vendor manifest counts
are retained as source metadata; evaluation counts should be computed from the
actual annotation records.

| Content | Files |
| --- | ---: |
| Training split | 115 |
| Test split | 115 |
| Standard templates | 7 |
| Total dataset and template files | 237 |

This repository distributes the detection dataset and its normal references.
Experiment results, model weights, runtime caches, API configurations and
credentials are excluded. No license is assigned by this export.
