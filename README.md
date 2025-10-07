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

`git clone https://github.com/kantaimperial/EazyVASP.git
echo 'export PATH=$PATH:~/EazyVASP' >> ~/.bashrc
source ~/.bashrc`

Then you can use the commands from anywhere:
`generate_config_vasp
generate_POTCAR /path/to/potpaw_PBE`




 
