README for Running Rachel KPMP Codes

Inside the kpmp-rp-apps Docker container, run the R and Python scripts using the following commands:

R Scripts

```
Rscript reformat_CODEX.R
Rscript cluster_CODEX.R
Rscript codex_rnaseq_mapping.R
Rscript LMD_mapping.R
```

Note: reformat_CODEX.R needs to be run before cluster_CODEX.R and codex_rnaseq_mapping.R

Python Scripts

```
python3 run_int_nsforest.py
python3 run_sc_nsforest.py
python3 run_sn_nsforest.py
```
