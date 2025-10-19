# EazyVASP

_A lightweight workflow assistant for automated VASP input generation and convergence testing, fully compatible with [vaspup2.0](https://github.com/kavanase/vaspup2.0)._

---

## 🧩 Overview

**EazyVASP** streamlines the setup of VASP calculations starting from experimental or database structures  
(e.g., ICSD, Materials Project) and integrates seamlessly with **vaspup2.0** for automated convergence and DFPT workflows.

---

## ⚙️ Requirements

- Python ≥ 3.10
- Valid VASP license (for access to POTCAR files)
- Installed tools:
  - `vaspup2.0`　(https://github.com/kavanase/vaspup2.0)
 
---
## Insatllation
Installation is quite simple, just clone this git repository and update your PATH to include the location of the bin folder.

```
git clone https://github.com/kantaimperial/EazyVASP.git
echo 'export PATH=$PATH:~/EazyVASP' >> ~/.bashrc
source ~/.bashrc
```

Then you can use the commands from anywhere:
```
generate_config_vasp
generate_POTCAR /path/to/potpaw_PBE
```

---
## Workflow (Usage)

Once installed, EazyVASP enables a fully automated setup of VASP input files from a single POSCAR.
The typical workflow is as follows.

### 1. Prepare structure

Obtain a POSCAR file (from experiment or database) and move it into your project directory.

```
cp POSCAR ./project/
cd project/
```

### 2. Generate input templates

Create the initial input/ directory and all template files.

`generate_config_vasp`

This creates the following structure:
```
input/
    /INCAR
    /KPOINTS
    /CONFIG
    /job
    /POSCAR
```
### 3. Generate POTCAR

Automatically create the pseudopotential file according to the element order in POSCAR.

generate_POTCAR $VASP_PSPDIR

This produces:
```
input/
├── POTCAR
└── POTCAR.symbols
```

Optional override example (use a different PAW for a specific element):
```
generate_POTCAR $VASP_PSPDIR –override Bi=Bi
```

### 4. Suggest suitable k-point meshes

Use kgs_gen_kpts (in vaspup2.0) to append reasonable k-point mesh candidates into CONFIG based on lattice parameters.

```
cd input
kgs_gen_kpts
```

CONFIG example after running kgs_gen_kpts:
```
conv_kpoint=“1”
kpoints=‘3 3 1,4 4 2,6 6 3,7 7 3’
```

5. Run convergence tests (via vaspup2.0)

Go back to the project root and run automated ENCUT/KPOINT convergence.

```
cd ../
generate-converge
```
This command creates two directories and runs the required VASP jobs inside them:
```
cutoff_converge/
kpoint_converge/
```
After the calculations are completed, use:

```
data-converge
```

Typical output example:
```
Directory:      Total Energy/eV:   (per atom):   Difference (meV/atom):   Average Force Difference (meV/Å):
k3,3,1          -26.40637281       -4.4010621
k4,4,1          -26.22520170       -4.3708669     -30.1952                 88.7890
k4,4,2          -26.00211908       -4.3336865     -37.1804                -51.4480
k5,5,2          -25.93543847       -4.3225730     -11.1135                  6.7630
k6,6,2          -25.89391903       -4.3156531      -6.9199                -54.3580
```
---
### Notes
	•	All generated files follow vaspup2.0 conventions.
	•	Default CONFIG enables both ENCUT and KPOINT convergence testing.
	•	kgs_gen_kpts appends suggested k-point meshes automatically into CONFIG.
	•	Scripts are optimized for HPC (Slurm) environments.
	•	INCAR templates include commented options for:
	  •	PBEsol
	  •	HSE06
	  •	DFT+U
	  •	D3 dispersion
	  •	MLFF molecular dynamics

---
### Author
Kanta Ogawa
Kyoto University, Japan (2025)
GitHub: https://github.com/kantaimperial

---
License

Released under the MIT License.
A valid VASP license is required to use the provided POTCAR files.
