---
title: Selection plus FunPDBe Study Case of Q13426
linktitle: Selection plus FunPDBe Study Case of Q13426
type: book
date: "2020-11-11T00:00:00+01:00"
weight: 4
authors:
  - admin
---

![cover](https://warehouse-camo.ingress.cmh1.psfhosted.org/aa7515a16c733e68b6682396ad8aef8009e11d03/68747470733a2f2f757365722d696d616765732e67697468756275736572636f6e74656e742e636f6d2f34333133343139392f39353031383134392d35386366633230302d303639302d313165622d396536342d3736306661656335313330662e706e67)

```bash
pip install --upgrade pdb-profiling
```

## Import Packages & Settings

```python
from pdb_profiling import default_config
default_config("C:/GitWorks/pdb-profiling/test/demo")

from pdb_profiling.processors import SIFTS, PDB, Base
from pdb_profiling.utils import DisplayPDB

from tqdm.notebook import tqdm
from pandas import concat, DataFrame
```

```python
# 链层面筛选过滤 (Chain Level Filtering)
# 设置SISTS.chain_filter条件: UNK_COUNT < SEQRES_COUNT，下面展示默认值(Default value is shown below)
SIFTS.chain_filter = '''
    UNK_COUNT < SEQRES_COUNT
    and ca_p_only == False
    and identity >=0.9
    and repeated == False
    and reversed == False
    and OBS_COUNT > 20'''
```

valid filters:

| Column Name       | Type     | Explaination     |
| :------------- | :----------: | -----------: |
|identity|float|provided by SIFTS: sequence identity of PDB Entity SEQRES with UniProt Isoform (0-1)|
|is_canonical|bool|whether the UniProt Isoform is the canonical isoform defined by UniProt-KB|
|sifts_range_tag|str|Safe or Insertion or Deletion or InDel ([example](https://naturegeorge.github.io/eigenblog/posts/introduce-pdb-profiling/#about-mapped-range-reformated-by-pdb-profiling))|
|reversed|bool|whether there is reversed mapped range in the aspect of UniProt Isoform Sequence ([example](https://naturegeorge.github.io/eigenblog/posts/introduce-pdb-profiling/#about-mapped-range-reformated-by-pdb-profiling))|
|repeated|bool|whether there is repeated mapped range in the aspect of UniProt Isoform Sequence ([example](https://naturegeorge.github.io/eigenblog/posts/introduce-pdb-profiling/#about-mapped-range-reformated-by-pdb-profiling))|
|InDel_sum|int|SEQRES residues that fall into the range of Insertion or Deletion or InDel of the PDB Chain Instance|
|unp_len|int|the length of the UniProt Isoform Sequence|
|BINDING_LIGAND_COUNT|int|the residues that binding to ligands(including carbohydrate polymer) of the PDB Chain Instance|
|OBS_COUNT|int|the observed/modelled (with coordinates) residues of the PDB Chain Instance|
|OBS_RATIO_SUM|float|the sum of the observed/modelled (with coordinates) residues's ratio of the PDB Chain Instance|
|NON_COUNT|int|the count non-standard residues of the PDB Entity (including UNK)|
|SEQRES_COUNT|int|the count of the residues in SEQRES|
|STD_COUNT|int|the count of the standard residues of the PDB Entity|
|UNK_COUNT|int|the count of the UNK residues of the PDB Entity|
|ca_p_only|bool|whether the PDB Entity only contains C-alpha atom for each residue|
|OBS_STD_COUNT|int|the count of the observed standard residues of the PDB Chain Instance|

```python
# PDB条目层面筛选过滤(Entry Level Filtering)
# 设置SISTS.entry_filter条件，下面展示默认值(Default value is shown below)
SIFTS.entry_filter = '''
    (experimental_method in ["X-ray diffraction", "Electron Microscopy"] and resolution <= 3) or 
    experimental_method == "Solution NMR"
    '''
```

valid filters:

| Column Name       | Type     | Explanation     |
| :------------- | :----------: | -----------: |
|resolution|float/nan|([pdb-101-explanation](http://pdb101.rcsb.org/learn/guide-to-understanding-pdb-data/resolution))|
|experimental_method_class|str|([pdb-101-explanation](https://pdb101.rcsb.org/learn/guide-to-understanding-pdb-data/methods-for-determining-structure))|
|experimental_method|str|x-ray, nmr, em, other|
|multi_method|bool|whether the PDB entry was determined by multiple method|
|revision_date|date|as name said|
|deposition_date|date|as name said|


```python
demo = SIFTS('Q13426')
```

## Select Monomeic Protein

> Implement `PDBe RESTful API` (`PDBe Entry` & `SIFTS`)


```python
%time df1 = demo.pipe_select_mo().result()
df1[df1.select_tag.eq(True)].T
```

    Wall time: 654 ms
    


<div>
<style scoped>
    table.dataframe {
    display: block;
    overflow-x: auto;
    white-space: nowrap;
    overflow-y: auto;
    height: 200px;
    }
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>4</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>UniProt</th>
      <td>Q13426</td>
    </tr>
    <tr>
      <th>chain_id</th>
      <td>A</td>
    </tr>
    <tr>
      <th>entity_id</th>
      <td>1</td>
    </tr>
    <tr>
      <th>identity</th>
      <td>0.99</td>
    </tr>
    <tr>
      <th>is_canonical</th>
      <td>True</td>
    </tr>
    <tr>
      <th>pdb_id</th>
      <td>3ii6</td>
    </tr>
    <tr>
      <th>struct_asym_id</th>
      <td>A</td>
    </tr>
    <tr>
      <th>pdb_range</th>
      <td>[[1,203]]</td>
    </tr>
    <tr>
      <th>unp_range</th>
      <td>[[1,203]]</td>
    </tr>
    <tr>
      <th>Entry</th>
      <td>Q13426</td>
    </tr>
    <tr>
      <th>range_diff</th>
      <td>[0]</td>
    </tr>
    <tr>
      <th>sifts_range_tag</th>
      <td>Safe</td>
    </tr>
    <tr>
      <th>repeated</th>
      <td>False</td>
    </tr>
    <tr>
      <th>reversed</th>
      <td>False</td>
    </tr>
    <tr>
      <th>InDel_sum</th>
      <td>0</td>
    </tr>
    <tr>
      <th>new_pdb_range</th>
      <td>[[1,203]]</td>
    </tr>
    <tr>
      <th>new_unp_range</th>
      <td>[[1,203]]</td>
    </tr>
    <tr>
      <th>conflict_pdb_index</th>
      <td>{"60":"A","134":"I"}</td>
    </tr>
    <tr>
      <th>conflict_pdb_range</th>
      <td>[[60,60],[134,134]]</td>
    </tr>
    <tr>
      <th>conflict_unp_range</th>
      <td>[[60,60],[134,134]]</td>
    </tr>
    <tr>
      <th>unp_len</th>
      <td>336</td>
    </tr>
    <tr>
      <th>BINDING_LIGAND_COUNT</th>
      <td>0</td>
    </tr>
    <tr>
      <th>BINDING_LIGAND_INDEX</th>
      <td>[]</td>
    </tr>
    <tr>
      <th>OBS_COUNT</th>
      <td>201</td>
    </tr>
    <tr>
      <th>OBS_INDEX</th>
      <td>[[1, 201]]</td>
    </tr>
    <tr>
      <th>OBS_RATIO_SUM</th>
      <td>201</td>
    </tr>
    <tr>
      <th>ARTIFACT_INDEX</th>
      <td>[]</td>
    </tr>
    <tr>
      <th>NON_COUNT</th>
      <td>0</td>
    </tr>
    <tr>
      <th>NON_INDEX</th>
      <td>[]</td>
    </tr>
    <tr>
      <th>SEQRES_COUNT</th>
      <td>203</td>
    </tr>
    <tr>
      <th>STD_COUNT</th>
      <td>203</td>
    </tr>
    <tr>
      <th>STD_INDEX</th>
      <td>[[1, 203]]</td>
    </tr>
    <tr>
      <th>UNK_COUNT</th>
      <td>0</td>
    </tr>
    <tr>
      <th>UNK_INDEX</th>
      <td>[]</td>
    </tr>
    <tr>
      <th>ca_p_only</th>
      <td>False</td>
    </tr>
    <tr>
      <th>molecule_type</th>
      <td>polypeptide(L)</td>
    </tr>
    <tr>
      <th>OBS_STD_INDEX</th>
      <td>((1, 201),)</td>
    </tr>
    <tr>
      <th>OBS_STD_COUNT</th>
      <td>201</td>
    </tr>
    <tr>
      <th>RAW_BS</th>
      <td>0.587555</td>
    </tr>
    <tr>
      <th>RAW_BS_IG3</th>
      <td>0.587555</td>
    </tr>
    <tr>
      <th>resolution</th>
      <td>2.4</td>
    </tr>
    <tr>
      <th>experimental_method_class</th>
      <td>x-ray</td>
    </tr>
    <tr>
      <th>experimental_method</th>
      <td>X-ray diffraction</td>
    </tr>
    <tr>
      <th>multi_method</th>
      <td>False</td>
    </tr>
    <tr>
      <th>revision_date</th>
      <td>20110713</td>
    </tr>
    <tr>
      <th>deposition_date</th>
      <td>20090731</td>
    </tr>
    <tr>
      <th>1/resolution</th>
      <td>0.416667</td>
    </tr>
    <tr>
      <th>id_score</th>
      <td>-65</td>
    </tr>
    <tr>
      <th>select_tag</th>
      <td>True</td>
    </tr>
    <tr>
      <th>select_rank</th>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>



```python
DisplayPDB(dark=True).show('3ii6', range(1,3))
```



<style>
    img.display {
        -webkit-filter: invert(1);
        filter: invert(1);
        }
</style>

<table align="center">
    <tr>
        <td>
            <b>Asymmetric unit</b> of 3ii6
        </td>
        <td>
            <b>Biological assembly 1</b> of 3ii6
        </td>
        <td>
            <b>Biological assembly 2</b> of 3ii6
        </td>
    </tr>
    <tr>
        <td>
            <img class="display" width="300em" src="https://cdn.rcsb.org/images/structures/ii/3ii6/3ii6_model-1.jpeg"/>
        </td>
        <td>
            <img class="display" width="300em" src="https://cdn.rcsb.org/images/structures/ii/3ii6/3ii6_assembly-1.jpeg"/>
        </td>
        <td>
            <img class="display" width="300em" src="https://cdn.rcsb.org/images/structures/ii/3ii6/3ii6_assembly-2.jpeg"/>
        </td>
    </tr>
</table>



### Prepare for Residue-Level Mapping


```python
record = df1[df1.select_tag.eq(True)].iloc[0]

mapping_df = PDB(record['pdb_id']).get_expanded_map_res_df(
    record['UniProt'], 
    record['new_unp_range'], 
    record['new_pdb_range'], 
    struct_asym_id=record['struct_asym_id']).result()

mapping_df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>unp_residue_number</th>
      <th>residue_number</th>
      <th>UniProt</th>
      <th>author_insertion_code</th>
      <th>author_residue_number</th>
      <th>chain_id</th>
      <th>entity_id</th>
      <th>multiple_conformers</th>
      <th>observed_ratio</th>
      <th>pdb_id</th>
      <th>residue_name</th>
      <th>struct_asym_id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>1</td>
      <td>Q13426</td>
      <td></td>
      <td>1</td>
      <td>A</td>
      <td>1</td>
      <td>NaN</td>
      <td>1</td>
      <td>3ii6</td>
      <td>MET</td>
      <td>A</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>2</td>
      <td>Q13426</td>
      <td></td>
      <td>2</td>
      <td>A</td>
      <td>1</td>
      <td>NaN</td>
      <td>1</td>
      <td>3ii6</td>
      <td>GLU</td>
      <td>A</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>3</td>
      <td>Q13426</td>
      <td></td>
      <td>3</td>
      <td>A</td>
      <td>1</td>
      <td>NaN</td>
      <td>1</td>
      <td>3ii6</td>
      <td>ARG</td>
      <td>A</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>4</td>
      <td>Q13426</td>
      <td></td>
      <td>4</td>
      <td>A</td>
      <td>1</td>
      <td>NaN</td>
      <td>1</td>
      <td>3ii6</td>
      <td>LYS</td>
      <td>A</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>5</td>
      <td>Q13426</td>
      <td></td>
      <td>5</td>
      <td>A</td>
      <td>1</td>
      <td>NaN</td>
      <td>1</td>
      <td>3ii6</td>
      <td>ILE</td>
      <td>A</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>198</th>
      <td>199</td>
      <td>199</td>
      <td>Q13426</td>
      <td></td>
      <td>199</td>
      <td>A</td>
      <td>1</td>
      <td>NaN</td>
      <td>1</td>
      <td>3ii6</td>
      <td>LEU</td>
      <td>A</td>
    </tr>
    <tr>
      <th>199</th>
      <td>200</td>
      <td>200</td>
      <td>Q13426</td>
      <td></td>
      <td>200</td>
      <td>A</td>
      <td>1</td>
      <td>NaN</td>
      <td>1</td>
      <td>3ii6</td>
      <td>ASN</td>
      <td>A</td>
    </tr>
    <tr>
      <th>200</th>
      <td>201</td>
      <td>201</td>
      <td>Q13426</td>
      <td></td>
      <td>201</td>
      <td>A</td>
      <td>1</td>
      <td>NaN</td>
      <td>1</td>
      <td>3ii6</td>
      <td>ALA</td>
      <td>A</td>
    </tr>
    <tr>
      <th>201</th>
      <td>202</td>
      <td>202</td>
      <td>Q13426</td>
      <td></td>
      <td>202</td>
      <td>A</td>
      <td>1</td>
      <td>NaN</td>
      <td>0</td>
      <td>3ii6</td>
      <td>ALA</td>
      <td>A</td>
    </tr>
    <tr>
      <th>202</th>
      <td>203</td>
      <td>203</td>
      <td>Q13426</td>
      <td></td>
      <td>203</td>
      <td>A</td>
      <td>1</td>
      <td>NaN</td>
      <td>0</td>
      <td>3ii6</td>
      <td>GLN</td>
      <td>A</td>
    </tr>
  </tbody>
</table>
<p>203 rows × 12 columns</p>
</div>



## Detecting Homomeric Interaction

> also annotated by `PISA` & `Interactome3D`

```py
from pdb_profiling.processors.i3d.api import Interactome3D

Interactome3D.pipe_init_interaction_meta().result()
```


```python
%time df2 = demo.pipe_select_ho(run_as_completed=True, progress_bar=tqdm).result()
df2[df2.i_select_tag.eq(True)]
```


    HBox(children=(FloatProgress(value=0.0, max=5.0), HTML(value='')))

    Wall time: 2.47 s
    




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>entity_id_1</th>
      <th>chain_id_1</th>
      <th>struct_asym_id_1</th>
      <th>struct_asym_id_in_assembly_1</th>
      <th>asym_id_rank_1</th>
      <th>model_id_1</th>
      <th>molecule_type_1</th>
      <th>surface_range_1</th>
      <th>interface_range_1</th>
      <th>entity_id_2</th>
      <th>...</th>
      <th>select_rank_2</th>
      <th>in_i3d</th>
      <th>unp_range_DSC</th>
      <th>best_select_rank_score</th>
      <th>second_select_rank_score</th>
      <th>unp_interface_range_1</th>
      <th>unp_interface_range_2</th>
      <th>i_group</th>
      <th>i_select_tag</th>
      <th>i_select_rank</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>A</td>
      <td>A</td>
      <td>A</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[15,35],[37,47],[49,108],[110,126],[128,227]]</td>
      <td>[[19,21],[30,31],[33,33],[51,54],[132,134],[13...</td>
      <td>1</td>
      <td>...</td>
      <td>4</td>
      <td>True</td>
      <td>1.0</td>
      <td>0.250000</td>
      <td>0.250000</td>
      <td>((5, 7), (16, 17), (19, 19), (37, 40), (118, 1...</td>
      <td>((5, 7), (16, 17), (19, 19), (37, 40), (118, 1...</td>
      <td>(Q13426, Q13426)</td>
      <td>True</td>
      <td>10</td>
    </tr>
    <tr>
      <th>7</th>
      <td>1</td>
      <td>A</td>
      <td>A</td>
      <td>A</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[1,21],[23,201]]</td>
      <td>[[11,16],[89,91],[103,103]]</td>
      <td>1</td>
      <td>...</td>
      <td>7</td>
      <td>False</td>
      <td>1.0</td>
      <td>1.000000</td>
      <td>0.142857</td>
      <td>((11, 16), (89, 91), (103, 103))</td>
      <td>((1, 1), (3, 3), (25, 25), (121, 121), (124, 1...</td>
      <td>(Q13426, Q13426)</td>
      <td>True</td>
      <td>4</td>
    </tr>
    <tr>
      <th>8</th>
      <td>1</td>
      <td>B</td>
      <td>B</td>
      <td>B</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[1,19],[21,35],[37,76],[82,94],[96,201]]</td>
      <td>[[117,118],[121,121],[124,124]]</td>
      <td>1</td>
      <td>...</td>
      <td>7</td>
      <td>False</td>
      <td>1.0</td>
      <td>0.200000</td>
      <td>0.142857</td>
      <td>((117, 118), (121, 121), (124, 124))</td>
      <td>((117, 118), (121, 121), (124, 124))</td>
      <td>(Q13426, Q13426)</td>
      <td>True</td>
      <td>11</td>
    </tr>
    <tr>
      <th>10</th>
      <td>1</td>
      <td>A</td>
      <td>A</td>
      <td>A</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[1,21],[23,201]]</td>
      <td>[[5,7],[15,17],[19,19],[37,40],[119,121],[123,...</td>
      <td>1</td>
      <td>...</td>
      <td>5</td>
      <td>True</td>
      <td>1.0</td>
      <td>1.000000</td>
      <td>0.200000</td>
      <td>((5, 7), (15, 17), (19, 19), (37, 40), (119, 1...</td>
      <td>((5, 7), (16, 17), (19, 19), (38, 40), (117, 1...</td>
      <td>(Q13426, Q13426)</td>
      <td>True</td>
      <td>2</td>
    </tr>
    <tr>
      <th>11</th>
      <td>1</td>
      <td>A</td>
      <td>A</td>
      <td>A</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[1,21],[23,201]]</td>
      <td>[[7,7],[9,9],[14,15],[17,17],[19,19],[80,80]]</td>
      <td>1</td>
      <td>...</td>
      <td>2</td>
      <td>False</td>
      <td>1.0</td>
      <td>1.000000</td>
      <td>0.500000</td>
      <td>((7, 7), (9, 9), (14, 15), (17, 17), (19, 19),...</td>
      <td>((7, 7), (9, 9), (14, 15), (17, 17), (80, 80))</td>
      <td>(Q13426, Q13426)</td>
      <td>True</td>
      <td>1</td>
    </tr>
    <tr>
      <th>16</th>
      <td>1</td>
      <td>A</td>
      <td>A</td>
      <td>AA</td>
      <td>2</td>
      <td>2</td>
      <td>polypeptide(L)</td>
      <td>[[1,35],[37,178]]</td>
      <td>[[57,62],[65,65],[98,98],[101,107]]</td>
      <td>1</td>
      <td>...</td>
      <td>6</td>
      <td>True</td>
      <td>1.0</td>
      <td>0.166667</td>
      <td>0.111111</td>
      <td>((57, 62), (65, 65), (98, 98), (101, 107))</td>
      <td>((1, 1), (3, 3), (23, 25), (30, 33), (46, 46),...</td>
      <td>(Q13426, Q13426)</td>
      <td>True</td>
      <td>15</td>
    </tr>
    <tr>
      <th>21</th>
      <td>1</td>
      <td>B</td>
      <td>B</td>
      <td>B</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[1,17],[19,33],[35,35],[37,41],[43,203]]</td>
      <td>[[145,145],[148,149],[152,152],[155,156],[158,...</td>
      <td>1</td>
      <td>...</td>
      <td>6</td>
      <td>True</td>
      <td>1.0</td>
      <td>0.166667</td>
      <td>0.166667</td>
      <td>((145, 145), (148, 149), (152, 152), (155, 156...</td>
      <td>((145, 145), (148, 149), (152, 152), (155, 156...</td>
      <td>(Q13426, Q13426)</td>
      <td>True</td>
      <td>12</td>
    </tr>
    <tr>
      <th>22</th>
      <td>1</td>
      <td>A</td>
      <td>A</td>
      <td>A</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[1,178]]</td>
      <td>[[7,7],[9,9],[15,17]]</td>
      <td>1</td>
      <td>...</td>
      <td>9</td>
      <td>True</td>
      <td>1.0</td>
      <td>0.111111</td>
      <td>0.111111</td>
      <td>((7, 7), (9, 9), (15, 17))</td>
      <td>((57, 57), (62, 62), (64, 64))</td>
      <td>(Q13426, Q13426)</td>
      <td>True</td>
      <td>21</td>
    </tr>
    <tr>
      <th>23</th>
      <td>1</td>
      <td>A</td>
      <td>A</td>
      <td>A</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[1,178]]</td>
      <td>[[166,166],[169,170],[173,174]]</td>
      <td>1</td>
      <td>...</td>
      <td>9</td>
      <td>False</td>
      <td>1.0</td>
      <td>0.111111</td>
      <td>0.111111</td>
      <td>((166, 166), (169, 170), (173, 174))</td>
      <td>((166, 166), (169, 170), (173, 174))</td>
      <td>(Q13426, Q13426)</td>
      <td>True</td>
      <td>22</td>
    </tr>
  </tbody>
</table>
<p>9 rows × 114 columns</p>
</div>



## Detecting Heteromeric Interaction

> also annotated by `PISA` & `Interactome3D`


```python
%time df3 = demo.pipe_select_he(run_as_completed=True, progress_bar=tqdm).result()
df3[df3.i_select_tag.eq(True)]
```


    HBox(children=(FloatProgress(value=0.0, max=3.0), HTML(value='')))

    Wall time: 2.23 s
    




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>entity_id_1</th>
      <th>chain_id_1</th>
      <th>struct_asym_id_1</th>
      <th>struct_asym_id_in_assembly_1</th>
      <th>asym_id_rank_1</th>
      <th>model_id_1</th>
      <th>molecule_type_1</th>
      <th>surface_range_1</th>
      <th>interface_range_1</th>
      <th>entity_id_2</th>
      <th>...</th>
      <th>select_tag_2</th>
      <th>select_rank_2</th>
      <th>in_i3d</th>
      <th>best_select_rank_score</th>
      <th>second_select_rank_score</th>
      <th>unp_interface_range_1</th>
      <th>unp_interface_range_2</th>
      <th>i_group</th>
      <th>i_select_tag</th>
      <th>i_select_rank</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>10</th>
      <td>1</td>
      <td>A</td>
      <td>A</td>
      <td>AA</td>
      <td>2</td>
      <td>2</td>
      <td>polypeptide(L)</td>
      <td>[[15,33],[35,35],[37,47],[49,108],[110,126],[1...</td>
      <td>[[169,169],[172,173],[176,177],[179,180],[183,...</td>
      <td>2</td>
      <td>...</td>
      <td>True</td>
      <td>1</td>
      <td>True</td>
      <td>1.0</td>
      <td>0.25</td>
      <td>((155, 155), (158, 159), (162, 163), (165, 166...</td>
      <td>((465, 466), (469, 470), (473, 473), (476, 477...</td>
      <td>(Q13426, Q0D2I5)</td>
      <td>True</td>
      <td>1</td>
    </tr>
    <tr>
      <th>11</th>
      <td>1</td>
      <td>A</td>
      <td>A</td>
      <td>AA</td>
      <td>2</td>
      <td>2</td>
      <td>polypeptide(L)</td>
      <td>[[15,33],[35,35],[37,47],[49,108],[110,126],[1...</td>
      <td>[[169,169],[172,173],[176,177],[179,180],[183,...</td>
      <td>2</td>
      <td>...</td>
      <td>True</td>
      <td>1</td>
      <td>True</td>
      <td>1.0</td>
      <td>0.25</td>
      <td>((155, 155), (158, 159), (162, 163), (165, 166...</td>
      <td>((105, 106), (109, 110), (113, 113), (116, 117...</td>
      <td>(Q13426, Q0D2I5-2)</td>
      <td>True</td>
      <td>1</td>
    </tr>
    <tr>
      <th>12</th>
      <td>1</td>
      <td>A</td>
      <td>A</td>
      <td>AA</td>
      <td>2</td>
      <td>2</td>
      <td>polypeptide(L)</td>
      <td>[[15,33],[35,35],[37,47],[49,108],[110,126],[1...</td>
      <td>[[169,169],[172,173],[176,177],[179,180],[183,...</td>
      <td>2</td>
      <td>...</td>
      <td>True</td>
      <td>1</td>
      <td>True</td>
      <td>1.0</td>
      <td>0.25</td>
      <td>((155, 155), (158, 159), (162, 163), (165, 166...</td>
      <td>((468, 469), (472, 473), (476, 476), (479, 480...</td>
      <td>(Q13426, Q0D2I5-4)</td>
      <td>True</td>
      <td>1</td>
    </tr>
    <tr>
      <th>13</th>
      <td>1</td>
      <td>A</td>
      <td>A</td>
      <td>AA</td>
      <td>2</td>
      <td>2</td>
      <td>polypeptide(L)</td>
      <td>[[15,33],[35,35],[37,47],[49,108],[110,126],[1...</td>
      <td>[[169,169],[172,173],[176,177],[179,180],[183,...</td>
      <td>2</td>
      <td>...</td>
      <td>True</td>
      <td>1</td>
      <td>True</td>
      <td>1.0</td>
      <td>0.25</td>
      <td>((155, 155), (158, 159), (162, 163), (165, 166...</td>
      <td>((469, 470), (473, 474), (477, 477), (480, 481...</td>
      <td>(Q13426, Q0D2I5-5)</td>
      <td>True</td>
      <td>1</td>
    </tr>
    <tr>
      <th>14</th>
      <td>1</td>
      <td>A</td>
      <td>A</td>
      <td>AA</td>
      <td>2</td>
      <td>2</td>
      <td>polypeptide(L)</td>
      <td>[[15,33],[35,35],[37,47],[49,108],[110,126],[1...</td>
      <td>[[169,169],[172,173],[176,177],[179,180],[183,...</td>
      <td>2</td>
      <td>...</td>
      <td>True</td>
      <td>1</td>
      <td>True</td>
      <td>1.0</td>
      <td>0.25</td>
      <td>((155, 155), (158, 159), (162, 163), (165, 166...</td>
      <td>((106, 107), (110, 111), (114, 114), (117, 118...</td>
      <td>(Q13426, Q0D2I5-6)</td>
      <td>True</td>
      <td>1</td>
    </tr>
    <tr>
      <th>15</th>
      <td>1</td>
      <td>A</td>
      <td>A</td>
      <td>AA</td>
      <td>2</td>
      <td>2</td>
      <td>polypeptide(L)</td>
      <td>[[15,33],[35,35],[37,47],[49,108],[110,126],[1...</td>
      <td>[[169,169],[172,173],[176,177],[179,180],[183,...</td>
      <td>2</td>
      <td>...</td>
      <td>True</td>
      <td>1</td>
      <td>True</td>
      <td>1.0</td>
      <td>0.25</td>
      <td>((155, 155), (158, 159), (162, 163), (165, 166...</td>
      <td>((468, 469), (472, 473), (476, 476), (479, 480...</td>
      <td>(Q13426, Q0D2I5-7)</td>
      <td>True</td>
      <td>1</td>
    </tr>
    <tr>
      <th>41</th>
      <td>1</td>
      <td>C</td>
      <td>C</td>
      <td>C</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[1,21],[23,201]]</td>
      <td>[[150,150],[153,154],[157,158],[161,161],[164,...</td>
      <td>2</td>
      <td>...</td>
      <td>True</td>
      <td>1</td>
      <td>True</td>
      <td>1.0</td>
      <td>0.50</td>
      <td>((150, 150), (153, 154), (157, 158), (161, 161...</td>
      <td>((763, 771), (774, 775), (778, 778), (800, 800...</td>
      <td>(Q13426, P49917)</td>
      <td>True</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
<p>7 rows × 117 columns</p>
</div>



## Collecting Residue-Level Annotation From `FunPDBe` via `PDBe Graph API`

> PDBe-KB consortium, PDBe-KB: a community-driven resource for structural and functional annotations, Nucleic Acids Research, Volume 48, Issue D1, 08 January 2020, Pages D344–D353, https://doi.org/10.1093/nar/gkz853

<table>
	<thead>
		<tr>
			<td>Partner resource (Reference)</td>
			<td>Resource leader</td>
			<td>Type of annotations</td>
			<td>Number of PDB entries</td>
		</tr>
	</thead>
	<tr>
		<td>COSPI-Depth (21)</td>
		<td>M. S. Madhusudhan</td>
		<td>Residue depth</td>
		<td>141 097</td>
	</tr>
	<tr>
		<td>P2rank (6)</td>
		<td>D. Hoksza</td>
		<td>Binding site predictions</td>
		<td>138 892</td>
	</tr>
	<tr>
		<td>Arpeggio (15)</td>
		<td>T. Blundell</td>
		<td>Ligand interactions</td>
		<td>117 023</td>
	</tr>
	<tr>
		<td>3DComplex (14)</td>
		<td>E. D. Levy</td>
		<td>Interaction interfaces</td>
		<td>111 555</td>
	</tr>
	<tr>
		<td>DynaMine (19)</td>
		<td>W. Vranken</td>
		<td>Backbone flexibility predictions</td>
		<td>98 548</td>
	</tr>
	<tr>
		<td>POPSCOMP (20)</td>
		<td>F. Fraternali</td>
		<td>Solvent accessibility</td>
		<td>77 578</td>
	</tr>
	<tr>
		<td>AKID (11)</td>
		<td>M. Helmer-Citterich</td>
		<td>Kinase-target predictor</td>
		<td>41 492</td>
	</tr>
	<tr>
		<td>ChannelsDB (9)</td>
		<td>R. Svobodova</td>
		<td>Molecular channels</td>
		<td>25 351</td>
	</tr>
	<tr>
		<td>CATH-FunSites (13)</td>
		<td>C. Orengo</td>
		<td>Functional site predictions</td>
		<td>23 975</td>
	</tr>
	<tr>
		<td>canSAR (7)</td>
		<td>B. al-Lazikani</td>
		<td>Druggable pocket predictions</td>
		<td>17 804</td>
	</tr>
	<tr>
		<td>FoldX (17)</td>
		<td>L. Serrano</td>
		<td>Energetic consequences of mutations</td>
		<td>3778</td>
	</tr>
	<tr>
		<td>ProKinO (10)</td>
		<td>N. Kannan</td>
		<td>Curated regulatory sites</td>
		<td>3673</td>
	</tr>
	<tr>
		<td>14–3-3-Pred (12)</td>
		<td>G. Barton</td>
		<td>Binding site predictions</td>
		<td>1941</td>
	</tr>
	<tr>
		<td>CaMKinet (in preparation)</td>
		<td>M. Kumar</td>
		<td>Curated PTM sites</td>
		<td>1076</td>
	</tr>
	<tr>
		<td>M-CSA (5)</td>
		<td>J. Thornton</td>
		<td>Curated catalytic sites</td>
		<td>919</td>
	</tr>
	<tr>
		<td>3DLigandSite (8)</td>
		<td>M. Wass</td>
		<td>Binding site predictions</td>
		<td>910</td>
	</tr>
	<tr>
		<td>Missense3D (18)</td>
		<td>M. Sternberg</td>
		<td>Mutations in Human Proteome</td>
		<td>0*</td>
	</tr>
	<tr>
		<td>MetalPDB (16)</td>
		<td>A. Rosato</td>
		<td>Curated metal binding sites</td>
		<td>0*</td>
	</tr>
	<tr>
		<td>ELM (24)</td>
		<td>T. Gibson</td>
		<td>Short linear motifs</td>
		<td>0*</td>
	</tr>
</table>

<table>
    <tr><td><img src="https://oup.silverchair-cdn.com/oup/backfile/Content_public/Journal/nar/48/D1/10.1093_nar_gkz853/1/gkz853fig1.jpeg?Expires=1607156024&Signature=t8tPmkcJZhzfrdYaKmN~EJar2F0LHRhI8mKvidHMPxNHtyhwKYYO0uva1m-cebL9B92NHi8~P9tvVtUCF9nqHJm63YBoPaV7srEf7HmvMStY~3yYQ9vxPhBPBbB0xYzY9GYr0eHsPSHFpjlcWdnvvhbS-Qb1nbDKWBCb9vRj5lG1G09wN2L9RM-TKsky5VejsApK8I9RbwQ3nIpgGFCCWey-YJD9ZTSIJHQP-X1Xvm~keZWVzjSoZCUUmS-wcz31B83JEgnu6do669sy4BppRlQEulSyKM8Oa8X2SvNGZ-71VENEZVhQGsUo6jV4CeMEbc2ZRSQfNWS1w9JcBoJa9g__&Key-Pair-Id=APKAIE5G5CRDK6RD3PGA" width="80%"><td></tr>
</table>


```python
pdb_ob = PDB(record['pdb_id'])
pdb_ob
```




    <PDB 3ii6>




```python
funpdbe_df = pdb_ob.fetch_from_web_api('graph-api/pdb/funpdbe_annotation/', Base.to_dataframe).result()
funpdbe_df[funpdbe_df.chain_id.eq(record['chain_id'])]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>author_insertion_code</th>
      <th>author_residue_number</th>
      <th>chain_id</th>
      <th>chem_comp_id</th>
      <th>confidence_classification</th>
      <th>confidence_score</th>
      <th>entity_id</th>
      <th>evidence_codes</th>
      <th>label</th>
      <th>origin</th>
      <th>pdb_id</th>
      <th>raw_score</th>
      <th>residue_number</th>
      <th>site_id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td></td>
      <td>1</td>
      <td>A</td>
      <td>MET</td>
      <td>NaN</td>
      <td>0.5</td>
      <td>1</td>
      <td>['ECO_0000364', 'ECO_0000203']</td>
      <td>backbone</td>
      <td>dynamine</td>
      <td>3ii6</td>
      <td>0.765000</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td></td>
      <td>2</td>
      <td>A</td>
      <td>GLU</td>
      <td>NaN</td>
      <td>0.5</td>
      <td>1</td>
      <td>['ECO_0000364', 'ECO_0000203']</td>
      <td>backbone</td>
      <td>dynamine</td>
      <td>3ii6</td>
      <td>0.773000</td>
      <td>2</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td></td>
      <td>3</td>
      <td>A</td>
      <td>ARG</td>
      <td>NaN</td>
      <td>0.5</td>
      <td>1</td>
      <td>['ECO_0000364', 'ECO_0000203']</td>
      <td>backbone</td>
      <td>dynamine</td>
      <td>3ii6</td>
      <td>0.784000</td>
      <td>3</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td></td>
      <td>4</td>
      <td>A</td>
      <td>LYS</td>
      <td>NaN</td>
      <td>0.5</td>
      <td>1</td>
      <td>['ECO_0000364', 'ECO_0000203']</td>
      <td>backbone</td>
      <td>dynamine</td>
      <td>3ii6</td>
      <td>0.788000</td>
      <td>4</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td></td>
      <td>5</td>
      <td>A</td>
      <td>ILE</td>
      <td>NaN</td>
      <td>0.5</td>
      <td>1</td>
      <td>['ECO_0000364', 'ECO_0000203']</td>
      <td>backbone</td>
      <td>dynamine</td>
      <td>3ii6</td>
      <td>0.792000</td>
      <td>5</td>
      <td>1</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>9282</th>
      <td></td>
      <td>161</td>
      <td>A</td>
      <td>ARG</td>
      <td>high</td>
      <td>NaN</td>
      <td>1</td>
      <td>['ECO_0000006', 'ECO_0000088']</td>
      <td>Disease</td>
      <td>FoldX</td>
      <td>3ii6</td>
      <td>1.124540</td>
      <td>161</td>
      <td>1</td>
    </tr>
    <tr>
      <th>9283</th>
      <td></td>
      <td>56</td>
      <td>A</td>
      <td>ALA</td>
      <td>high</td>
      <td>NaN</td>
      <td>1</td>
      <td>['ECO_0000006', 'ECO_0000088']</td>
      <td>Polymorphism</td>
      <td>FoldX</td>
      <td>3ii6</td>
      <td>2.279820</td>
      <td>56</td>
      <td>2</td>
    </tr>
    <tr>
      <th>9284</th>
      <td></td>
      <td>12</td>
      <td>A</td>
      <td>SER</td>
      <td>high</td>
      <td>NaN</td>
      <td>1</td>
      <td>['ECO_0000006', 'ECO_0000088']</td>
      <td>Polymorphism</td>
      <td>FoldX</td>
      <td>3ii6</td>
      <td>0.314961</td>
      <td>12</td>
      <td>3</td>
    </tr>
    <tr>
      <th>9285</th>
      <td></td>
      <td>43</td>
      <td>A</td>
      <td>TRP</td>
      <td>high</td>
      <td>NaN</td>
      <td>1</td>
      <td>['ECO_0000006', 'ECO_0000088']</td>
      <td>Disease</td>
      <td>FoldX</td>
      <td>3ii6</td>
      <td>2.777570</td>
      <td>43</td>
      <td>4</td>
    </tr>
    <tr>
      <th>9286</th>
      <td></td>
      <td>142</td>
      <td>A</td>
      <td>GLU</td>
      <td>high</td>
      <td>NaN</td>
      <td>1</td>
      <td>['ECO_0000006', 'ECO_0000088']</td>
      <td>Polymorphism</td>
      <td>FoldX</td>
      <td>3ii6</td>
      <td>-0.196969</td>
      <td>142</td>
      <td>5</td>
    </tr>
  </tbody>
</table>
<p>1613 rows × 14 columns</p>
</div>



## Collecting Chain|Residue-Level Functional Annotation From `SIFTS API` | `PDBe Graph API`

> Jose M Dana, Aleksandras Gutmanas, Nidhi Tyagi, Guoying Qi, Claire O’Donovan, Maria Martin, Sameer Velankar, SIFTS: updated Structure Integration with Function, Taxonomy and Sequences resource allows 40-fold increase in coverage of structure-based annotations for proteins, Nucleic Acids Research, Volume 47, Issue D1, 08 January 2019, Pages D482–D489, https://doi.org/10.1093/nar/gky1114

Structure Integration with Function, Taxonomy and Sequence (SIFTS) is a project in the PDBe-KB resource for residue-level mapping between UniProt and PDB entries. SIFTS also provides annotation from the IntEnz, GO, InterPro, Pfam, CATH, SCOP, PubMed, Ensembl and Homologene resources. The information is updated and released every week concurrently with the release of new PDB entries and is widely used by resources such as RCSB PDB, PDBj, PDBsum, Pfam, SCOP and InterPro.

<table>
    <tr><td><img src="https://www.ebi.ac.uk/pdbe/docs/sifts/images/all_logos.png" width="50%"><td></tr>
</table>

* `api/mappings/` or `graph-api/mappings/`
    * `api/mappings/sequence_domains/`
        * NOTE: (interpro+pfam)
        * `api/mappings/interpro/`
        * `api/mappings/pfam/`
    * `api/mappings/structural_domains/`
        * NOTE: (scop+cath)
        * `api/mappings/scop/`
        * `api/mappings/cath/`
    * `api/mappings/cath_b/`
    * `api/mappings/go/` (chain-level)
    * `api/mappings/ec/` (chain-level)
    * `api/mappings/hmmer/`

* `api/pdb/entry/secondary_structure/`
* `graph-api/pdb/sequence_conservation/`


```python
pdb_ob.fetch_from_web_api('api/mappings/interpro/', Base.to_dataframe).result().query('chain_id == "{}"'.format(record['chain_id']))
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>InterPro</th>
      <th>chain_id</th>
      <th>end</th>
      <th>entity_id</th>
      <th>identifier</th>
      <th>name</th>
      <th>pdb_id</th>
      <th>start</th>
      <th>struct_asym_id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>IPR009089</td>
      <td>A</td>
      <td>{"author_residue_number":117,"author_insertion...</td>
      <td>1</td>
      <td>XRCC4, N-terminal domain superfamily</td>
      <td>XRCC4, N-terminal domain superfamily</td>
      <td>3ii6</td>
      <td>{"author_residue_number":1,"author_insertion_c...</td>
      <td>A</td>
    </tr>
    <tr>
      <th>22</th>
      <td>IPR010585</td>
      <td>A</td>
      <td>{"author_residue_number":200,"author_insertion...</td>
      <td>1</td>
      <td>DNA repair protein XRCC4</td>
      <td>DNA repair protein XRCC4</td>
      <td>3ii6</td>
      <td>{"author_residue_number":1,"author_insertion_c...</td>
      <td>A</td>
    </tr>
    <tr>
      <th>23</th>
      <td>IPR010585</td>
      <td>A</td>
      <td>{"author_residue_number":201,"author_insertion...</td>
      <td>1</td>
      <td>DNA repair protein XRCC4</td>
      <td>DNA repair protein XRCC4</td>
      <td>3ii6</td>
      <td>{"author_residue_number":2,"author_insertion_c...</td>
      <td>A</td>
    </tr>
  </tbody>
</table>
</div>




```python
pdb_ob.fetch_from_web_api('api/mappings/pfam/', Base.to_dataframe).result().query('chain_id == "{}"'.format(record['chain_id']))
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Pfam</th>
      <th>chain_id</th>
      <th>coverage</th>
      <th>description</th>
      <th>end</th>
      <th>entity_id</th>
      <th>identifier</th>
      <th>name</th>
      <th>pdb_id</th>
      <th>start</th>
      <th>struct_asym_id</th>
    </tr>
  </thead>
  <tbody>
  </tbody>
</table>
</div>




```python
pdb_ob.fetch_from_web_api('api/mappings/structural_domains/', Base.to_dataframe).result().query('chain_id == "{}"'.format(record['chain_id']))
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>CATH</th>
      <th>architecture</th>
      <th>chain_id</th>
      <th>class</th>
      <th>domain</th>
      <th>end</th>
      <th>entity_id</th>
      <th>homology</th>
      <th>identifier</th>
      <th>name</th>
      <th>pdb_id</th>
      <th>segment_id</th>
      <th>start</th>
      <th>struct_asym_id</th>
      <th>topology</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>4</th>
      <td>1.20.5.370</td>
      <td>Up-down Bundle</td>
      <td>A</td>
      <td>Mainly Alpha</td>
      <td>3ii6A02</td>
      <td>{"author_residue_number":176,"author_insertion...</td>
      <td>1</td>
      <td>Single alpha-helices involved in coiled-coils ...</td>
      <td>Single alpha-helices involved in coiled-coils ...</td>
      <td>Dna repair protein xrcc4. Chain: a, b, c, d. F...</td>
      <td>3ii6</td>
      <td>1</td>
      <td>{"author_residue_number":119,"author_insertion...</td>
      <td>A</td>
      <td>Single alpha-helices involved in coiled-coils ...</td>
    </tr>
    <tr>
      <th>8</th>
      <td>2.170.210.10</td>
      <td>Beta Complex</td>
      <td>A</td>
      <td>Mainly Beta</td>
      <td>3ii6A01</td>
      <td>{"author_residue_number":118,"author_insertion...</td>
      <td>1</td>
      <td>DNA double-strand break repair and VJ recombin...</td>
      <td>Dna Repair Protein Xrcc4; Chain: A, domain 1</td>
      <td>Dna repair protein xrcc4. Chain: a, b, c, d. F...</td>
      <td>3ii6</td>
      <td>1</td>
      <td>{"author_residue_number":1,"author_insertion_c...</td>
      <td>A</td>
      <td>Dna Repair Protein Xrcc4; Chain: A, domain 1</td>
    </tr>
  </tbody>
</table>
</div>




```python
pdb_ob.fetch_from_web_api('api/mappings/cath_b/', Base.to_dataframe).result().query('chain_id == "{}"'.format(record['chain_id']))
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>CATH-B</th>
      <th>architecture</th>
      <th>chain_id</th>
      <th>class</th>
      <th>domain</th>
      <th>end</th>
      <th>entity_id</th>
      <th>homology</th>
      <th>identifier</th>
      <th>name</th>
      <th>pdb_id</th>
      <th>segment_id</th>
      <th>start</th>
      <th>struct_asym_id</th>
      <th>topology</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>4</th>
      <td>1.20.5.370</td>
      <td>Up-down Bundle</td>
      <td>A</td>
      <td>Mainly Alpha</td>
      <td>3ii6A02</td>
      <td>{"author_residue_number":176,"author_insertion...</td>
      <td>1</td>
      <td>Single alpha-helices involved in coiled-coils ...</td>
      <td>Single alpha-helices involved in coiled-coils ...</td>
      <td>Dna repair protein xrcc4. Chain: a, b, c, d. F...</td>
      <td>3ii6</td>
      <td>1</td>
      <td>{"author_residue_number":119,"author_insertion...</td>
      <td>A</td>
      <td>Single alpha-helices involved in coiled-coils ...</td>
    </tr>
    <tr>
      <th>8</th>
      <td>2.170.210.10</td>
      <td>Beta Complex</td>
      <td>A</td>
      <td>Mainly Beta</td>
      <td>3ii6A01</td>
      <td>{"author_residue_number":118,"author_insertion...</td>
      <td>1</td>
      <td>DNA double-strand break repair and VJ recombin...</td>
      <td>Dna Repair Protein Xrcc4; Chain: A, domain 1</td>
      <td>Dna repair protein xrcc4. Chain: a, b, c, d. F...</td>
      <td>3ii6</td>
      <td>1</td>
      <td>{"author_residue_number":1,"author_insertion_c...</td>
      <td>A</td>
      <td>Dna Repair Protein Xrcc4; Chain: A, domain 1</td>
    </tr>
  </tbody>
</table>
</div>




```python
pdb_ob.fetch_from_web_api('api/mappings/go/', Base.to_dataframe).result().query('chain_id == "{}"'.format(record['chain_id']))
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>GO</th>
      <th>category</th>
      <th>chain_id</th>
      <th>definition</th>
      <th>entity_id</th>
      <th>identifier</th>
      <th>name</th>
      <th>pdb_id</th>
      <th>struct_asym_id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>GO:0006310</td>
      <td>Biological_process</td>
      <td>A</td>
      <td>Any process in which a new genotype is formed ...</td>
      <td>1</td>
      <td>DNA recombination</td>
      <td>DNA recombination</td>
      <td>3ii6</td>
      <td>A</td>
    </tr>
    <tr>
      <th>4</th>
      <td>GO:0006302</td>
      <td>Biological_process</td>
      <td>A</td>
      <td>The repair of double-strand breaks in DNA via ...</td>
      <td>1</td>
      <td>double-strand break repair</td>
      <td>double-strand break repair</td>
      <td>3ii6</td>
      <td>A</td>
    </tr>
    <tr>
      <th>10</th>
      <td>GO:0005634</td>
      <td>Cellular_component</td>
      <td>A</td>
      <td>A membrane-bounded organelle of eukaryotic cel...</td>
      <td>1</td>
      <td>nucleus</td>
      <td>nucleus</td>
      <td>3ii6</td>
      <td>A</td>
    </tr>
    <tr>
      <th>18</th>
      <td>GO:0003677</td>
      <td>Molecular_function</td>
      <td>A</td>
      <td>Any molecular function by which a gene product...</td>
      <td>1</td>
      <td>DNA binding</td>
      <td>DNA binding</td>
      <td>3ii6</td>
      <td>A</td>
    </tr>
  </tbody>
</table>
</div>




```python
pdb_ob.fetch_from_web_api('api/mappings/ec/', Base.to_dataframe).result().query('chain_id == "{}"'.format(record['chain_id']))
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>EC</th>
      <th>accepted_name</th>
      <th>chain_id</th>
      <th>entity_id</th>
      <th>identifier</th>
      <th>pdb_id</th>
      <th>reaction</th>
      <th>struct_asym_id</th>
      <th>synonyms</th>
      <th>systematic_name</th>
    </tr>
  </thead>
  <tbody>
  </tbody>
</table>
</div>




```python
pdb_ob.fetch_from_web_api('api/mappings/hmmer/', Base.to_dataframe).result().query('chain_id == "{}"'.format(record['chain_id']))
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>HMMER</th>
      <th>chain_id</th>
      <th>coverage</th>
      <th>description</th>
      <th>end</th>
      <th>entity_id</th>
      <th>hmm_end</th>
      <th>hmm_length</th>
      <th>hmm_start</th>
      <th>identifier</th>
      <th>name</th>
      <th>pdb_id</th>
      <th>start</th>
      <th>struct_asym_id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>6</th>
      <td>PF06632</td>
      <td>A</td>
      <td>0.608</td>
      <td>DNA double-strand break repair and V(D)J recom...</td>
      <td>{"author_residue_number":200,"author_insertion...</td>
      <td>1</td>
      <td>205</td>
      <td>337</td>
      <td>1</td>
      <td>DNA double-strand break repair and V(D)J recom...</td>
      <td>XRCC4</td>
      <td>3ii6</td>
      <td>{"author_residue_number":1,"author_insertion_c...</td>
      <td>A</td>
    </tr>
  </tbody>
</table>
</div>




```python
pdb_ob.fetch_from_web_api('api/pdb/entry/secondary_structure/', Base.to_dataframe).result().query('chain_id == "{}"'.format(record['chain_id']))
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>chain_id</th>
      <th>end</th>
      <th>entity_id</th>
      <th>pdb_id</th>
      <th>secondary_structure</th>
      <th>sheet_id</th>
      <th>start</th>
      <th>struct_asym_id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>A</td>
      <td>{"author_residue_number":59,"author_insertion_...</td>
      <td>1</td>
      <td>3ii6</td>
      <td>helices</td>
      <td>NaN</td>
      <td>{"author_residue_number":49,"author_insertion_...</td>
      <td>A</td>
    </tr>
    <tr>
      <th>1</th>
      <td>A</td>
      <td>{"author_residue_number":75,"author_insertion_...</td>
      <td>1</td>
      <td>3ii6</td>
      <td>helices</td>
      <td>NaN</td>
      <td>{"author_residue_number":62,"author_insertion_...</td>
      <td>A</td>
    </tr>
    <tr>
      <th>2</th>
      <td>A</td>
      <td>{"author_residue_number":201,"author_insertion...</td>
      <td>1</td>
      <td>3ii6</td>
      <td>helices</td>
      <td>NaN</td>
      <td>{"author_residue_number":118,"author_insertion...</td>
      <td>A</td>
    </tr>
    <tr>
      <th>3</th>
      <td>A</td>
      <td>{"author_residue_number":10,"author_insertion_...</td>
      <td>1</td>
      <td>3ii6</td>
      <td>strands</td>
      <td>1.0</td>
      <td>{"author_residue_number":3,"author_insertion_c...</td>
      <td>A</td>
    </tr>
    <tr>
      <th>4</th>
      <td>A</td>
      <td>{"author_residue_number":23,"author_insertion_...</td>
      <td>1</td>
      <td>3ii6</td>
      <td>strands</td>
      <td>1.0</td>
      <td>{"author_residue_number":13,"author_insertion_...</td>
      <td>A</td>
    </tr>
    <tr>
      <th>5</th>
      <td>A</td>
      <td>{"author_residue_number":37,"author_insertion_...</td>
      <td>1</td>
      <td>3ii6</td>
      <td>strands</td>
      <td>1.0</td>
      <td>{"author_residue_number":31,"author_insertion_...</td>
      <td>A</td>
    </tr>
    <tr>
      <th>6</th>
      <td>A</td>
      <td>{"author_residue_number":44,"author_insertion_...</td>
      <td>1</td>
      <td>3ii6</td>
      <td>strands</td>
      <td>1.0</td>
      <td>{"author_residue_number":42,"author_insertion_...</td>
      <td>A</td>
    </tr>
    <tr>
      <th>7</th>
      <td>A</td>
      <td>{"author_residue_number":48,"author_insertion_...</td>
      <td>1</td>
      <td>3ii6</td>
      <td>strands</td>
      <td>1.0</td>
      <td>{"author_residue_number":46,"author_insertion_...</td>
      <td>A</td>
    </tr>
    <tr>
      <th>8</th>
      <td>A</td>
      <td>{"author_residue_number":88,"author_insertion_...</td>
      <td>1</td>
      <td>3ii6</td>
      <td>strands</td>
      <td>2.0</td>
      <td>{"author_residue_number":84,"author_insertion_...</td>
      <td>A</td>
    </tr>
    <tr>
      <th>9</th>
      <td>A</td>
      <td>{"author_residue_number":100,"author_insertion...</td>
      <td>1</td>
      <td>3ii6</td>
      <td>strands</td>
      <td>2.0</td>
      <td>{"author_residue_number":94,"author_insertion_...</td>
      <td>A</td>
    </tr>
    <tr>
      <th>10</th>
      <td>A</td>
      <td>{"author_residue_number":112,"author_insertion...</td>
      <td>1</td>
      <td>3ii6</td>
      <td>strands</td>
      <td>2.0</td>
      <td>{"author_residue_number":105,"author_insertion...</td>
      <td>A</td>
    </tr>
    <tr>
      <th>11</th>
      <td>A</td>
      <td>{"author_residue_number":115,"author_insertion...</td>
      <td>1</td>
      <td>3ii6</td>
      <td>strands</td>
      <td>1.0</td>
      <td>{"author_residue_number":114,"author_insertion...</td>
      <td>A</td>
    </tr>
  </tbody>
</table>
</div>




```python
seq_conser_df = pdb_ob.fetch_from_web_api(
    'graph-api/pdb/sequence_conservation/', 
    Base.to_dataframe, 
    mask_id="%s/%s" % (record['pdb_id'], record['entity_id'])
).result()

seq_conser_df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>conservation_score</th>
      <th>entity_id</th>
      <th>length</th>
      <th>letter_array</th>
      <th>pdb_id</th>
      <th>proba_array</th>
      <th>residue_number</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>1</td>
      <td>203</td>
      <td>["M","L","I","V","A","F","T","S","K","R","E","...</td>
      <td>3ii6</td>
      <td>[0.217,0.168,0.096,0.096,0.054,0.042,0.04,0.03...</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0</td>
      <td>1</td>
      <td>203</td>
      <td>["E","D","K","S","N","A","Q","R","T","G","L","...</td>
      <td>3ii6</td>
      <td>[0.239,0.101,0.082,0.071,0.065,0.062,0.062,0.0...</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0</td>
      <td>1</td>
      <td>203</td>
      <td>["R","K","E","T","S","A","Q","N","D","G","L","...</td>
      <td>3ii6</td>
      <td>[0.158,0.151,0.08,0.071,0.07,0.064,0.064,0.049...</td>
      <td>3</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0</td>
      <td>1</td>
      <td>203</td>
      <td>["K","S","R","A","E","T","Q","N","D","V","L","...</td>
      <td>3ii6</td>
      <td>[0.121,0.097,0.089,0.088,0.087,0.085,0.064,0.0...</td>
      <td>4</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2</td>
      <td>1</td>
      <td>203</td>
      <td>["V","I","L","A","M","T","F","S","C","Y","E","...</td>
      <td>3ii6</td>
      <td>[0.444,0.227,0.128,0.033,0.029,0.026,0.021,0.0...</td>
      <td>5</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>197</th>
      <td>0</td>
      <td>1</td>
      <td>203</td>
      <td>["L","V","I","A","T","K","S","Q","E","F","M","...</td>
      <td>3ii6</td>
      <td>[0.286,0.099,0.079,0.07,0.051,0.046,0.046,0.03...</td>
      <td>198</td>
    </tr>
    <tr>
      <th>198</th>
      <td>0</td>
      <td>1</td>
      <td>203</td>
      <td>["L","A","K","E","S","V","T","R","I","Q","N","...</td>
      <td>3ii6</td>
      <td>[0.156,0.08,0.075,0.071,0.068,0.067,0.066,0.05...</td>
      <td>199</td>
    </tr>
    <tr>
      <th>199</th>
      <td>0</td>
      <td>1</td>
      <td>203</td>
      <td>["N","S","E","K","A","D","Q","R","T","V","L","...</td>
      <td>3ii6</td>
      <td>[0.109,0.106,0.103,0.094,0.077,0.068,0.067,0.0...</td>
      <td>200</td>
    </tr>
    <tr>
      <th>200</th>
      <td>0</td>
      <td>1</td>
      <td>203</td>
      <td>["E","A","K","S","D","T","N","Q","V","R","L","...</td>
      <td>3ii6</td>
      <td>[0.142,0.093,0.081,0.074,0.072,0.065,0.057,0.0...</td>
      <td>201</td>
    </tr>
    <tr>
      <th>201</th>
      <td>0</td>
      <td>1</td>
      <td>203</td>
      <td>["A","V","S","L","I","T","K","E","G","D","R","...</td>
      <td>3ii6</td>
      <td>[0.136,0.094,0.083,0.082,0.071,0.066,0.055,0.0...</td>
      <td>202</td>
    </tr>
  </tbody>
</table>
<p>202 rows × 7 columns</p>
</div>



## Visualization


```python
import matplotlib.pyplot as plt
import seaborn as sns
import orjson as json
plt.style.use('ggplot')
```


```python
expanded_seq_conser_df = DataFrame(
    seq_conser_df.apply(lambda x: dict(zip(json.loads(x['letter_array']), json.loads(x['proba_array']))), axis=1).tolist(),
    index=seq_conser_df.residue_number
)
expanded_seq_conser_df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>M</th>
      <th>L</th>
      <th>I</th>
      <th>V</th>
      <th>A</th>
      <th>F</th>
      <th>T</th>
      <th>S</th>
      <th>K</th>
      <th>R</th>
      <th>E</th>
      <th>Q</th>
      <th>G</th>
      <th>Y</th>
      <th>N</th>
      <th>D</th>
      <th>P</th>
      <th>H</th>
      <th>C</th>
      <th>W</th>
    </tr>
    <tr>
      <th>residue_number</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>0.217</td>
      <td>0.168</td>
      <td>0.096</td>
      <td>0.096</td>
      <td>0.054</td>
      <td>0.042</td>
      <td>0.040</td>
      <td>0.039</td>
      <td>0.036</td>
      <td>0.029</td>
      <td>0.028</td>
      <td>0.024</td>
      <td>0.023</td>
      <td>0.023</td>
      <td>0.021</td>
      <td>0.019</td>
      <td>0.014</td>
      <td>0.013</td>
      <td>0.011</td>
      <td>0.007</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0.013</td>
      <td>0.032</td>
      <td>0.021</td>
      <td>0.030</td>
      <td>0.062</td>
      <td>0.012</td>
      <td>0.047</td>
      <td>0.071</td>
      <td>0.082</td>
      <td>0.051</td>
      <td>0.239</td>
      <td>0.062</td>
      <td>0.041</td>
      <td>0.015</td>
      <td>0.065</td>
      <td>0.101</td>
      <td>0.023</td>
      <td>0.025</td>
      <td>0.006</td>
      <td>0.004</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0.017</td>
      <td>0.038</td>
      <td>0.024</td>
      <td>0.034</td>
      <td>0.064</td>
      <td>0.013</td>
      <td>0.071</td>
      <td>0.070</td>
      <td>0.151</td>
      <td>0.158</td>
      <td>0.080</td>
      <td>0.064</td>
      <td>0.045</td>
      <td>0.016</td>
      <td>0.049</td>
      <td>0.045</td>
      <td>0.021</td>
      <td>0.028</td>
      <td>0.007</td>
      <td>0.004</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0.019</td>
      <td>0.042</td>
      <td>0.031</td>
      <td>0.044</td>
      <td>0.088</td>
      <td>0.015</td>
      <td>0.085</td>
      <td>0.097</td>
      <td>0.121</td>
      <td>0.089</td>
      <td>0.087</td>
      <td>0.064</td>
      <td>0.032</td>
      <td>0.018</td>
      <td>0.053</td>
      <td>0.050</td>
      <td>0.021</td>
      <td>0.032</td>
      <td>0.007</td>
      <td>0.005</td>
    </tr>
    <tr>
      <th>5</th>
      <td>0.029</td>
      <td>0.128</td>
      <td>0.227</td>
      <td>0.444</td>
      <td>0.033</td>
      <td>0.021</td>
      <td>0.026</td>
      <td>0.013</td>
      <td>0.008</td>
      <td>0.007</td>
      <td>0.008</td>
      <td>0.007</td>
      <td>0.007</td>
      <td>0.009</td>
      <td>0.006</td>
      <td>0.005</td>
      <td>0.006</td>
      <td>0.004</td>
      <td>0.010</td>
      <td>0.003</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>198</th>
      <td>0.034</td>
      <td>0.286</td>
      <td>0.079</td>
      <td>0.099</td>
      <td>0.070</td>
      <td>0.034</td>
      <td>0.051</td>
      <td>0.046</td>
      <td>0.046</td>
      <td>0.030</td>
      <td>0.038</td>
      <td>0.039</td>
      <td>0.022</td>
      <td>0.026</td>
      <td>0.025</td>
      <td>0.019</td>
      <td>0.018</td>
      <td>0.017</td>
      <td>0.014</td>
      <td>0.007</td>
    </tr>
    <tr>
      <th>199</th>
      <td>0.028</td>
      <td>0.156</td>
      <td>0.051</td>
      <td>0.067</td>
      <td>0.080</td>
      <td>0.027</td>
      <td>0.066</td>
      <td>0.068</td>
      <td>0.075</td>
      <td>0.059</td>
      <td>0.071</td>
      <td>0.051</td>
      <td>0.029</td>
      <td>0.023</td>
      <td>0.044</td>
      <td>0.036</td>
      <td>0.023</td>
      <td>0.023</td>
      <td>0.015</td>
      <td>0.007</td>
    </tr>
    <tr>
      <th>200</th>
      <td>0.018</td>
      <td>0.042</td>
      <td>0.027</td>
      <td>0.043</td>
      <td>0.077</td>
      <td>0.016</td>
      <td>0.056</td>
      <td>0.106</td>
      <td>0.094</td>
      <td>0.058</td>
      <td>0.103</td>
      <td>0.067</td>
      <td>0.036</td>
      <td>0.017</td>
      <td>0.109</td>
      <td>0.068</td>
      <td>0.023</td>
      <td>0.029</td>
      <td>0.008</td>
      <td>0.005</td>
    </tr>
    <tr>
      <th>201</th>
      <td>0.020</td>
      <td>0.048</td>
      <td>0.037</td>
      <td>0.056</td>
      <td>0.093</td>
      <td>0.018</td>
      <td>0.065</td>
      <td>0.074</td>
      <td>0.081</td>
      <td>0.055</td>
      <td>0.142</td>
      <td>0.056</td>
      <td>0.045</td>
      <td>0.018</td>
      <td>0.057</td>
      <td>0.072</td>
      <td>0.024</td>
      <td>0.025</td>
      <td>0.010</td>
      <td>0.005</td>
    </tr>
    <tr>
      <th>202</th>
      <td>0.025</td>
      <td>0.082</td>
      <td>0.071</td>
      <td>0.094</td>
      <td>0.136</td>
      <td>0.029</td>
      <td>0.066</td>
      <td>0.083</td>
      <td>0.055</td>
      <td>0.043</td>
      <td>0.053</td>
      <td>0.036</td>
      <td>0.052</td>
      <td>0.022</td>
      <td>0.041</td>
      <td>0.043</td>
      <td>0.026</td>
      <td>0.019</td>
      <td>0.017</td>
      <td>0.006</td>
    </tr>
  </tbody>
</table>
<p>202 rows × 20 columns</p>
</div>




```python
plt.figure(figsize=(10,8))
sns.heatmap(expanded_seq_conser_df, cmap='viridis')
```

{{< figure library="true" src="output_30_1.png" title="HeatMap" >}}


```python
sns.clustermap(expanded_seq_conser_df, cmap='viridis', method='ward')
```


{{< figure library="true" src="output_31_1.png" title="ClusterMap" >}}