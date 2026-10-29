# Network Configuration Detection Datasets

Research datasets for cross-platform network configuration matching and anomaly detection.

## Dataset organization

```text
datasets/
  dataset1/
    train/                     # Source: train_dataset1
      normal/<vendor>/         # Normal configuration text
      abnormal/<vendor>/       # Perturbed configuration text
      annotations/<vendor>/    # Original abnormal-sample annotations
      metadata/                # Original split summary
    test/                      # Source: test_dataset_1; same layout
  dataset2/
    train/                     # Source: train_dataset2
      abnormal/<vendor>/       # Configuration text grouped by anomaly type
      annotations/<vendor>/    # Original per-type annotations
      metadata/                # Vendor manifests and split summary
    test/                      # Source: test_dataset_2; same layout
templates/                     # Original standard templates / normal references
file_manifest.csv              # Exact source-to-repository mapping and SHA-256
SHA256SUMS                     # Checksums for all copied source files
```

Dataset 1 provides all four combinations: training normal, training abnormal,
test normal, and test abnormal. Dataset 2 supplies the anomaly-detection train
and test corpora grouped by error type. Its source directories do not contain
separate normal files; standard templates in `templates/` provide their normal
reference. No normal dataset has been synthesized or substituted during export.
The datasets are template-based controlled perturbation corpora; angle-bracket
placeholders in the original configuration text are intentionally retained.

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
The original dataset uses `ORDER_DEPENDENCY_ERROR` in some filenames and JSON
fields; this is the legacy alias of `ORDER_ERROR`. Original labels, filenames,
Chinese annotation keys, line numbers, and metadata are retained for traceability.

## Integrity and reproducibility

All source dataset and template files are copied byte-for-byte. No records are
regenerated, resampled, merged, relabeled, or normalized. `file_manifest.csv`
records every original relative path, published path, file size, and SHA-256.
JSON files were checked for valid UTF-8 JSON during export. Original summary
and vendor manifest counts are retained as source metadata; use the actual
annotation records when computing evaluation sample counts.

| Dataset | Split | Source files |
| --- | --- | ---: |
| dataset1 | test | 19 |
| dataset1 | train | 19 |
| dataset2 | test | 115 |
| dataset2 | train | 115 |
| templates | reference | 7 |

The obsolete `train_val_dataset2` directory is excluded because current matching
and detection runners use `train_dataset1` / `train_dataset2` for development and
`test_dataset_1` / `test_dataset_2` for final testing. Experiment results, model
weights, runtime caches, API configurations and credentials are not included.

No redistribution license is assigned by this export; applicable source-data
rights must be confirmed before any public redistribution.
