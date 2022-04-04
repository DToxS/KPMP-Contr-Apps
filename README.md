# README for Using KPMP Docker Containers

This README file includes the instructions of how to use the Docker containers built for the data analysis programs of the KPMP project.

## System Requirements

The computers to run KPMP Docker containers must meet the following requirements:

- A modern CPU with a minimum of 2 cores and hardware virtualization technology, such as  Intel VT and AMD-V
- A minimum of 32GB memory for running Windows container and 128GB for running Linux container
- A minimum of 50GB hard drive space
- Microsoft Windows 10 operating system

## Installing Docker Desktop

Go to the [Docker Desktop](https://www.docker.com/products/docker-desktop/) webpage to download and install the latest Docker Desktop for Windows. Note that during its installation the Docker Desktop will also install the Windows Subsystem for Linux (WSL), a component of Windows 10 needed by Docker.

## Obtaining Docker Containers

Two KPMP Docker containers need to be downloaded: a Windows container for C# program and a Linux container for R and Python programs.

### Windows Container for C# program

Open the Docker Desktop menu by right clicking the Docker icon in the Notifications area (or System Tray) and Select the option `Switch to Windows containers...`. Then open a *Command Prompt* command-line application and issue the following command to download the Windows container for C# program:

```bash
docker pull iyengarlab/kpmp-cs-apps
```

### Linux Container for R and Python programs

Open the Docker Desktop menu by right clicking the Docker icon in the Notifications area (or System Tray) and Select the option `Switch to Linux containers...`. Then open a *Ubuntu on Windows* command-line application and issue the following command to download the Linux container for R and Python programs:

```bash
docker pull iyengarlab/kpmp-rp-apps
```

## Downloading KPMP Datasets

Before start using the Docker containers, one needs to prepare required data for both containers by downloading the required KPMP dataset file `KPMP-Datasets.zip` from the *Zenodo* repository ([https://doi.org/10.5281/zenodo.6410326](https://doi.org/10.5281/zenodo.6410326)) and extracting it to a drive, e.g. `D`. After the ZIP file is extracted, a folder tree will be created with the following structure:

```
D:\KPMP-Datasets
├── jens
├── rachel
└── raji
```

Besides the ZIP file downloaded from Zenodo repository, one also needs to download the following datasets to corresponding sub-directories.

**Molecular Biology of the Cell Ontology ([www.mbc-ontology.org](www.mbc-ontology.org))**

- Link to website: [https://github.com/SBCNY/Molecular-Biology-of-the-Cell/MBCO_windows_application/MBCO_datasets/](https://github.com/SBCNY/Molecular-Biology-of-the-Cell/MBCO_windows_application/MBCO_datasets/)
- Download the files:
  - `MBCO_v1.1_inferred_SCP_relationships.txt`
  - `MBCO_v1.1_gene-SCP_associations_human.txt`

- Copy these files into subdirectory: `KPMP-Datasets\jens\KPMP_reference_atlas_code\MBCO_datasets`

**Gene Ontology Biological Processes**

- Link to website: [https://maayanlab.cloud/Enrichr/#libraries](https://maayanlab.cloud/Enrichr/#libraries)
- Download the file `GO_Biological_Process_2018` (we downloaded this file on July 17, 2018)
- Copy these files into subdirectory: `KPMP-Datasets\jens\KPMP_reference_atlas_code\GeneOntology_datasets`
- Rename to `Geneontology_BiologicalProcess_2018_2018July17.txt`

**Metabolic and transmembrane transport ontologies**

- Link to website: [https://github.com/SBCNY/Molecular-Biology-of-the-Cell/Additional_MBCO_gene_libraries/](https://github.com/SBCNY/Molecular-Biology-of-the-Cell/Additional_MBCO_gene_libraries/)
- Download the files:
  - `Metabolic_energy_generation_pathways_human.txt`
  - `NaAndGluTMTransport_scpGeneAssociations.txt`
  - `Parent_child_transmembrane_transport_scps.txt`                                        
  - `Sphingolipid_metabolism.txt`

- Copy these files into subdirectory: `KPMP-Datasets\jens\KPMP_reference_atlas_code\MBCO_datasets`

**jensenLab_compartments**

- Link to website: [https://compartments.jensenlab.org/Downloads](https://compartments.jensenlab.org/Downloads)
- Download `All channels integrated: human` (we downloaded this file on February 21, 2020)
- Copy this file into subdirectory `KPMP-Datasets\jens\KPMP_reference_atlas_code\jensenLab_compartments`
- Rename downloaded file `human_compartment_integrated_full.tsv` to `human_compartment_integrated_full_2020February21.tsv`

**Single nucleus dataset by Wu et al. PMID:29980650 **

- Download `GSE114156_Human.kidney.dge.txt.gz` from NCBI GEO website - GSE114156 (the last time we downloaded this file was March 17, 2022)
- Copy file into subdirectory `KPMP-Datasets\jens\KPMP_reference_atlas_code\Experimental_data\SingleCell_datasets`
- Rename file to `Wu_MTS.kidney_PMID29980650.dge.txt`

**Single nucleus dataset by Muto et al. 2021 Apr 13;12(1):2190. doi: 10.1038/s41467-021-22368-w. PMID:33850129 **

- Link to website: [https://cellxgene.cziscience.com/collections/9b02383a-9358-4f0f-9795-a891ec523bcc](https://cellxgene.cziscience.com/collections/9b02383a-9358-4f0f-9795-a891ec523bcc)
- Download the dataset `Single cell transcriptional and chromatin accessibility profiling redefine cellular heterogeneity in the adult human kidney - RNAseq` in `.rds` format (our last download of this file was on March 17, 2022)
- Copy file into subdirectory `KPMP-Datasets\jens\KPMP_reference_atlas_code\Experimental_data\SingleCell_datasets`
- Rename file to `Muto_singleNucleus_seurat_PMID33850129.rds`

At last, one needs to create a `Results` sub-directory using the following command:

```powershell
md D:\Data\jens\KPMP_reference_atlas_code\Results
```

## Launching Docker Containers

Now, one can launch two KPMP Docker containers and connect them to the downloaded datasets.

### Windows Container for C# program

When Docker Desktop is set to the Windows container mode, open a *Command Prompt* command-line application and issue the following command to launch the Windows container for C# program:

```powershell
docker run -it --name kpmp-cs-apps --cpus 2 --memory 24g --mount type=bind,source=D:\KPMP-Datasets\jens\KPMP_reference_atlas_code,target=C:\Data iyengarlab/kpmp-cs-apps cmd.exe
```

### Linux Container for R and Python programs

When Docker Desktop is set to the Linux container mode, open a *Ubuntu on Windows* command-line application and issue the following command to launch the Linux container for R and Python programs:

```bash
docker run -it --name kpmp-rp-apps --cpus 2 --memory 100g --mount type=bind,source=/mnt/d/KPMP-Datasets,target=/data iyengarlab/kpmp-rp-apps bash -l
```

## Using Data Analysis Programs

### kpmp-cs-apps Container

Once inside the *Command Prompt* command-line application of the *kpmp-cs-apps* container, one needs to change current directory using the following command:

```powershell
cd \CS-Codes\KPMP_reference_atlas_csharp_code\Executable_script
```

Then, the C# program can be launched using the following command:

```powershell
KPMP_reference_kidney_tissue_atlas.exe
```

Note: please refer to [README for Running Jens KPMP Codes.txt](README%20for%20Running%20Jens%20KPMP%20Codes.txt) for the usage details of this program.

When the program is finished, one can use the following command to quit the container and the container will be stopped automatically:

```powershell
exit
```

### kpmp-rp-apps Container

Once inside the *kpmp-rp-apps* container, first one needs to issue the following command to grant accessibility to the mounted `/data` folder:

```bash
find /data -maxdepth 1 -type d -print0 | xargs -0 chmod 755
```

Then, one can switch to any of three sets of R and Python programs, by setting `USER_NAME` in the following command to one of `jens`, `rachel` or `raji`:

```bash
su - USER_NAME
```

Note that one can use the following commands to switch to another set of programs by setting `USER_NAME` to a different value:

```bash
exit
su - USER_NAME
```

After entering the directory of selected program set, one needs to execute the following command to gain full accessibility to corresponding `~/Data` directory:

```bash
sudo /bin/chown -R ${USER}:users ~/Data/
```

Note that above command needs to be executed only once for each set of programs.

Finally, one can launch corresponding R and Python programs in the following way:

#### Running R Programs

```bash
Rscript "r-file.R"
```

#### Running Python Programs

```bash
python3 "python-file.py"
```

Note: please refer to the README file of the selected set of programs for their usage details.

When the program is finished, one can use the following commands to quit the container and the container will be stopped automatically:

```bash
exit
exit
```

