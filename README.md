# Data for spin-resolved oxygen evolution on NiOOH

Computational data accompanying the manuscript:

**Beyond the Ground State: A Spin-Resolved Reaction Network for Oxygen Evolution Reaction on NiOOH**

**Ilia M. Odud, Vitaly G. Kiselev, and Sergey V. Levchenko**

Prepared for submission to the *Journal of Catalysis*. Publication details and
an article DOI will be added when available.

This repository provides optimized structures, a representative ORCA input,
embedding-optimization information, and spin-resolved thermochemical data for
the embedded-cluster model used in the study.

## Download

Download `NiOOH_data.zip` and extract it to access the directory structure below.

## Contents

| Directory | Contents |
| --- | --- |
| `Cluster_optimized_geometries/` | 38 optimized embedded-cluster geometries in XYZ format, grouped by intermediate and spin multiplicity. |
| `Cluster_ORCA_input/` | Representative `m4_nope_NiOOHs.inp`, with comments explaining how to prepare `init.gbw`. |
| `Bulk_optimized_geometry/` | Final bulk geometry in P1 CIF format and a CRYSTAL23-oriented input. |
| `Slab_optimized_geometry/` | Final slab geometry in P1 CIF format and a CRYSTAL23-oriented input. |
| `CTPP_optimization/` | Saved annotated optimizer restart input, launch arguments, and attribution/link to the author's CTPP optimization script. |
| `Charge_optimization/` | Link to the embedding-charge fitting script and notes on total charge and physical interpretation. |
| `Thermochemistry/` | Standalone Python file containing model GFE values for 38 spin states at 298.15 K and molecular reference values. |

## Intermediate labels

| Code | Intermediate | Geometry directory | Meaning |
| --- | --- | --- | --- |
| a | O* | `nope` | Intact oxygen-centered active site without an additional adsorbate. |
| b | O*OH | `OH` | Hydroxyl-containing intermediate. |
| c | O*O | `O` | Deprotonated oxygen-containing intermediate shared by the LOM and AEM pathways. |
| d | * | `hole` | Oxygen vacancy after O2 release along the LOM pathway. |
| e | O*H | `Habs` | Protonated lattice-oxygen intermediate. |
| f | O*OOH | `OOH` | Hydroperoxo-containing intermediate along the AEM pathway. |
| g | O*O2 | `OO` | Molecular-oxygen-containing intermediate before O2 release along the AEM pathway. |

`multN` and the filename prefix `mN` denote spin multiplicity M = 2S + 1.
They are not energy-order indices. LOM follows a–b–c–d–e–a; AEM follows
a–b–c–f–g–a. Solution species and electrons are omitted from this shorthand.

## Reading the data

Coordinates in the XYZ files are in angstrom. The comment line reports
**EE + ZPE** as two separate terms in Hartree; it does not report GFE.
The XYZ files retain embedding centers: `Pd` labels custom boundary centers
and does not indicate Pd doping; `Q` labels point-charge centers. XYZ alone
does not encode point-charge magnitudes or the custom ECP definitions.
See the representative ORCA input and the geometry README for details.

Final model Gibbs free energies are provided in Hartree in
`Thermochemistry/NiOOH_thermochemistry.py`, without component decomposition.
To print the table with Python 3 (no third-party packages required):

```sh
python3 Thermochemistry/NiOOH_thermochemistry.py
```

The bulk and slab CIF files explicitly list atoms in P1, without symmetry
reconstruction. The slab CIF uses a 30 angstrom visualization cell along the
nonperiodic direction; the corresponding CRYSTAL input retains a genuinely
2D SLAB model. CRYSTAL23-oriented inputs were prepared from archived CRYSTAL17
calculations and have not been validated by rerunning CRYSTAL23.

## Scope and limitations

The dataset contains selected reusable inputs and processed results; it is
not a complete archive of raw output files, wavefunctions, or kinetic
simulation software. The original cluster outputs contain imaginary
frequencies; geometry convergence alone does not establish an unconstrained
minimum. See the directory documentation for interpretation and limitations.

The charge-fitting script has not been tested for total-charge conservation.
Charged embeddings are not intrinsically erroneous, but the physical basis
and applicability of charged solutions produced by this fitting procedure
were not thoroughly investigated in this work.

## Software attribution

- CTPP optimization: locally modified script from [dlmv/qcldm](https://github.com/dlmv/qcldm); see `CTPP_optimization/README.md` for the exact reference and modifications.
- Embedding-charge optimization: [Ilia Odud's ChOpt_3_pik_4.py](https://github.com/IlyaOdud/Support-scripts/blob/Charge-Optimize/ChOpt_3_pik_4.py); see `Charge_optimization/README.md`.

Please cite the associated article when using these data. An archive DOI and
formal citation will be added when available. Third-party software remains
subject to the terms of its original repository.
