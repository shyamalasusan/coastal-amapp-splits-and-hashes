# Coastal-AMAPP: split lists and protocol hashes

Companion material for the letter on risk-proportional obfuscation of coastal satellite imagery. It lets a reader check that
the evaluation splits are site-disjoint and that the protocols and models were fixed before the confirmatory runs.

**This repository contains no images, labels, code or model weights.** It lists image file names and scene keys only, and
SHA-256 fingerprints.

## Contents

| File | What it is |
|---|---|
| `splits/shiprsimagenet_site_disjoint_split.csv` | Every ShipRSImageNet V1.1 image (3,435) with its subset (train 2,239; validation 626; sealed test 570), scene key and source collection. No scene appears in more than one subset |
| `splits/ssdd_split.csv` | SSDD images with subset (train 742; validation 186; benchmark 232) and whether a benchmark image is an inshore scene |
| `splits/dota_v1_validation_tiles.csv` | The 389 DOTA v1.0 validation tiles used, with their source image |
| `hashes/split_fingerprints.csv` | Fingerprints of the three ShipRSImageNet subsets and the scene map |
| `hashes/frozen_protocols.csv` | SHA-256 of each frozen protocol file, with the date and what it fixed |
| `hashes/model_fingerprints.csv` | Fingerprints of the detector and attacker weight files recorded before the runs |
| `hashes/dataset_archives.csv` | Size and SHA-256 of the downloaded DOTA archives |
| `LICENSE` | CC BY 4.0 legal code |
| `SHA256SUMS.txt` | SHA-256 of every other file in this folder |

## How to check the splits

1. Obtain ShipRSImageNet V1.1 from its authors (it is for academic use only).
2. For each subset, sort the image file names in `shiprsimagenet_site_disjoint_split.csv`, join them with a newline after
   each name, and take the first 16 hex characters of the SHA-256. The values must equal `hashes/split_fingerprints.csv`
   (train `9b05f4b260adeecf`, validation `6704ba295c1c6f99`, test `0623ec28e5647178`).
3. Check that no `scene_key` occurs in two subsets (it does not).

## Notes

- **Why a new split.** The official ShipRSImageNet split places all 17 FGSD harbours, all 6 HRSC2016 harbours and 78 of
  120 xView scenes in more than one subset. This split assigns each harbour or scene to exactly one subset.
- **The sealed test** (570 images) was used once, under the sealed-test protocol, and was not read again.
- **Protocol wording.** The frozen protocol files are hashed as written; they call the sensitivity policy "illustrative".
  The policy (Warship and DOCK 0.9, Ship 0.5, Merchant 0.3; sensitive at 0.7 or above) was adopted as the study policy on
  21 November 2026; the values did not change.
- **Datasets and licences.** ShipRSImageNet and DOTA are for academic, non-commercial use, and imagery from Google Earth is
  subject to Google's terms; SSDD is released under Apache 2.0. The datasets are not redistributed here.
- **Licence for this material:** Creative Commons Attribution 4.0 International (CC BY 4.0), see `LICENSE`. It covers these lists and hashes only; the datasets keep their own terms.
