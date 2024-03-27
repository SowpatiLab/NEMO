# <span style="padding: 2px 10px; border-radius: 5px; background: #fbc44a; color:black;">NEMO</span> | Improved and accurate models for identification of 6mA using Nanopore sequencing
NEMO enables the study of N6-methyladenine at a single-base resolution in nanopore datasets. NEMO can be run in two different modes for methylation calling - one specific for GATC context (NEMO_R9_GATC), and one which is sequence context-agnostic (NEMO_R9_6mA).

## Contents
[Dependencies](#dependencies)<br/>
[Installation](#installation)<br/>
[Models](#available-models)<br/>
[Usage](#usage)<br/>
[Generating Bed files](#2-converting-modbam-to-bedmethyl-using-modkit)<br/>

## Dependencies
* [Dorado Basecaller](https://github.com/nanoporetech/dorado) OR
* [Bonito Basecaller](https://github.com/nanoporetech/bonito)
* [modkit](https://github.com/nanoporetech/modkit/)

## Installation
NEMO can be downloaded by cloning from GitHub
<span style="background: #ececec; color: black; margin-left: 5px; padding: 2px 10px; border-radius: 5px; text-decoration: none; font-weight: bold;">**git clone git@github.com:SowpatiLab/NEMO.git**<span>

## Available Models

<table>
    <tr>
        <th>Basecalling Models</th>
        <th>Works with</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>DORADO_MODELS/NEMO_R9_GATC</td>
        <td>dorado</td>
        <td>GaTC context model</td>
    </tr>
    <tr>
        <td>BONITO_MODELS/NEMO_R9_GATC</td>
        <td>bonito</td>
        <td>GaTC context model</td>
    </tr>
    <tr>
        <td>DORADO_MODELS/NEMO_R9_6mA</td>
        <td>dorado</td>
        <td>All context model</td>
    </tr>
    <tr>
        <td>BONITO_MODELS/NEMO_R9_6mA</td>
        <td>bonito</td>
        <td>All context model</td>
    </tr>

</table>

## Usage
### 1. Basecalling
<div style="margin-left: 20px; border: 0.25px #353535 solid; padding: 20px;border-radius: 10px; margin-bottom: 20px">


### A. Using Dorado Models
***
##### <u>6mA Calling in GATC context</u>
```bash
dorado basecaller dna_r9.4.1_e8_sup@v3.6 POD5_DIR \
    --modified-bases-models DORADO_MODELS/NEMO_R9_GATC \
    --reference REFERENCE_GENOME > mod_calls.bam
```
##### <u>6mA Methylation Calling</u>
```bash
dorado basecaller dna_r9.4.1_e8_sup@v3.6 POD5_DIR \
    --modified-bases-models DORADO_MODELS/NEMO_R9_6mA \
    --reference REFERENCE_GENOME > mod_calls.bam
```

</div>

<div style="margin-left: 20px; border: 0.25px #353535 solid; padding: 20px;border-radius: 10px">

### B. Using Bonito Models
***
##### <u>6mA Calling in GATC context</u>
```bash
bonito basecaller dna_r9.4.1_e8_sup@v3.3 POD5_DIR \
    --modified-base-model BONITO_MODELS/NEMO_R9_GATC.pt> \
    --reference REFERENCE_GENOME > mod_calls.bam
```

##### <u>6mA Methylation Calling</u>
```bash
bonito basecaller dna_r9.4.1_e8_sup@v3.3 POD5_DIR \
    --modified-base-model BONITO_MODELS/NEMO_R9_6mA.pt> \
    --reference REFERENCE_GENOME > mod_calls.bam
```
    
</div>
<br/>

***

### 2. converting modBAM to bedMethyl using [modkit](https://github.com/nanoporetech/modkit/)
```bash
modkit pileup mod_calls.bam mod_calls.bed
```
