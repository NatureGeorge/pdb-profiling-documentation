---
# Title, summary, and page position.
linktitle: Tutorials
summary: Learning-Oriented
weight: 2
icon: book-reader
icon_pack: fas

# Page metadata.
title: Tutorials
date: "2020-11-05T00:00:00Z"
type: book  # Do not modify.
---

## 预备知识

这是一篇写给使用者中的初学者的指南，将介绍`pdb-profiling`的基本功能。阅读之前，请先了解以下知识点:

* 什么是`PDB`
* 什么是`UniProt-KB`
* 什么是可变剪切(Alternative Splicing)
* 什么是蛋白质一级结构 (序列)
* 什么是蛋白质三级结构 (晶体结构)
* 什么是蛋白-蛋白相互作用 (Protein-Protein Interaction, PPI)
* 基础Python编程知识
* pip安装Python Package知识
* 熟悉Pandas包的DataFrame相关知识

阅读这部分不需要对Python Asynchronous Programming有任何了解。

## 安装

`pdb-profiling`基于Python3，是一个Python Package，需要您的电脑预先安装了Python3.6及以上版本才可使用。

请在终端中执行以下pip命令以安装`pdb-profiling`:

```bash
pip install pdb-profiling
```

这个过程中会同时安装相关依赖包。

如果您已经安装过先前版本的`pdb-profiling`，请运行以下命令以对`pdb-profiling`进行更新:

```bash
pip install --upgrade pdb-profiling
```

以上步骤即可完成安装。

## 初始化输出文件夹

```python
from pdb_profiling import default_config

default_config(your_output_folder)
```

利用`default_config`函数即可初始化相关设置，若有细节化的设置需求请参见**Section5: Reference**。

`your_output_folder`变量即您设定的输出文件夹/工作目录。若不传入任何参数，默认采用当前目录。

`default_config`运行完后会在工作目录下创建众多子文件夹以及数据库文件，请不要删除它们。

## 调用PDBe RESTful API

以PDB Entry `3hl2`为例:

### 导入所需class/function

```python
from pdb_profiling.processors import PDB
```

### 检索并获取Tabular Format结果

下面以获取<https://www.ebi.ac.uk/pdbe/api/pdb/entry/molecules/3hl2>的信息为例:

```python
pdb_object = PDB('3hl2')

dfrm = pdb_object.fetch_from_web_api('api/pdb/entry/molecules/', PDB.to_dataframe).result()
```

<details>
<summary>Click to view dataframe</summary>
<table class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
      <th>5</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>ca_p_only</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>entity_id</th>
      <td>1</td>
      <td>2</td>
      <td>3</td>
      <td>4</td>
      <td>5</td>
      <td>6</td>
    </tr>
    <tr>
      <th>gene_name</th>
      <td>["SEPSECS","TRNP48"]</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>in_chains</th>
      <td>["A","B","C","D"]</td>
      <td>["E"]</td>
      <td>["A","B","C","D"]</td>
      <td>["A","C"]</td>
      <td>["B","D"]</td>
      <td>["A","B","C","D","E"]</td>
    </tr>
    <tr>
      <th>in_struct_asyms</th>
      <td>["A","B","C","D"]</td>
      <td>["E"]</td>
      <td>["F","I","L","N"]</td>
      <td>["G","H","M"]</td>
      <td>["J","K","O","P"]</td>
      <td>["Q","R","S","T","U"]</td>
    </tr>
    <tr>
      <th>length</th>
      <td>501</td>
      <td>90</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>molecule_name</th>
      <td>["O-phosphoseryl-tRNA(Sec) selenium transferase"]</td>
      <td>["tRNASec"]</td>
      <td>["(5-HYDROXY-4,6-DIMETHYLPYRIDIN-3-YL)METHYL D...</td>
      <td>["Monothiophosphate"]</td>
      <td>["PHOSPHOSERINE"]</td>
      <td>["water"]</td>
    </tr>
    <tr>
      <th>molecule_type</th>
      <td>polypeptide(L)</td>
      <td>polyribonucleotide</td>
      <td>bound</td>
      <td>bound</td>
      <td>bound</td>
      <td>water</td>
    </tr>
    <tr>
      <th>mutation_flag</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>number_of_copies</th>
      <td>4</td>
      <td>1</td>
      <td>4</td>
      <td>3</td>
      <td>4</td>
      <td>288</td>
    </tr>
    <tr>
      <th>pdb_sequence</th>
      <td>MNRESFAAGERLVSPAYVRQGCEARRSHEHLIRLLLEKGKCPENGW...</td>
      <td>GCCCGGAUGAUCCUCAGUGGUCUGGGGUGCAGGCUUCAAACCUGUA...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>pdb_sequence_indices_with_multiple_residues</th>
      <td>{}</td>
      <td>{}</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>sample_preparation</th>
      <td>Genetically manipulated</td>
      <td>Genetically manipulated</td>
      <td>Synthetically obtained</td>
      <td>Synthetically obtained</td>
      <td>Synthetically obtained</td>
      <td>Natural source</td>
    </tr>
    <tr>
      <th>sequence</th>
      <td>MNRESFAAGERLVSPAYVRQGCEARRSHEHLIRLLLEKGKCPENGW...</td>
      <td>GCCCGGAUGAUCCUCAGUGGUCUGGGGUGCAGGCUUCAAACCUGUA...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>source</th>
      <td>[{"expression_host_scientific_name":"Escherich...</td>
      <td>[{"expression_host_scientific_name":"Escherich...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>synonym</th>
      <td>O-phosphoseryl-tRNA(Sec) selenium transferase</td>
      <td>tRNASec</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>weight</th>
      <td>55801.2</td>
      <td>28908.1</td>
      <td>233.158</td>
      <td>114.061</td>
      <td>185.072</td>
      <td>18.015</td>
    </tr>
    <tr>
      <th>pdb_id</th>
      <td>3hl2</td>
      <td>3hl2</td>
      <td>3hl2</td>
      <td>3hl2</td>
      <td>3hl2</td>
      <td>3hl2</td>
    </tr>
  </tbody>
</table>
</details>

也可通过不传入其他参数而直接获取文件路径:

```python
pdb_object.fetch_from_web_api('api/pdb/entry/molecules/').result()
# >>> WindowsPath('./api/pdb/entry/molecules/api%pdb%entry%molecules%+3hl2.tsv')
```

可通过如下代码查看所有可用的api集:

```python
from pdb_profiling.processors.pdbe.record import API_SET
print(API_SET)
```

<details>
<summary>Click to view API_SET</summary>

```python
{"api/mappings/",
 "api/mappings/all_isoforms/",
 "api/mappings/best_structures/",
 "api/mappings/cath/",
 "api/mappings/cath_b/",
 "api/mappings/ec/",
 "api/mappings/ensembl/",
 "api/mappings/go/",
 "api/mappings/hmmer/",
 "api/mappings/homologene/",
 "api/mappings/homologene_uniref90/",
 "api/mappings/interpro/",
 "api/mappings/isoforms/",
 "api/mappings/pfam/",
 "api/mappings/scop/",
 "api/mappings/sequence_domains/",
 "api/mappings/structural_domains/",
 "api/mappings/uniprot/",
 "api/mappings/uniprot_publications/",
 "api/mappings/uniprot_segments/",
 "api/mappings/uniprot_to_pfam/",
 "api/mappings/uniref90/",
 "api/pdb/entry/assembly/",
 "api/pdb/entry/binding_sites/",
 "api/pdb/entry/carbohydrate_polymer/",
 "api/pdb/entry/cofactor/",
 "api/pdb/entry/drugbank/",
 "api/pdb/entry/electron_density_statistics/",
 "api/pdb/entry/experiment/",
 "api/pdb/entry/files/",
 "api/pdb/entry/ligand_monomers/",
 "api/pdb/entry/modified_AA_or_NA/",
 "api/pdb/entry/molecules/",
 "api/pdb/entry/mutated_AA_or_NA/",
 "api/pdb/entry/observed_residues_ratio/",
 "api/pdb/entry/polymer_coverage/",
 "api/pdb/entry/related_experiment_data/",
 "api/pdb/entry/residue_listing/",
 "api/pdb/entry/secondary_structure/",
 "api/pdb/entry/status/",
 "api/pdb/entry/summary/",
 "api/pisa/interfacedetail/",
 "api/pisa/interfacelist/",
 "graph-api/compound/atoms/",
 "graph-api/compound/bonds/",
 "graph-api/compound/cofactors/",
 "graph-api/compound/summary/",
 "graph-api/mappings/",
 "graph-api/mappings/all_isoforms/",
 "graph-api/mappings/best_structures/",
 "graph-api/mappings/ensembl/",
 "graph-api/mappings/homologene/",
 "graph-api/mappings/isoforms/",
 "graph-api/mappings/sequence_domains/",
 "graph-api/mappings/uniprot/",
 "graph-api/mappings/uniprot_segments/",
 "graph-api/pdb/bound_excluding_branched/",
 "graph-api/pdb/bound_molecules/",
 "graph-api/pdb/funpdbe/",
 "graph-api/pdb/funpdbe_annotation/",
 "graph-api/pdb/funpdbe_annotation/14-3-3-pred/",
 "graph-api/pdb/funpdbe_annotation/3Dcomplex/",
 "graph-api/pdb/funpdbe_annotation/3dligandsite/",
 "graph-api/pdb/funpdbe_annotation/ChannelsDB/",
 "graph-api/pdb/funpdbe_annotation/FoldX/",
 "graph-api/pdb/funpdbe_annotation/M-CSA/",
 "graph-api/pdb/funpdbe_annotation/MetalPDB/",
 "graph-api/pdb/funpdbe_annotation/Missense3D/",
 "graph-api/pdb/funpdbe_annotation/POPScomp_PDBML/",
 "graph-api/pdb/funpdbe_annotation/ProKinO/",
 "graph-api/pdb/funpdbe_annotation/akid/",
 "graph-api/pdb/funpdbe_annotation/camkinet/",
 "graph-api/pdb/funpdbe_annotation/canSAR/",
 "graph-api/pdb/funpdbe_annotation/cath-funsites/",
 "graph-api/pdb/funpdbe_annotation/depth/",
 "graph-api/pdb/funpdbe_annotation/dynamine/",
 "graph-api/pdb/funpdbe_annotation/p2rank/",
 "graph-api/pdb/ligand_monomers/",
 "graph-api/pdb/modified_AA_or_NA/",
 "graph-api/pdb/mutated_AA_or_NA/",
 "graph-api/pdb/secondary_structure/",
 "graph-api/pdb/sequence_conservation/",
 "graph-api/residue_mapping/"}
```

</details>

若使用不符要求或暂不支持的API则会抛出异常。

### 批量获取

```python
from pdb_profiling.processors import PDBs

pdb_objects = PDBs(['1a01', '2xyn', '3hl2', '4hho'])
```

这样即得到了一个PDBs集合对象，内含多个PDB对象:

```txt
(<PDB 1a01>, <PDB 2xyn>, <PDB 3hl2>, <PDB 4hho>)
```

直接对该PDBs进行相关函数的调用即可批量获取所有PDB的相关结果:

```python
res = pdb_objects.fetch(
    'fetch_from_web_api', 
    api_suffix='api/pdb/entry/summary/', 
    then_func=PDB.to_dataframe).run().result()
```

返回的res是一个`list`，每个元素都是一个`pandas.DataFrame`，可用`pandas.concat`将多个dataframe整合。

> 注意: 此步骤得到的res中，结果出现次序并不一定按照PDBs中PDB的顺序

```python
from pandas import concat
concat(res, sort=False, ignore_index=True).T
```

<details>
<summary>Click to view dataframe</summary>
<table class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>assemblies</th>
      <td>[{"preferred":true,"form":"hetero","name":"pen...</td>
      <td>[{"assembly_id":"1","form":"Non-polymer only",...</td>
      <td>[{"preferred":true,"form":"homo","name":"monom...</td>
      <td>[{"assembly_id":"1","form":"homo","preferred":...</td>
    </tr>
    <tr>
      <th>deposition_date</th>
      <td>20090526</td>
      <td>19971208</td>
      <td>20101118</td>
      <td>20121010</td>
    </tr>
    <tr>
      <th>deposition_site</th>
      <td>RCSB</td>
      <td>NaN</td>
      <td>PDBE</td>
      <td>RCSB</td>
    </tr>
    <tr>
      <th>entry_authors</th>
      <td>["Palioura, S.","Steitz, T.A.","Soll, D.","Sim...</td>
      <td>["Kavanaugh, J.S.","Arnone, A."]</td>
      <td>["Salah, E.","Ugochukwu, E.","Elkins, J.M.","B...</td>
      <td>["Moshe, B.-D.","Grzegorz, W.","Mikael, E.","I...</td>
    </tr>
    <tr>
      <th>experimental_method</th>
      <td>["X-ray diffraction"]</td>
      <td>["X-ray diffraction"]</td>
      <td>["X-ray diffraction"]</td>
      <td>["X-ray diffraction"]</td>
    </tr>
    <tr>
      <th>experimental_method_class</th>
      <td>["x-ray"]</td>
      <td>["x-ray"]</td>
      <td>["x-ray"]</td>
      <td>["x-ray"]</td>
    </tr>
    <tr>
      <th>number_of_entities</th>
      <td>{"water":1,"polypeptide":1,"other":0,"dna":0,"...</td>
      <td>{"polypeptide":2,"dna":0,"ligand":1,"dna/rna":...</td>
      <td>{"water":1,"polypeptide":1,"other":0,"dna":0,"...</td>
      <td>{"polypeptide":1,"dna":0,"ligand":3,"dna/rna":...</td>
    </tr>
    <tr>
      <th>pdb_id</th>
      <td>3hl2</td>
      <td>1a01</td>
      <td>2xyn</td>
      <td>4hho</td>
    </tr>
    <tr>
      <th>processing_site</th>
      <td>RCSB</td>
      <td>BNL</td>
      <td>PDBE</td>
      <td>RCSB</td>
    </tr>
    <tr>
      <th>related_structures</th>
      <td>[]</td>
      <td>[]</td>
      <td>[]</td>
      <td>[]</td>
    </tr>
    <tr>
      <th>release_date</th>
      <td>20091006</td>
      <td>19980318</td>
      <td>20101201</td>
      <td>20130327</td>
    </tr>
    <tr>
      <th>revision_date</th>
      <td>20180124</td>
      <td>20110713</td>
      <td>20190403</td>
      <td>20130327</td>
    </tr>
    <tr>
      <th>split_entry</th>
      <td>[]</td>
      <td>[]</td>
      <td>[]</td>
      <td>[]</td>
    </tr>
    <tr>
      <th>title</th>
      <td>The crystal structure of the human SepSecS-tRN...</td>
      <td>HEMOGLOBIN (VAL BETA1 MET, TRP BETA37 ALA) MUTANT</td>
      <td>HUMAN ABL2 IN COMPLEX WITH AURORA KINASE INHIB...</td>
      <td>Serum paraoxonase-1 by directed evolution with...</td>
    </tr>
  </tbody>
</table>
</details>

#### 批量获取内置函数

`PDBs`类也内置了几个预先设定好的信息获取流程函数。

获取实验方法相关信息:

```python
from pandas import DataFrame

exp_res = pdb_objects.fetch(PDBs.fetch_exp_pipe).run().result()

DataFrame(
    (j for i in exp_res for j in i),
    columns=['pdb_id',
             'resolution',
             'experimental_method_class',
             'experimental_method',
             'multi_method'])
```

<details>
<summary>Click to view dataframe</summary>
<table class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>pdb_id</th>
      <th>resolution</th>
      <th>experimental_method_class</th>
      <th>experimental_method</th>
      <th>multi_method</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>4hho</td>
      <td>2.10</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1a01</td>
      <td>1.80</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3hl2</td>
      <td>2.81</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2xyn</td>
      <td>2.81</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
    </tr>
  </tbody>
</table>
</details>

获取日期相关信息:

```python
date_res = pdb_objects.fetch(PDBs.fetch_date).run().result()
DataFrame(date_res, columns=['pdb_id', 'revision_date', 'deposition_date'])
```

## 调用SIFTS API

```python
from pdb_profiling.processors import SIFTS, SIFTSs

sifts_from_pdb_demo = SIFTS('1a01')    # <SIFTS PDB Entry 1a01>
sifts_from_unp_demo = SIFTS('Q5VST9')  # <SIFTS UniProt Q5VST9>
```

`SIFTS`类会自动检测输入的identifier的类型，若不符要求则会报错。

### From PDB to UniProt Isoform

下面展示利用`SIFTS API`获取目标PDB对应的所有蛋白链已知的对应UniProt Isoform信息:

```python
sifts_from_pdb_demo.fetch_from_web_api('api/mappings/all_isoforms/', SIFTS.to_dataframe).result()
```

<details>
<summary>Click to view dataframe</summary>
<table class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>UniProt</th>
      <td>P68871</td>
      <td>P68871</td>
      <td>P69905</td>
      <td>P69905</td>
    </tr>
    <tr>
      <th>chain_id</th>
      <td>B</td>
      <td>D</td>
      <td>A</td>
      <td>C</td>
    </tr>
    <tr>
      <th>end</th>
      <td>{"author_residue_number":146,"author_insertion...</td>
      <td>{"author_residue_number":146,"author_insertion...</td>
      <td>{"author_residue_number":141,"author_insertion...</td>
      <td>{"author_residue_number":141,"author_insertion...</td>
    </tr>
    <tr>
      <th>entity_id</th>
      <td>2</td>
      <td>2</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>identifier</th>
      <td>HBB_HUMAN</td>
      <td>HBB_HUMAN</td>
      <td>HBA_HUMAN</td>
      <td>HBA_HUMAN</td>
    </tr>
    <tr>
      <th>identity</th>
      <td>0.99</td>
      <td>0.99</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>is_canonical</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>name</th>
      <td>HBB_HUMAN</td>
      <td>HBB_HUMAN</td>
      <td>HBA_HUMAN</td>
      <td>HBA_HUMAN</td>
    </tr>
    <tr>
      <th>pdb_end</th>
      <td>146</td>
      <td>146</td>
      <td>141</td>
      <td>141</td>
    </tr>
    <tr>
      <th>pdb_id</th>
      <td>1a01</td>
      <td>1a01</td>
      <td>1a01</td>
      <td>1a01</td>
    </tr>
    <tr>
      <th>pdb_start</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>start</th>
      <td>{"author_residue_number":1,"author_insertion_c...</td>
      <td>{"author_residue_number":1,"author_insertion_c...</td>
      <td>{"author_residue_number":1,"author_insertion_c...</td>
      <td>{"author_residue_number":1,"author_insertion_c...</td>
    </tr>
    <tr>
      <th>struct_asym_id</th>
      <td>B</td>
      <td>D</td>
      <td>A</td>
      <td>C</td>
    </tr>
    <tr>
      <th>unp_end</th>
      <td>147</td>
      <td>147</td>
      <td>142</td>
      <td>142</td>
    </tr>
    <tr>
      <th>unp_start</th>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
</details>


### From UniProt Isoform to PDB

利用`SIFTS API`获取目标UniPRot Isoform对应的所有PDB链信息也是同理:

```python
sifts_from_unp_demo.fetch_from_web_api('api/mappings/all_isoforms/', SIFTS.to_dataframe).result()
```

### Reformat & Detect

对于SIFTS中提供的信息，`pdb-profiling`还可进行后续的匹配区域修正和InDel segment、repeated segment、reversed segment以及conflict segment的检测:

```python
SIFTS('P21359-2').fetch_from_web_api('api/mappings/all_isoforms/', SIFTS.to_dataframe
    ).then(SIFTS.reformat
    ).then(SIFTS.dealWithInDel
    ).then(SIFTS.fix_range
    ).then(SIFTS.add_residue_conflict).result()
```

<details>
<summary>Click to view dataframe</summary>
<table class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
      <th>5</th>
      <th>6</th>
      <th>7</th>
      <th>8</th>
      <th>9</th>
      <th>10</th>
      <th>11</th>
      <th>12</th>
      <th>13</th>
      <th>14</th>
      <th>15</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>UniProt</th>
      <td>P21359-2</td>
      <td>P21359-2</td>
      <td>P21359-2</td>
      <td>P21359-2</td>
      <td>P21359-2</td>
      <td>P21359-2</td>
      <td>P21359-2</td>
      <td>P21359-2</td>
      <td>P21359-2</td>
      <td>P21359-2</td>
      <td>P21359-2</td>
      <td>P21359-2</td>
      <td>P21359-2</td>
      <td>P21359-2</td>
      <td>P21359-2</td>
      <td>P21359-2</td>
    </tr>
    <tr>
      <th>chain_id</th>
      <td>A</td>
      <td>A</td>
      <td>B</td>
      <td>A</td>
      <td>B</td>
      <td>A</td>
      <td>B</td>
      <td>A</td>
      <td>A</td>
      <td>B</td>
      <td>B</td>
      <td>D</td>
      <td>B</td>
      <td>D</td>
      <td>B</td>
      <td>B</td>
    </tr>
    <tr>
      <th>entity_id</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
    </tr>
    <tr>
      <th>identity</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>0.99</td>
      <td>0.99</td>
      <td>0.98</td>
      <td>0.98</td>
      <td>0.94</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>is_canonical</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>pdb_id</th>
      <td>1nf1</td>
      <td>2d4q</td>
      <td>2d4q</td>
      <td>2e2x</td>
      <td>2e2x</td>
      <td>3p7z</td>
      <td>3p7z</td>
      <td>3peg</td>
      <td>3pg7</td>
      <td>3pg7</td>
      <td>6ob2</td>
      <td>6ob2</td>
      <td>6ob3</td>
      <td>6ob3</td>
      <td>6v65</td>
      <td>6v6f</td>
    </tr>
    <tr>
      <th>struct_asym_id</th>
      <td>A</td>
      <td>A</td>
      <td>B</td>
      <td>A</td>
      <td>B</td>
      <td>A</td>
      <td>B</td>
      <td>A</td>
      <td>A</td>
      <td>B</td>
      <td>B</td>
      <td>D</td>
      <td>B</td>
      <td>D</td>
      <td>B</td>
      <td>B</td>
    </tr>
    <tr>
      <th>pdb_range</th>
      <td>[[1,333]]</td>
      <td>[[1,257]]</td>
      <td>[[1,257]]</td>
      <td>[[6,277]]</td>
      <td>[[6,277]]</td>
      <td>[[5,276]]</td>
      <td>[[5,276]]</td>
      <td>[[5,172],[174,290]]</td>
      <td>[[1,256]]</td>
      <td>[[1,256]]</td>
      <td>[[2,256]]</td>
      <td>[[2,256]]</td>
      <td>[[2,256]]</td>
      <td>[[2,256]]</td>
      <td>[[2,329]]</td>
      <td>[[2,329]]</td>
    </tr>
    <tr>
      <th>unp_range</th>
      <td>[[1198,1530]]</td>
      <td>[[1560,1816]]</td>
      <td>[[1560,1816]]</td>
      <td>[[1545,1816]]</td>
      <td>[[1545,1816]]</td>
      <td>[[1545,1816]]</td>
      <td>[[1545,1816]]</td>
      <td>[[1545,1712],[1700,1816]]</td>
      <td>[[1560,1816]]</td>
      <td>[[1560,1816]]</td>
      <td>[[1209,1463]]</td>
      <td>[[1209,1463]]</td>
      <td>[[1209,1463]]</td>
      <td>[[1209,1463]]</td>
      <td>[[1203,1530]]</td>
      <td>[[1203,1530]]</td>
    </tr>
    <tr>
      <th>Entry</th>
      <td>P21359</td>
      <td>P21359</td>
      <td>P21359</td>
      <td>P21359</td>
      <td>P21359</td>
      <td>P21359</td>
      <td>P21359</td>
      <td>P21359</td>
      <td>P21359</td>
      <td>P21359</td>
      <td>P21359</td>
      <td>P21359</td>
      <td>P21359</td>
      <td>P21359</td>
      <td>P21359</td>
      <td>P21359</td>
    </tr>
    <tr>
      <th>range_diff</th>
      <td>[0]</td>
      <td>[0]</td>
      <td>[0]</td>
      <td>[0]</td>
      <td>[0]</td>
      <td>[0]</td>
      <td>[0]</td>
      <td>[0, 0]</td>
      <td>[1]</td>
      <td>[1]</td>
      <td>[0]</td>
      <td>[0]</td>
      <td>[0]</td>
      <td>[0]</td>
      <td>[0]</td>
      <td>[0]</td>
    </tr>
    <tr>
      <th>sifts_range_tag</th>
      <td>Safe</td>
      <td>Safe</td>
      <td>Safe</td>
      <td>Safe</td>
      <td>Safe</td>
      <td>Safe</td>
      <td>Safe</td>
      <td>InDel_1</td>
      <td>Deletion</td>
      <td>Deletion</td>
      <td>Safe</td>
      <td>Safe</td>
      <td>Safe</td>
      <td>Safe</td>
      <td>Safe</td>
      <td>Safe</td>
    </tr>
    <tr>
      <th>repeated</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>reversed</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>InDel_sum</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>-12</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>new_pdb_range</th>
      <td>[[1,333]]</td>
      <td>[[1,257]]</td>
      <td>[[1,257]]</td>
      <td>[[6,277]]</td>
      <td>[[6,277]]</td>
      <td>[[5,276]]</td>
      <td>[[5,276]]</td>
      <td>[[5,172],[174,290]]</td>
      <td>((1, 191), (192, 256))</td>
      <td>((1, 191), (192, 256))</td>
      <td>[[2,256]]</td>
      <td>[[2,256]]</td>
      <td>[[2,256]]</td>
      <td>[[2,256]]</td>
      <td>[[2,329]]</td>
      <td>[[2,329]]</td>
    </tr>
    <tr>
      <th>new_unp_range</th>
      <td>[[1198,1530]]</td>
      <td>[[1560,1816]]</td>
      <td>[[1560,1816]]</td>
      <td>[[1545,1816]]</td>
      <td>[[1545,1816]]</td>
      <td>[[1545,1816]]</td>
      <td>[[1545,1816]]</td>
      <td>[[1545,1712],[1700,1816]]</td>
      <td>((1560, 1750), (1752, 1816))</td>
      <td>((1560, 1750), (1752, 1816))</td>
      <td>[[1209,1463]]</td>
      <td>[[1209,1463]]</td>
      <td>[[1209,1463]]</td>
      <td>[[1209,1463]]</td>
      <td>[[1203,1530]]</td>
      <td>[[1203,1530]]</td>
    </tr>
    <tr>
      <th>conflict_pdb_index</th>
      <td>{"216":"R"}</td>
      <td>{}</td>
      <td>{}</td>
      <td>{}</td>
      <td>{}</td>
      <td>{"44":"I"}</td>
      <td>{"44":"I"}</td>
      <td>{}</td>
      <td>{"191":"K"}</td>
      <td>{"191":"K"}</td>
      <td>{}</td>
      <td>{}</td>
      <td>{}</td>
      <td>{}</td>
      <td>{}</td>
      <td>{}</td>
    </tr>
    <tr>
      <th>conflict_pdb_range</th>
      <td>[[216,216]]</td>
      <td>[]</td>
      <td>[]</td>
      <td>[]</td>
      <td>[]</td>
      <td>[[44,44]]</td>
      <td>[[44,44]]</td>
      <td>[]</td>
      <td>[[191,191]]</td>
      <td>[[191,191]]</td>
      <td>[]</td>
      <td>[]</td>
      <td>[]</td>
      <td>[]</td>
      <td>[]</td>
      <td>[]</td>
    </tr>
    <tr>
      <th>conflict_unp_range</th>
      <td>[[1413,1413]]</td>
      <td>[]</td>
      <td>[]</td>
      <td>[]</td>
      <td>[]</td>
      <td>[[1584,1584]]</td>
      <td>[[1584,1584]]</td>
      <td>[]</td>
      <td>[[1750,1750]]</td>
      <td>[[1750,1750]]</td>
      <td>[]</td>
      <td>[]</td>
      <td>[]</td>
      <td>[]</td>
      <td>[]</td>
      <td>[]</td>
    </tr>
    <tr>
      <th>unp_len</th>
      <td>2818</td>
      <td>2818</td>
      <td>2818</td>
      <td>2818</td>
      <td>2818</td>
      <td>2818</td>
      <td>2818</td>
      <td>2818</td>
      <td>2818</td>
      <td>2818</td>
      <td>2818</td>
      <td>2818</td>
      <td>2818</td>
      <td>2818</td>
      <td>2818</td>
      <td>2818</td>
    </tr>
  </tbody>
</table>
</details>


### 批量检索SIFTS

同样，`pdb-profling`也提供了`SIFTSs`类供用户批量检索`SIFTS API`相关数据。

```python
SIFTSs(('P21359', 'Q5VST9', 'P21359-5')).fetch('fetch_from_web_api', api_suffix='api/mappings/all_isoforms/', then_func=SIFTS.to_dataframe).run().result()
```

### 对SIFTS匹配关系进行打分

尽管SIFTS提供了`identity`指标可用来评判UniProt Isoform序列与相应匹配上的PDB Chain的SEQRES序列的一致性，但这一`identity`只能体现局部匹配区域的情况，未能兼顾匹配区域外序列以及倒序匹配等对于蛋白质结构研究的影响。因此`pdb-profiling`并通过整理出6个指标提供了`RAW_BS`这一加权分值来辅助用户评判出UniProt Isoform与PDB Chain的相符度。

```python
sifts_info, score_detail, experimental_info = SIFTS('P21359-3').pipe_score().result()
```

函数返回3个`dataframe`。

## 检索Assembly与Interface相关信息

现在让我们回到`PDB`类来，重点来看看`Entry-Assembly/Model-Chain`这几个层次的数据。

对于一个PDB，其对应的Assembly相关信息可以通过如下方式获取:

```python
pdb_object.profile_id().result().query('molecule_type == "polypeptide(L)"').T
```

<details>
<summary>Click to view dataframe</summary>
<table class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>16</th>
      <th>17</th>
      <th>24</th>
      <th>25</th>
      <th>33</th>
      <th>34</th>
      <th>40</th>
      <th>41</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>pdb_id</th>
      <td>3hl2</td>
      <td>3hl2</td>
      <td>3hl2</td>
      <td>3hl2</td>
      <td>3hl2</td>
      <td>3hl2</td>
      <td>3hl2</td>
      <td>3hl2</td>
      <td>3hl2</td>
      <td>3hl2</td>
      <td>3hl2</td>
      <td>3hl2</td>
    </tr>
    <tr>
      <th>entity_id</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>molecule_type</th>
      <td>polypeptide(L)</td>
      <td>polypeptide(L)</td>
      <td>polypeptide(L)</td>
      <td>polypeptide(L)</td>
      <td>polypeptide(L)</td>
      <td>polypeptide(L)</td>
      <td>polypeptide(L)</td>
      <td>polypeptide(L)</td>
      <td>polypeptide(L)</td>
      <td>polypeptide(L)</td>
      <td>polypeptide(L)</td>
      <td>polypeptide(L)</td>
    </tr>
    <tr>
      <th>chain_id</th>
      <td>A</td>
      <td>C</td>
      <td>B</td>
      <td>D</td>
      <td>A</td>
      <td>B</td>
      <td>A</td>
      <td>B</td>
      <td>C</td>
      <td>D</td>
      <td>C</td>
      <td>D</td>
    </tr>
    <tr>
      <th>struct_asym_id</th>
      <td>A</td>
      <td>C</td>
      <td>B</td>
      <td>D</td>
      <td>A</td>
      <td>B</td>
      <td>A</td>
      <td>B</td>
      <td>C</td>
      <td>D</td>
      <td>C</td>
      <td>D</td>
    </tr>
    <tr>
      <th>assembly_id</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
    </tr>
    <tr>
      <th>model_id</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>2</td>
      <td>2</td>
      <td>1</td>
      <td>1</td>
      <td>2</td>
      <td>2</td>
    </tr>
    <tr>
      <th>asym_id_rank</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>2</td>
      <td>2</td>
      <td>1</td>
      <td>1</td>
      <td>2</td>
      <td>2</td>
    </tr>
    <tr>
      <th>oper_expression</th>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td>["1"]</td>
      <td>["1"]</td>
      <td>["2"]</td>
      <td>["2"]</td>
      <td>["3"]</td>
      <td>["3"]</td>
      <td>["2"]</td>
      <td>["2"]</td>
    </tr>
    <tr>
      <th>symmetry_operation</th>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td>["x,x-y-1,-z"]</td>
      <td>["x,x-y-1,-z"]</td>
      <td>["x,y,z"]</td>
      <td>["x,y,z"]</td>
      <td>["-x+y,y,-z+1/3"]</td>
      <td>["-x+y,y,-z+1/3"]</td>
      <td>["x,y,z"]</td>
      <td>["x,y,z"]</td>
    </tr>
    <tr>
      <th>symmetry_id</th>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td>["6_545"]</td>
      <td>["6_545"]</td>
      <td>["1_555"]</td>
      <td>["1_555"]</td>
      <td>["5_555"]</td>
      <td>["5_555"]</td>
      <td>["1_555"]</td>
      <td>["1_555"]</td>
    </tr>
    <tr>
      <th>struct_asym_id_in_assembly</th>
      <td>A</td>
      <td>C</td>
      <td>B</td>
      <td>D</td>
      <td>A</td>
      <td>B</td>
      <td>AA</td>
      <td>BA</td>
      <td>C</td>
      <td>D</td>
      <td>CA</td>
      <td>DA</td>
    </tr>
    <tr>
      <th>au_subset</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>details</th>
      <td>asymmetric_unit</td>
      <td>asymmetric_unit</td>
      <td>asymmetric_unit</td>
      <td>asymmetric_unit</td>
      <td>author_defined_assembly</td>
      <td>author_defined_assembly</td>
      <td>author_defined_assembly</td>
      <td>author_defined_assembly</td>
      <td>author_defined_assembly</td>
      <td>author_defined_assembly</td>
      <td>author_defined_assembly</td>
      <td>author_defined_assembly</td>
    </tr>
  </tbody>
</table>
</details>

其中`assembly_id`为0指`asymmetric unit`。

### 与PISA资源对接

#### Assembly

`pdb-profiling`依照面对对象编程的思想，也提供了Assembly的相应类`PDBAssemble`，可通过如下方式获取到PDB的相关Biological Assembly:

```python
pdb_object.set_assembly().result()
assemblies = pdb_object.assembly
'''
>>> assemblies  # Note a python dictionary
>>> {0: <PDBAssemble 3hl2/0>, 1: <PDBAssemble 3hl2/1>, 2: <PDBAssemble 3hl2/2>}
'''
```

如若事先知道PDB条目的某一Assembly的编号，也可通过下面的方式获得对应对象:

```python
from pdb_profiling.processors import PDBAssemble

pdb_assembly_object = PDBAssemble('3hl2/1')
pdb_assembly_object.assemble_summary
'''
{'preferred': True, 'form': 'hetero', 'name': 'pentamer', 'assembly_id': '1'}
'''
```

#### Interface

> 整合PDBe PISA API 资源

对于PISA资源中定义的Interface，`pdb-profiling`也提供了Assembly的相应类`PDBInterface`，可通过如下方式获取到PDBAssemble的相关Interface:

```python
pdb_assembly_object = assemblies[1]
pdb_assembly_object.pipe_protein_protein_interface().result()
interfaces = pdb_assembly_object.interface
interfaces
'''
{1: <PDBInterface 3hl2/1/1>,
 2: <PDBInterface 3hl2/1/2>,
 3: <PDBInterface 3hl2/1/3>,
 4: <PDBInterface 3hl2/1/4>,
 13: <PDBInterface 3hl2/1/13>,
 14: <PDBInterface 3hl2/1/14>}
'''
```

如若事先知道PDB Assembly下某一Interface的编号，也可通过下面的方式获得对应对象:

```python
from pdb_profiling.processors import PDBInterface

pdb_interface_object = PDBInterface('3hl2/1/3')
pdb_interface_object.get_interface_res_dict().result()
'''
{'entity_id_1': 1,
 'chain_id_1': 'A',
 'struct_asym_id_1': 'A',
 'struct_asym_id_in_assembly_1': 'AA',
 'asym_id_rank_1': 2,
 'model_id_1': 2,
 'molecule_type_1': 'polypeptide(L)',
 'surface_range_1': '[[23,61],[63,109],[111,120],[123,124],[127,130],[132,139],[141,146],[148,151],[153,164],[168,178],[180,204],[206,208],[210,216],[223,223],[225,227],[230,234],[236,237],[240,241],[243,246],[248,248],[252,252],[254,255],[257,262],[264,265],[267,268],[270,276],[281,284],[286,292],[298,302],[304,305],[307,321],[324,325],[328,329],[331,373],[375,390],[392,424],[426,437],[439,456],[458,463]]',
 'interface_range_1': '[[23,25],[27,28],[31,31],[47,50],[52,53],[56,57],[60,61],[65,68],[82,82],[86,86],[89,90],[109,109]]',
 'entity_id_2': 1,
 'chain_id_2': 'B',
 'struct_asym_id_2': 'B',
 'struct_asym_id_in_assembly_2': 'B',
 'asym_id_rank_2': 1,
 'model_id_2': 1,
 'molecule_type_2': 'polypeptide(L)',
 'surface_range_2': '[[21,61],[63,109],[111,121],[123,125],[127,130],[132,139],[141,146],[149,150],[153,164],[167,178],[180,204],[206,208],[210,216],[223,223],[225,227],[230,234],[236,237],[240,241],[243,246],[248,248],[252,252],[254,255],[257,262],[264,265],[267,268],[270,276],[280,284],[286,292],[294,294],[298,302],[304,305],[307,326],[328,329],[331,424],[426,437],[439,446],[448,453],[455,456],[458,463]]',
 'interface_range_2': '[[21,22],[24,25],[27,28],[31,31],[47,50],[52,53],[56,57],[60,61],[65,68],[82,82],[86,86],[90,90]]',
 'pdb_id': '3hl2',
 'assembly_id': 1,
 'interface_id': 3,
 'use_au': False}
'''
```

### 与Interactome3D资源对接

首先是准备`Interactome3D`全物种完整interaction数据集，`pdb-profiling`目前仅取其中的PDB实验晶体结构相关相互作用信息:

```python
from pdb_profiling.processors.i3d.api import Interactome3D

Interactome3D.pipe_init_interaction_meta().result()
```

> 注意，上面这两行代码一旦运行过就再也不用运行，就算是重新开启python进程也是；因为上述代码是下载文件与准备数据库步骤

准备好数据后即可访问相关相互作用信息:

```python
SIFTS.search_partner_from_i3d('P21359', ('ho','he')).result()
```

<details>
<summary>Click to view dataframe</summary>
<table class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>pdb_id</th>
      <th>Entry_1</th>
      <th>Entry_2</th>
      <th>assembly_id</th>
      <th>model_id_1</th>
      <th>chain_id_1</th>
      <th>model_id_2</th>
      <th>chain_id_2</th>
      <th>organism</th>
      <th>interaction_type</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>6ob3</td>
      <td>P01116</td>
      <td>P21359</td>
      <td>1</td>
      <td>1</td>
      <td>A</td>
      <td>1</td>
      <td>B</td>
      <td>human</td>
      <td>he</td>
    </tr>
    <tr>
      <th>1</th>
      <td>6ob3</td>
      <td>P01116</td>
      <td>P21359</td>
      <td>2</td>
      <td>1</td>
      <td>C</td>
      <td>1</td>
      <td>D</td>
      <td>human</td>
      <td>he</td>
    </tr>
    <tr>
      <th>2</th>
      <td>6ob2</td>
      <td>P01116</td>
      <td>P21359</td>
      <td>1</td>
      <td>1</td>
      <td>A</td>
      <td>1</td>
      <td>B</td>
      <td>human</td>
      <td>he</td>
    </tr>
    <tr>
      <th>3</th>
      <td>6ob2</td>
      <td>P01116</td>
      <td>P21359</td>
      <td>2</td>
      <td>1</td>
      <td>C</td>
      <td>1</td>
      <td>D</td>
      <td>human</td>
      <td>he</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2d4q</td>
      <td>P21359</td>
      <td>P21359</td>
      <td>1</td>
      <td>1</td>
      <td>B</td>
      <td>1</td>
      <td>A</td>
      <td>human</td>
      <td>ho</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2e2x</td>
      <td>P21359</td>
      <td>P21359</td>
      <td>1</td>
      <td>1</td>
      <td>B</td>
      <td>1</td>
      <td>A</td>
      <td>human</td>
      <td>ho</td>
    </tr>
    <tr>
      <th>6</th>
      <td>3peg</td>
      <td>P21359</td>
      <td>P21359</td>
      <td>2</td>
      <td>1</td>
      <td>A</td>
      <td>2</td>
      <td>A</td>
      <td>human</td>
      <td>ho</td>
    </tr>
    <tr>
      <th>7</th>
      <td>3p7z</td>
      <td>P21359</td>
      <td>P21359</td>
      <td>1</td>
      <td>1</td>
      <td>B</td>
      <td>1</td>
      <td>A</td>
      <td>human</td>
      <td>ho</td>
    </tr>
  </tbody>
</table>
</details>

## 单体代表集结构选择

```python
sifts_demo = SIFTS('P21359-2')
df1 = sifts_demo.pipe_select_mo().result()
df1
```

<details>
<summary>Click to view dataframe</summary>
<table class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
      <th>5</th>
      <th>6</th>
      <th>7</th>
      <th>8</th>
      <th>9</th>
      <th>10</th>
      <th>11</th>
      <th>12</th>
      <th>13</th>
      <th>14</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>UniProt</th>
      <td>P21359-2</td>
      <td>P21359-2</td>
      <td>P21359-2</td>
      <td>P21359-2</td>
      <td>P21359-2</td>
      <td>P21359-2</td>
      <td>P21359-2</td>
      <td>P21359-2</td>
      <td>P21359-2</td>
      <td>P21359-2</td>
      <td>P21359-2</td>
      <td>P21359-2</td>
      <td>P21359-2</td>
      <td>P21359-2</td>
      <td>P21359-2</td>
    </tr>
    <tr>
      <th>chain_id</th>
      <td>A</td>
      <td>A</td>
      <td>B</td>
      <td>A</td>
      <td>B</td>
      <td>A</td>
      <td>B</td>
      <td>A</td>
      <td>B</td>
      <td>B</td>
      <td>D</td>
      <td>B</td>
      <td>D</td>
      <td>B</td>
      <td>B</td>
    </tr>
    <tr>
      <th>entity_id</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
    </tr>
    <tr>
      <th>identity</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>0.99</td>
      <td>0.99</td>
      <td>0.98</td>
      <td>0.98</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>is_canonical</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>pdb_id</th>
      <td>1nf1</td>
      <td>2d4q</td>
      <td>2d4q</td>
      <td>2e2x</td>
      <td>2e2x</td>
      <td>3p7z</td>
      <td>3p7z</td>
      <td>3pg7</td>
      <td>3pg7</td>
      <td>6ob2</td>
      <td>6ob2</td>
      <td>6ob3</td>
      <td>6ob3</td>
      <td>6v65</td>
      <td>6v6f</td>
    </tr>
    <tr>
      <th>struct_asym_id</th>
      <td>A</td>
      <td>A</td>
      <td>B</td>
      <td>A</td>
      <td>B</td>
      <td>A</td>
      <td>B</td>
      <td>A</td>
      <td>B</td>
      <td>B</td>
      <td>D</td>
      <td>B</td>
      <td>D</td>
      <td>B</td>
      <td>B</td>
    </tr>
    <tr>
      <th>pdb_range</th>
      <td>[[1,333]]</td>
      <td>[[1,257]]</td>
      <td>[[1,257]]</td>
      <td>[[6,277]]</td>
      <td>[[6,277]]</td>
      <td>[[5,276]]</td>
      <td>[[5,276]]</td>
      <td>[[1,256]]</td>
      <td>[[1,256]]</td>
      <td>[[2,256]]</td>
      <td>[[2,256]]</td>
      <td>[[2,256]]</td>
      <td>[[2,256]]</td>
      <td>[[2,329]]</td>
      <td>[[2,329]]</td>
    </tr>
    <tr>
      <th>unp_range</th>
      <td>[[1198,1530]]</td>
      <td>[[1560,1816]]</td>
      <td>[[1560,1816]]</td>
      <td>[[1545,1816]]</td>
      <td>[[1545,1816]]</td>
      <td>[[1545,1816]]</td>
      <td>[[1545,1816]]</td>
      <td>[[1560,1816]]</td>
      <td>[[1560,1816]]</td>
      <td>[[1209,1463]]</td>
      <td>[[1209,1463]]</td>
      <td>[[1209,1463]]</td>
      <td>[[1209,1463]]</td>
      <td>[[1203,1530]]</td>
      <td>[[1203,1530]]</td>
    </tr>
    <tr>
      <th>Entry</th>
      <td>P21359</td>
      <td>P21359</td>
      <td>P21359</td>
      <td>P21359</td>
      <td>P21359</td>
      <td>P21359</td>
      <td>P21359</td>
      <td>P21359</td>
      <td>P21359</td>
      <td>P21359</td>
      <td>P21359</td>
      <td>P21359</td>
      <td>P21359</td>
      <td>P21359</td>
      <td>P21359</td>
    </tr>
    <tr>
      <th>range_diff</th>
      <td>[0]</td>
      <td>[0]</td>
      <td>[0]</td>
      <td>[0]</td>
      <td>[0]</td>
      <td>[0]</td>
      <td>[0]</td>
      <td>[1]</td>
      <td>[1]</td>
      <td>[0]</td>
      <td>[0]</td>
      <td>[0]</td>
      <td>[0]</td>
      <td>[0]</td>
      <td>[0]</td>
    </tr>
    <tr>
      <th>sifts_range_tag</th>
      <td>Safe</td>
      <td>Safe</td>
      <td>Safe</td>
      <td>Safe</td>
      <td>Safe</td>
      <td>Safe</td>
      <td>Safe</td>
      <td>Deletion</td>
      <td>Deletion</td>
      <td>Safe</td>
      <td>Safe</td>
      <td>Safe</td>
      <td>Safe</td>
      <td>Safe</td>
      <td>Safe</td>
    </tr>
    <tr>
      <th>repeated</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>reversed</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>InDel_sum</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>new_pdb_range</th>
      <td>[[1,333]]</td>
      <td>[[1,257]]</td>
      <td>[[1,257]]</td>
      <td>[[6,277]]</td>
      <td>[[6,277]]</td>
      <td>[[5,276]]</td>
      <td>[[5,276]]</td>
      <td>((1, 191), (192, 256))</td>
      <td>((1, 191), (192, 256))</td>
      <td>[[2,256]]</td>
      <td>[[2,256]]</td>
      <td>[[2,256]]</td>
      <td>[[2,256]]</td>
      <td>[[2,329]]</td>
      <td>[[2,329]]</td>
    </tr>
    <tr>
      <th>new_unp_range</th>
      <td>[[1198,1530]]</td>
      <td>[[1560,1816]]</td>
      <td>[[1560,1816]]</td>
      <td>[[1545,1816]]</td>
      <td>[[1545,1816]]</td>
      <td>[[1545,1816]]</td>
      <td>[[1545,1816]]</td>
      <td>((1560, 1750), (1752, 1816))</td>
      <td>((1560, 1750), (1752, 1816))</td>
      <td>[[1209,1463]]</td>
      <td>[[1209,1463]]</td>
      <td>[[1209,1463]]</td>
      <td>[[1209,1463]]</td>
      <td>[[1203,1530]]</td>
      <td>[[1203,1530]]</td>
    </tr>
    <tr>
      <th>conflict_pdb_index</th>
      <td>{"216":"R"}</td>
      <td>{}</td>
      <td>{}</td>
      <td>{}</td>
      <td>{}</td>
      <td>{"44":"I"}</td>
      <td>{"44":"I"}</td>
      <td>{"191":"K"}</td>
      <td>{"191":"K"}</td>
      <td>{}</td>
      <td>{}</td>
      <td>{}</td>
      <td>{}</td>
      <td>{}</td>
      <td>{}</td>
    </tr>
    <tr>
      <th>conflict_pdb_range</th>
      <td>[[216,216]]</td>
      <td>[]</td>
      <td>[]</td>
      <td>[]</td>
      <td>[]</td>
      <td>[[44,44]]</td>
      <td>[[44,44]]</td>
      <td>[[191,191]]</td>
      <td>[[191,191]]</td>
      <td>[]</td>
      <td>[]</td>
      <td>[]</td>
      <td>[]</td>
      <td>[]</td>
      <td>[]</td>
    </tr>
    <tr>
      <th>conflict_unp_range</th>
      <td>[[1413,1413]]</td>
      <td>[]</td>
      <td>[]</td>
      <td>[]</td>
      <td>[]</td>
      <td>[[1584,1584]]</td>
      <td>[[1584,1584]]</td>
      <td>[[1750,1750]]</td>
      <td>[[1750,1750]]</td>
      <td>[]</td>
      <td>[]</td>
      <td>[]</td>
      <td>[]</td>
      <td>[]</td>
      <td>[]</td>
    </tr>
    <tr>
      <th>unp_len</th>
      <td>2818</td>
      <td>2818</td>
      <td>2818</td>
      <td>2818</td>
      <td>2818</td>
      <td>2818</td>
      <td>2818</td>
      <td>2818</td>
      <td>2818</td>
      <td>2818</td>
      <td>2818</td>
      <td>2818</td>
      <td>2818</td>
      <td>2818</td>
      <td>2818</td>
    </tr>
    <tr>
      <th>BINDING_LIGAND_COUNT</th>
      <td>0</td>
      <td>12</td>
      <td>11</td>
      <td>0</td>
      <td>0</td>
      <td>23</td>
      <td>16</td>
      <td>15</td>
      <td>17</td>
      <td>8</td>
      <td>0</td>
      <td>10</td>
      <td>7</td>
      <td>2</td>
      <td>1</td>
    </tr>
    <tr>
      <th>BINDING_LIGAND_INDEX</th>
      <td>[]</td>
      <td>[[61, 61], [73, 76], [82, 82], [86, 86], [107,...</td>
      <td>[[28, 28], [63, 63], [73, 76], [107, 107], [10...</td>
      <td>[]</td>
      <td>[]</td>
      <td>[[40, 42], [47, 47], [66, 66], [70, 70], [78, ...</td>
      <td>[[80, 80], [92, 95], [101, 102], [110, 110], [...</td>
      <td>[[13, 13], [28, 28], [61, 61], [73, 73], [75, ...</td>
      <td>[[61, 61], [73, 74], [76, 76], [82, 83], [91, ...</td>
      <td>[[18, 19], [22, 22], [191, 192], [202, 202], [...</td>
      <td>[]</td>
      <td>[[41, 41], [51, 51], [69, 69], [129, 130], [13...</td>
      <td>[[41, 41], [44, 44], [126, 126], [133, 133], [...</td>
      <td>[[240, 240], [243, 243]]</td>
      <td>[[218, 218]]</td>
    </tr>
    <tr>
      <th>OBS_COUNT</th>
      <td>260</td>
      <td>257</td>
      <td>255</td>
      <td>250</td>
      <td>250</td>
      <td>270</td>
      <td>270</td>
      <td>256</td>
      <td>256</td>
      <td>241</td>
      <td>245</td>
      <td>245</td>
      <td>247</td>
      <td>300</td>
      <td>301</td>
    </tr>
    <tr>
      <th>OBS_INDEX</th>
      <td>[[9, 107], [134, 206], [215, 266], [288, 306],...</td>
      <td>[[1, 257]]</td>
      <td>[[1, 120], [123, 257]]</td>
      <td>[[28, 277]]</td>
      <td>[[28, 277]]</td>
      <td>[[7, 276]]</td>
      <td>[[7, 276]]</td>
      <td>[[1, 256]]</td>
      <td>[[1, 256]]</td>
      <td>[[12, 103], [107, 255]]</td>
      <td>[[12, 256]]</td>
      <td>[[12, 256]]</td>
      <td>[[10, 256]]</td>
      <td>[[4, 263], [277, 300], [312, 327]]</td>
      <td>[[4, 263], [276, 300], [312, 327]]</td>
    </tr>
    <tr>
      <th>OBS_RATIO_SUM</th>
      <td>243.807</td>
      <td>257</td>
      <td>254.009</td>
      <td>248.894</td>
      <td>249.18</td>
      <td>267.845</td>
      <td>269.18</td>
      <td>247.929</td>
      <td>249.123</td>
      <td>236.933</td>
      <td>239.938</td>
      <td>241.495</td>
      <td>244.327</td>
      <td>293.261</td>
      <td>294.205</td>
    </tr>
    <tr>
      <th>ARTIFACT_INDEX</th>
      <td>[]</td>
      <td>[]</td>
      <td>[]</td>
      <td>[[1, 5]]</td>
      <td>[[1, 5]]</td>
      <td>[[1, 4]]</td>
      <td>[[1, 4]]</td>
      <td>[]</td>
      <td>[]</td>
      <td>[[1, 1]]</td>
      <td>[[1, 1]]</td>
      <td>[[1, 1]]</td>
      <td>[[1, 1]]</td>
      <td>[[1, 1]]</td>
      <td>[[1, 1]]</td>
    </tr>
    <tr>
      <th>NON_COUNT</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>NON_INDEX</th>
      <td>[]</td>
      <td>[]</td>
      <td>[]</td>
      <td>[]</td>
      <td>[]</td>
      <td>[]</td>
      <td>[]</td>
      <td>[]</td>
      <td>[]</td>
      <td>[]</td>
      <td>[]</td>
      <td>[]</td>
      <td>[]</td>
      <td>[]</td>
      <td>[]</td>
    </tr>
    <tr>
      <th>SEQRES_COUNT</th>
      <td>333</td>
      <td>257</td>
      <td>257</td>
      <td>277</td>
      <td>277</td>
      <td>276</td>
      <td>276</td>
      <td>256</td>
      <td>256</td>
      <td>256</td>
      <td>256</td>
      <td>256</td>
      <td>256</td>
      <td>329</td>
      <td>329</td>
    </tr>
    <tr>
      <th>STD_COUNT</th>
      <td>333</td>
      <td>257</td>
      <td>257</td>
      <td>277</td>
      <td>277</td>
      <td>276</td>
      <td>276</td>
      <td>256</td>
      <td>256</td>
      <td>256</td>
      <td>256</td>
      <td>256</td>
      <td>256</td>
      <td>329</td>
      <td>329</td>
    </tr>
    <tr>
      <th>STD_INDEX</th>
      <td>[[1, 333]]</td>
      <td>[[1, 257]]</td>
      <td>[[1, 257]]</td>
      <td>[[1, 277]]</td>
      <td>[[1, 277]]</td>
      <td>[[1, 276]]</td>
      <td>[[1, 276]]</td>
      <td>[[1, 256]]</td>
      <td>[[1, 256]]</td>
      <td>[[1, 256]]</td>
      <td>[[1, 256]]</td>
      <td>[[1, 256]]</td>
      <td>[[1, 256]]</td>
      <td>[[1, 329]]</td>
      <td>[[1, 329]]</td>
    </tr>
    <tr>
      <th>UNK_COUNT</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>UNK_INDEX</th>
      <td>[]</td>
      <td>[]</td>
      <td>[]</td>
      <td>[]</td>
      <td>[]</td>
      <td>[]</td>
      <td>[]</td>
      <td>[]</td>
      <td>[]</td>
      <td>[]</td>
      <td>[]</td>
      <td>[]</td>
      <td>[]</td>
      <td>[]</td>
      <td>[]</td>
    </tr>
    <tr>
      <th>ca_p_only</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>molecule_type</th>
      <td>polypeptide(L)</td>
      <td>polypeptide(L)</td>
      <td>polypeptide(L)</td>
      <td>polypeptide(L)</td>
      <td>polypeptide(L)</td>
      <td>polypeptide(L)</td>
      <td>polypeptide(L)</td>
      <td>polypeptide(L)</td>
      <td>polypeptide(L)</td>
      <td>polypeptide(L)</td>
      <td>polypeptide(L)</td>
      <td>polypeptide(L)</td>
      <td>polypeptide(L)</td>
      <td>polypeptide(L)</td>
      <td>polypeptide(L)</td>
    </tr>
    <tr>
      <th>OBS_STD_INDEX</th>
      <td>((9, 107), (134, 206), (215, 266), (288, 306),...</td>
      <td>((1, 257),)</td>
      <td>((1, 120), (123, 257))</td>
      <td>((28, 277),)</td>
      <td>((28, 277),)</td>
      <td>((7, 276),)</td>
      <td>((7, 276),)</td>
      <td>((1, 256),)</td>
      <td>((1, 256),)</td>
      <td>((12, 103), (107, 255))</td>
      <td>((12, 256),)</td>
      <td>((12, 256),)</td>
      <td>((10, 256),)</td>
      <td>((4, 263), (277, 300), (312, 327))</td>
      <td>((4, 263), (276, 300), (312, 327))</td>
    </tr>
    <tr>
      <th>OBS_STD_COUNT</th>
      <td>260</td>
      <td>257</td>
      <td>255</td>
      <td>250</td>
      <td>250</td>
      <td>270</td>
      <td>270</td>
      <td>256</td>
      <td>256</td>
      <td>241</td>
      <td>245</td>
      <td>245</td>
      <td>247</td>
      <td>300</td>
      <td>301</td>
    </tr>
    <tr>
      <th>RAW_BS</th>
      <td>0.0458754</td>
      <td>0.0869411</td>
      <td>0.0853153</td>
      <td>0.0747353</td>
      <td>0.0747353</td>
      <td>0.0863799</td>
      <td>0.0888639</td>
      <td>0.0838811</td>
      <td>0.0831713</td>
      <td>0.0737863</td>
      <td>0.0805865</td>
      <td>0.0770379</td>
      <td>0.0800831</td>
      <td>0.0879559</td>
      <td>0.0893011</td>
    </tr>
    <tr>
      <th>RAW_BS_IG3</th>
      <td>0.0458754</td>
      <td>0.0911994</td>
      <td>0.0892188</td>
      <td>0.0747353</td>
      <td>0.0747353</td>
      <td>0.0945417</td>
      <td>0.0945417</td>
      <td>0.089204</td>
      <td>0.089204</td>
      <td>0.0766252</td>
      <td>0.0805865</td>
      <td>0.0805865</td>
      <td>0.0825671</td>
      <td>0.0886656</td>
      <td>0.0896559</td>
    </tr>
    <tr>
      <th>resolution</th>
      <td>2.5</td>
      <td>2.3</td>
      <td>2.3</td>
      <td>2.5</td>
      <td>2.5</td>
      <td>2.65</td>
      <td>2.65</td>
      <td>2.189</td>
      <td>2.189</td>
      <td>2.845</td>
      <td>2.845</td>
      <td>2.1</td>
      <td>2.1</td>
      <td>2.763</td>
      <td>2.542</td>
    </tr>
    <tr>
      <th>experimental_method_class</th>
      <td>x-ray</td>
      <td>x-ray</td>
      <td>x-ray</td>
      <td>x-ray</td>
      <td>x-ray</td>
      <td>x-ray</td>
      <td>x-ray</td>
      <td>x-ray</td>
      <td>x-ray</td>
      <td>x-ray</td>
      <td>x-ray</td>
      <td>x-ray</td>
      <td>x-ray</td>
      <td>x-ray</td>
      <td>x-ray</td>
    </tr>
    <tr>
      <th>experimental_method</th>
      <td>X-ray diffraction</td>
      <td>X-ray diffraction</td>
      <td>X-ray diffraction</td>
      <td>X-ray diffraction</td>
      <td>X-ray diffraction</td>
      <td>X-ray diffraction</td>
      <td>X-ray diffraction</td>
      <td>X-ray diffraction</td>
      <td>X-ray diffraction</td>
      <td>X-ray diffraction</td>
      <td>X-ray diffraction</td>
      <td>X-ray diffraction</td>
      <td>X-ray diffraction</td>
      <td>X-ray diffraction</td>
      <td>X-ray diffraction</td>
    </tr>
    <tr>
      <th>multi_method</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>revision_date</th>
      <td>20171004</td>
      <td>20110713</td>
      <td>20110713</td>
      <td>20110713</td>
      <td>20110713</td>
      <td>20190717</td>
      <td>20190717</td>
      <td>20110713</td>
      <td>20110713</td>
      <td>20191113</td>
      <td>20191113</td>
      <td>20191113</td>
      <td>20191113</td>
      <td>20200805</td>
      <td>20200805</td>
    </tr>
    <tr>
      <th>deposition_date</th>
      <td>19980708</td>
      <td>20051022</td>
      <td>20051022</td>
      <td>20061118</td>
      <td>20061118</td>
      <td>20101013</td>
      <td>20101013</td>
      <td>20101031</td>
      <td>20101031</td>
      <td>20190319</td>
      <td>20190319</td>
      <td>20190319</td>
      <td>20190319</td>
      <td>20191204</td>
      <td>20191205</td>
    </tr>
    <tr>
      <th>1/resolution</th>
      <td>0.4</td>
      <td>0.434783</td>
      <td>0.434783</td>
      <td>0.4</td>
      <td>0.4</td>
      <td>0.377358</td>
      <td>0.377358</td>
      <td>0.45683</td>
      <td>0.45683</td>
      <td>0.351494</td>
      <td>0.351494</td>
      <td>0.47619</td>
      <td>0.47619</td>
      <td>0.361925</td>
      <td>0.393391</td>
    </tr>
    <tr>
      <th>id_score</th>
      <td>-65</td>
      <td>-65</td>
      <td>-66</td>
      <td>-65</td>
      <td>-66</td>
      <td>-65</td>
      <td>-66</td>
      <td>-65</td>
      <td>-66</td>
      <td>-66</td>
      <td>-68</td>
      <td>-66</td>
      <td>-68</td>
      <td>-66</td>
      <td>-66</td>
    </tr>
    <tr>
      <th>select_tag</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>select_rank</th>
      <td>15</td>
      <td>4</td>
      <td>6</td>
      <td>12</td>
      <td>13</td>
      <td>5</td>
      <td>2</td>
      <td>7</td>
      <td>8</td>
      <td>14</td>
      <td>9</td>
      <td>11</td>
      <td>10</td>
      <td>3</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</details>

这个过程自动完成了上面提及的reformat及打分等步骤。

## 同聚体代表集结构选择

```python
df2 = sifts_demo.pipe_select_ho(run_as_completed=True).result()
df2
```

<details>
<summary>Click to view dataframe</summary>
<table class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
      <th>5</th>
      <th>6</th>
      <th>7</th>
      <th>8</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>entity_id_1</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>2</td>
      <td>2</td>
    </tr>
    <tr>
      <th>chain_id_1</th>
      <td>A</td>
      <td>A</td>
      <td>A</td>
      <td>A</td>
      <td>A</td>
      <td>A</td>
      <td>A</td>
      <td>B</td>
      <td>B</td>
    </tr>
    <tr>
      <th>struct_asym_id_1</th>
      <td>A</td>
      <td>A</td>
      <td>A</td>
      <td>A</td>
      <td>A</td>
      <td>A</td>
      <td>A</td>
      <td>B</td>
      <td>B</td>
    </tr>
    <tr>
      <th>struct_asym_id_in_assembly_1</th>
      <td>A</td>
      <td>A</td>
      <td>A</td>
      <td>A</td>
      <td>A</td>
      <td>A</td>
      <td>A</td>
      <td>B</td>
      <td>B</td>
    </tr>
    <tr>
      <th>asym_id_rank_1</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
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
    </tr>
    <tr>
      <th>unp_interface_range_1</th>
      <td>((1590, 1591), (1593, 1593), (1626, 1626), (16...</td>
      <td>((1590, 1591), (1593, 1593), (1626, 1626), (16...</td>
      <td>((1590, 1591), (1593, 1593), (1626, 1626), (16...</td>
      <td>((1590, 1591), (1593, 1593), (1626, 1626), (16...</td>
      <td>((1590, 1591), (1593, 1593), (1626, 1626), (16...</td>
      <td>((1590, 1591), (1593, 1593), (1626, 1626), (16...</td>
      <td>((1590, 1591), (1593, 1593), (1626, 1626), (16...</td>
      <td>((1332, 1332), (1438, 1438), (1441, 1442), (14...</td>
      <td>((1435, 1435), (1438, 1439), (1441, 1442), (14...</td>
    </tr>
    <tr>
      <th>unp_interface_range_2</th>
      <td>((1569, 1569), (1590, 1591), (1593, 1593), (16...</td>
      <td>((1569, 1569), (1590, 1591), (1593, 1593), (16...</td>
      <td>((1590, 1591), (1593, 1593), (1626, 1626), (16...</td>
      <td>((1590, 1591), (1593, 1593), (1626, 1626), (16...</td>
      <td>((1590, 1591), (1593, 1593), (1626, 1626), (16...</td>
      <td>((1590, 1591), (1593, 1593), (1626, 1626), (16...</td>
      <td>((1590, 1591), (1593, 1593), (1626, 1626), (16...</td>
      <td>((1306, 1306), (1401, 1401), (1404, 1404), (14...</td>
      <td>((1298, 1298), (1302, 1302), (1306, 1306), (14...</td>
    </tr>
    <tr>
      <th>i_group</th>
      <td>(P21359-2, P21359-2)</td>
      <td>(P21359-2, P21359-2)</td>
      <td>(P21359-2, P21359-2)</td>
      <td>(P21359-2, P21359-2)</td>
      <td>(P21359-2, P21359-2)</td>
      <td>(P21359-2, P21359-2)</td>
      <td>(P21359-2, P21359-2)</td>
      <td>(P21359-2, P21359-2)</td>
      <td>(P21359-2, P21359-2)</td>
    </tr>
    <tr>
      <th>i_select_tag</th>
      <td>False</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
      <td>False</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>i_select_rank</th>
      <td>4</td>
      <td>3</td>
      <td>9</td>
      <td>8</td>
      <td>2</td>
      <td>1</td>
      <td>5</td>
      <td>6</td>
      <td>7</td>
    </tr>
  </tbody>
</table>
</details>

这个过程自动完成了上面提及的reformat、打分及与PISA、Interactome3D数据资源整合等步骤，下面的`pipe_select_ho_iso,pipe_select_he`同理。

## 同聚体(isofrom)代表集结构选择

```python
df3 = sifts_demo.pipe_select_ho_iso(run_as_completed=True).result()
df3.sample(10)
```

<details>
<summary>Click to view dataframe</summary>
<table class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>43</th>
      <th>42</th>
      <th>21</th>
      <th>4</th>
      <th>13</th>
      <th>45</th>
      <th>37</th>
      <th>38</th>
      <th>44</th>
      <th>30</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>entity_id_1</th>
      <td>2</td>
      <td>2</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>1</td>
    </tr>
    <tr>
      <th>chain_id_1</th>
      <td>B</td>
      <td>B</td>
      <td>A</td>
      <td>B</td>
      <td>A</td>
      <td>D</td>
      <td>B</td>
      <td>D</td>
      <td>D</td>
      <td>A</td>
    </tr>
    <tr>
      <th>struct_asym_id_1</th>
      <td>B</td>
      <td>B</td>
      <td>A</td>
      <td>B</td>
      <td>A</td>
      <td>D</td>
      <td>B</td>
      <td>D</td>
      <td>D</td>
      <td>A</td>
    </tr>
    <tr>
      <th>struct_asym_id_in_assembly_1</th>
      <td>B</td>
      <td>B</td>
      <td>A</td>
      <td>B</td>
      <td>A</td>
      <td>D</td>
      <td>B</td>
      <td>D</td>
      <td>D</td>
      <td>A</td>
    </tr>
    <tr>
      <th>asym_id_rank_1</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
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
    </tr>
    <tr>
      <th>unp_interface_range_1</th>
      <td>((1435, 1435), (1438, 1439), (1441, 1442), (14...</td>
      <td>((1435, 1435), (1438, 1439), (1441, 1442), (14...</td>
      <td>((1590, 1591), (1593, 1593), (1626, 1626), (16...</td>
      <td>((1569, 1569), (1590, 1591), (1593, 1593), (16...</td>
      <td>((1590, 1591), (1593, 1593), (1626, 1626), (16...</td>
      <td>((1298, 1298), (1302, 1302), (1306, 1306), (14...</td>
      <td>((1332, 1332), (1438, 1438), (1441, 1442), (14...</td>
      <td>((1306, 1306), (1401, 1401), (1404, 1404), (14...</td>
      <td>((1298, 1298), (1302, 1302), (1306, 1306), (14...</td>
      <td>((1590, 1591), (1593, 1593), (1626, 1626), (16...</td>
    </tr>
    <tr>
      <th>unp_interface_range_2</th>
      <td>((1298, 1298), (1302, 1302), (1306, 1306), (14...</td>
      <td>((1298, 1298), (1302, 1302), (1306, 1306), (14...</td>
      <td>((1611, 1612), (1614, 1614), (1647, 1647), (16...</td>
      <td>()</td>
      <td>((1611, 1612), (1614, 1614), (1647, 1647), (16...</td>
      <td>((1435, 1435), (1438, 1439), (1441, 1442), (14...</td>
      <td>((1306, 1306), (1401, 1401), (1404, 1404), (14...</td>
      <td>((1332, 1332), (1459, 1459), (1462, 1463), (14...</td>
      <td>((1456, 1456), (1459, 1460), (1462, 1463), (14...</td>
      <td>()</td>
    </tr>
    <tr>
      <th>i_group</th>
      <td>(P21359-2, P21359-6)</td>
      <td>(P21359-2, P21359-4)</td>
      <td>(P21359-2, P21359)</td>
      <td>(P21359-2, P21359-4)</td>
      <td>(P21359-2, P21359)</td>
      <td>(P21359-2, P21359-6)</td>
      <td>(P21359-2, P21359-6)</td>
      <td>(P21359-2, P21359-4)</td>
      <td>(P21359-2, P21359-4)</td>
      <td>(P21359-2, P21359-4)</td>
    </tr>
    <tr>
      <th>i_select_tag</th>
      <td>True</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
      <td>False</td>
    </tr>
    <tr>
      <th>i_select_rank</th>
      <td>11</td>
      <td>1</td>
      <td>4</td>
      <td>-1</td>
      <td>13</td>
      <td>12</td>
      <td>17</td>
      <td>4</td>
      <td>2</td>
      <td>-1</td>
    </tr>
  </tbody>
</table>
</details>

## 异聚体代表集结构选择

```python
df4 = sifts_demo.pipe_select_he(run_as_completed=True).result()
df4.sample(10)
```

<details>
<summary>Click to view dataframe</summary>
<table class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>11</th>
      <th>3</th>
      <th>6</th>
      <th>15</th>
      <th>29</th>
      <th>22</th>
      <th>31</th>
      <th>5</th>
      <th>18</th>
      <th>26</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>entity_id_1</th>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
    </tr>
    <tr>
      <th>chain_id_1</th>
      <td>B</td>
      <td>B</td>
      <td>B</td>
      <td>B</td>
      <td>D</td>
      <td>B</td>
      <td>D</td>
      <td>B</td>
      <td>D</td>
      <td>D</td>
    </tr>
    <tr>
      <th>struct_asym_id_1</th>
      <td>B</td>
      <td>B</td>
      <td>B</td>
      <td>B</td>
      <td>D</td>
      <td>B</td>
      <td>D</td>
      <td>B</td>
      <td>D</td>
      <td>D</td>
    </tr>
    <tr>
      <th>struct_asym_id_in_assembly_1</th>
      <td>B</td>
      <td>B</td>
      <td>B</td>
      <td>B</td>
      <td>D</td>
      <td>B</td>
      <td>D</td>
      <td>B</td>
      <td>D</td>
      <td>D</td>
    </tr>
    <tr>
      <th>asym_id_rank_1</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
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
    </tr>
    <tr>
      <th>unp_interface_range_1</th>
      <td>((1369, 1369), (1378, 1379), (1430, 1432), (14...</td>
      <td>((1233, 1234), (1236, 1236), (1272, 1273), (12...</td>
      <td>((1233, 1234), (1237, 1237), (1272, 1273), (12...</td>
      <td>((1233, 1234), (1236, 1237), (1272, 1273), (12...</td>
      <td>((1233, 1234), (1236, 1237), (1272, 1278), (12...</td>
      <td>((1232, 1234), (1237, 1237), (1271, 1278), (12...</td>
      <td>((1233, 1234), (1236, 1237), (1272, 1278), (12...</td>
      <td>((1378, 1379), (1430, 1432), (1451, 1452), (14...</td>
      <td>((1233, 1233), (1272, 1273), (1276, 1278), (12...</td>
      <td>((1235, 1235), (1238, 1238), (1241, 1242), (12...</td>
    </tr>
    <tr>
      <th>unp_interface_range_2</th>
      <td>((47, 51), (55, 57), (75, 75), (77, 78), (96, ...</td>
      <td>((12, 12), (17, 17), (21, 21), (25, 25), (29, ...</td>
      <td>((11, 12), (17, 17), (21, 21), (25, 25), (29, ...</td>
      <td>((12, 12), (17, 17), (21, 21), (25, 25), (29, ...</td>
      <td>((11, 13), (17, 17), (21, 21), (25, 25), (27, ...</td>
      <td>((12, 13), (17, 17), (21, 21), (24, 25), (30, ...</td>
      <td>((11, 13), (17, 17), (21, 21), (25, 25), (27, ...</td>
      <td>((47, 50), (52, 52), (55, 57), (75, 75), (78, ...</td>
      <td>((11, 12), (17, 17), (21, 21), (29, 41), (54, ...</td>
      <td>((23, 23), (25, 27), (42, 45), (50, 50), (148,...</td>
    </tr>
    <tr>
      <th>i_group</th>
      <td>(P21359-2, Q7Z699)</td>
      <td>(P21359-2, P01116-2)</td>
      <td>(P21359-2, P01116)</td>
      <td>(P21359-2, P01116-2)</td>
      <td>(P21359-2, P01116-2)</td>
      <td>(P21359-2, P01116)</td>
      <td>(P21359-2, P01116-2)</td>
      <td>(P21359-2, Q7Z699)</td>
      <td>(P21359-2, P01116)</td>
      <td>(P21359-2, P01116)</td>
    </tr>
    <tr>
      <th>i_select_tag</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>i_select_rank</th>
      <td>4</td>
      <td>14</td>
      <td>11</td>
      <td>5</td>
      <td>8</td>
      <td>3</td>
      <td>7</td>
      <td>2</td>
      <td>10</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</details>

## SWISS-MODEL资源的加入

```python
df5 = sifts_demo.pipe_select_smr_mo(sifts_mo_df=df1).result()
df5
```

<details>
<summary>Click to view dataframe</summary>
<table class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
      <th>5</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>UniProt</th>
      <td>P21359-2</td>
      <td>P21359-2</td>
      <td>P21359-2</td>
      <td>P21359-2</td>
      <td>P21359-2</td>
      <td>P21359-2</td>
    </tr>
    <tr>
      <th>chains</th>
      <td>[{"id":"A","segments":[{"smtl":{"aligned_seque...</td>
      <td>[{"id":"A","segments":[{"smtl":{"aligned_seque...</td>
      <td>[{"id":"A","segments":[{"smtl":{"aligned_seque...</td>
      <td>[{"id":"A","segments":[{"smtl":{"aligned_seque...</td>
      <td>[{"id":"L","segments":[{"smtl":{"aligned_seque...</td>
      <td>[{"id":"A","segments":[{"smtl":{"aligned_seque...</td>
    </tr>
    <tr>
      <th>coordinates</th>
      <td>https://swissmodel.expasy.org/repository/unipr...</td>
      <td>https://swissmodel.expasy.org/repository/unipr...</td>
      <td>https://swissmodel.expasy.org/repository/unipr...</td>
      <td>https://swissmodel.expasy.org/repository/unipr...</td>
      <td>https://swissmodel.expasy.org/repository/unipr...</td>
      <td>https://swissmodel.expasy.org/repository/unipr...</td>
    </tr>
    <tr>
      <th>coverage</th>
      <td>0.0958126</td>
      <td>0.114975</td>
      <td>0.0489709</td>
      <td>0.0468417</td>
      <td>0.0493258</td>
      <td>0.0532292</td>
    </tr>
    <tr>
      <th>created_date</th>
      <td>2020-11-01T18:53:29.485000+00:00</td>
      <td>2020-11-01T18:53:29.436000+00:00</td>
      <td>2020-11-01T18:53:29.457000+00:00</td>
      <td>2020-11-01T18:53:29.405000+00:00</td>
      <td>2020-11-01T18:53:29.362000+00:00</td>
      <td>2020-11-01T18:53:29.384000+00:00</td>
    </tr>
    <tr>
      <th>found_by</th>
      <td>BLAST</td>
      <td>HHblits</td>
      <td>HHblits</td>
      <td>HHblits</td>
      <td>HHblits</td>
      <td>HHblits</td>
    </tr>
    <tr>
      <th>gmqe</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>identifier</th>
      <td>NF1_HUMAN</td>
      <td>NF1_HUMAN</td>
      <td>NF1_HUMAN</td>
      <td>NF1_HUMAN</td>
      <td>NF1_HUMAN</td>
      <td>NF1_HUMAN</td>
    </tr>
    <tr>
      <th>identity</th>
      <td>0.996324</td>
      <td>1</td>
      <td>0.15942</td>
      <td>0.10687</td>
      <td>0.214815</td>
      <td>0.11194</td>
    </tr>
    <tr>
      <th>isoid</th>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
    </tr>
    <tr>
      <th>ligand_chains</th>
      <td>[{"count":1,"ligands":[{"description":"(1S)-2-...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>md5</th>
      <td>fc83f587346226e60cc701448008f89f</td>
      <td>fc83f587346226e60cc701448008f89f</td>
      <td>fc83f587346226e60cc701448008f89f</td>
      <td>fc83f587346226e60cc701448008f89f</td>
      <td>fc83f587346226e60cc701448008f89f</td>
      <td>fc83f587346226e60cc701448008f89f</td>
    </tr>
    <tr>
      <th>method</th>
      <td>HOMOLOGY MODELLING</td>
      <td>HOMOLOGY MODELLING</td>
      <td>HOMOLOGY MODELLING</td>
      <td>HOMOLOGY MODELLING</td>
      <td>HOMOLOGY MODELLING</td>
      <td>HOMOLOGY MODELLING</td>
    </tr>
    <tr>
      <th>oligo-state</th>
      <td>monomer</td>
      <td>monomer</td>
      <td>monomer</td>
      <td>monomer</td>
      <td>monomer</td>
      <td>monomer</td>
    </tr>
    <tr>
      <th>provider</th>
      <td>SWISSMODEL</td>
      <td>SWISSMODEL</td>
      <td>SWISSMODEL</td>
      <td>SWISSMODEL</td>
      <td>SWISSMODEL</td>
      <td>SWISSMODEL</td>
    </tr>
    <tr>
      <th>unp_len</th>
      <td>2818</td>
      <td>2818</td>
      <td>2818</td>
      <td>2818</td>
      <td>2818</td>
      <td>2818</td>
    </tr>
    <tr>
      <th>similarity</th>
      <td>0.615442</td>
      <td>0.612197</td>
      <td>0.284541</td>
      <td>0.254453</td>
      <td>0.299259</td>
      <td>0.260199</td>
    </tr>
    <tr>
      <th>template</th>
      <td>3p7z.1.A</td>
      <td>6v6f.1.A</td>
      <td>5owu.1.A</td>
      <td>3woy.1.A</td>
      <td>6ltj.1.L</td>
      <td>1h2t.1.A</td>
    </tr>
    <tr>
      <th>unp_range</th>
      <td>[[1547,1816]]</td>
      <td>[[1205,1528]]</td>
      <td>[[2221,2358]]</td>
      <td>[[2268,2399]]</td>
      <td>[[1074,1212]]</td>
      <td>[[1986,2135]]</td>
    </tr>
    <tr>
      <th>acc_agreement_norm_score</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>acc_agreement_z_score</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>avg_local_score</th>
      <td>0.716453</td>
      <td>0.725275</td>
      <td>0.508763</td>
      <td>0.423608</td>
      <td>0.414444</td>
      <td>0.409797</td>
    </tr>
    <tr>
      <th>avg_local_score_error</th>
      <td>0.051</td>
      <td>0.052</td>
      <td>0.071</td>
      <td>0.072</td>
      <td>0.071</td>
      <td>0.067</td>
    </tr>
    <tr>
      <th>cbeta_norm_score</th>
      <td>-0.0111416</td>
      <td>-0.0120866</td>
      <td>0.00738831</td>
      <td>0.0114884</td>
      <td>-0.00335261</td>
      <td>0.00871135</td>
    </tr>
    <tr>
      <th>cbeta_z_score</th>
      <td>-0.509795</td>
      <td>-0.252126</td>
      <td>-3.78703</td>
      <td>-4.45243</td>
      <td>-1.86066</td>
      <td>-4.26843</td>
    </tr>
    <tr>
      <th>interaction_norm_score</th>
      <td>-0.0201178</td>
      <td>-0.0230367</td>
      <td>-0.0165123</td>
      <td>-0.0141633</td>
      <td>-0.016426</td>
      <td>-0.0122362</td>
    </tr>
    <tr>
      <th>interaction_z_score</th>
      <td>-0.777705</td>
      <td>0.00858758</td>
      <td>-1.40313</td>
      <td>-1.7064</td>
      <td>-1.42372</td>
      <td>-2.12794</td>
    </tr>
    <tr>
      <th>packing_norm_score</th>
      <td>-0.389243</td>
      <td>-0.400769</td>
      <td>-0.270749</td>
      <td>-0.299886</td>
      <td>-0.34727</td>
      <td>-0.346139</td>
    </tr>
    <tr>
      <th>packing_z_score</th>
      <td>0.302031</td>
      <td>0.585791</td>
      <td>-1.33267</td>
      <td>-0.922307</td>
      <td>-0.361593</td>
      <td>-0.413069</td>
    </tr>
    <tr>
      <th>qmean4_norm_score</th>
      <td>0.76744</td>
      <td>0.708347</td>
      <td>0.591839</td>
      <td>0.589486</td>
      <td>0.588397</td>
      <td>0.582163</td>
    </tr>
    <tr>
      <th>qmean4_z_score</th>
      <td>-0.164094</td>
      <td>-1.88541</td>
      <td>-3.58124</td>
      <td>-3.59226</td>
      <td>-3.62587</td>
      <td>-4.04823</td>
    </tr>
    <tr>
      <th>qmean6_norm_score</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>qmean6_z_score</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>ss_agreement_norm_score</th>
      <td>0.597907</td>
      <td>0.590228</td>
      <td>0.338587</td>
      <td>0.23634</td>
      <td>0.129832</td>
      <td>0.350606</td>
    </tr>
    <tr>
      <th>ss_agreement_z_score</th>
      <td>-0.394816</td>
      <td>-0.466057</td>
      <td>-2.29499</td>
      <td>-2.87268</td>
      <td>-3.59137</td>
      <td>-2.1998</td>
    </tr>
    <tr>
      <th>torsion_norm_score</th>
      <td>-0.304895</td>
      <td>-0.112651</td>
      <td>0.0274821</td>
      <td>0.0282064</td>
      <td>0.151137</td>
      <td>0.0952523</td>
    </tr>
    <tr>
      <th>torsion_z_score</th>
      <td>-0.147987</td>
      <td>-2.13314</td>
      <td>-2.45158</td>
      <td>-2.44197</td>
      <td>-3.25616</td>
      <td>-3.05407</td>
    </tr>
    <tr>
      <th>select_rank</th>
      <td>1</td>
      <td>2</td>
      <td>3</td>
      <td>4</td>
      <td>5</td>
      <td>6</td>
    </tr>
    <tr>
      <th>select_tag</th>
      <td>False</td>
      <td>False</td>
      <td>True</td>
      <td>False</td>
      <td>True</td>
      <td>True</td>
    </tr>
  </tbody>
</table>
</details>

`pipe_select_smr_mo`会根据传入的SIFTS单体选择结果结合SMR提供的model的覆盖范围来判断可用选择哪些模型结构作为补充。