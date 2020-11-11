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
authors:
  - admin
---

<style>
table.dataframe {
    display: block;
    overflow-x: auto;
    white-space: nowrap;
    overflow-y: auto;
    height: 200px;
}
</style>

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

{{% callout note %}}
阅读这部分不需要对**Python Asynchronous Programming**有任何了解。
{{% /callout %}}

## 安装

`pdb-profiling`基于Python3，是一个Python Package，需要您的电脑预先安装了Python3.6及以上版本才可使用。

### *安装之前

{{% callout note %}}

* 确保您的64位电脑安装了64位的Python
* 为了避免一些意想不到的错误，请先运行以下命令以升级`pip`:

{{% /callout %}}

```bash
pip install --upgrade pip
``` 

### 正式安装步骤

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

下面以获取<https://www.ebi.ac.uk/pdbe/api/pdb/entry/molecules/3hl2>的信息为例,其给出PDB条目中所有分子Entity-Chain level元数据信息，包括分子类型、分子名称、SEQRES序列等:

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
      <th>ca_p_only</th>
      <th>entity_id</th>
      <th>gene_name</th>
      <th>in_chains</th>
      <th>in_struct_asyms</th>
      <th>length</th>
      <th>molecule_name</th>
      <th>molecule_type</th>
      <th>mutation_flag</th>
      <th>number_of_copies</th>
      <th>pdb_sequence</th>
      <th>pdb_sequence_indices_with_multiple_residues</th>
      <th>sample_preparation</th>
      <th>sequence</th>
      <th>source</th>
      <th>synonym</th>
      <th>weight</th>
      <th>pdb_id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>False</td>
      <td>1</td>
      <td>["SEPSECS","TRNP48"]</td>
      <td>["A","B","C","D"]</td>
      <td>["A","B","C","D"]</td>
      <td>501.0</td>
      <td>["O-phosphoseryl-tRNA(Sec) selenium transferase"]</td>
      <td>polypeptide(L)</td>
      <td>NaN</td>
      <td>4</td>
      <td>MNRESFAAGERLVSPAYVRQGCEARRSHEHLIRLLLEKGKCPENGW...</td>
      <td>{}</td>
      <td>Genetically manipulated</td>
      <td>MNRESFAAGERLVSPAYVRQGCEARRSHEHLIRLLLEKGKCPENGW...</td>
      <td>[{"expression_host_scientific_name":"Escherich...</td>
      <td>O-phosphoseryl-tRNA(Sec) selenium transferase</td>
      <td>55801.211</td>
      <td>3hl2</td>
    </tr>
    <tr>
      <th>1</th>
      <td>False</td>
      <td>2</td>
      <td>NaN</td>
      <td>["E"]</td>
      <td>["E"]</td>
      <td>90.0</td>
      <td>["tRNASec"]</td>
      <td>polyribonucleotide</td>
      <td>NaN</td>
      <td>1</td>
      <td>GCCCGGAUGAUCCUCAGUGGUCUGGGGUGCAGGCUUCAAACCUGUA...</td>
      <td>{}</td>
      <td>Genetically manipulated</td>
      <td>GCCCGGAUGAUCCUCAGUGGUCUGGGGUGCAGGCUUCAAACCUGUA...</td>
      <td>[{"expression_host_scientific_name":"Escherich...</td>
      <td>tRNASec</td>
      <td>28908.084</td>
      <td>3hl2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>False</td>
      <td>3</td>
      <td>NaN</td>
      <td>["A","B","C","D"]</td>
      <td>["F","I","L","N"]</td>
      <td>NaN</td>
      <td>["(5-HYDROXY-4,6-DIMETHYLPYRIDIN-3-YL)METHYL D...</td>
      <td>bound</td>
      <td>NaN</td>
      <td>4</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Synthetically obtained</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>233.158</td>
      <td>3hl2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>False</td>
      <td>4</td>
      <td>NaN</td>
      <td>["A","C"]</td>
      <td>["G","H","M"]</td>
      <td>NaN</td>
      <td>["Monothiophosphate"]</td>
      <td>bound</td>
      <td>NaN</td>
      <td>3</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Synthetically obtained</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>114.061</td>
      <td>3hl2</td>
    </tr>
    <tr>
      <th>4</th>
      <td>False</td>
      <td>5</td>
      <td>NaN</td>
      <td>["B","D"]</td>
      <td>["J","K","O","P"]</td>
      <td>NaN</td>
      <td>["PHOSPHOSERINE"]</td>
      <td>bound</td>
      <td>NaN</td>
      <td>4</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Synthetically obtained</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>185.072</td>
      <td>3hl2</td>
    </tr>
    <tr>
      <th>5</th>
      <td>False</td>
      <td>6</td>
      <td>NaN</td>
      <td>["A","B","C","D","E"]</td>
      <td>["Q","R","S","T","U"]</td>
      <td>NaN</td>
      <td>["water"]</td>
      <td>water</td>
      <td>NaN</td>
      <td>288</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Natural source</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>18.015</td>
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

{{% callout warning %}}
若使用不符要求或暂不支持的API则会抛出异常。
{{% /callout %}}

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

{{% callout note %}}
注意: 此步骤得到的res中，结果出现次序并不一定按照PDBs中PDB的顺序。
{{% /callout %}}

```python
from pandas import concat
concat(res, sort=False, ignore_index=True)
```

<details>
<summary>Click to view dataframe</summary>
<table class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>assemblies</th>
      <th>deposition_date</th>
      <th>deposition_site</th>
      <th>entry_authors</th>
      <th>experimental_method</th>
      <th>experimental_method_class</th>
      <th>number_of_entities</th>
      <th>pdb_id</th>
      <th>processing_site</th>
      <th>related_structures</th>
      <th>release_date</th>
      <th>revision_date</th>
      <th>split_entry</th>
      <th>title</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>[{"assembly_id":"1","form":"Non-polymer only",...</td>
      <td>19971208</td>
      <td>NaN</td>
      <td>["Kavanaugh, J.S.","Arnone, A."]</td>
      <td>["X-ray diffraction"]</td>
      <td>["x-ray"]</td>
      <td>{"polypeptide":2,"dna":0,"ligand":1,"dna/rna":...</td>
      <td>1a01</td>
      <td>BNL</td>
      <td>[]</td>
      <td>19980318</td>
      <td>20110713</td>
      <td>[]</td>
      <td>HEMOGLOBIN (VAL BETA1 MET, TRP BETA37 ALA) MUTANT</td>
    </tr>
    <tr>
      <th>1</th>
      <td>[{"preferred":true,"form":"homo","name":"monom...</td>
      <td>20101118</td>
      <td>PDBE</td>
      <td>["Salah, E.","Ugochukwu, E.","Elkins, J.M.","B...</td>
      <td>["X-ray diffraction"]</td>
      <td>["x-ray"]</td>
      <td>{"water":1,"polypeptide":1,"other":0,"dna":0,"...</td>
      <td>2xyn</td>
      <td>PDBE</td>
      <td>[]</td>
      <td>20101201</td>
      <td>20190403</td>
      <td>[]</td>
      <td>HUMAN ABL2 IN COMPLEX WITH AURORA KINASE INHIB...</td>
    </tr>
    <tr>
      <th>2</th>
      <td>[{"preferred":true,"form":"hetero","name":"pen...</td>
      <td>20090526</td>
      <td>RCSB</td>
      <td>["Palioura, S.","Steitz, T.A.","Soll, D.","Sim...</td>
      <td>["X-ray diffraction"]</td>
      <td>["x-ray"]</td>
      <td>{"water":1,"polypeptide":1,"other":0,"dna":0,"...</td>
      <td>3hl2</td>
      <td>RCSB</td>
      <td>[]</td>
      <td>20091006</td>
      <td>20180124</td>
      <td>[]</td>
      <td>The crystal structure of the human SepSecS-tRN...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>[{"assembly_id":"1","form":"homo","preferred":...</td>
      <td>20121010</td>
      <td>RCSB</td>
      <td>["Moshe, B.-D.","Grzegorz, W.","Mikael, E.","I...</td>
      <td>["X-ray diffraction"]</td>
      <td>["x-ray"]</td>
      <td>{"polypeptide":1,"dna":0,"ligand":3,"dna/rna":...</td>
      <td>4hho</td>
      <td>RCSB</td>
      <td>[]</td>
      <td>20130327</td>
      <td>20130327</td>
      <td>[]</td>
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
      <th>UniProt</th>
      <th>chain_id</th>
      <th>end</th>
      <th>entity_id</th>
      <th>identifier</th>
      <th>identity</th>
      <th>is_canonical</th>
      <th>name</th>
      <th>pdb_end</th>
      <th>pdb_id</th>
      <th>pdb_start</th>
      <th>start</th>
      <th>struct_asym_id</th>
      <th>unp_end</th>
      <th>unp_start</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>P68871</td>
      <td>B</td>
      <td>{"author_residue_number":146,"author_insertion...</td>
      <td>2</td>
      <td>HBB_HUMAN</td>
      <td>0.99</td>
      <td>True</td>
      <td>HBB_HUMAN</td>
      <td>146</td>
      <td>1a01</td>
      <td>1</td>
      <td>{"author_residue_number":1,"author_insertion_c...</td>
      <td>B</td>
      <td>147</td>
      <td>2</td>
    </tr>
    <tr>
      <th>1</th>
      <td>P68871</td>
      <td>D</td>
      <td>{"author_residue_number":146,"author_insertion...</td>
      <td>2</td>
      <td>HBB_HUMAN</td>
      <td>0.99</td>
      <td>True</td>
      <td>HBB_HUMAN</td>
      <td>146</td>
      <td>1a01</td>
      <td>1</td>
      <td>{"author_residue_number":1,"author_insertion_c...</td>
      <td>D</td>
      <td>147</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>P69905</td>
      <td>A</td>
      <td>{"author_residue_number":141,"author_insertion...</td>
      <td>1</td>
      <td>HBA_HUMAN</td>
      <td>1.00</td>
      <td>True</td>
      <td>HBA_HUMAN</td>
      <td>141</td>
      <td>1a01</td>
      <td>1</td>
      <td>{"author_residue_number":1,"author_insertion_c...</td>
      <td>A</td>
      <td>142</td>
      <td>2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>P69905</td>
      <td>C</td>
      <td>{"author_residue_number":141,"author_insertion...</td>
      <td>1</td>
      <td>HBA_HUMAN</td>
      <td>1.00</td>
      <td>True</td>
      <td>HBA_HUMAN</td>
      <td>141</td>
      <td>1a01</td>
      <td>1</td>
      <td>{"author_residue_number":1,"author_insertion_c...</td>
      <td>C</td>
      <td>142</td>
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

<details>
<summary>Click to view dataframe</summary>
<table class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>UniProt</th>
      <th>chain_id</th>
      <th>end</th>
      <th>entity_id</th>
      <th>identity</th>
      <th>is_canonical</th>
      <th>pdb_id</th>
      <th>start</th>
      <th>struct_asym_id</th>
      <th>unp_end</th>
      <th>unp_start</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Q5VST9</td>
      <td>A</td>
      <td>{"author_residue_number":97,"author_insertion_...</td>
      <td>1</td>
      <td>1.00</td>
      <td>True</td>
      <td>2dku</td>
      <td>{"author_residue_number":8,"author_insertion_c...</td>
      <td>A</td>
      <td>3004</td>
      <td>2915</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Q5VST9</td>
      <td>A</td>
      <td>{"author_residue_number":102,"author_insertion...</td>
      <td>1</td>
      <td>0.75</td>
      <td>True</td>
      <td>2dm7</td>
      <td>{"author_residue_number":8,"author_insertion_c...</td>
      <td>A</td>
      <td>3631</td>
      <td>3537</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Q5VST9</td>
      <td>A</td>
      <td>{"author_residue_number":548,"author_insertion...</td>
      <td>1</td>
      <td>0.89</td>
      <td>True</td>
      <td>2yz8</td>
      <td>{"author_residue_number":459,"author_insertion...</td>
      <td>A</td>
      <td>3273</td>
      <td>3184</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Q5VST9</td>
      <td>A</td>
      <td>{"author_residue_number":null,"author_insertio...</td>
      <td>1</td>
      <td>0.98</td>
      <td>True</td>
      <td>5tzm</td>
      <td>{"author_residue_number":3,"author_insertion_c...</td>
      <td>A</td>
      <td>4521</td>
      <td>4431</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Q5VST9</td>
      <td>A</td>
      <td>{"author_residue_number":null,"author_insertio...</td>
      <td>1</td>
      <td>0.93</td>
      <td>True</td>
      <td>4rsv</td>
      <td>{"author_residue_number":null,"author_insertio...</td>
      <td>A</td>
      <td>4429</td>
      <td>4337</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Q5VST9</td>
      <td>O</td>
      <td>{"author_residue_number":null,"author_insertio...</td>
      <td>1</td>
      <td>1.00</td>
      <td>True</td>
      <td>4c4k</td>
      <td>{"author_residue_number":9,"author_insertion_c...</td>
      <td>A</td>
      <td>103</td>
      <td>9</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Q5VST9</td>
      <td>A</td>
      <td>{"author_residue_number":109,"author_insertion...</td>
      <td>1</td>
      <td>1.00</td>
      <td>True</td>
      <td>2cr6</td>
      <td>{"author_residue_number":8,"author_insertion_c...</td>
      <td>A</td>
      <td>3100</td>
      <td>2999</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Q5VST9</td>
      <td>A</td>
      <td>{"author_residue_number":68,"author_insertion_...</td>
      <td>1</td>
      <td>1.00</td>
      <td>True</td>
      <td>1v1c</td>
      <td>{"author_residue_number":1,"author_insertion_c...</td>
      <td>A</td>
      <td>5668</td>
      <td>5601</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Q5VST9</td>
      <td>A</td>
      <td>{"author_residue_number":93,"author_insertion_...</td>
      <td>1</td>
      <td>0.93</td>
      <td>True</td>
      <td>2mwc</td>
      <td>{"author_residue_number":1,"author_insertion_c...</td>
      <td>A</td>
      <td>4429</td>
      <td>4337</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Q5VST9</td>
      <td>A</td>
      <td>{"author_residue_number":96,"author_insertion_...</td>
      <td>1</td>
      <td>1.00</td>
      <td>True</td>
      <td>2edr</td>
      <td>{"author_residue_number":8,"author_insertion_c...</td>
      <td>A</td>
      <td>3449</td>
      <td>3361</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Q5VST9</td>
      <td>A</td>
      <td>{"author_residue_number":101,"author_insertion...</td>
      <td>1</td>
      <td>1.00</td>
      <td>True</td>
      <td>2edq</td>
      <td>{"author_residue_number":8,"author_insertion_c...</td>
      <td>A</td>
      <td>3806</td>
      <td>3713</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Q5VST9</td>
      <td>A</td>
      <td>{"author_residue_number":101,"author_insertion...</td>
      <td>1</td>
      <td>1.00</td>
      <td>True</td>
      <td>2edw</td>
      <td>{"author_residue_number":8,"author_insertion_c...</td>
      <td>A</td>
      <td>3630</td>
      <td>3537</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Q5VST9</td>
      <td>A</td>
      <td>{"author_residue_number":96,"author_insertion_...</td>
      <td>1</td>
      <td>1.00</td>
      <td>True</td>
      <td>2edt</td>
      <td>{"author_residue_number":8,"author_insertion_c...</td>
      <td>A</td>
      <td>3537</td>
      <td>3449</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Q5VST9</td>
      <td>A</td>
      <td>{"author_residue_number":101,"author_insertion...</td>
      <td>1</td>
      <td>0.82</td>
      <td>True</td>
      <td>2gqh</td>
      <td>{"author_residue_number":8,"author_insertion_c...</td>
      <td>A</td>
      <td>3807</td>
      <td>3714</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Q5VST9</td>
      <td>0</td>
      <td>{"author_residue_number":98,"author_insertion_...</td>
      <td>1</td>
      <td>0.30</td>
      <td>True</td>
      <td>4uow</td>
      <td>{"author_residue_number":5,"author_insertion_c...</td>
      <td>A</td>
      <td>203</td>
      <td>110</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Q5VST9</td>
      <td>2</td>
      <td>{"author_residue_number":98,"author_insertion_...</td>
      <td>1</td>
      <td>0.30</td>
      <td>True</td>
      <td>4uow</td>
      <td>{"author_residue_number":5,"author_insertion_c...</td>
      <td>C</td>
      <td>203</td>
      <td>110</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Q5VST9</td>
      <td>4</td>
      <td>{"author_residue_number":98,"author_insertion_...</td>
      <td>1</td>
      <td>0.30</td>
      <td>True</td>
      <td>4uow</td>
      <td>{"author_residue_number":5,"author_insertion_c...</td>
      <td>E</td>
      <td>203</td>
      <td>110</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Q5VST9</td>
      <td>6</td>
      <td>{"author_residue_number":98,"author_insertion_...</td>
      <td>1</td>
      <td>0.30</td>
      <td>True</td>
      <td>4uow</td>
      <td>{"author_residue_number":5,"author_insertion_c...</td>
      <td>G</td>
      <td>203</td>
      <td>110</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Q5VST9</td>
      <td>8</td>
      <td>{"author_residue_number":98,"author_insertion_...</td>
      <td>1</td>
      <td>0.30</td>
      <td>True</td>
      <td>4uow</td>
      <td>{"author_residue_number":5,"author_insertion_c...</td>
      <td>I</td>
      <td>203</td>
      <td>110</td>
    </tr>
    <tr>
      <th>19</th>
      <td>Q5VST9</td>
      <td>A</td>
      <td>{"author_residue_number":98,"author_insertion_...</td>
      <td>1</td>
      <td>0.30</td>
      <td>True</td>
      <td>4uow</td>
      <td>{"author_residue_number":5,"author_insertion_c...</td>
      <td>K</td>
      <td>203</td>
      <td>110</td>
    </tr>
    <tr>
      <th>20</th>
      <td>Q5VST9</td>
      <td>C</td>
      <td>{"author_residue_number":98,"author_insertion_...</td>
      <td>1</td>
      <td>0.30</td>
      <td>True</td>
      <td>4uow</td>
      <td>{"author_residue_number":5,"author_insertion_c...</td>
      <td>M</td>
      <td>203</td>
      <td>110</td>
    </tr>
    <tr>
      <th>21</th>
      <td>Q5VST9</td>
      <td>E</td>
      <td>{"author_residue_number":98,"author_insertion_...</td>
      <td>1</td>
      <td>0.30</td>
      <td>True</td>
      <td>4uow</td>
      <td>{"author_residue_number":5,"author_insertion_c...</td>
      <td>O</td>
      <td>203</td>
      <td>110</td>
    </tr>
    <tr>
      <th>22</th>
      <td>Q5VST9</td>
      <td>G</td>
      <td>{"author_residue_number":98,"author_insertion_...</td>
      <td>1</td>
      <td>0.30</td>
      <td>True</td>
      <td>4uow</td>
      <td>{"author_residue_number":5,"author_insertion_c...</td>
      <td>Q</td>
      <td>203</td>
      <td>110</td>
    </tr>
    <tr>
      <th>23</th>
      <td>Q5VST9</td>
      <td>I</td>
      <td>{"author_residue_number":98,"author_insertion_...</td>
      <td>1</td>
      <td>0.30</td>
      <td>True</td>
      <td>4uow</td>
      <td>{"author_residue_number":5,"author_insertion_c...</td>
      <td>S</td>
      <td>203</td>
      <td>110</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Q5VST9</td>
      <td>K</td>
      <td>{"author_residue_number":98,"author_insertion_...</td>
      <td>1</td>
      <td>0.30</td>
      <td>True</td>
      <td>4uow</td>
      <td>{"author_residue_number":5,"author_insertion_c...</td>
      <td>U</td>
      <td>203</td>
      <td>110</td>
    </tr>
    <tr>
      <th>25</th>
      <td>Q5VST9</td>
      <td>M</td>
      <td>{"author_residue_number":98,"author_insertion_...</td>
      <td>1</td>
      <td>0.30</td>
      <td>True</td>
      <td>4uow</td>
      <td>{"author_residue_number":5,"author_insertion_c...</td>
      <td>W</td>
      <td>203</td>
      <td>110</td>
    </tr>
    <tr>
      <th>26</th>
      <td>Q5VST9</td>
      <td>O</td>
      <td>{"author_residue_number":98,"author_insertion_...</td>
      <td>1</td>
      <td>0.30</td>
      <td>True</td>
      <td>4uow</td>
      <td>{"author_residue_number":5,"author_insertion_c...</td>
      <td>Y</td>
      <td>203</td>
      <td>110</td>
    </tr>
    <tr>
      <th>27</th>
      <td>Q5VST9</td>
      <td>Q</td>
      <td>{"author_residue_number":98,"author_insertion_...</td>
      <td>1</td>
      <td>0.30</td>
      <td>True</td>
      <td>4uow</td>
      <td>{"author_residue_number":5,"author_insertion_c...</td>
      <td>AA</td>
      <td>203</td>
      <td>110</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Q5VST9</td>
      <td>S</td>
      <td>{"author_residue_number":98,"author_insertion_...</td>
      <td>1</td>
      <td>0.30</td>
      <td>True</td>
      <td>4uow</td>
      <td>{"author_residue_number":5,"author_insertion_c...</td>
      <td>CA</td>
      <td>203</td>
      <td>110</td>
    </tr>
    <tr>
      <th>29</th>
      <td>Q5VST9</td>
      <td>U</td>
      <td>{"author_residue_number":98,"author_insertion_...</td>
      <td>1</td>
      <td>0.30</td>
      <td>True</td>
      <td>4uow</td>
      <td>{"author_residue_number":5,"author_insertion_c...</td>
      <td>EA</td>
      <td>203</td>
      <td>110</td>
    </tr>
    <tr>
      <th>30</th>
      <td>Q5VST9</td>
      <td>W</td>
      <td>{"author_residue_number":98,"author_insertion_...</td>
      <td>1</td>
      <td>0.30</td>
      <td>True</td>
      <td>4uow</td>
      <td>{"author_residue_number":5,"author_insertion_c...</td>
      <td>GA</td>
      <td>203</td>
      <td>110</td>
    </tr>
    <tr>
      <th>31</th>
      <td>Q5VST9</td>
      <td>Y</td>
      <td>{"author_residue_number":98,"author_insertion_...</td>
      <td>1</td>
      <td>0.30</td>
      <td>True</td>
      <td>4uow</td>
      <td>{"author_residue_number":5,"author_insertion_c...</td>
      <td>IA</td>
      <td>203</td>
      <td>110</td>
    </tr>
    <tr>
      <th>32</th>
      <td>Q5VST9</td>
      <td>A</td>
      <td>{"author_residue_number":97,"author_insertion_...</td>
      <td>1</td>
      <td>1.00</td>
      <td>True</td>
      <td>2edf</td>
      <td>{"author_residue_number":8,"author_insertion_c...</td>
      <td>A</td>
      <td>2915</td>
      <td>2826</td>
    </tr>
    <tr>
      <th>33</th>
      <td>Q5VST9</td>
      <td>A</td>
      <td>{"author_residue_number":97,"author_insertion_...</td>
      <td>1</td>
      <td>1.00</td>
      <td>True</td>
      <td>2eo1</td>
      <td>{"author_residue_number":8,"author_insertion_c...</td>
      <td>A</td>
      <td>1712</td>
      <td>1623</td>
    </tr>
    <tr>
      <th>34</th>
      <td>Q5VST9</td>
      <td>A</td>
      <td>{"author_residue_number":98,"author_insertion_...</td>
      <td>1</td>
      <td>0.94</td>
      <td>True</td>
      <td>2eny</td>
      <td>{"author_residue_number":8,"author_insertion_c...</td>
      <td>A</td>
      <td>2825</td>
      <td>2735</td>
    </tr>
    <tr>
      <th>35</th>
      <td>Q5VST9</td>
      <td>A</td>
      <td>{"author_residue_number":107,"author_insertion...</td>
      <td>1</td>
      <td>1.00</td>
      <td>True</td>
      <td>2edh</td>
      <td>{"author_residue_number":8,"author_insertion_c...</td>
      <td>A</td>
      <td>3713</td>
      <td>3614</td>
    </tr>
    <tr>
      <th>36</th>
      <td>Q5VST9</td>
      <td>A</td>
      <td>{"author_residue_number":104,"author_insertion...</td>
      <td>1</td>
      <td>0.92</td>
      <td>True</td>
      <td>2edl</td>
      <td>{"author_residue_number":8,"author_insertion_c...</td>
      <td>A</td>
      <td>3897</td>
      <td>3801</td>
    </tr>
    <tr>
      <th>37</th>
      <td>Q5VST9</td>
      <td>A</td>
      <td>{"author_residue_number":93,"author_insertion_...</td>
      <td>1</td>
      <td>0.95</td>
      <td>True</td>
      <td>6mg9</td>
      <td>{"author_residue_number":2,"author_insertion_c...</td>
      <td>A</td>
      <td>4338</td>
      <td>4247</td>
    </tr>
    <tr>
      <th>38</th>
      <td>Q5VST9</td>
      <td>A</td>
      <td>{"author_residue_number":95,"author_insertion_...</td>
      <td>1</td>
      <td>0.99</td>
      <td>True</td>
      <td>2n56</td>
      <td>{"author_residue_number":1,"author_insertion_c...</td>
      <td>A</td>
      <td>4524</td>
      <td>4430</td>
    </tr>
    <tr>
      <th>39</th>
      <td>Q5VST9</td>
      <td>A</td>
      <td>{"author_residue_number":97,"author_insertion_...</td>
      <td>1</td>
      <td>1.00</td>
      <td>True</td>
      <td>2e7b</td>
      <td>{"author_residue_number":8,"author_insertion_c...</td>
      <td>A</td>
      <td>3273</td>
      <td>3184</td>
    </tr>
  </tbody>
</table>
</details>

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
      <th>UniProt</th>
      <th>chain_id</th>
      <th>entity_id</th>
      <th>identity</th>
      <th>is_canonical</th>
      <th>pdb_id</th>
      <th>struct_asym_id</th>
      <th>pdb_range</th>
      <th>unp_range</th>
      <th>Entry</th>
      <th>...</th>
      <th>sifts_range_tag</th>
      <th>repeated</th>
      <th>reversed</th>
      <th>InDel_sum</th>
      <th>new_pdb_range</th>
      <th>new_unp_range</th>
      <th>conflict_pdb_index</th>
      <th>conflict_pdb_range</th>
      <th>conflict_unp_range</th>
      <th>unp_len</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>P21359-2</td>
      <td>A</td>
      <td>1</td>
      <td>1.00</td>
      <td>False</td>
      <td>1nf1</td>
      <td>A</td>
      <td>[[1,333]]</td>
      <td>[[1198,1530]]</td>
      <td>P21359</td>
      <td>...</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[1,333]]</td>
      <td>[[1198,1530]]</td>
      <td>{"216":"R"}</td>
      <td>[[216,216]]</td>
      <td>[[1413,1413]]</td>
      <td>2818</td>
    </tr>
    <tr>
      <th>1</th>
      <td>P21359-2</td>
      <td>A</td>
      <td>1</td>
      <td>1.00</td>
      <td>False</td>
      <td>2d4q</td>
      <td>A</td>
      <td>[[1,257]]</td>
      <td>[[1560,1816]]</td>
      <td>P21359</td>
      <td>...</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[1,257]]</td>
      <td>[[1560,1816]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2818</td>
    </tr>
    <tr>
      <th>2</th>
      <td>P21359-2</td>
      <td>B</td>
      <td>1</td>
      <td>1.00</td>
      <td>False</td>
      <td>2d4q</td>
      <td>B</td>
      <td>[[1,257]]</td>
      <td>[[1560,1816]]</td>
      <td>P21359</td>
      <td>...</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[1,257]]</td>
      <td>[[1560,1816]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2818</td>
    </tr>
    <tr>
      <th>3</th>
      <td>P21359-2</td>
      <td>A</td>
      <td>1</td>
      <td>0.99</td>
      <td>False</td>
      <td>2e2x</td>
      <td>A</td>
      <td>[[6,277]]</td>
      <td>[[1545,1816]]</td>
      <td>P21359</td>
      <td>...</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[6,277]]</td>
      <td>[[1545,1816]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2818</td>
    </tr>
    <tr>
      <th>4</th>
      <td>P21359-2</td>
      <td>B</td>
      <td>1</td>
      <td>0.99</td>
      <td>False</td>
      <td>2e2x</td>
      <td>B</td>
      <td>[[6,277]]</td>
      <td>[[1545,1816]]</td>
      <td>P21359</td>
      <td>...</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[6,277]]</td>
      <td>[[1545,1816]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2818</td>
    </tr>
    <tr>
      <th>5</th>
      <td>P21359-2</td>
      <td>A</td>
      <td>1</td>
      <td>0.98</td>
      <td>False</td>
      <td>3p7z</td>
      <td>A</td>
      <td>[[5,276]]</td>
      <td>[[1545,1816]]</td>
      <td>P21359</td>
      <td>...</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[5,276]]</td>
      <td>[[1545,1816]]</td>
      <td>{"44":"I"}</td>
      <td>[[44,44]]</td>
      <td>[[1584,1584]]</td>
      <td>2818</td>
    </tr>
    <tr>
      <th>6</th>
      <td>P21359-2</td>
      <td>B</td>
      <td>1</td>
      <td>0.98</td>
      <td>False</td>
      <td>3p7z</td>
      <td>B</td>
      <td>[[5,276]]</td>
      <td>[[1545,1816]]</td>
      <td>P21359</td>
      <td>...</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[5,276]]</td>
      <td>[[1545,1816]]</td>
      <td>{"44":"I"}</td>
      <td>[[44,44]]</td>
      <td>[[1584,1584]]</td>
      <td>2818</td>
    </tr>
    <tr>
      <th>7</th>
      <td>P21359-2</td>
      <td>A</td>
      <td>1</td>
      <td>0.94</td>
      <td>False</td>
      <td>3peg</td>
      <td>A</td>
      <td>[[5,172],[174,290]]</td>
      <td>[[1545,1712],[1700,1816]]</td>
      <td>P21359</td>
      <td>...</td>
      <td>InDel_1</td>
      <td>True</td>
      <td>False</td>
      <td>-12</td>
      <td>[[5,172],[174,290]]</td>
      <td>[[1545,1712],[1700,1816]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2818</td>
    </tr>
    <tr>
      <th>8</th>
      <td>P21359-2</td>
      <td>A</td>
      <td>1</td>
      <td>1.00</td>
      <td>False</td>
      <td>3pg7</td>
      <td>A</td>
      <td>[[1,256]]</td>
      <td>[[1560,1816]]</td>
      <td>P21359</td>
      <td>...</td>
      <td>Deletion</td>
      <td>False</td>
      <td>False</td>
      <td>1</td>
      <td>((1, 191), (192, 256))</td>
      <td>((1560, 1750), (1752, 1816))</td>
      <td>{"191":"K"}</td>
      <td>[[191,191]]</td>
      <td>[[1750,1750]]</td>
      <td>2818</td>
    </tr>
    <tr>
      <th>9</th>
      <td>P21359-2</td>
      <td>B</td>
      <td>1</td>
      <td>1.00</td>
      <td>False</td>
      <td>3pg7</td>
      <td>B</td>
      <td>[[1,256]]</td>
      <td>[[1560,1816]]</td>
      <td>P21359</td>
      <td>...</td>
      <td>Deletion</td>
      <td>False</td>
      <td>False</td>
      <td>1</td>
      <td>((1, 191), (192, 256))</td>
      <td>((1560, 1750), (1752, 1816))</td>
      <td>{"191":"K"}</td>
      <td>[[191,191]]</td>
      <td>[[1750,1750]]</td>
      <td>2818</td>
    </tr>
    <tr>
      <th>10</th>
      <td>P21359-2</td>
      <td>B</td>
      <td>2</td>
      <td>1.00</td>
      <td>False</td>
      <td>6ob2</td>
      <td>B</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>P21359</td>
      <td>...</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2818</td>
    </tr>
    <tr>
      <th>11</th>
      <td>P21359-2</td>
      <td>D</td>
      <td>2</td>
      <td>1.00</td>
      <td>False</td>
      <td>6ob2</td>
      <td>D</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>P21359</td>
      <td>...</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2818</td>
    </tr>
    <tr>
      <th>12</th>
      <td>P21359-2</td>
      <td>B</td>
      <td>2</td>
      <td>1.00</td>
      <td>False</td>
      <td>6ob3</td>
      <td>B</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>P21359</td>
      <td>...</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2818</td>
    </tr>
    <tr>
      <th>13</th>
      <td>P21359-2</td>
      <td>D</td>
      <td>2</td>
      <td>1.00</td>
      <td>False</td>
      <td>6ob3</td>
      <td>D</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>P21359</td>
      <td>...</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2818</td>
    </tr>
    <tr>
      <th>14</th>
      <td>P21359-2</td>
      <td>B</td>
      <td>2</td>
      <td>1.00</td>
      <td>False</td>
      <td>6v65</td>
      <td>B</td>
      <td>[[2,329]]</td>
      <td>[[1203,1530]]</td>
      <td>P21359</td>
      <td>...</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[2,329]]</td>
      <td>[[1203,1530]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2818</td>
    </tr>
    <tr>
      <th>15</th>
      <td>P21359-2</td>
      <td>B</td>
      <td>2</td>
      <td>1.00</td>
      <td>False</td>
      <td>6v6f</td>
      <td>B</td>
      <td>[[2,329]]</td>
      <td>[[1203,1530]]</td>
      <td>P21359</td>
      <td>...</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[2,329]]</td>
      <td>[[1203,1530]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
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
pdb_object.profile_id().result()
```

<details>
<summary>Click to view dataframe</summary>

<table class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>pdb_id</th>
      <th>entity_id</th>
      <th>molecule_type</th>
      <th>chain_id</th>
      <th>struct_asym_id</th>
      <th>assembly_id</th>
      <th>model_id</th>
      <th>asym_id_rank</th>
      <th>oper_expression</th>
      <th>symmetry_operation</th>
      <th>symmetry_id</th>
      <th>struct_asym_id_in_assembly</th>
      <th>au_subset</th>
      <th>details</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>3hl2</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>A</td>
      <td>A</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td></td>
      <td></td>
      <td></td>
      <td>A</td>
      <td>False</td>
      <td>asymmetric_unit</td>
    </tr>
    <tr>
      <th>1</th>
      <td>3hl2</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>C</td>
      <td>C</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td></td>
      <td></td>
      <td></td>
      <td>C</td>
      <td>False</td>
      <td>asymmetric_unit</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3hl2</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>B</td>
      <td>B</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td></td>
      <td></td>
      <td></td>
      <td>B</td>
      <td>False</td>
      <td>asymmetric_unit</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3hl2</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>D</td>
      <td>D</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td></td>
      <td></td>
      <td></td>
      <td>D</td>
      <td>False</td>
      <td>asymmetric_unit</td>
    </tr>
    <tr>
      <th>4</th>
      <td>3hl2</td>
      <td>2</td>
      <td>polyribonucleotide</td>
      <td>E</td>
      <td>E</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td></td>
      <td></td>
      <td></td>
      <td>E</td>
      <td>False</td>
      <td>asymmetric_unit</td>
    </tr>
    <tr>
      <th>5</th>
      <td>3hl2</td>
      <td>3</td>
      <td>bound</td>
      <td>B</td>
      <td>I</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td></td>
      <td></td>
      <td></td>
      <td>I</td>
      <td>False</td>
      <td>asymmetric_unit</td>
    </tr>
    <tr>
      <th>6</th>
      <td>3hl2</td>
      <td>3</td>
      <td>bound</td>
      <td>D</td>
      <td>N</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td></td>
      <td></td>
      <td></td>
      <td>N</td>
      <td>False</td>
      <td>asymmetric_unit</td>
    </tr>
    <tr>
      <th>7</th>
      <td>3hl2</td>
      <td>3</td>
      <td>bound</td>
      <td>C</td>
      <td>L</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td></td>
      <td></td>
      <td></td>
      <td>L</td>
      <td>False</td>
      <td>asymmetric_unit</td>
    </tr>
    <tr>
      <th>8</th>
      <td>3hl2</td>
      <td>3</td>
      <td>bound</td>
      <td>A</td>
      <td>F</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td></td>
      <td></td>
      <td></td>
      <td>F</td>
      <td>False</td>
      <td>asymmetric_unit</td>
    </tr>
    <tr>
      <th>9</th>
      <td>3hl2</td>
      <td>4</td>
      <td>bound</td>
      <td>A</td>
      <td>H</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td></td>
      <td></td>
      <td></td>
      <td>H</td>
      <td>False</td>
      <td>asymmetric_unit</td>
    </tr>
    <tr>
      <th>10</th>
      <td>3hl2</td>
      <td>4</td>
      <td>bound</td>
      <td>C</td>
      <td>M</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td></td>
      <td></td>
      <td></td>
      <td>M</td>
      <td>False</td>
      <td>asymmetric_unit</td>
    </tr>
    <tr>
      <th>11</th>
      <td>3hl2</td>
      <td>4</td>
      <td>bound</td>
      <td>A</td>
      <td>G</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td></td>
      <td></td>
      <td></td>
      <td>G</td>
      <td>False</td>
      <td>asymmetric_unit</td>
    </tr>
    <tr>
      <th>12</th>
      <td>3hl2</td>
      <td>5</td>
      <td>bound</td>
      <td>D</td>
      <td>P</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td></td>
      <td></td>
      <td></td>
      <td>P</td>
      <td>False</td>
      <td>asymmetric_unit</td>
    </tr>
    <tr>
      <th>13</th>
      <td>3hl2</td>
      <td>5</td>
      <td>bound</td>
      <td>B</td>
      <td>K</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td></td>
      <td></td>
      <td></td>
      <td>K</td>
      <td>False</td>
      <td>asymmetric_unit</td>
    </tr>
    <tr>
      <th>14</th>
      <td>3hl2</td>
      <td>5</td>
      <td>bound</td>
      <td>B</td>
      <td>J</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td></td>
      <td></td>
      <td></td>
      <td>J</td>
      <td>False</td>
      <td>asymmetric_unit</td>
    </tr>
    <tr>
      <th>15</th>
      <td>3hl2</td>
      <td>5</td>
      <td>bound</td>
      <td>D</td>
      <td>O</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td></td>
      <td></td>
      <td></td>
      <td>O</td>
      <td>False</td>
      <td>asymmetric_unit</td>
    </tr>
    <tr>
      <th>16</th>
      <td>3hl2</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>A</td>
      <td>A</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>["1"]</td>
      <td>["x,x-y-1,-z"]</td>
      <td>["6_545"]</td>
      <td>A</td>
      <td>False</td>
      <td>author_defined_assembly</td>
    </tr>
    <tr>
      <th>17</th>
      <td>3hl2</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>B</td>
      <td>B</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>["1"]</td>
      <td>["x,x-y-1,-z"]</td>
      <td>["6_545"]</td>
      <td>B</td>
      <td>False</td>
      <td>author_defined_assembly</td>
    </tr>
    <tr>
      <th>18</th>
      <td>3hl2</td>
      <td>3</td>
      <td>bound</td>
      <td>A</td>
      <td>F</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>["1"]</td>
      <td>["x,x-y-1,-z"]</td>
      <td>["6_545"]</td>
      <td>F</td>
      <td>False</td>
      <td>author_defined_assembly</td>
    </tr>
    <tr>
      <th>19</th>
      <td>3hl2</td>
      <td>4</td>
      <td>bound</td>
      <td>A</td>
      <td>G</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>["1"]</td>
      <td>["x,x-y-1,-z"]</td>
      <td>["6_545"]</td>
      <td>G</td>
      <td>False</td>
      <td>author_defined_assembly</td>
    </tr>
    <tr>
      <th>20</th>
      <td>3hl2</td>
      <td>4</td>
      <td>bound</td>
      <td>A</td>
      <td>H</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>["1"]</td>
      <td>["x,x-y-1,-z"]</td>
      <td>["6_545"]</td>
      <td>H</td>
      <td>False</td>
      <td>author_defined_assembly</td>
    </tr>
    <tr>
      <th>21</th>
      <td>3hl2</td>
      <td>3</td>
      <td>bound</td>
      <td>B</td>
      <td>I</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>["1"]</td>
      <td>["x,x-y-1,-z"]</td>
      <td>["6_545"]</td>
      <td>I</td>
      <td>False</td>
      <td>author_defined_assembly</td>
    </tr>
    <tr>
      <th>22</th>
      <td>3hl2</td>
      <td>5</td>
      <td>bound</td>
      <td>B</td>
      <td>J</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>["1"]</td>
      <td>["x,x-y-1,-z"]</td>
      <td>["6_545"]</td>
      <td>J</td>
      <td>False</td>
      <td>author_defined_assembly</td>
    </tr>
    <tr>
      <th>23</th>
      <td>3hl2</td>
      <td>5</td>
      <td>bound</td>
      <td>B</td>
      <td>K</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>["1"]</td>
      <td>["x,x-y-1,-z"]</td>
      <td>["6_545"]</td>
      <td>K</td>
      <td>False</td>
      <td>author_defined_assembly</td>
    </tr>
    <tr>
      <th>24</th>
      <td>3hl2</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>A</td>
      <td>A</td>
      <td>1</td>
      <td>2</td>
      <td>2</td>
      <td>["2"]</td>
      <td>["x,y,z"]</td>
      <td>["1_555"]</td>
      <td>AA</td>
      <td>False</td>
      <td>author_defined_assembly</td>
    </tr>
    <tr>
      <th>25</th>
      <td>3hl2</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>B</td>
      <td>B</td>
      <td>1</td>
      <td>2</td>
      <td>2</td>
      <td>["2"]</td>
      <td>["x,y,z"]</td>
      <td>["1_555"]</td>
      <td>BA</td>
      <td>False</td>
      <td>author_defined_assembly</td>
    </tr>
    <tr>
      <th>26</th>
      <td>3hl2</td>
      <td>2</td>
      <td>polyribonucleotide</td>
      <td>E</td>
      <td>E</td>
      <td>1</td>
      <td>2</td>
      <td>1</td>
      <td>["2"]</td>
      <td>["x,y,z"]</td>
      <td>["1_555"]</td>
      <td>E</td>
      <td>False</td>
      <td>author_defined_assembly</td>
    </tr>
    <tr>
      <th>27</th>
      <td>3hl2</td>
      <td>3</td>
      <td>bound</td>
      <td>A</td>
      <td>F</td>
      <td>1</td>
      <td>2</td>
      <td>2</td>
      <td>["2"]</td>
      <td>["x,y,z"]</td>
      <td>["1_555"]</td>
      <td>FA</td>
      <td>False</td>
      <td>author_defined_assembly</td>
    </tr>
    <tr>
      <th>28</th>
      <td>3hl2</td>
      <td>4</td>
      <td>bound</td>
      <td>A</td>
      <td>G</td>
      <td>1</td>
      <td>2</td>
      <td>2</td>
      <td>["2"]</td>
      <td>["x,y,z"]</td>
      <td>["1_555"]</td>
      <td>GA</td>
      <td>False</td>
      <td>author_defined_assembly</td>
    </tr>
    <tr>
      <th>29</th>
      <td>3hl2</td>
      <td>4</td>
      <td>bound</td>
      <td>A</td>
      <td>H</td>
      <td>1</td>
      <td>2</td>
      <td>2</td>
      <td>["2"]</td>
      <td>["x,y,z"]</td>
      <td>["1_555"]</td>
      <td>HA</td>
      <td>False</td>
      <td>author_defined_assembly</td>
    </tr>
    <tr>
      <th>30</th>
      <td>3hl2</td>
      <td>3</td>
      <td>bound</td>
      <td>B</td>
      <td>I</td>
      <td>1</td>
      <td>2</td>
      <td>2</td>
      <td>["2"]</td>
      <td>["x,y,z"]</td>
      <td>["1_555"]</td>
      <td>IA</td>
      <td>False</td>
      <td>author_defined_assembly</td>
    </tr>
    <tr>
      <th>31</th>
      <td>3hl2</td>
      <td>5</td>
      <td>bound</td>
      <td>B</td>
      <td>J</td>
      <td>1</td>
      <td>2</td>
      <td>2</td>
      <td>["2"]</td>
      <td>["x,y,z"]</td>
      <td>["1_555"]</td>
      <td>JA</td>
      <td>False</td>
      <td>author_defined_assembly</td>
    </tr>
    <tr>
      <th>32</th>
      <td>3hl2</td>
      <td>5</td>
      <td>bound</td>
      <td>B</td>
      <td>K</td>
      <td>1</td>
      <td>2</td>
      <td>2</td>
      <td>["2"]</td>
      <td>["x,y,z"]</td>
      <td>["1_555"]</td>
      <td>KA</td>
      <td>False</td>
      <td>author_defined_assembly</td>
    </tr>
    <tr>
      <th>33</th>
      <td>3hl2</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>C</td>
      <td>C</td>
      <td>2</td>
      <td>1</td>
      <td>1</td>
      <td>["3"]</td>
      <td>["-x+y,y,-z+1/3"]</td>
      <td>["5_555"]</td>
      <td>C</td>
      <td>False</td>
      <td>author_defined_assembly</td>
    </tr>
    <tr>
      <th>34</th>
      <td>3hl2</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>D</td>
      <td>D</td>
      <td>2</td>
      <td>1</td>
      <td>1</td>
      <td>["3"]</td>
      <td>["-x+y,y,-z+1/3"]</td>
      <td>["5_555"]</td>
      <td>D</td>
      <td>False</td>
      <td>author_defined_assembly</td>
    </tr>
    <tr>
      <th>35</th>
      <td>3hl2</td>
      <td>3</td>
      <td>bound</td>
      <td>C</td>
      <td>L</td>
      <td>2</td>
      <td>1</td>
      <td>1</td>
      <td>["3"]</td>
      <td>["-x+y,y,-z+1/3"]</td>
      <td>["5_555"]</td>
      <td>L</td>
      <td>False</td>
      <td>author_defined_assembly</td>
    </tr>
    <tr>
      <th>36</th>
      <td>3hl2</td>
      <td>4</td>
      <td>bound</td>
      <td>C</td>
      <td>M</td>
      <td>2</td>
      <td>1</td>
      <td>1</td>
      <td>["3"]</td>
      <td>["-x+y,y,-z+1/3"]</td>
      <td>["5_555"]</td>
      <td>M</td>
      <td>False</td>
      <td>author_defined_assembly</td>
    </tr>
    <tr>
      <th>37</th>
      <td>3hl2</td>
      <td>3</td>
      <td>bound</td>
      <td>D</td>
      <td>N</td>
      <td>2</td>
      <td>1</td>
      <td>1</td>
      <td>["3"]</td>
      <td>["-x+y,y,-z+1/3"]</td>
      <td>["5_555"]</td>
      <td>N</td>
      <td>False</td>
      <td>author_defined_assembly</td>
    </tr>
    <tr>
      <th>38</th>
      <td>3hl2</td>
      <td>5</td>
      <td>bound</td>
      <td>D</td>
      <td>O</td>
      <td>2</td>
      <td>1</td>
      <td>1</td>
      <td>["3"]</td>
      <td>["-x+y,y,-z+1/3"]</td>
      <td>["5_555"]</td>
      <td>O</td>
      <td>False</td>
      <td>author_defined_assembly</td>
    </tr>
    <tr>
      <th>39</th>
      <td>3hl2</td>
      <td>5</td>
      <td>bound</td>
      <td>D</td>
      <td>P</td>
      <td>2</td>
      <td>1</td>
      <td>1</td>
      <td>["3"]</td>
      <td>["-x+y,y,-z+1/3"]</td>
      <td>["5_555"]</td>
      <td>P</td>
      <td>False</td>
      <td>author_defined_assembly</td>
    </tr>
    <tr>
      <th>40</th>
      <td>3hl2</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>C</td>
      <td>C</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>["2"]</td>
      <td>["x,y,z"]</td>
      <td>["1_555"]</td>
      <td>CA</td>
      <td>False</td>
      <td>author_defined_assembly</td>
    </tr>
    <tr>
      <th>41</th>
      <td>3hl2</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>D</td>
      <td>D</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>["2"]</td>
      <td>["x,y,z"]</td>
      <td>["1_555"]</td>
      <td>DA</td>
      <td>False</td>
      <td>author_defined_assembly</td>
    </tr>
    <tr>
      <th>42</th>
      <td>3hl2</td>
      <td>2</td>
      <td>polyribonucleotide</td>
      <td>E</td>
      <td>E</td>
      <td>2</td>
      <td>2</td>
      <td>1</td>
      <td>["2"]</td>
      <td>["x,y,z"]</td>
      <td>["1_555"]</td>
      <td>E</td>
      <td>False</td>
      <td>author_defined_assembly</td>
    </tr>
    <tr>
      <th>43</th>
      <td>3hl2</td>
      <td>3</td>
      <td>bound</td>
      <td>C</td>
      <td>L</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>["2"]</td>
      <td>["x,y,z"]</td>
      <td>["1_555"]</td>
      <td>LA</td>
      <td>False</td>
      <td>author_defined_assembly</td>
    </tr>
    <tr>
      <th>44</th>
      <td>3hl2</td>
      <td>4</td>
      <td>bound</td>
      <td>C</td>
      <td>M</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>["2"]</td>
      <td>["x,y,z"]</td>
      <td>["1_555"]</td>
      <td>MA</td>
      <td>False</td>
      <td>author_defined_assembly</td>
    </tr>
    <tr>
      <th>45</th>
      <td>3hl2</td>
      <td>3</td>
      <td>bound</td>
      <td>D</td>
      <td>N</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>["2"]</td>
      <td>["x,y,z"]</td>
      <td>["1_555"]</td>
      <td>NA</td>
      <td>False</td>
      <td>author_defined_assembly</td>
    </tr>
    <tr>
      <th>46</th>
      <td>3hl2</td>
      <td>5</td>
      <td>bound</td>
      <td>D</td>
      <td>O</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>["2"]</td>
      <td>["x,y,z"]</td>
      <td>["1_555"]</td>
      <td>OA</td>
      <td>False</td>
      <td>author_defined_assembly</td>
    </tr>
    <tr>
      <th>47</th>
      <td>3hl2</td>
      <td>5</td>
      <td>bound</td>
      <td>D</td>
      <td>P</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>["2"]</td>
      <td>["x,y,z"]</td>
      <td>["1_555"]</td>
      <td>PA</td>
      <td>False</td>
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

对于PISA资源中定义的Interface，`pdb-profiling`也提供了Interface的相应类`PDBInterface`，可通过如下方式获取到PDBAssemble的相关Interface:

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

{{% callout note %}}
注意: 上面这两行代码一旦运行过就再也不用运行，就算是重新开启python进程也是。因为上述代码是下载文件与准备数据库步骤。
{{% /callout %}}

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
      <th>UniProt</th>
      <th>chain_id</th>
      <th>entity_id</th>
      <th>identity</th>
      <th>is_canonical</th>
      <th>pdb_id</th>
      <th>struct_asym_id</th>
      <th>pdb_range</th>
      <th>unp_range</th>
      <th>Entry</th>
      <th>...</th>
      <th>resolution</th>
      <th>experimental_method_class</th>
      <th>experimental_method</th>
      <th>multi_method</th>
      <th>revision_date</th>
      <th>deposition_date</th>
      <th>1/resolution</th>
      <th>id_score</th>
      <th>select_tag</th>
      <th>select_rank</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>P21359-2</td>
      <td>A</td>
      <td>1</td>
      <td>1.00</td>
      <td>False</td>
      <td>1nf1</td>
      <td>A</td>
      <td>[[1,333]]</td>
      <td>[[1198,1530]]</td>
      <td>P21359</td>
      <td>...</td>
      <td>2.500</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20171004</td>
      <td>19980708</td>
      <td>0.400000</td>
      <td>-65</td>
      <td>False</td>
      <td>15</td>
    </tr>
    <tr>
      <th>1</th>
      <td>P21359-2</td>
      <td>A</td>
      <td>1</td>
      <td>1.00</td>
      <td>False</td>
      <td>2d4q</td>
      <td>A</td>
      <td>[[1,257]]</td>
      <td>[[1560,1816]]</td>
      <td>P21359</td>
      <td>...</td>
      <td>2.300</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20110713</td>
      <td>20051022</td>
      <td>0.434783</td>
      <td>-65</td>
      <td>False</td>
      <td>4</td>
    </tr>
    <tr>
      <th>2</th>
      <td>P21359-2</td>
      <td>B</td>
      <td>1</td>
      <td>1.00</td>
      <td>False</td>
      <td>2d4q</td>
      <td>B</td>
      <td>[[1,257]]</td>
      <td>[[1560,1816]]</td>
      <td>P21359</td>
      <td>...</td>
      <td>2.300</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20110713</td>
      <td>20051022</td>
      <td>0.434783</td>
      <td>-66</td>
      <td>False</td>
      <td>6</td>
    </tr>
    <tr>
      <th>3</th>
      <td>P21359-2</td>
      <td>A</td>
      <td>1</td>
      <td>0.99</td>
      <td>False</td>
      <td>2e2x</td>
      <td>A</td>
      <td>[[6,277]]</td>
      <td>[[1545,1816]]</td>
      <td>P21359</td>
      <td>...</td>
      <td>2.500</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20110713</td>
      <td>20061118</td>
      <td>0.400000</td>
      <td>-65</td>
      <td>False</td>
      <td>12</td>
    </tr>
    <tr>
      <th>4</th>
      <td>P21359-2</td>
      <td>B</td>
      <td>1</td>
      <td>0.99</td>
      <td>False</td>
      <td>2e2x</td>
      <td>B</td>
      <td>[[6,277]]</td>
      <td>[[1545,1816]]</td>
      <td>P21359</td>
      <td>...</td>
      <td>2.500</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20110713</td>
      <td>20061118</td>
      <td>0.400000</td>
      <td>-66</td>
      <td>False</td>
      <td>13</td>
    </tr>
    <tr>
      <th>5</th>
      <td>P21359-2</td>
      <td>A</td>
      <td>1</td>
      <td>0.98</td>
      <td>False</td>
      <td>3p7z</td>
      <td>A</td>
      <td>[[5,276]]</td>
      <td>[[1545,1816]]</td>
      <td>P21359</td>
      <td>...</td>
      <td>2.650</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20190717</td>
      <td>20101013</td>
      <td>0.377358</td>
      <td>-65</td>
      <td>False</td>
      <td>5</td>
    </tr>
    <tr>
      <th>6</th>
      <td>P21359-2</td>
      <td>B</td>
      <td>1</td>
      <td>0.98</td>
      <td>False</td>
      <td>3p7z</td>
      <td>B</td>
      <td>[[5,276]]</td>
      <td>[[1545,1816]]</td>
      <td>P21359</td>
      <td>...</td>
      <td>2.650</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20190717</td>
      <td>20101013</td>
      <td>0.377358</td>
      <td>-66</td>
      <td>True</td>
      <td>2</td>
    </tr>
    <tr>
      <th>7</th>
      <td>P21359-2</td>
      <td>A</td>
      <td>1</td>
      <td>1.00</td>
      <td>False</td>
      <td>3pg7</td>
      <td>A</td>
      <td>[[1,256]]</td>
      <td>[[1560,1816]]</td>
      <td>P21359</td>
      <td>...</td>
      <td>2.189</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20110713</td>
      <td>20101031</td>
      <td>0.456830</td>
      <td>-65</td>
      <td>False</td>
      <td>7</td>
    </tr>
    <tr>
      <th>8</th>
      <td>P21359-2</td>
      <td>B</td>
      <td>1</td>
      <td>1.00</td>
      <td>False</td>
      <td>3pg7</td>
      <td>B</td>
      <td>[[1,256]]</td>
      <td>[[1560,1816]]</td>
      <td>P21359</td>
      <td>...</td>
      <td>2.189</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20110713</td>
      <td>20101031</td>
      <td>0.456830</td>
      <td>-66</td>
      <td>False</td>
      <td>8</td>
    </tr>
    <tr>
      <th>9</th>
      <td>P21359-2</td>
      <td>B</td>
      <td>2</td>
      <td>1.00</td>
      <td>False</td>
      <td>6ob2</td>
      <td>B</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>P21359</td>
      <td>...</td>
      <td>2.845</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20191113</td>
      <td>20190319</td>
      <td>0.351494</td>
      <td>-66</td>
      <td>False</td>
      <td>14</td>
    </tr>
    <tr>
      <th>10</th>
      <td>P21359-2</td>
      <td>D</td>
      <td>2</td>
      <td>1.00</td>
      <td>False</td>
      <td>6ob2</td>
      <td>D</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>P21359</td>
      <td>...</td>
      <td>2.845</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20191113</td>
      <td>20190319</td>
      <td>0.351494</td>
      <td>-68</td>
      <td>False</td>
      <td>9</td>
    </tr>
    <tr>
      <th>11</th>
      <td>P21359-2</td>
      <td>B</td>
      <td>2</td>
      <td>1.00</td>
      <td>False</td>
      <td>6ob3</td>
      <td>B</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>P21359</td>
      <td>...</td>
      <td>2.100</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20191113</td>
      <td>20190319</td>
      <td>0.476190</td>
      <td>-66</td>
      <td>False</td>
      <td>11</td>
    </tr>
    <tr>
      <th>12</th>
      <td>P21359-2</td>
      <td>D</td>
      <td>2</td>
      <td>1.00</td>
      <td>False</td>
      <td>6ob3</td>
      <td>D</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>P21359</td>
      <td>...</td>
      <td>2.100</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20191113</td>
      <td>20190319</td>
      <td>0.476190</td>
      <td>-68</td>
      <td>False</td>
      <td>10</td>
    </tr>
    <tr>
      <th>13</th>
      <td>P21359-2</td>
      <td>B</td>
      <td>2</td>
      <td>1.00</td>
      <td>False</td>
      <td>6v65</td>
      <td>B</td>
      <td>[[2,329]]</td>
      <td>[[1203,1530]]</td>
      <td>P21359</td>
      <td>...</td>
      <td>2.763</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20200805</td>
      <td>20191204</td>
      <td>0.361925</td>
      <td>-66</td>
      <td>False</td>
      <td>3</td>
    </tr>
    <tr>
      <th>14</th>
      <td>P21359-2</td>
      <td>B</td>
      <td>2</td>
      <td>1.00</td>
      <td>False</td>
      <td>6v6f</td>
      <td>B</td>
      <td>[[2,329]]</td>
      <td>[[1203,1530]]</td>
      <td>P21359</td>
      <td>...</td>
      <td>2.542</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20200805</td>
      <td>20191205</td>
      <td>0.393391</td>
      <td>-66</td>
      <td>True</td>
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
      <th>chain_id_2</th>
      <th>struct_asym_id_2</th>
      <th>struct_asym_id_in_assembly_2</th>
      <th>asym_id_rank_2</th>
      <th>model_id_2</th>
      <th>molecule_type_2</th>
      <th>surface_range_2</th>
      <th>interface_range_2</th>
      <th>pdb_id</th>
      <th>assembly_id</th>
      <th>interface_id</th>
      <th>use_au</th>
      <th>UniProt_1</th>
      <th>identity_1</th>
      <th>is_canonical_1</th>
      <th>pdb_range_1</th>
      <th>unp_range_1</th>
      <th>Entry_1</th>
      <th>range_diff_1</th>
      <th>sifts_range_tag_1</th>
      <th>repeated_1</th>
      <th>reversed_1</th>
      <th>InDel_sum_1</th>
      <th>new_pdb_range_1</th>
      <th>new_unp_range_1</th>
      <th>conflict_pdb_index_1</th>
      <th>conflict_pdb_range_1</th>
      <th>conflict_unp_range_1</th>
      <th>unp_len_1</th>
      <th>BINDING_LIGAND_COUNT_1</th>
      <th>BINDING_LIGAND_INDEX_1</th>
      <th>OBS_COUNT_1</th>
      <th>OBS_INDEX_1</th>
      <th>OBS_RATIO_SUM_1</th>
      <th>ARTIFACT_INDEX_1</th>
      <th>NON_COUNT_1</th>
      <th>NON_INDEX_1</th>
      <th>SEQRES_COUNT_1</th>
      <th>STD_COUNT_1</th>
      <th>STD_INDEX_1</th>
      <th>UNK_COUNT_1</th>
      <th>UNK_INDEX_1</th>
      <th>ca_p_only_1</th>
      <th>OBS_STD_INDEX_1</th>
      <th>OBS_STD_COUNT_1</th>
      <th>RAW_BS_1</th>
      <th>RAW_BS_IG3_1</th>
      <th>resolution</th>
      <th>experimental_method_class</th>
      <th>experimental_method</th>
      <th>multi_method</th>
      <th>revision_date</th>
      <th>deposition_date</th>
      <th>1/resolution</th>
      <th>id_score_1</th>
      <th>select_tag_1</th>
      <th>select_rank_1</th>
      <th>UniProt_2</th>
      <th>identity_2</th>
      <th>is_canonical_2</th>
      <th>pdb_range_2</th>
      <th>unp_range_2</th>
      <th>Entry_2</th>
      <th>range_diff_2</th>
      <th>sifts_range_tag_2</th>
      <th>repeated_2</th>
      <th>reversed_2</th>
      <th>InDel_sum_2</th>
      <th>new_pdb_range_2</th>
      <th>new_unp_range_2</th>
      <th>conflict_pdb_index_2</th>
      <th>conflict_pdb_range_2</th>
      <th>conflict_unp_range_2</th>
      <th>unp_len_2</th>
      <th>BINDING_LIGAND_COUNT_2</th>
      <th>BINDING_LIGAND_INDEX_2</th>
      <th>OBS_COUNT_2</th>
      <th>OBS_INDEX_2</th>
      <th>OBS_RATIO_SUM_2</th>
      <th>ARTIFACT_INDEX_2</th>
      <th>NON_COUNT_2</th>
      <th>NON_INDEX_2</th>
      <th>SEQRES_COUNT_2</th>
      <th>STD_COUNT_2</th>
      <th>STD_INDEX_2</th>
      <th>UNK_COUNT_2</th>
      <th>UNK_INDEX_2</th>
      <th>ca_p_only_2</th>
      <th>OBS_STD_INDEX_2</th>
      <th>OBS_STD_COUNT_2</th>
      <th>RAW_BS_2</th>
      <th>RAW_BS_IG3_2</th>
      <th>id_score_2</th>
      <th>select_tag_2</th>
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
      <td>[[1,11],[13,25],[27,28],[30,42],[44,236],[238,...</td>
      <td>[[31,32],[34,34],[67,67],[72,72],[148,149],[15...</td>
      <td>1</td>
      <td>B</td>
      <td>B</td>
      <td>B</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[1,24],[28,28],[30,63],[65,65],[67,120],[123,...</td>
      <td>[[10,10],[31,32],[34,34],[67,67],[72,72],[148,...</td>
      <td>2d4q</td>
      <td>0</td>
      <td>3</td>
      <td>False</td>
      <td>P21359-2</td>
      <td>1.00</td>
      <td>False</td>
      <td>[[1,257]]</td>
      <td>[[1560,1816]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[1,257]]</td>
      <td>[[1560,1816]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2818</td>
      <td>12</td>
      <td>[[61, 61], [73, 76], [82, 82], [86, 86], [107,...</td>
      <td>257</td>
      <td>[[1, 257]]</td>
      <td>257.000</td>
      <td>[]</td>
      <td>0</td>
      <td>[]</td>
      <td>257</td>
      <td>257</td>
      <td>[[1, 257]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((1, 257),)</td>
      <td>257</td>
      <td>0.086941</td>
      <td>0.091199</td>
      <td>2.300</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20110713</td>
      <td>20051022</td>
      <td>0.434783</td>
      <td>-65</td>
      <td>False</td>
      <td>4</td>
      <td>P21359-2</td>
      <td>1.00</td>
      <td>False</td>
      <td>[[1,257]]</td>
      <td>[[1560,1816]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[1,257]]</td>
      <td>[[1560,1816]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2818</td>
      <td>11</td>
      <td>[[28, 28], [63, 63], [73, 76], [107, 107], [10...</td>
      <td>255</td>
      <td>[[1, 120], [123, 257]]</td>
      <td>254.009</td>
      <td>[]</td>
      <td>0</td>
      <td>[]</td>
      <td>257</td>
      <td>257</td>
      <td>[[1, 257]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((1, 120), (123, 257))</td>
      <td>255</td>
      <td>0.085315</td>
      <td>0.089219</td>
      <td>-66</td>
      <td>False</td>
      <td>6</td>
      <td>False</td>
      <td>1.0</td>
      <td>0.250000</td>
      <td>0.166667</td>
      <td>((1590, 1591), (1593, 1593), (1626, 1626), (16...</td>
      <td>((1569, 1569), (1590, 1591), (1593, 1593), (16...</td>
      <td>(P21359-2, P21359-2)</td>
      <td>False</td>
      <td>4</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>A</td>
      <td>A</td>
      <td>A</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[1,11],[13,25],[27,28],[30,42],[44,236],[238,...</td>
      <td>[[31,32],[34,34],[67,67],[72,72],[148,149],[15...</td>
      <td>1</td>
      <td>B</td>
      <td>B</td>
      <td>B</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[1,24],[28,28],[30,63],[65,65],[67,120],[123,...</td>
      <td>[[10,10],[31,32],[34,34],[67,67],[72,72],[148,...</td>
      <td>2d4q</td>
      <td>1</td>
      <td>3</td>
      <td>True</td>
      <td>P21359-2</td>
      <td>1.00</td>
      <td>False</td>
      <td>[[1,257]]</td>
      <td>[[1560,1816]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[1,257]]</td>
      <td>[[1560,1816]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2818</td>
      <td>12</td>
      <td>[[61, 61], [73, 76], [82, 82], [86, 86], [107,...</td>
      <td>257</td>
      <td>[[1, 257]]</td>
      <td>257.000</td>
      <td>[]</td>
      <td>0</td>
      <td>[]</td>
      <td>257</td>
      <td>257</td>
      <td>[[1, 257]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((1, 257),)</td>
      <td>257</td>
      <td>0.086941</td>
      <td>0.091199</td>
      <td>2.300</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20110713</td>
      <td>20051022</td>
      <td>0.434783</td>
      <td>-65</td>
      <td>False</td>
      <td>4</td>
      <td>P21359-2</td>
      <td>1.00</td>
      <td>False</td>
      <td>[[1,257]]</td>
      <td>[[1560,1816]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[1,257]]</td>
      <td>[[1560,1816]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2818</td>
      <td>11</td>
      <td>[[28, 28], [63, 63], [73, 76], [107, 107], [10...</td>
      <td>255</td>
      <td>[[1, 120], [123, 257]]</td>
      <td>254.009</td>
      <td>[]</td>
      <td>0</td>
      <td>[]</td>
      <td>257</td>
      <td>257</td>
      <td>[[1, 257]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((1, 120), (123, 257))</td>
      <td>255</td>
      <td>0.085315</td>
      <td>0.089219</td>
      <td>-66</td>
      <td>False</td>
      <td>6</td>
      <td>True</td>
      <td>1.0</td>
      <td>0.250000</td>
      <td>0.166667</td>
      <td>((1590, 1591), (1593, 1593), (1626, 1626), (16...</td>
      <td>((1569, 1569), (1590, 1591), (1593, 1593), (16...</td>
      <td>(P21359-2, P21359-2)</td>
      <td>True</td>
      <td>3</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>A</td>
      <td>A</td>
      <td>A</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[28,44],[47,48],[50,52],[54,62],[64,81],[83,8...</td>
      <td>[[51,52],[54,54],[87,87],[92,92],[168,169],[17...</td>
      <td>1</td>
      <td>B</td>
      <td>B</td>
      <td>B</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[28,44],[48,48],[50,62],[64,81],[83,83],[85,8...</td>
      <td>[[51,52],[54,54],[87,87],[92,92],[168,169],[17...</td>
      <td>2e2x</td>
      <td>0</td>
      <td>5</td>
      <td>False</td>
      <td>P21359-2</td>
      <td>0.99</td>
      <td>False</td>
      <td>[[6,277]]</td>
      <td>[[1545,1816]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[6,277]]</td>
      <td>[[1545,1816]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2818</td>
      <td>0</td>
      <td>[]</td>
      <td>250</td>
      <td>[[28, 277]]</td>
      <td>248.894</td>
      <td>[[1, 5]]</td>
      <td>0</td>
      <td>[]</td>
      <td>277</td>
      <td>277</td>
      <td>[[1, 277]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((28, 277),)</td>
      <td>250</td>
      <td>0.074735</td>
      <td>0.074735</td>
      <td>2.500</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20110713</td>
      <td>20061118</td>
      <td>0.400000</td>
      <td>-65</td>
      <td>False</td>
      <td>12</td>
      <td>P21359-2</td>
      <td>0.99</td>
      <td>False</td>
      <td>[[6,277]]</td>
      <td>[[1545,1816]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[6,277]]</td>
      <td>[[1545,1816]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2818</td>
      <td>0</td>
      <td>[]</td>
      <td>250</td>
      <td>[[28, 277]]</td>
      <td>249.180</td>
      <td>[[1, 5]]</td>
      <td>0</td>
      <td>[]</td>
      <td>277</td>
      <td>277</td>
      <td>[[1, 277]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((28, 277),)</td>
      <td>250</td>
      <td>0.074735</td>
      <td>0.074735</td>
      <td>-66</td>
      <td>False</td>
      <td>13</td>
      <td>False</td>
      <td>1.0</td>
      <td>0.083333</td>
      <td>0.076923</td>
      <td>((1590, 1591), (1593, 1593), (1626, 1626), (16...</td>
      <td>((1590, 1591), (1593, 1593), (1626, 1626), (16...</td>
      <td>(P21359-2, P21359-2)</td>
      <td>False</td>
      <td>9</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
      <td>A</td>
      <td>A</td>
      <td>A</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[28,44],[47,48],[50,52],[54,62],[64,81],[83,8...</td>
      <td>[[51,52],[54,54],[87,87],[92,92],[168,169],[17...</td>
      <td>1</td>
      <td>B</td>
      <td>B</td>
      <td>B</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[28,44],[48,48],[50,62],[64,81],[83,83],[85,8...</td>
      <td>[[51,52],[54,54],[87,87],[92,92],[168,169],[17...</td>
      <td>2e2x</td>
      <td>1</td>
      <td>5</td>
      <td>True</td>
      <td>P21359-2</td>
      <td>0.99</td>
      <td>False</td>
      <td>[[6,277]]</td>
      <td>[[1545,1816]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[6,277]]</td>
      <td>[[1545,1816]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2818</td>
      <td>0</td>
      <td>[]</td>
      <td>250</td>
      <td>[[28, 277]]</td>
      <td>248.894</td>
      <td>[[1, 5]]</td>
      <td>0</td>
      <td>[]</td>
      <td>277</td>
      <td>277</td>
      <td>[[1, 277]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((28, 277),)</td>
      <td>250</td>
      <td>0.074735</td>
      <td>0.074735</td>
      <td>2.500</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20110713</td>
      <td>20061118</td>
      <td>0.400000</td>
      <td>-65</td>
      <td>False</td>
      <td>12</td>
      <td>P21359-2</td>
      <td>0.99</td>
      <td>False</td>
      <td>[[6,277]]</td>
      <td>[[1545,1816]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[6,277]]</td>
      <td>[[1545,1816]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2818</td>
      <td>0</td>
      <td>[]</td>
      <td>250</td>
      <td>[[28, 277]]</td>
      <td>249.180</td>
      <td>[[1, 5]]</td>
      <td>0</td>
      <td>[]</td>
      <td>277</td>
      <td>277</td>
      <td>[[1, 277]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((28, 277),)</td>
      <td>250</td>
      <td>0.074735</td>
      <td>0.074735</td>
      <td>-66</td>
      <td>False</td>
      <td>13</td>
      <td>True</td>
      <td>1.0</td>
      <td>0.083333</td>
      <td>0.076923</td>
      <td>((1590, 1591), (1593, 1593), (1626, 1626), (16...</td>
      <td>((1590, 1591), (1593, 1593), (1626, 1626), (16...</td>
      <td>(P21359-2, P21359-2)</td>
      <td>False</td>
      <td>8</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1</td>
      <td>A</td>
      <td>A</td>
      <td>A</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[7,44],[46,47],[49,62],[64,82],[84,84],[86,25...</td>
      <td>[[50,51],[53,53],[86,86],[91,91],[167,168],[17...</td>
      <td>1</td>
      <td>B</td>
      <td>B</td>
      <td>B</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[7,43],[46,61],[63,80],[82,84],[86,157],[159,...</td>
      <td>[[50,51],[53,53],[86,86],[91,91],[167,168],[17...</td>
      <td>3p7z</td>
      <td>0</td>
      <td>5</td>
      <td>False</td>
      <td>P21359-2</td>
      <td>0.98</td>
      <td>False</td>
      <td>[[5,276]]</td>
      <td>[[1545,1816]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[5,276]]</td>
      <td>[[1545,1816]]</td>
      <td>{"44":"I"}</td>
      <td>[[44,44]]</td>
      <td>[[1584,1584]]</td>
      <td>2818</td>
      <td>23</td>
      <td>[[40, 42], [47, 47], [66, 66], [70, 70], [78, ...</td>
      <td>270</td>
      <td>[[7, 276]]</td>
      <td>267.845</td>
      <td>[[1, 4]]</td>
      <td>0</td>
      <td>[]</td>
      <td>276</td>
      <td>276</td>
      <td>[[1, 276]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((7, 276),)</td>
      <td>270</td>
      <td>0.086380</td>
      <td>0.094542</td>
      <td>2.650</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20190717</td>
      <td>20101013</td>
      <td>0.377358</td>
      <td>-65</td>
      <td>False</td>
      <td>5</td>
      <td>P21359-2</td>
      <td>0.98</td>
      <td>False</td>
      <td>[[5,276]]</td>
      <td>[[1545,1816]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[5,276]]</td>
      <td>[[1545,1816]]</td>
      <td>{"44":"I"}</td>
      <td>[[44,44]]</td>
      <td>[[1584,1584]]</td>
      <td>2818</td>
      <td>16</td>
      <td>[[80, 80], [92, 95], [101, 102], [110, 110], [...</td>
      <td>270</td>
      <td>[[7, 276]]</td>
      <td>269.180</td>
      <td>[[1, 4]]</td>
      <td>0</td>
      <td>[]</td>
      <td>276</td>
      <td>276</td>
      <td>[[1, 276]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((7, 276),)</td>
      <td>270</td>
      <td>0.088864</td>
      <td>0.094542</td>
      <td>-66</td>
      <td>True</td>
      <td>2</td>
      <td>False</td>
      <td>1.0</td>
      <td>0.500000</td>
      <td>0.200000</td>
      <td>((1590, 1591), (1593, 1593), (1626, 1626), (16...</td>
      <td>((1590, 1591), (1593, 1593), (1626, 1626), (16...</td>
      <td>(P21359-2, P21359-2)</td>
      <td>False</td>
      <td>2</td>
    </tr>
    <tr>
      <th>5</th>
      <td>1</td>
      <td>A</td>
      <td>A</td>
      <td>A</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[7,44],[46,47],[49,62],[64,82],[84,84],[86,25...</td>
      <td>[[50,51],[53,53],[86,86],[91,91],[167,168],[17...</td>
      <td>1</td>
      <td>B</td>
      <td>B</td>
      <td>B</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[7,43],[46,61],[63,80],[82,84],[86,157],[159,...</td>
      <td>[[50,51],[53,53],[86,86],[91,91],[167,168],[17...</td>
      <td>3p7z</td>
      <td>1</td>
      <td>5</td>
      <td>True</td>
      <td>P21359-2</td>
      <td>0.98</td>
      <td>False</td>
      <td>[[5,276]]</td>
      <td>[[1545,1816]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[5,276]]</td>
      <td>[[1545,1816]]</td>
      <td>{"44":"I"}</td>
      <td>[[44,44]]</td>
      <td>[[1584,1584]]</td>
      <td>2818</td>
      <td>23</td>
      <td>[[40, 42], [47, 47], [66, 66], [70, 70], [78, ...</td>
      <td>270</td>
      <td>[[7, 276]]</td>
      <td>267.845</td>
      <td>[[1, 4]]</td>
      <td>0</td>
      <td>[]</td>
      <td>276</td>
      <td>276</td>
      <td>[[1, 276]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((7, 276),)</td>
      <td>270</td>
      <td>0.086380</td>
      <td>0.094542</td>
      <td>2.650</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20190717</td>
      <td>20101013</td>
      <td>0.377358</td>
      <td>-65</td>
      <td>False</td>
      <td>5</td>
      <td>P21359-2</td>
      <td>0.98</td>
      <td>False</td>
      <td>[[5,276]]</td>
      <td>[[1545,1816]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[5,276]]</td>
      <td>[[1545,1816]]</td>
      <td>{"44":"I"}</td>
      <td>[[44,44]]</td>
      <td>[[1584,1584]]</td>
      <td>2818</td>
      <td>16</td>
      <td>[[80, 80], [92, 95], [101, 102], [110, 110], [...</td>
      <td>270</td>
      <td>[[7, 276]]</td>
      <td>269.180</td>
      <td>[[1, 4]]</td>
      <td>0</td>
      <td>[]</td>
      <td>276</td>
      <td>276</td>
      <td>[[1, 276]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((7, 276),)</td>
      <td>270</td>
      <td>0.088864</td>
      <td>0.094542</td>
      <td>-66</td>
      <td>True</td>
      <td>2</td>
      <td>True</td>
      <td>1.0</td>
      <td>0.500000</td>
      <td>0.200000</td>
      <td>((1590, 1591), (1593, 1593), (1626, 1626), (16...</td>
      <td>((1590, 1591), (1593, 1593), (1626, 1626), (16...</td>
      <td>(P21359-2, P21359-2)</td>
      <td>True</td>
      <td>1</td>
    </tr>
    <tr>
      <th>6</th>
      <td>1</td>
      <td>A</td>
      <td>A</td>
      <td>A</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[1,24],[28,235],[237,238],[240,256]]</td>
      <td>[[31,32],[34,34],[67,67],[72,72],[148,149],[15...</td>
      <td>1</td>
      <td>B</td>
      <td>B</td>
      <td>B</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[1,24],[28,28],[30,61],[63,63],[65,134],[136,...</td>
      <td>[[31,32],[34,34],[67,67],[72,72],[148,149],[15...</td>
      <td>3pg7</td>
      <td>0</td>
      <td>4</td>
      <td>False</td>
      <td>P21359-2</td>
      <td>1.00</td>
      <td>False</td>
      <td>[[1,256]]</td>
      <td>[[1560,1816]]</td>
      <td>P21359</td>
      <td>[1]</td>
      <td>Deletion</td>
      <td>False</td>
      <td>False</td>
      <td>1</td>
      <td>((1, 191), (192, 256))</td>
      <td>((1560, 1750), (1752, 1816))</td>
      <td>{"191":"K"}</td>
      <td>[[191,191]]</td>
      <td>[[1750,1750]]</td>
      <td>2818</td>
      <td>15</td>
      <td>[[13, 13], [28, 28], [61, 61], [73, 73], [75, ...</td>
      <td>256</td>
      <td>[[1, 256]]</td>
      <td>247.929</td>
      <td>[]</td>
      <td>0</td>
      <td>[]</td>
      <td>256</td>
      <td>256</td>
      <td>[[1, 256]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((1, 256),)</td>
      <td>256</td>
      <td>0.083881</td>
      <td>0.089204</td>
      <td>2.189</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20110713</td>
      <td>20101031</td>
      <td>0.456830</td>
      <td>-65</td>
      <td>False</td>
      <td>7</td>
      <td>P21359-2</td>
      <td>1.00</td>
      <td>False</td>
      <td>[[1,256]]</td>
      <td>[[1560,1816]]</td>
      <td>P21359</td>
      <td>[1]</td>
      <td>Deletion</td>
      <td>False</td>
      <td>False</td>
      <td>1</td>
      <td>((1, 191), (192, 256))</td>
      <td>((1560, 1750), (1752, 1816))</td>
      <td>{"191":"K"}</td>
      <td>[[191,191]]</td>
      <td>[[1750,1750]]</td>
      <td>2818</td>
      <td>17</td>
      <td>[[61, 61], [73, 74], [76, 76], [82, 83], [91, ...</td>
      <td>256</td>
      <td>[[1, 256]]</td>
      <td>249.123</td>
      <td>[]</td>
      <td>0</td>
      <td>[]</td>
      <td>256</td>
      <td>256</td>
      <td>[[1, 256]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((1, 256),)</td>
      <td>256</td>
      <td>0.083171</td>
      <td>0.089204</td>
      <td>-66</td>
      <td>False</td>
      <td>8</td>
      <td>False</td>
      <td>1.0</td>
      <td>0.142857</td>
      <td>0.125000</td>
      <td>((1590, 1591), (1593, 1593), (1626, 1626), (16...</td>
      <td>((1590, 1591), (1593, 1593), (1626, 1626), (16...</td>
      <td>(P21359-2, P21359-2)</td>
      <td>False</td>
      <td>5</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2</td>
      <td>B</td>
      <td>B</td>
      <td>B</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[12,48],[50,53],[55,73],[75,76],[78,80],[82,8...</td>
      <td>[[228,228],[231,232],[234,235],[237,238],[241,...</td>
      <td>2</td>
      <td>D</td>
      <td>D</td>
      <td>D</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[10,48],[50,53],[55,76],[79,80],[82,85],[87,9...</td>
      <td>[[91,91],[95,95],[99,99],[194,195],[197,197],[...</td>
      <td>6ob3</td>
      <td>0</td>
      <td>10</td>
      <td>False</td>
      <td>P21359-2</td>
      <td>1.00</td>
      <td>False</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2818</td>
      <td>10</td>
      <td>[[41, 41], [51, 51], [69, 69], [129, 130], [13...</td>
      <td>245</td>
      <td>[[12, 256]]</td>
      <td>241.495</td>
      <td>[[1, 1]]</td>
      <td>0</td>
      <td>[]</td>
      <td>256</td>
      <td>256</td>
      <td>[[1, 256]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((12, 256),)</td>
      <td>245</td>
      <td>0.077038</td>
      <td>0.080586</td>
      <td>2.100</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20191113</td>
      <td>20190319</td>
      <td>0.476190</td>
      <td>-66</td>
      <td>False</td>
      <td>11</td>
      <td>P21359-2</td>
      <td>1.00</td>
      <td>False</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2818</td>
      <td>7</td>
      <td>[[41, 41], [44, 44], [126, 126], [133, 133], [...</td>
      <td>247</td>
      <td>[[10, 256]]</td>
      <td>244.327</td>
      <td>[[1, 1]]</td>
      <td>0</td>
      <td>[]</td>
      <td>256</td>
      <td>256</td>
      <td>[[1, 256]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((10, 256),)</td>
      <td>247</td>
      <td>0.080083</td>
      <td>0.082567</td>
      <td>-68</td>
      <td>False</td>
      <td>10</td>
      <td>False</td>
      <td>1.0</td>
      <td>0.100000</td>
      <td>0.090909</td>
      <td>((1435, 1435), (1438, 1439), (1441, 1442), (14...</td>
      <td>((1298, 1298), (1302, 1302), (1306, 1306), (14...</td>
      <td>(P21359-2, P21359-2)</td>
      <td>True</td>
      <td>7</td>
    </tr>
    <tr>
      <th>8</th>
      <td>2</td>
      <td>B</td>
      <td>B</td>
      <td>B</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[12,48],[50,53],[55,76],[78,80],[82,85],[87,1...</td>
      <td>[[125,125],[231,231],[234,235],[237,238],[241,...</td>
      <td>2</td>
      <td>D</td>
      <td>D</td>
      <td>D</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[12,53],[55,76],[78,80],[82,85],[87,100],[102...</td>
      <td>[[99,99],[194,194],[197,197],[199,201]]</td>
      <td>6ob2</td>
      <td>0</td>
      <td>9</td>
      <td>False</td>
      <td>P21359-2</td>
      <td>1.00</td>
      <td>False</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2818</td>
      <td>8</td>
      <td>[[18, 19], [22, 22], [191, 192], [202, 202], [...</td>
      <td>241</td>
      <td>[[12, 103], [107, 255]]</td>
      <td>236.933</td>
      <td>[[1, 1]]</td>
      <td>0</td>
      <td>[]</td>
      <td>256</td>
      <td>256</td>
      <td>[[1, 256]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((12, 103), (107, 255))</td>
      <td>241</td>
      <td>0.073786</td>
      <td>0.076625</td>
      <td>2.845</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20191113</td>
      <td>20190319</td>
      <td>0.351494</td>
      <td>-66</td>
      <td>False</td>
      <td>14</td>
      <td>P21359-2</td>
      <td>1.00</td>
      <td>False</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2818</td>
      <td>0</td>
      <td>[]</td>
      <td>245</td>
      <td>[[12, 256]]</td>
      <td>239.938</td>
      <td>[[1, 1]]</td>
      <td>0</td>
      <td>[]</td>
      <td>256</td>
      <td>256</td>
      <td>[[1, 256]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((12, 256),)</td>
      <td>245</td>
      <td>0.080586</td>
      <td>0.080586</td>
      <td>-68</td>
      <td>False</td>
      <td>9</td>
      <td>False</td>
      <td>1.0</td>
      <td>0.111111</td>
      <td>0.071429</td>
      <td>((1332, 1332), (1438, 1438), (1441, 1442), (14...</td>
      <td>((1306, 1306), (1401, 1401), (1404, 1404), (14...</td>
      <td>(P21359-2, P21359-2)</td>
      <td>True</td>
      <td>6</td>
    </tr>
  </tbody>
</table>

</details>

这个过程自动完成了上面提及的reformat、打分及与PISA、Interactome3D数据资源整合等步骤，下面的`pipe_select_ho_iso,pipe_select_he`同理。

## 同聚体(isoform)代表集结构选择

```python
df3 = sifts_demo.pipe_select_ho_iso(run_as_completed=True).result()
df3
```

<details>
<summary>Click to view dataframe</summary>

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
      <th>chain_id_2</th>
      <th>struct_asym_id_2</th>
      <th>struct_asym_id_in_assembly_2</th>
      <th>asym_id_rank_2</th>
      <th>model_id_2</th>
      <th>molecule_type_2</th>
      <th>surface_range_2</th>
      <th>interface_range_2</th>
      <th>pdb_id</th>
      <th>assembly_id</th>
      <th>interface_id</th>
      <th>use_au</th>
      <th>UniProt_1</th>
      <th>identifier_1</th>
      <th>identity_1</th>
      <th>is_canonical_1</th>
      <th>name_1</th>
      <th>pdb_range_1</th>
      <th>unp_range_1</th>
      <th>Entry_1</th>
      <th>range_diff_1</th>
      <th>sifts_range_tag_1</th>
      <th>repeated_1</th>
      <th>reversed_1</th>
      <th>InDel_sum_1</th>
      <th>new_pdb_range_1</th>
      <th>new_unp_range_1</th>
      <th>conflict_pdb_index_1</th>
      <th>conflict_pdb_range_1</th>
      <th>conflict_unp_range_1</th>
      <th>unp_len_1</th>
      <th>BINDING_LIGAND_COUNT_1</th>
      <th>BINDING_LIGAND_INDEX_1</th>
      <th>OBS_COUNT_1</th>
      <th>OBS_INDEX_1</th>
      <th>OBS_RATIO_SUM_1</th>
      <th>ARTIFACT_INDEX_1</th>
      <th>NON_COUNT_1</th>
      <th>NON_INDEX_1</th>
      <th>SEQRES_COUNT_1</th>
      <th>STD_COUNT_1</th>
      <th>STD_INDEX_1</th>
      <th>UNK_COUNT_1</th>
      <th>UNK_INDEX_1</th>
      <th>ca_p_only_1</th>
      <th>OBS_STD_INDEX_1</th>
      <th>OBS_STD_COUNT_1</th>
      <th>RAW_BS_1</th>
      <th>RAW_BS_IG3_1</th>
      <th>resolution</th>
      <th>experimental_method_class</th>
      <th>experimental_method</th>
      <th>multi_method</th>
      <th>revision_date</th>
      <th>deposition_date</th>
      <th>1/resolution</th>
      <th>id_score_1</th>
      <th>select_tag_1</th>
      <th>select_rank_1</th>
      <th>UniProt_2</th>
      <th>identifier_2</th>
      <th>identity_2</th>
      <th>is_canonical_2</th>
      <th>name_2</th>
      <th>pdb_range_2</th>
      <th>unp_range_2</th>
      <th>Entry_2</th>
      <th>range_diff_2</th>
      <th>sifts_range_tag_2</th>
      <th>repeated_2</th>
      <th>reversed_2</th>
      <th>InDel_sum_2</th>
      <th>new_pdb_range_2</th>
      <th>new_unp_range_2</th>
      <th>conflict_pdb_index_2</th>
      <th>conflict_pdb_range_2</th>
      <th>conflict_unp_range_2</th>
      <th>unp_len_2</th>
      <th>BINDING_LIGAND_COUNT_2</th>
      <th>BINDING_LIGAND_INDEX_2</th>
      <th>OBS_COUNT_2</th>
      <th>OBS_INDEX_2</th>
      <th>OBS_RATIO_SUM_2</th>
      <th>ARTIFACT_INDEX_2</th>
      <th>NON_COUNT_2</th>
      <th>NON_INDEX_2</th>
      <th>SEQRES_COUNT_2</th>
      <th>STD_COUNT_2</th>
      <th>STD_INDEX_2</th>
      <th>UNK_COUNT_2</th>
      <th>UNK_INDEX_2</th>
      <th>ca_p_only_2</th>
      <th>OBS_STD_INDEX_2</th>
      <th>OBS_STD_COUNT_2</th>
      <th>RAW_BS_2</th>
      <th>RAW_BS_IG3_2</th>
      <th>id_score_2</th>
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
      <th>0</th>
      <td>1</td>
      <td>B</td>
      <td>B</td>
      <td>B</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[1,24],[28,28],[30,63],[65,65],[67,120],[123,...</td>
      <td>[[10,10],[31,32],[34,34],[67,67],[72,72],[148,...</td>
      <td>1</td>
      <td>A</td>
      <td>A</td>
      <td>A</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[1,11],[13,25],[27,28],[30,42],[44,236],[238,...</td>
      <td>[[31,32],[34,34],[67,67],[72,72],[148,149],[15...</td>
      <td>2d4q</td>
      <td>0</td>
      <td>3</td>
      <td>False</td>
      <td>P21359-2</td>
      <td>NF1_HUMAN</td>
      <td>1.00</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[1,257]]</td>
      <td>[[1560,1816]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[1,257]]</td>
      <td>[[1560,1816]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2818</td>
      <td>11</td>
      <td>[[28, 28], [63, 63], [73, 76], [107, 107], [10...</td>
      <td>255</td>
      <td>[[1, 120], [123, 257]]</td>
      <td>254.009</td>
      <td>[]</td>
      <td>0</td>
      <td>[]</td>
      <td>257</td>
      <td>257</td>
      <td>[[1, 257]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((1, 120), (123, 257))</td>
      <td>255</td>
      <td>0.085315</td>
      <td>0.089219</td>
      <td>2.300</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20110713</td>
      <td>20051022</td>
      <td>0.434783</td>
      <td>-66</td>
      <td>False</td>
      <td>6</td>
      <td>P21359</td>
      <td>NF1_HUMAN</td>
      <td>1.00</td>
      <td>True</td>
      <td>NF1_HUMAN</td>
      <td>[[1,257]]</td>
      <td>[[1581,1837]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[1,257]]</td>
      <td>[[1581,1837]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2839</td>
      <td>12</td>
      <td>[[61, 61], [73, 76], [82, 82], [86, 86], [107,...</td>
      <td>257</td>
      <td>[[1, 257]]</td>
      <td>257.000</td>
      <td>[]</td>
      <td>0</td>
      <td>[]</td>
      <td>257</td>
      <td>257</td>
      <td>[[1, 257]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((1, 257),)</td>
      <td>257</td>
      <td>0.086298</td>
      <td>0.090525</td>
      <td>-65</td>
      <td>False</td>
      <td>2</td>
      <td>False</td>
      <td>0.500000</td>
      <td>0.166667</td>
      <td>((1569, 1569), (1590, 1591), (1593, 1593), (16...</td>
      <td>((1611, 1612), (1614, 1614), (1647, 1647), (16...</td>
      <td>(P21359-2, P21359)</td>
      <td>False</td>
      <td>6</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>A</td>
      <td>A</td>
      <td>A</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[1,11],[13,25],[27,28],[30,42],[44,236],[238,...</td>
      <td>[[31,32],[34,34],[67,67],[72,72],[148,149],[15...</td>
      <td>1</td>
      <td>B</td>
      <td>B</td>
      <td>B</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[1,24],[28,28],[30,63],[65,65],[67,120],[123,...</td>
      <td>[[10,10],[31,32],[34,34],[67,67],[72,72],[148,...</td>
      <td>2d4q</td>
      <td>0</td>
      <td>3</td>
      <td>False</td>
      <td>P21359-2</td>
      <td>NF1_HUMAN</td>
      <td>1.00</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[1,257]]</td>
      <td>[[1560,1816]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[1,257]]</td>
      <td>[[1560,1816]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2818</td>
      <td>12</td>
      <td>[[61, 61], [73, 76], [82, 82], [86, 86], [107,...</td>
      <td>257</td>
      <td>[[1, 257]]</td>
      <td>257.000</td>
      <td>[]</td>
      <td>0</td>
      <td>[]</td>
      <td>257</td>
      <td>257</td>
      <td>[[1, 257]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((1, 257),)</td>
      <td>257</td>
      <td>0.086941</td>
      <td>0.091199</td>
      <td>2.300</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20110713</td>
      <td>20051022</td>
      <td>0.434783</td>
      <td>-65</td>
      <td>False</td>
      <td>4</td>
      <td>P21359</td>
      <td>NF1_HUMAN</td>
      <td>1.00</td>
      <td>True</td>
      <td>NF1_HUMAN</td>
      <td>[[1,257]]</td>
      <td>[[1581,1837]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[1,257]]</td>
      <td>[[1581,1837]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2839</td>
      <td>11</td>
      <td>[[28, 28], [63, 63], [73, 76], [107, 107], [10...</td>
      <td>255</td>
      <td>[[1, 120], [123, 257]]</td>
      <td>254.009</td>
      <td>[]</td>
      <td>0</td>
      <td>[]</td>
      <td>257</td>
      <td>257</td>
      <td>[[1, 257]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((1, 120), (123, 257))</td>
      <td>255</td>
      <td>0.084684</td>
      <td>0.088559</td>
      <td>-66</td>
      <td>False</td>
      <td>4</td>
      <td>False</td>
      <td>0.250000</td>
      <td>0.250000</td>
      <td>((1590, 1591), (1593, 1593), (1626, 1626), (16...</td>
      <td>((1590, 1590), (1611, 1612), (1614, 1614), (16...</td>
      <td>(P21359-2, P21359)</td>
      <td>False</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>A</td>
      <td>A</td>
      <td>A</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[1,11],[13,25],[27,28],[30,42],[44,236],[238,...</td>
      <td>[[31,32],[34,34],[67,67],[72,72],[148,149],[15...</td>
      <td>1</td>
      <td>B</td>
      <td>B</td>
      <td>B</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[1,24],[28,28],[30,63],[65,65],[67,120],[123,...</td>
      <td>[[10,10],[31,32],[34,34],[67,67],[72,72],[148,...</td>
      <td>2d4q</td>
      <td>0</td>
      <td>3</td>
      <td>False</td>
      <td>P21359-2</td>
      <td>NF1_HUMAN</td>
      <td>1.00</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[1,257]]</td>
      <td>[[1560,1816]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[1,257]]</td>
      <td>[[1560,1816]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2818</td>
      <td>12</td>
      <td>[[61, 61], [73, 76], [82, 82], [86, 86], [107,...</td>
      <td>257</td>
      <td>[[1, 257]]</td>
      <td>257.000</td>
      <td>[]</td>
      <td>0</td>
      <td>[]</td>
      <td>257</td>
      <td>257</td>
      <td>[[1, 257]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((1, 257),)</td>
      <td>257</td>
      <td>0.086941</td>
      <td>0.091199</td>
      <td>2.300</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20110713</td>
      <td>20051022</td>
      <td>0.434783</td>
      <td>-65</td>
      <td>False</td>
      <td>4</td>
      <td>P21359-4</td>
      <td>NF1_HUMAN</td>
      <td>0.91</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[1,11]]</td>
      <td>[[1581,1591]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[1,11]]</td>
      <td>[[1581,1591]]</td>
      <td>{"11":"T"}</td>
      <td>[[11,11]]</td>
      <td>[[1591,1591]]</td>
      <td>1598</td>
      <td>11</td>
      <td>[[28, 28], [63, 63], [73, 76], [107, 107], [10...</td>
      <td>255</td>
      <td>[[1, 120], [123, 257]]</td>
      <td>254.009</td>
      <td>[]</td>
      <td>0</td>
      <td>[]</td>
      <td>257</td>
      <td>257</td>
      <td>[[1, 257]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((1, 120), (123, 257))</td>
      <td>255</td>
      <td>-0.150814</td>
      <td>-0.143930</td>
      <td>-66</td>
      <td>False</td>
      <td>-1</td>
      <td>False</td>
      <td>-1.000000</td>
      <td>0.250000</td>
      <td>((1590, 1591), (1593, 1593), (1626, 1626), (16...</td>
      <td>((1590, 1590),)</td>
      <td>(P21359-2, P21359-4)</td>
      <td>False</td>
      <td>-1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
      <td>A</td>
      <td>A</td>
      <td>A</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[1,11],[13,25],[27,28],[30,42],[44,236],[238,...</td>
      <td>[[31,32],[34,34],[67,67],[72,72],[148,149],[15...</td>
      <td>1</td>
      <td>B</td>
      <td>B</td>
      <td>B</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[1,24],[28,28],[30,63],[65,65],[67,120],[123,...</td>
      <td>[[10,10],[31,32],[34,34],[67,67],[72,72],[148,...</td>
      <td>2d4q</td>
      <td>0</td>
      <td>3</td>
      <td>False</td>
      <td>P21359-2</td>
      <td>NF1_HUMAN</td>
      <td>1.00</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[1,257]]</td>
      <td>[[1560,1816]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[1,257]]</td>
      <td>[[1560,1816]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2818</td>
      <td>12</td>
      <td>[[61, 61], [73, 76], [82, 82], [86, 86], [107,...</td>
      <td>257</td>
      <td>[[1, 257]]</td>
      <td>257.000</td>
      <td>[]</td>
      <td>0</td>
      <td>[]</td>
      <td>257</td>
      <td>257</td>
      <td>[[1, 257]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((1, 257),)</td>
      <td>257</td>
      <td>0.086941</td>
      <td>0.091199</td>
      <td>2.300</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20110713</td>
      <td>20051022</td>
      <td>0.434783</td>
      <td>-65</td>
      <td>False</td>
      <td>4</td>
      <td>P21359-6</td>
      <td>NF1_HUMAN</td>
      <td>1.00</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[1,257]]</td>
      <td>[[1560,1816]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[1,257]]</td>
      <td>[[1560,1816]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2836</td>
      <td>11</td>
      <td>[[28, 28], [63, 63], [73, 76], [107, 107], [10...</td>
      <td>255</td>
      <td>[[1, 120], [123, 257]]</td>
      <td>254.009</td>
      <td>[]</td>
      <td>0</td>
      <td>[]</td>
      <td>257</td>
      <td>257</td>
      <td>[[1, 257]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((1, 120), (123, 257))</td>
      <td>255</td>
      <td>0.084774</td>
      <td>0.088653</td>
      <td>-66</td>
      <td>False</td>
      <td>6</td>
      <td>False</td>
      <td>0.250000</td>
      <td>0.166667</td>
      <td>((1590, 1591), (1593, 1593), (1626, 1626), (16...</td>
      <td>((1569, 1569), (1590, 1591), (1593, 1593), (16...</td>
      <td>(P21359-2, P21359-6)</td>
      <td>False</td>
      <td>2</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1</td>
      <td>B</td>
      <td>B</td>
      <td>B</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[1,24],[28,28],[30,63],[65,65],[67,120],[123,...</td>
      <td>[[10,10],[31,32],[34,34],[67,67],[72,72],[148,...</td>
      <td>1</td>
      <td>A</td>
      <td>A</td>
      <td>A</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[1,11],[13,25],[27,28],[30,42],[44,236],[238,...</td>
      <td>[[31,32],[34,34],[67,67],[72,72],[148,149],[15...</td>
      <td>2d4q</td>
      <td>0</td>
      <td>3</td>
      <td>False</td>
      <td>P21359-2</td>
      <td>NF1_HUMAN</td>
      <td>1.00</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[1,257]]</td>
      <td>[[1560,1816]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[1,257]]</td>
      <td>[[1560,1816]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2818</td>
      <td>11</td>
      <td>[[28, 28], [63, 63], [73, 76], [107, 107], [10...</td>
      <td>255</td>
      <td>[[1, 120], [123, 257]]</td>
      <td>254.009</td>
      <td>[]</td>
      <td>0</td>
      <td>[]</td>
      <td>257</td>
      <td>257</td>
      <td>[[1, 257]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((1, 120), (123, 257))</td>
      <td>255</td>
      <td>0.085315</td>
      <td>0.089219</td>
      <td>2.300</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20110713</td>
      <td>20051022</td>
      <td>0.434783</td>
      <td>-66</td>
      <td>False</td>
      <td>6</td>
      <td>P21359-4</td>
      <td>NF1_HUMAN</td>
      <td>0.91</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[1,11]]</td>
      <td>[[1581,1591]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[1,11]]</td>
      <td>[[1581,1591]]</td>
      <td>{"11":"T"}</td>
      <td>[[11,11]]</td>
      <td>[[1591,1591]]</td>
      <td>1598</td>
      <td>12</td>
      <td>[[61, 61], [73, 76], [82, 82], [86, 86], [107,...</td>
      <td>257</td>
      <td>[[1, 257]]</td>
      <td>257.000</td>
      <td>[]</td>
      <td>0</td>
      <td>[]</td>
      <td>257</td>
      <td>257</td>
      <td>[[1, 257]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((1, 257),)</td>
      <td>257</td>
      <td>-0.151439</td>
      <td>-0.143930</td>
      <td>-65</td>
      <td>False</td>
      <td>-1</td>
      <td>False</td>
      <td>-1.000000</td>
      <td>0.166667</td>
      <td>((1569, 1569), (1590, 1591), (1593, 1593), (16...</td>
      <td>()</td>
      <td>(P21359-2, P21359-4)</td>
      <td>False</td>
      <td>-1</td>
    </tr>
    <tr>
      <th>5</th>
      <td>1</td>
      <td>B</td>
      <td>B</td>
      <td>B</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[1,24],[28,28],[30,63],[65,65],[67,120],[123,...</td>
      <td>[[10,10],[31,32],[34,34],[67,67],[72,72],[148,...</td>
      <td>1</td>
      <td>A</td>
      <td>A</td>
      <td>A</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[1,11],[13,25],[27,28],[30,42],[44,236],[238,...</td>
      <td>[[31,32],[34,34],[67,67],[72,72],[148,149],[15...</td>
      <td>2d4q</td>
      <td>0</td>
      <td>3</td>
      <td>False</td>
      <td>P21359-2</td>
      <td>NF1_HUMAN</td>
      <td>1.00</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[1,257]]</td>
      <td>[[1560,1816]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[1,257]]</td>
      <td>[[1560,1816]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2818</td>
      <td>11</td>
      <td>[[28, 28], [63, 63], [73, 76], [107, 107], [10...</td>
      <td>255</td>
      <td>[[1, 120], [123, 257]]</td>
      <td>254.009</td>
      <td>[]</td>
      <td>0</td>
      <td>[]</td>
      <td>257</td>
      <td>257</td>
      <td>[[1, 257]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((1, 120), (123, 257))</td>
      <td>255</td>
      <td>0.085315</td>
      <td>0.089219</td>
      <td>2.300</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20110713</td>
      <td>20051022</td>
      <td>0.434783</td>
      <td>-66</td>
      <td>False</td>
      <td>6</td>
      <td>P21359-6</td>
      <td>NF1_HUMAN</td>
      <td>1.00</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[1,257]]</td>
      <td>[[1560,1816]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[1,257]]</td>
      <td>[[1560,1816]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2836</td>
      <td>12</td>
      <td>[[61, 61], [73, 76], [82, 82], [86, 86], [107,...</td>
      <td>257</td>
      <td>[[1, 257]]</td>
      <td>257.000</td>
      <td>[]</td>
      <td>0</td>
      <td>[]</td>
      <td>257</td>
      <td>257</td>
      <td>[[1, 257]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((1, 257),)</td>
      <td>257</td>
      <td>0.086389</td>
      <td>0.090621</td>
      <td>-65</td>
      <td>False</td>
      <td>4</td>
      <td>False</td>
      <td>0.250000</td>
      <td>0.166667</td>
      <td>((1569, 1569), (1590, 1591), (1593, 1593), (16...</td>
      <td>((1590, 1591), (1593, 1593), (1626, 1626), (16...</td>
      <td>(P21359-2, P21359-6)</td>
      <td>False</td>
      <td>4</td>
    </tr>
    <tr>
      <th>6</th>
      <td>1</td>
      <td>B</td>
      <td>B</td>
      <td>B</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[1,24],[28,28],[30,63],[65,65],[67,120],[123,...</td>
      <td>[[10,10],[31,32],[34,34],[67,67],[72,72],[148,...</td>
      <td>1</td>
      <td>A</td>
      <td>A</td>
      <td>A</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[1,11],[13,25],[27,28],[30,42],[44,236],[238,...</td>
      <td>[[31,32],[34,34],[67,67],[72,72],[148,149],[15...</td>
      <td>2d4q</td>
      <td>1</td>
      <td>3</td>
      <td>True</td>
      <td>P21359-2</td>
      <td>NF1_HUMAN</td>
      <td>1.00</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[1,257]]</td>
      <td>[[1560,1816]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[1,257]]</td>
      <td>[[1560,1816]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2818</td>
      <td>11</td>
      <td>[[28, 28], [63, 63], [73, 76], [107, 107], [10...</td>
      <td>255</td>
      <td>[[1, 120], [123, 257]]</td>
      <td>254.009</td>
      <td>[]</td>
      <td>0</td>
      <td>[]</td>
      <td>257</td>
      <td>257</td>
      <td>[[1, 257]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((1, 120), (123, 257))</td>
      <td>255</td>
      <td>0.085315</td>
      <td>0.089219</td>
      <td>2.300</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20110713</td>
      <td>20051022</td>
      <td>0.434783</td>
      <td>-66</td>
      <td>False</td>
      <td>6</td>
      <td>P21359</td>
      <td>NF1_HUMAN</td>
      <td>1.00</td>
      <td>True</td>
      <td>NF1_HUMAN</td>
      <td>[[1,257]]</td>
      <td>[[1581,1837]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[1,257]]</td>
      <td>[[1581,1837]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2839</td>
      <td>12</td>
      <td>[[61, 61], [73, 76], [82, 82], [86, 86], [107,...</td>
      <td>257</td>
      <td>[[1, 257]]</td>
      <td>257.000</td>
      <td>[]</td>
      <td>0</td>
      <td>[]</td>
      <td>257</td>
      <td>257</td>
      <td>[[1, 257]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((1, 257),)</td>
      <td>257</td>
      <td>0.086298</td>
      <td>0.090525</td>
      <td>-65</td>
      <td>False</td>
      <td>2</td>
      <td>True</td>
      <td>0.500000</td>
      <td>0.166667</td>
      <td>((1569, 1569), (1590, 1591), (1593, 1593), (16...</td>
      <td>((1611, 1612), (1614, 1614), (1647, 1647), (16...</td>
      <td>(P21359-2, P21359)</td>
      <td>False</td>
      <td>5</td>
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
      <td>[[1,11],[13,25],[27,28],[30,42],[44,236],[238,...</td>
      <td>[[31,32],[34,34],[67,67],[72,72],[148,149],[15...</td>
      <td>1</td>
      <td>B</td>
      <td>B</td>
      <td>B</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[1,24],[28,28],[30,63],[65,65],[67,120],[123,...</td>
      <td>[[10,10],[31,32],[34,34],[67,67],[72,72],[148,...</td>
      <td>2d4q</td>
      <td>1</td>
      <td>3</td>
      <td>True</td>
      <td>P21359-2</td>
      <td>NF1_HUMAN</td>
      <td>1.00</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[1,257]]</td>
      <td>[[1560,1816]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[1,257]]</td>
      <td>[[1560,1816]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2818</td>
      <td>12</td>
      <td>[[61, 61], [73, 76], [82, 82], [86, 86], [107,...</td>
      <td>257</td>
      <td>[[1, 257]]</td>
      <td>257.000</td>
      <td>[]</td>
      <td>0</td>
      <td>[]</td>
      <td>257</td>
      <td>257</td>
      <td>[[1, 257]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((1, 257),)</td>
      <td>257</td>
      <td>0.086941</td>
      <td>0.091199</td>
      <td>2.300</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20110713</td>
      <td>20051022</td>
      <td>0.434783</td>
      <td>-65</td>
      <td>False</td>
      <td>4</td>
      <td>P21359</td>
      <td>NF1_HUMAN</td>
      <td>1.00</td>
      <td>True</td>
      <td>NF1_HUMAN</td>
      <td>[[1,257]]</td>
      <td>[[1581,1837]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[1,257]]</td>
      <td>[[1581,1837]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2839</td>
      <td>11</td>
      <td>[[28, 28], [63, 63], [73, 76], [107, 107], [10...</td>
      <td>255</td>
      <td>[[1, 120], [123, 257]]</td>
      <td>254.009</td>
      <td>[]</td>
      <td>0</td>
      <td>[]</td>
      <td>257</td>
      <td>257</td>
      <td>[[1, 257]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((1, 120), (123, 257))</td>
      <td>255</td>
      <td>0.084684</td>
      <td>0.088559</td>
      <td>-66</td>
      <td>False</td>
      <td>4</td>
      <td>True</td>
      <td>0.250000</td>
      <td>0.250000</td>
      <td>((1590, 1591), (1593, 1593), (1626, 1626), (16...</td>
      <td>((1590, 1590), (1611, 1612), (1614, 1614), (16...</td>
      <td>(P21359-2, P21359)</td>
      <td>True</td>
      <td>1</td>
    </tr>
    <tr>
      <th>8</th>
      <td>1</td>
      <td>A</td>
      <td>A</td>
      <td>A</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[1,11],[13,25],[27,28],[30,42],[44,236],[238,...</td>
      <td>[[31,32],[34,34],[67,67],[72,72],[148,149],[15...</td>
      <td>1</td>
      <td>B</td>
      <td>B</td>
      <td>B</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[1,24],[28,28],[30,63],[65,65],[67,120],[123,...</td>
      <td>[[10,10],[31,32],[34,34],[67,67],[72,72],[148,...</td>
      <td>2d4q</td>
      <td>1</td>
      <td>3</td>
      <td>True</td>
      <td>P21359-2</td>
      <td>NF1_HUMAN</td>
      <td>1.00</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[1,257]]</td>
      <td>[[1560,1816]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[1,257]]</td>
      <td>[[1560,1816]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2818</td>
      <td>12</td>
      <td>[[61, 61], [73, 76], [82, 82], [86, 86], [107,...</td>
      <td>257</td>
      <td>[[1, 257]]</td>
      <td>257.000</td>
      <td>[]</td>
      <td>0</td>
      <td>[]</td>
      <td>257</td>
      <td>257</td>
      <td>[[1, 257]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((1, 257),)</td>
      <td>257</td>
      <td>0.086941</td>
      <td>0.091199</td>
      <td>2.300</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20110713</td>
      <td>20051022</td>
      <td>0.434783</td>
      <td>-65</td>
      <td>False</td>
      <td>4</td>
      <td>P21359-4</td>
      <td>NF1_HUMAN</td>
      <td>0.91</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[1,11]]</td>
      <td>[[1581,1591]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[1,11]]</td>
      <td>[[1581,1591]]</td>
      <td>{"11":"T"}</td>
      <td>[[11,11]]</td>
      <td>[[1591,1591]]</td>
      <td>1598</td>
      <td>11</td>
      <td>[[28, 28], [63, 63], [73, 76], [107, 107], [10...</td>
      <td>255</td>
      <td>[[1, 120], [123, 257]]</td>
      <td>254.009</td>
      <td>[]</td>
      <td>0</td>
      <td>[]</td>
      <td>257</td>
      <td>257</td>
      <td>[[1, 257]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((1, 120), (123, 257))</td>
      <td>255</td>
      <td>-0.150814</td>
      <td>-0.143930</td>
      <td>-66</td>
      <td>False</td>
      <td>-1</td>
      <td>True</td>
      <td>-1.000000</td>
      <td>0.250000</td>
      <td>((1590, 1591), (1593, 1593), (1626, 1626), (16...</td>
      <td>((1590, 1590),)</td>
      <td>(P21359-2, P21359-4)</td>
      <td>False</td>
      <td>-1</td>
    </tr>
    <tr>
      <th>9</th>
      <td>1</td>
      <td>A</td>
      <td>A</td>
      <td>A</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[1,11],[13,25],[27,28],[30,42],[44,236],[238,...</td>
      <td>[[31,32],[34,34],[67,67],[72,72],[148,149],[15...</td>
      <td>1</td>
      <td>B</td>
      <td>B</td>
      <td>B</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[1,24],[28,28],[30,63],[65,65],[67,120],[123,...</td>
      <td>[[10,10],[31,32],[34,34],[67,67],[72,72],[148,...</td>
      <td>2d4q</td>
      <td>1</td>
      <td>3</td>
      <td>True</td>
      <td>P21359-2</td>
      <td>NF1_HUMAN</td>
      <td>1.00</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[1,257]]</td>
      <td>[[1560,1816]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[1,257]]</td>
      <td>[[1560,1816]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2818</td>
      <td>12</td>
      <td>[[61, 61], [73, 76], [82, 82], [86, 86], [107,...</td>
      <td>257</td>
      <td>[[1, 257]]</td>
      <td>257.000</td>
      <td>[]</td>
      <td>0</td>
      <td>[]</td>
      <td>257</td>
      <td>257</td>
      <td>[[1, 257]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((1, 257),)</td>
      <td>257</td>
      <td>0.086941</td>
      <td>0.091199</td>
      <td>2.300</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20110713</td>
      <td>20051022</td>
      <td>0.434783</td>
      <td>-65</td>
      <td>False</td>
      <td>4</td>
      <td>P21359-6</td>
      <td>NF1_HUMAN</td>
      <td>1.00</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[1,257]]</td>
      <td>[[1560,1816]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[1,257]]</td>
      <td>[[1560,1816]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2836</td>
      <td>11</td>
      <td>[[28, 28], [63, 63], [73, 76], [107, 107], [10...</td>
      <td>255</td>
      <td>[[1, 120], [123, 257]]</td>
      <td>254.009</td>
      <td>[]</td>
      <td>0</td>
      <td>[]</td>
      <td>257</td>
      <td>257</td>
      <td>[[1, 257]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((1, 120), (123, 257))</td>
      <td>255</td>
      <td>0.084774</td>
      <td>0.088653</td>
      <td>-66</td>
      <td>False</td>
      <td>6</td>
      <td>True</td>
      <td>0.250000</td>
      <td>0.166667</td>
      <td>((1590, 1591), (1593, 1593), (1626, 1626), (16...</td>
      <td>((1569, 1569), (1590, 1591), (1593, 1593), (16...</td>
      <td>(P21359-2, P21359-6)</td>
      <td>True</td>
      <td>1</td>
    </tr>
    <tr>
      <th>10</th>
      <td>1</td>
      <td>B</td>
      <td>B</td>
      <td>B</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[1,24],[28,28],[30,63],[65,65],[67,120],[123,...</td>
      <td>[[10,10],[31,32],[34,34],[67,67],[72,72],[148,...</td>
      <td>1</td>
      <td>A</td>
      <td>A</td>
      <td>A</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[1,11],[13,25],[27,28],[30,42],[44,236],[238,...</td>
      <td>[[31,32],[34,34],[67,67],[72,72],[148,149],[15...</td>
      <td>2d4q</td>
      <td>1</td>
      <td>3</td>
      <td>True</td>
      <td>P21359-2</td>
      <td>NF1_HUMAN</td>
      <td>1.00</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[1,257]]</td>
      <td>[[1560,1816]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[1,257]]</td>
      <td>[[1560,1816]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2818</td>
      <td>11</td>
      <td>[[28, 28], [63, 63], [73, 76], [107, 107], [10...</td>
      <td>255</td>
      <td>[[1, 120], [123, 257]]</td>
      <td>254.009</td>
      <td>[]</td>
      <td>0</td>
      <td>[]</td>
      <td>257</td>
      <td>257</td>
      <td>[[1, 257]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((1, 120), (123, 257))</td>
      <td>255</td>
      <td>0.085315</td>
      <td>0.089219</td>
      <td>2.300</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20110713</td>
      <td>20051022</td>
      <td>0.434783</td>
      <td>-66</td>
      <td>False</td>
      <td>6</td>
      <td>P21359-4</td>
      <td>NF1_HUMAN</td>
      <td>0.91</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[1,11]]</td>
      <td>[[1581,1591]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[1,11]]</td>
      <td>[[1581,1591]]</td>
      <td>{"11":"T"}</td>
      <td>[[11,11]]</td>
      <td>[[1591,1591]]</td>
      <td>1598</td>
      <td>12</td>
      <td>[[61, 61], [73, 76], [82, 82], [86, 86], [107,...</td>
      <td>257</td>
      <td>[[1, 257]]</td>
      <td>257.000</td>
      <td>[]</td>
      <td>0</td>
      <td>[]</td>
      <td>257</td>
      <td>257</td>
      <td>[[1, 257]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((1, 257),)</td>
      <td>257</td>
      <td>-0.151439</td>
      <td>-0.143930</td>
      <td>-65</td>
      <td>False</td>
      <td>-1</td>
      <td>True</td>
      <td>-1.000000</td>
      <td>0.166667</td>
      <td>((1569, 1569), (1590, 1591), (1593, 1593), (16...</td>
      <td>()</td>
      <td>(P21359-2, P21359-4)</td>
      <td>False</td>
      <td>-1</td>
    </tr>
    <tr>
      <th>11</th>
      <td>1</td>
      <td>B</td>
      <td>B</td>
      <td>B</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[1,24],[28,28],[30,63],[65,65],[67,120],[123,...</td>
      <td>[[10,10],[31,32],[34,34],[67,67],[72,72],[148,...</td>
      <td>1</td>
      <td>A</td>
      <td>A</td>
      <td>A</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[1,11],[13,25],[27,28],[30,42],[44,236],[238,...</td>
      <td>[[31,32],[34,34],[67,67],[72,72],[148,149],[15...</td>
      <td>2d4q</td>
      <td>1</td>
      <td>3</td>
      <td>True</td>
      <td>P21359-2</td>
      <td>NF1_HUMAN</td>
      <td>1.00</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[1,257]]</td>
      <td>[[1560,1816]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[1,257]]</td>
      <td>[[1560,1816]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2818</td>
      <td>11</td>
      <td>[[28, 28], [63, 63], [73, 76], [107, 107], [10...</td>
      <td>255</td>
      <td>[[1, 120], [123, 257]]</td>
      <td>254.009</td>
      <td>[]</td>
      <td>0</td>
      <td>[]</td>
      <td>257</td>
      <td>257</td>
      <td>[[1, 257]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((1, 120), (123, 257))</td>
      <td>255</td>
      <td>0.085315</td>
      <td>0.089219</td>
      <td>2.300</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20110713</td>
      <td>20051022</td>
      <td>0.434783</td>
      <td>-66</td>
      <td>False</td>
      <td>6</td>
      <td>P21359-6</td>
      <td>NF1_HUMAN</td>
      <td>1.00</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[1,257]]</td>
      <td>[[1560,1816]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[1,257]]</td>
      <td>[[1560,1816]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2836</td>
      <td>12</td>
      <td>[[61, 61], [73, 76], [82, 82], [86, 86], [107,...</td>
      <td>257</td>
      <td>[[1, 257]]</td>
      <td>257.000</td>
      <td>[]</td>
      <td>0</td>
      <td>[]</td>
      <td>257</td>
      <td>257</td>
      <td>[[1, 257]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((1, 257),)</td>
      <td>257</td>
      <td>0.086389</td>
      <td>0.090621</td>
      <td>-65</td>
      <td>False</td>
      <td>4</td>
      <td>True</td>
      <td>0.250000</td>
      <td>0.166667</td>
      <td>((1569, 1569), (1590, 1591), (1593, 1593), (16...</td>
      <td>((1590, 1591), (1593, 1593), (1626, 1626), (16...</td>
      <td>(P21359-2, P21359-6)</td>
      <td>False</td>
      <td>3</td>
    </tr>
    <tr>
      <th>12</th>
      <td>1</td>
      <td>B</td>
      <td>B</td>
      <td>B</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[28,44],[48,48],[50,62],[64,81],[83,83],[85,8...</td>
      <td>[[51,52],[54,54],[87,87],[92,92],[168,169],[17...</td>
      <td>1</td>
      <td>A</td>
      <td>A</td>
      <td>A</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[28,44],[47,48],[50,52],[54,62],[64,81],[83,8...</td>
      <td>[[51,52],[54,54],[87,87],[92,92],[168,169],[17...</td>
      <td>2e2x</td>
      <td>0</td>
      <td>5</td>
      <td>False</td>
      <td>P21359-2</td>
      <td>NF1_HUMAN</td>
      <td>0.99</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[6,277]]</td>
      <td>[[1545,1816]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[6,277]]</td>
      <td>[[1545,1816]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2818</td>
      <td>0</td>
      <td>[]</td>
      <td>250</td>
      <td>[[28, 277]]</td>
      <td>249.180</td>
      <td>[[1, 5]]</td>
      <td>0</td>
      <td>[]</td>
      <td>277</td>
      <td>277</td>
      <td>[[1, 277]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((28, 277),)</td>
      <td>250</td>
      <td>0.074735</td>
      <td>0.074735</td>
      <td>2.500</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20110713</td>
      <td>20061118</td>
      <td>0.400000</td>
      <td>-66</td>
      <td>False</td>
      <td>13</td>
      <td>P21359</td>
      <td>NF1_HUMAN</td>
      <td>0.99</td>
      <td>True</td>
      <td>NF1_HUMAN</td>
      <td>[[6,277]]</td>
      <td>[[1566,1837]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[6,277]]</td>
      <td>[[1566,1837]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2839</td>
      <td>0</td>
      <td>[]</td>
      <td>250</td>
      <td>[[28, 277]]</td>
      <td>248.894</td>
      <td>[[1, 5]]</td>
      <td>0</td>
      <td>[]</td>
      <td>277</td>
      <td>277</td>
      <td>[[1, 277]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((28, 277),)</td>
      <td>250</td>
      <td>0.074182</td>
      <td>0.074182</td>
      <td>-65</td>
      <td>False</td>
      <td>7</td>
      <td>False</td>
      <td>0.142857</td>
      <td>0.076923</td>
      <td>((1590, 1591), (1593, 1593), (1626, 1626), (16...</td>
      <td>((1611, 1612), (1614, 1614), (1647, 1647), (16...</td>
      <td>(P21359-2, P21359)</td>
      <td>False</td>
      <td>15</td>
    </tr>
    <tr>
      <th>13</th>
      <td>1</td>
      <td>A</td>
      <td>A</td>
      <td>A</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[28,44],[47,48],[50,52],[54,62],[64,81],[83,8...</td>
      <td>[[51,52],[54,54],[87,87],[92,92],[168,169],[17...</td>
      <td>1</td>
      <td>B</td>
      <td>B</td>
      <td>B</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[28,44],[48,48],[50,62],[64,81],[83,83],[85,8...</td>
      <td>[[51,52],[54,54],[87,87],[92,92],[168,169],[17...</td>
      <td>2e2x</td>
      <td>0</td>
      <td>5</td>
      <td>False</td>
      <td>P21359-2</td>
      <td>NF1_HUMAN</td>
      <td>0.99</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[6,277]]</td>
      <td>[[1545,1816]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[6,277]]</td>
      <td>[[1545,1816]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2818</td>
      <td>0</td>
      <td>[]</td>
      <td>250</td>
      <td>[[28, 277]]</td>
      <td>248.894</td>
      <td>[[1, 5]]</td>
      <td>0</td>
      <td>[]</td>
      <td>277</td>
      <td>277</td>
      <td>[[1, 277]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((28, 277),)</td>
      <td>250</td>
      <td>0.074735</td>
      <td>0.074735</td>
      <td>2.500</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20110713</td>
      <td>20061118</td>
      <td>0.400000</td>
      <td>-65</td>
      <td>False</td>
      <td>12</td>
      <td>P21359</td>
      <td>NF1_HUMAN</td>
      <td>0.99</td>
      <td>True</td>
      <td>NF1_HUMAN</td>
      <td>[[6,277]]</td>
      <td>[[1566,1837]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[6,277]]</td>
      <td>[[1566,1837]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2839</td>
      <td>0</td>
      <td>[]</td>
      <td>250</td>
      <td>[[28, 277]]</td>
      <td>249.180</td>
      <td>[[1, 5]]</td>
      <td>0</td>
      <td>[]</td>
      <td>277</td>
      <td>277</td>
      <td>[[1, 277]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((28, 277),)</td>
      <td>250</td>
      <td>0.074182</td>
      <td>0.074182</td>
      <td>-66</td>
      <td>False</td>
      <td>8</td>
      <td>False</td>
      <td>0.125000</td>
      <td>0.083333</td>
      <td>((1590, 1591), (1593, 1593), (1626, 1626), (16...</td>
      <td>((1611, 1612), (1614, 1614), (1647, 1647), (16...</td>
      <td>(P21359-2, P21359)</td>
      <td>False</td>
      <td>13</td>
    </tr>
    <tr>
      <th>14</th>
      <td>1</td>
      <td>A</td>
      <td>A</td>
      <td>A</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[28,44],[47,48],[50,52],[54,62],[64,81],[83,8...</td>
      <td>[[51,52],[54,54],[87,87],[92,92],[168,169],[17...</td>
      <td>1</td>
      <td>B</td>
      <td>B</td>
      <td>B</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[28,44],[48,48],[50,62],[64,81],[83,83],[85,8...</td>
      <td>[[51,52],[54,54],[87,87],[92,92],[168,169],[17...</td>
      <td>2e2x</td>
      <td>0</td>
      <td>5</td>
      <td>False</td>
      <td>P21359-2</td>
      <td>NF1_HUMAN</td>
      <td>0.99</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[6,277]]</td>
      <td>[[1545,1816]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[6,277]]</td>
      <td>[[1545,1816]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2818</td>
      <td>0</td>
      <td>[]</td>
      <td>250</td>
      <td>[[28, 277]]</td>
      <td>248.894</td>
      <td>[[1, 5]]</td>
      <td>0</td>
      <td>[]</td>
      <td>277</td>
      <td>277</td>
      <td>[[1, 277]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((28, 277),)</td>
      <td>250</td>
      <td>0.074735</td>
      <td>0.074735</td>
      <td>2.500</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20110713</td>
      <td>20061118</td>
      <td>0.400000</td>
      <td>-65</td>
      <td>False</td>
      <td>12</td>
      <td>P21359-6</td>
      <td>NF1_HUMAN</td>
      <td>0.99</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[6,277]]</td>
      <td>[[1545,1816]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[6,277]]</td>
      <td>[[1545,1816]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2836</td>
      <td>0</td>
      <td>[]</td>
      <td>250</td>
      <td>[[28, 277]]</td>
      <td>249.180</td>
      <td>[[1, 5]]</td>
      <td>0</td>
      <td>[]</td>
      <td>277</td>
      <td>277</td>
      <td>[[1, 277]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((28, 277),)</td>
      <td>250</td>
      <td>0.074261</td>
      <td>0.074261</td>
      <td>-66</td>
      <td>False</td>
      <td>13</td>
      <td>False</td>
      <td>0.083333</td>
      <td>0.076923</td>
      <td>((1590, 1591), (1593, 1593), (1626, 1626), (16...</td>
      <td>((1590, 1591), (1593, 1593), (1626, 1626), (16...</td>
      <td>(P21359-2, P21359-6)</td>
      <td>False</td>
      <td>14</td>
    </tr>
    <tr>
      <th>15</th>
      <td>1</td>
      <td>B</td>
      <td>B</td>
      <td>B</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[28,44],[48,48],[50,62],[64,81],[83,83],[85,8...</td>
      <td>[[51,52],[54,54],[87,87],[92,92],[168,169],[17...</td>
      <td>1</td>
      <td>A</td>
      <td>A</td>
      <td>A</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[28,44],[47,48],[50,52],[54,62],[64,81],[83,8...</td>
      <td>[[51,52],[54,54],[87,87],[92,92],[168,169],[17...</td>
      <td>2e2x</td>
      <td>0</td>
      <td>5</td>
      <td>False</td>
      <td>P21359-2</td>
      <td>NF1_HUMAN</td>
      <td>0.99</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[6,277]]</td>
      <td>[[1545,1816]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[6,277]]</td>
      <td>[[1545,1816]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2818</td>
      <td>0</td>
      <td>[]</td>
      <td>250</td>
      <td>[[28, 277]]</td>
      <td>249.180</td>
      <td>[[1, 5]]</td>
      <td>0</td>
      <td>[]</td>
      <td>277</td>
      <td>277</td>
      <td>[[1, 277]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((28, 277),)</td>
      <td>250</td>
      <td>0.074735</td>
      <td>0.074735</td>
      <td>2.500</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20110713</td>
      <td>20061118</td>
      <td>0.400000</td>
      <td>-66</td>
      <td>False</td>
      <td>13</td>
      <td>P21359-6</td>
      <td>NF1_HUMAN</td>
      <td>0.99</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[6,277]]</td>
      <td>[[1545,1816]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[6,277]]</td>
      <td>[[1545,1816]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2836</td>
      <td>0</td>
      <td>[]</td>
      <td>250</td>
      <td>[[28, 277]]</td>
      <td>248.894</td>
      <td>[[1, 5]]</td>
      <td>0</td>
      <td>[]</td>
      <td>277</td>
      <td>277</td>
      <td>[[1, 277]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((28, 277),)</td>
      <td>250</td>
      <td>0.074261</td>
      <td>0.074261</td>
      <td>-65</td>
      <td>False</td>
      <td>12</td>
      <td>False</td>
      <td>0.083333</td>
      <td>0.076923</td>
      <td>((1590, 1591), (1593, 1593), (1626, 1626), (16...</td>
      <td>((1590, 1591), (1593, 1593), (1626, 1626), (16...</td>
      <td>(P21359-2, P21359-6)</td>
      <td>False</td>
      <td>16</td>
    </tr>
    <tr>
      <th>16</th>
      <td>1</td>
      <td>B</td>
      <td>B</td>
      <td>B</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[28,44],[48,48],[50,62],[64,81],[83,83],[85,8...</td>
      <td>[[51,52],[54,54],[87,87],[92,92],[168,169],[17...</td>
      <td>1</td>
      <td>A</td>
      <td>A</td>
      <td>A</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[28,44],[47,48],[50,52],[54,62],[64,81],[83,8...</td>
      <td>[[51,52],[54,54],[87,87],[92,92],[168,169],[17...</td>
      <td>2e2x</td>
      <td>1</td>
      <td>5</td>
      <td>True</td>
      <td>P21359-2</td>
      <td>NF1_HUMAN</td>
      <td>0.99</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[6,277]]</td>
      <td>[[1545,1816]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[6,277]]</td>
      <td>[[1545,1816]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2818</td>
      <td>0</td>
      <td>[]</td>
      <td>250</td>
      <td>[[28, 277]]</td>
      <td>249.180</td>
      <td>[[1, 5]]</td>
      <td>0</td>
      <td>[]</td>
      <td>277</td>
      <td>277</td>
      <td>[[1, 277]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((28, 277),)</td>
      <td>250</td>
      <td>0.074735</td>
      <td>0.074735</td>
      <td>2.500</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20110713</td>
      <td>20061118</td>
      <td>0.400000</td>
      <td>-66</td>
      <td>False</td>
      <td>13</td>
      <td>P21359</td>
      <td>NF1_HUMAN</td>
      <td>0.99</td>
      <td>True</td>
      <td>NF1_HUMAN</td>
      <td>[[6,277]]</td>
      <td>[[1566,1837]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[6,277]]</td>
      <td>[[1566,1837]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2839</td>
      <td>0</td>
      <td>[]</td>
      <td>250</td>
      <td>[[28, 277]]</td>
      <td>248.894</td>
      <td>[[1, 5]]</td>
      <td>0</td>
      <td>[]</td>
      <td>277</td>
      <td>277</td>
      <td>[[1, 277]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((28, 277),)</td>
      <td>250</td>
      <td>0.074182</td>
      <td>0.074182</td>
      <td>-65</td>
      <td>False</td>
      <td>7</td>
      <td>True</td>
      <td>0.142857</td>
      <td>0.076923</td>
      <td>((1590, 1591), (1593, 1593), (1626, 1626), (16...</td>
      <td>((1611, 1612), (1614, 1614), (1647, 1647), (16...</td>
      <td>(P21359-2, P21359)</td>
      <td>False</td>
      <td>14</td>
    </tr>
    <tr>
      <th>17</th>
      <td>1</td>
      <td>A</td>
      <td>A</td>
      <td>A</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[28,44],[47,48],[50,52],[54,62],[64,81],[83,8...</td>
      <td>[[51,52],[54,54],[87,87],[92,92],[168,169],[17...</td>
      <td>1</td>
      <td>B</td>
      <td>B</td>
      <td>B</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[28,44],[48,48],[50,62],[64,81],[83,83],[85,8...</td>
      <td>[[51,52],[54,54],[87,87],[92,92],[168,169],[17...</td>
      <td>2e2x</td>
      <td>1</td>
      <td>5</td>
      <td>True</td>
      <td>P21359-2</td>
      <td>NF1_HUMAN</td>
      <td>0.99</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[6,277]]</td>
      <td>[[1545,1816]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[6,277]]</td>
      <td>[[1545,1816]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2818</td>
      <td>0</td>
      <td>[]</td>
      <td>250</td>
      <td>[[28, 277]]</td>
      <td>248.894</td>
      <td>[[1, 5]]</td>
      <td>0</td>
      <td>[]</td>
      <td>277</td>
      <td>277</td>
      <td>[[1, 277]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((28, 277),)</td>
      <td>250</td>
      <td>0.074735</td>
      <td>0.074735</td>
      <td>2.500</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20110713</td>
      <td>20061118</td>
      <td>0.400000</td>
      <td>-65</td>
      <td>False</td>
      <td>12</td>
      <td>P21359</td>
      <td>NF1_HUMAN</td>
      <td>0.99</td>
      <td>True</td>
      <td>NF1_HUMAN</td>
      <td>[[6,277]]</td>
      <td>[[1566,1837]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[6,277]]</td>
      <td>[[1566,1837]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2839</td>
      <td>0</td>
      <td>[]</td>
      <td>250</td>
      <td>[[28, 277]]</td>
      <td>249.180</td>
      <td>[[1, 5]]</td>
      <td>0</td>
      <td>[]</td>
      <td>277</td>
      <td>277</td>
      <td>[[1, 277]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((28, 277),)</td>
      <td>250</td>
      <td>0.074182</td>
      <td>0.074182</td>
      <td>-66</td>
      <td>False</td>
      <td>8</td>
      <td>True</td>
      <td>0.125000</td>
      <td>0.083333</td>
      <td>((1590, 1591), (1593, 1593), (1626, 1626), (16...</td>
      <td>((1611, 1612), (1614, 1614), (1647, 1647), (16...</td>
      <td>(P21359-2, P21359)</td>
      <td>False</td>
      <td>12</td>
    </tr>
    <tr>
      <th>18</th>
      <td>1</td>
      <td>A</td>
      <td>A</td>
      <td>A</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[28,44],[47,48],[50,52],[54,62],[64,81],[83,8...</td>
      <td>[[51,52],[54,54],[87,87],[92,92],[168,169],[17...</td>
      <td>1</td>
      <td>B</td>
      <td>B</td>
      <td>B</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[28,44],[48,48],[50,62],[64,81],[83,83],[85,8...</td>
      <td>[[51,52],[54,54],[87,87],[92,92],[168,169],[17...</td>
      <td>2e2x</td>
      <td>1</td>
      <td>5</td>
      <td>True</td>
      <td>P21359-2</td>
      <td>NF1_HUMAN</td>
      <td>0.99</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[6,277]]</td>
      <td>[[1545,1816]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[6,277]]</td>
      <td>[[1545,1816]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2818</td>
      <td>0</td>
      <td>[]</td>
      <td>250</td>
      <td>[[28, 277]]</td>
      <td>248.894</td>
      <td>[[1, 5]]</td>
      <td>0</td>
      <td>[]</td>
      <td>277</td>
      <td>277</td>
      <td>[[1, 277]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((28, 277),)</td>
      <td>250</td>
      <td>0.074735</td>
      <td>0.074735</td>
      <td>2.500</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20110713</td>
      <td>20061118</td>
      <td>0.400000</td>
      <td>-65</td>
      <td>False</td>
      <td>12</td>
      <td>P21359-6</td>
      <td>NF1_HUMAN</td>
      <td>0.99</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[6,277]]</td>
      <td>[[1545,1816]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[6,277]]</td>
      <td>[[1545,1816]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2836</td>
      <td>0</td>
      <td>[]</td>
      <td>250</td>
      <td>[[28, 277]]</td>
      <td>249.180</td>
      <td>[[1, 5]]</td>
      <td>0</td>
      <td>[]</td>
      <td>277</td>
      <td>277</td>
      <td>[[1, 277]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((28, 277),)</td>
      <td>250</td>
      <td>0.074261</td>
      <td>0.074261</td>
      <td>-66</td>
      <td>False</td>
      <td>13</td>
      <td>True</td>
      <td>0.083333</td>
      <td>0.076923</td>
      <td>((1590, 1591), (1593, 1593), (1626, 1626), (16...</td>
      <td>((1590, 1591), (1593, 1593), (1626, 1626), (16...</td>
      <td>(P21359-2, P21359-6)</td>
      <td>False</td>
      <td>13</td>
    </tr>
    <tr>
      <th>19</th>
      <td>1</td>
      <td>B</td>
      <td>B</td>
      <td>B</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[28,44],[48,48],[50,62],[64,81],[83,83],[85,8...</td>
      <td>[[51,52],[54,54],[87,87],[92,92],[168,169],[17...</td>
      <td>1</td>
      <td>A</td>
      <td>A</td>
      <td>A</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[28,44],[47,48],[50,52],[54,62],[64,81],[83,8...</td>
      <td>[[51,52],[54,54],[87,87],[92,92],[168,169],[17...</td>
      <td>2e2x</td>
      <td>1</td>
      <td>5</td>
      <td>True</td>
      <td>P21359-2</td>
      <td>NF1_HUMAN</td>
      <td>0.99</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[6,277]]</td>
      <td>[[1545,1816]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[6,277]]</td>
      <td>[[1545,1816]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2818</td>
      <td>0</td>
      <td>[]</td>
      <td>250</td>
      <td>[[28, 277]]</td>
      <td>249.180</td>
      <td>[[1, 5]]</td>
      <td>0</td>
      <td>[]</td>
      <td>277</td>
      <td>277</td>
      <td>[[1, 277]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((28, 277),)</td>
      <td>250</td>
      <td>0.074735</td>
      <td>0.074735</td>
      <td>2.500</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20110713</td>
      <td>20061118</td>
      <td>0.400000</td>
      <td>-66</td>
      <td>False</td>
      <td>13</td>
      <td>P21359-6</td>
      <td>NF1_HUMAN</td>
      <td>0.99</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[6,277]]</td>
      <td>[[1545,1816]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[6,277]]</td>
      <td>[[1545,1816]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2836</td>
      <td>0</td>
      <td>[]</td>
      <td>250</td>
      <td>[[28, 277]]</td>
      <td>248.894</td>
      <td>[[1, 5]]</td>
      <td>0</td>
      <td>[]</td>
      <td>277</td>
      <td>277</td>
      <td>[[1, 277]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((28, 277),)</td>
      <td>250</td>
      <td>0.074261</td>
      <td>0.074261</td>
      <td>-65</td>
      <td>False</td>
      <td>12</td>
      <td>True</td>
      <td>0.083333</td>
      <td>0.076923</td>
      <td>((1590, 1591), (1593, 1593), (1626, 1626), (16...</td>
      <td>((1590, 1591), (1593, 1593), (1626, 1626), (16...</td>
      <td>(P21359-2, P21359-6)</td>
      <td>False</td>
      <td>15</td>
    </tr>
    <tr>
      <th>20</th>
      <td>1</td>
      <td>B</td>
      <td>B</td>
      <td>B</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[7,43],[46,61],[63,80],[82,84],[86,157],[159,...</td>
      <td>[[50,51],[53,53],[86,86],[91,91],[167,168],[17...</td>
      <td>1</td>
      <td>A</td>
      <td>A</td>
      <td>A</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[7,44],[46,47],[49,62],[64,82],[84,84],[86,25...</td>
      <td>[[50,51],[53,53],[86,86],[91,91],[167,168],[17...</td>
      <td>3p7z</td>
      <td>0</td>
      <td>5</td>
      <td>False</td>
      <td>P21359-2</td>
      <td>NF1_HUMAN</td>
      <td>0.98</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[5,276]]</td>
      <td>[[1545,1816]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[5,276]]</td>
      <td>[[1545,1816]]</td>
      <td>{"44":"I"}</td>
      <td>[[44,44]]</td>
      <td>[[1584,1584]]</td>
      <td>2818</td>
      <td>16</td>
      <td>[[80, 80], [92, 95], [101, 102], [110, 110], [...</td>
      <td>270</td>
      <td>[[7, 276]]</td>
      <td>269.180</td>
      <td>[[1, 4]]</td>
      <td>0</td>
      <td>[]</td>
      <td>276</td>
      <td>276</td>
      <td>[[1, 276]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((7, 276),)</td>
      <td>270</td>
      <td>0.088864</td>
      <td>0.094542</td>
      <td>2.650</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20190717</td>
      <td>20101013</td>
      <td>0.377358</td>
      <td>-66</td>
      <td>True</td>
      <td>2</td>
      <td>P21359</td>
      <td>NF1_HUMAN</td>
      <td>0.98</td>
      <td>True</td>
      <td>NF1_HUMAN</td>
      <td>[[5,276]]</td>
      <td>[[1566,1837]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[5,276]]</td>
      <td>[[1566,1837]]</td>
      <td>{"44":"I"}</td>
      <td>[[44,44]]</td>
      <td>[[1605,1605]]</td>
      <td>2839</td>
      <td>23</td>
      <td>[[40, 42], [47, 47], [66, 66], [70, 70], [78, ...</td>
      <td>270</td>
      <td>[[7, 276]]</td>
      <td>267.845</td>
      <td>[[1, 4]]</td>
      <td>0</td>
      <td>[]</td>
      <td>276</td>
      <td>276</td>
      <td>[[1, 276]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((7, 276),)</td>
      <td>270</td>
      <td>0.085741</td>
      <td>0.093842</td>
      <td>-65</td>
      <td>False</td>
      <td>3</td>
      <td>False</td>
      <td>0.500000</td>
      <td>0.333333</td>
      <td>((1590, 1591), (1593, 1593), (1626, 1626), (16...</td>
      <td>((1611, 1612), (1614, 1614), (1647, 1647), (16...</td>
      <td>(P21359-2, P21359)</td>
      <td>False</td>
      <td>8</td>
    </tr>
    <tr>
      <th>21</th>
      <td>1</td>
      <td>A</td>
      <td>A</td>
      <td>A</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[7,44],[46,47],[49,62],[64,82],[84,84],[86,25...</td>
      <td>[[50,51],[53,53],[86,86],[91,91],[167,168],[17...</td>
      <td>1</td>
      <td>B</td>
      <td>B</td>
      <td>B</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[7,43],[46,61],[63,80],[82,84],[86,157],[159,...</td>
      <td>[[50,51],[53,53],[86,86],[91,91],[167,168],[17...</td>
      <td>3p7z</td>
      <td>0</td>
      <td>5</td>
      <td>False</td>
      <td>P21359-2</td>
      <td>NF1_HUMAN</td>
      <td>0.98</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[5,276]]</td>
      <td>[[1545,1816]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[5,276]]</td>
      <td>[[1545,1816]]</td>
      <td>{"44":"I"}</td>
      <td>[[44,44]]</td>
      <td>[[1584,1584]]</td>
      <td>2818</td>
      <td>23</td>
      <td>[[40, 42], [47, 47], [66, 66], [70, 70], [78, ...</td>
      <td>270</td>
      <td>[[7, 276]]</td>
      <td>267.845</td>
      <td>[[1, 4]]</td>
      <td>0</td>
      <td>[]</td>
      <td>276</td>
      <td>276</td>
      <td>[[1, 276]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((7, 276),)</td>
      <td>270</td>
      <td>0.086380</td>
      <td>0.094542</td>
      <td>2.650</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20190717</td>
      <td>20101013</td>
      <td>0.377358</td>
      <td>-65</td>
      <td>False</td>
      <td>5</td>
      <td>P21359</td>
      <td>NF1_HUMAN</td>
      <td>0.98</td>
      <td>True</td>
      <td>NF1_HUMAN</td>
      <td>[[5,276]]</td>
      <td>[[1566,1837]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[5,276]]</td>
      <td>[[1566,1837]]</td>
      <td>{"44":"I"}</td>
      <td>[[44,44]]</td>
      <td>[[1605,1605]]</td>
      <td>2839</td>
      <td>16</td>
      <td>[[80, 80], [92, 95], [101, 102], [110, 110], [...</td>
      <td>270</td>
      <td>[[7, 276]]</td>
      <td>269.180</td>
      <td>[[1, 4]]</td>
      <td>0</td>
      <td>[]</td>
      <td>276</td>
      <td>276</td>
      <td>[[1, 276]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((7, 276),)</td>
      <td>270</td>
      <td>0.088207</td>
      <td>0.093842</td>
      <td>-66</td>
      <td>True</td>
      <td>1</td>
      <td>False</td>
      <td>1.000000</td>
      <td>0.200000</td>
      <td>((1590, 1591), (1593, 1593), (1626, 1626), (16...</td>
      <td>((1611, 1612), (1614, 1614), (1647, 1647), (16...</td>
      <td>(P21359-2, P21359)</td>
      <td>False</td>
      <td>4</td>
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
      <td>[[7,44],[46,47],[49,62],[64,82],[84,84],[86,25...</td>
      <td>[[50,51],[53,53],[86,86],[91,91],[167,168],[17...</td>
      <td>1</td>
      <td>B</td>
      <td>B</td>
      <td>B</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[7,43],[46,61],[63,80],[82,84],[86,157],[159,...</td>
      <td>[[50,51],[53,53],[86,86],[91,91],[167,168],[17...</td>
      <td>3p7z</td>
      <td>0</td>
      <td>5</td>
      <td>False</td>
      <td>P21359-2</td>
      <td>NF1_HUMAN</td>
      <td>0.98</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[5,276]]</td>
      <td>[[1545,1816]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[5,276]]</td>
      <td>[[1545,1816]]</td>
      <td>{"44":"I"}</td>
      <td>[[44,44]]</td>
      <td>[[1584,1584]]</td>
      <td>2818</td>
      <td>23</td>
      <td>[[40, 42], [47, 47], [66, 66], [70, 70], [78, ...</td>
      <td>270</td>
      <td>[[7, 276]]</td>
      <td>267.845</td>
      <td>[[1, 4]]</td>
      <td>0</td>
      <td>[]</td>
      <td>276</td>
      <td>276</td>
      <td>[[1, 276]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((7, 276),)</td>
      <td>270</td>
      <td>0.086380</td>
      <td>0.094542</td>
      <td>2.650</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20190717</td>
      <td>20101013</td>
      <td>0.377358</td>
      <td>-65</td>
      <td>False</td>
      <td>5</td>
      <td>P21359-6</td>
      <td>NF1_HUMAN</td>
      <td>0.98</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[5,276]]</td>
      <td>[[1545,1816]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[5,276]]</td>
      <td>[[1545,1816]]</td>
      <td>{"44":"I"}</td>
      <td>[[44,44]]</td>
      <td>[[1584,1584]]</td>
      <td>2836</td>
      <td>16</td>
      <td>[[80, 80], [92, 95], [101, 102], [110, 110], [...</td>
      <td>270</td>
      <td>[[7, 276]]</td>
      <td>269.180</td>
      <td>[[1, 4]]</td>
      <td>0</td>
      <td>[]</td>
      <td>276</td>
      <td>276</td>
      <td>[[1, 276]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((7, 276),)</td>
      <td>270</td>
      <td>0.088300</td>
      <td>0.093942</td>
      <td>-66</td>
      <td>True</td>
      <td>2</td>
      <td>False</td>
      <td>0.500000</td>
      <td>0.200000</td>
      <td>((1590, 1591), (1593, 1593), (1626, 1626), (16...</td>
      <td>((1590, 1591), (1593, 1593), (1626, 1626), (16...</td>
      <td>(P21359-2, P21359-6)</td>
      <td>False</td>
      <td>6</td>
    </tr>
    <tr>
      <th>23</th>
      <td>1</td>
      <td>B</td>
      <td>B</td>
      <td>B</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[7,43],[46,61],[63,80],[82,84],[86,157],[159,...</td>
      <td>[[50,51],[53,53],[86,86],[91,91],[167,168],[17...</td>
      <td>1</td>
      <td>A</td>
      <td>A</td>
      <td>A</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[7,44],[46,47],[49,62],[64,82],[84,84],[86,25...</td>
      <td>[[50,51],[53,53],[86,86],[91,91],[167,168],[17...</td>
      <td>3p7z</td>
      <td>0</td>
      <td>5</td>
      <td>False</td>
      <td>P21359-2</td>
      <td>NF1_HUMAN</td>
      <td>0.98</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[5,276]]</td>
      <td>[[1545,1816]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[5,276]]</td>
      <td>[[1545,1816]]</td>
      <td>{"44":"I"}</td>
      <td>[[44,44]]</td>
      <td>[[1584,1584]]</td>
      <td>2818</td>
      <td>16</td>
      <td>[[80, 80], [92, 95], [101, 102], [110, 110], [...</td>
      <td>270</td>
      <td>[[7, 276]]</td>
      <td>269.180</td>
      <td>[[1, 4]]</td>
      <td>0</td>
      <td>[]</td>
      <td>276</td>
      <td>276</td>
      <td>[[1, 276]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((7, 276),)</td>
      <td>270</td>
      <td>0.088864</td>
      <td>0.094542</td>
      <td>2.650</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20190717</td>
      <td>20101013</td>
      <td>0.377358</td>
      <td>-66</td>
      <td>True</td>
      <td>2</td>
      <td>P21359-6</td>
      <td>NF1_HUMAN</td>
      <td>0.98</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[5,276]]</td>
      <td>[[1545,1816]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[5,276]]</td>
      <td>[[1545,1816]]</td>
      <td>{"44":"I"}</td>
      <td>[[44,44]]</td>
      <td>[[1584,1584]]</td>
      <td>2836</td>
      <td>23</td>
      <td>[[40, 42], [47, 47], [66, 66], [70, 70], [78, ...</td>
      <td>270</td>
      <td>[[7, 276]]</td>
      <td>267.845</td>
      <td>[[1, 4]]</td>
      <td>0</td>
      <td>[]</td>
      <td>276</td>
      <td>276</td>
      <td>[[1, 276]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((7, 276),)</td>
      <td>270</td>
      <td>0.085832</td>
      <td>0.093942</td>
      <td>-65</td>
      <td>False</td>
      <td>5</td>
      <td>False</td>
      <td>0.500000</td>
      <td>0.200000</td>
      <td>((1590, 1591), (1593, 1593), (1626, 1626), (16...</td>
      <td>((1590, 1591), (1593, 1593), (1626, 1626), (16...</td>
      <td>(P21359-2, P21359-6)</td>
      <td>False</td>
      <td>8</td>
    </tr>
    <tr>
      <th>24</th>
      <td>1</td>
      <td>B</td>
      <td>B</td>
      <td>B</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[7,43],[46,61],[63,80],[82,84],[86,157],[159,...</td>
      <td>[[50,51],[53,53],[86,86],[91,91],[167,168],[17...</td>
      <td>1</td>
      <td>A</td>
      <td>A</td>
      <td>A</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[7,44],[46,47],[49,62],[64,82],[84,84],[86,25...</td>
      <td>[[50,51],[53,53],[86,86],[91,91],[167,168],[17...</td>
      <td>3p7z</td>
      <td>1</td>
      <td>5</td>
      <td>True</td>
      <td>P21359-2</td>
      <td>NF1_HUMAN</td>
      <td>0.98</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[5,276]]</td>
      <td>[[1545,1816]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[5,276]]</td>
      <td>[[1545,1816]]</td>
      <td>{"44":"I"}</td>
      <td>[[44,44]]</td>
      <td>[[1584,1584]]</td>
      <td>2818</td>
      <td>16</td>
      <td>[[80, 80], [92, 95], [101, 102], [110, 110], [...</td>
      <td>270</td>
      <td>[[7, 276]]</td>
      <td>269.180</td>
      <td>[[1, 4]]</td>
      <td>0</td>
      <td>[]</td>
      <td>276</td>
      <td>276</td>
      <td>[[1, 276]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((7, 276),)</td>
      <td>270</td>
      <td>0.088864</td>
      <td>0.094542</td>
      <td>2.650</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20190717</td>
      <td>20101013</td>
      <td>0.377358</td>
      <td>-66</td>
      <td>True</td>
      <td>2</td>
      <td>P21359</td>
      <td>NF1_HUMAN</td>
      <td>0.98</td>
      <td>True</td>
      <td>NF1_HUMAN</td>
      <td>[[5,276]]</td>
      <td>[[1566,1837]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[5,276]]</td>
      <td>[[1566,1837]]</td>
      <td>{"44":"I"}</td>
      <td>[[44,44]]</td>
      <td>[[1605,1605]]</td>
      <td>2839</td>
      <td>23</td>
      <td>[[40, 42], [47, 47], [66, 66], [70, 70], [78, ...</td>
      <td>270</td>
      <td>[[7, 276]]</td>
      <td>267.845</td>
      <td>[[1, 4]]</td>
      <td>0</td>
      <td>[]</td>
      <td>276</td>
      <td>276</td>
      <td>[[1, 276]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((7, 276),)</td>
      <td>270</td>
      <td>0.085741</td>
      <td>0.093842</td>
      <td>-65</td>
      <td>False</td>
      <td>3</td>
      <td>True</td>
      <td>0.500000</td>
      <td>0.333333</td>
      <td>((1590, 1591), (1593, 1593), (1626, 1626), (16...</td>
      <td>((1611, 1612), (1614, 1614), (1647, 1647), (16...</td>
      <td>(P21359-2, P21359)</td>
      <td>False</td>
      <td>7</td>
    </tr>
    <tr>
      <th>25</th>
      <td>1</td>
      <td>A</td>
      <td>A</td>
      <td>A</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[7,44],[46,47],[49,62],[64,82],[84,84],[86,25...</td>
      <td>[[50,51],[53,53],[86,86],[91,91],[167,168],[17...</td>
      <td>1</td>
      <td>B</td>
      <td>B</td>
      <td>B</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[7,43],[46,61],[63,80],[82,84],[86,157],[159,...</td>
      <td>[[50,51],[53,53],[86,86],[91,91],[167,168],[17...</td>
      <td>3p7z</td>
      <td>1</td>
      <td>5</td>
      <td>True</td>
      <td>P21359-2</td>
      <td>NF1_HUMAN</td>
      <td>0.98</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[5,276]]</td>
      <td>[[1545,1816]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[5,276]]</td>
      <td>[[1545,1816]]</td>
      <td>{"44":"I"}</td>
      <td>[[44,44]]</td>
      <td>[[1584,1584]]</td>
      <td>2818</td>
      <td>23</td>
      <td>[[40, 42], [47, 47], [66, 66], [70, 70], [78, ...</td>
      <td>270</td>
      <td>[[7, 276]]</td>
      <td>267.845</td>
      <td>[[1, 4]]</td>
      <td>0</td>
      <td>[]</td>
      <td>276</td>
      <td>276</td>
      <td>[[1, 276]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((7, 276),)</td>
      <td>270</td>
      <td>0.086380</td>
      <td>0.094542</td>
      <td>2.650</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20190717</td>
      <td>20101013</td>
      <td>0.377358</td>
      <td>-65</td>
      <td>False</td>
      <td>5</td>
      <td>P21359</td>
      <td>NF1_HUMAN</td>
      <td>0.98</td>
      <td>True</td>
      <td>NF1_HUMAN</td>
      <td>[[5,276]]</td>
      <td>[[1566,1837]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[5,276]]</td>
      <td>[[1566,1837]]</td>
      <td>{"44":"I"}</td>
      <td>[[44,44]]</td>
      <td>[[1605,1605]]</td>
      <td>2839</td>
      <td>16</td>
      <td>[[80, 80], [92, 95], [101, 102], [110, 110], [...</td>
      <td>270</td>
      <td>[[7, 276]]</td>
      <td>269.180</td>
      <td>[[1, 4]]</td>
      <td>0</td>
      <td>[]</td>
      <td>276</td>
      <td>276</td>
      <td>[[1, 276]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((7, 276),)</td>
      <td>270</td>
      <td>0.088207</td>
      <td>0.093842</td>
      <td>-66</td>
      <td>True</td>
      <td>1</td>
      <td>True</td>
      <td>1.000000</td>
      <td>0.200000</td>
      <td>((1590, 1591), (1593, 1593), (1626, 1626), (16...</td>
      <td>((1611, 1612), (1614, 1614), (1647, 1647), (16...</td>
      <td>(P21359-2, P21359)</td>
      <td>False</td>
      <td>3</td>
    </tr>
    <tr>
      <th>26</th>
      <td>1</td>
      <td>A</td>
      <td>A</td>
      <td>A</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[7,44],[46,47],[49,62],[64,82],[84,84],[86,25...</td>
      <td>[[50,51],[53,53],[86,86],[91,91],[167,168],[17...</td>
      <td>1</td>
      <td>B</td>
      <td>B</td>
      <td>B</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[7,43],[46,61],[63,80],[82,84],[86,157],[159,...</td>
      <td>[[50,51],[53,53],[86,86],[91,91],[167,168],[17...</td>
      <td>3p7z</td>
      <td>1</td>
      <td>5</td>
      <td>True</td>
      <td>P21359-2</td>
      <td>NF1_HUMAN</td>
      <td>0.98</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[5,276]]</td>
      <td>[[1545,1816]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[5,276]]</td>
      <td>[[1545,1816]]</td>
      <td>{"44":"I"}</td>
      <td>[[44,44]]</td>
      <td>[[1584,1584]]</td>
      <td>2818</td>
      <td>23</td>
      <td>[[40, 42], [47, 47], [66, 66], [70, 70], [78, ...</td>
      <td>270</td>
      <td>[[7, 276]]</td>
      <td>267.845</td>
      <td>[[1, 4]]</td>
      <td>0</td>
      <td>[]</td>
      <td>276</td>
      <td>276</td>
      <td>[[1, 276]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((7, 276),)</td>
      <td>270</td>
      <td>0.086380</td>
      <td>0.094542</td>
      <td>2.650</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20190717</td>
      <td>20101013</td>
      <td>0.377358</td>
      <td>-65</td>
      <td>False</td>
      <td>5</td>
      <td>P21359-6</td>
      <td>NF1_HUMAN</td>
      <td>0.98</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[5,276]]</td>
      <td>[[1545,1816]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[5,276]]</td>
      <td>[[1545,1816]]</td>
      <td>{"44":"I"}</td>
      <td>[[44,44]]</td>
      <td>[[1584,1584]]</td>
      <td>2836</td>
      <td>16</td>
      <td>[[80, 80], [92, 95], [101, 102], [110, 110], [...</td>
      <td>270</td>
      <td>[[7, 276]]</td>
      <td>269.180</td>
      <td>[[1, 4]]</td>
      <td>0</td>
      <td>[]</td>
      <td>276</td>
      <td>276</td>
      <td>[[1, 276]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((7, 276),)</td>
      <td>270</td>
      <td>0.088300</td>
      <td>0.093942</td>
      <td>-66</td>
      <td>True</td>
      <td>2</td>
      <td>True</td>
      <td>0.500000</td>
      <td>0.200000</td>
      <td>((1590, 1591), (1593, 1593), (1626, 1626), (16...</td>
      <td>((1590, 1591), (1593, 1593), (1626, 1626), (16...</td>
      <td>(P21359-2, P21359-6)</td>
      <td>False</td>
      <td>5</td>
    </tr>
    <tr>
      <th>27</th>
      <td>1</td>
      <td>B</td>
      <td>B</td>
      <td>B</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[7,43],[46,61],[63,80],[82,84],[86,157],[159,...</td>
      <td>[[50,51],[53,53],[86,86],[91,91],[167,168],[17...</td>
      <td>1</td>
      <td>A</td>
      <td>A</td>
      <td>A</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[7,44],[46,47],[49,62],[64,82],[84,84],[86,25...</td>
      <td>[[50,51],[53,53],[86,86],[91,91],[167,168],[17...</td>
      <td>3p7z</td>
      <td>1</td>
      <td>5</td>
      <td>True</td>
      <td>P21359-2</td>
      <td>NF1_HUMAN</td>
      <td>0.98</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[5,276]]</td>
      <td>[[1545,1816]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[5,276]]</td>
      <td>[[1545,1816]]</td>
      <td>{"44":"I"}</td>
      <td>[[44,44]]</td>
      <td>[[1584,1584]]</td>
      <td>2818</td>
      <td>16</td>
      <td>[[80, 80], [92, 95], [101, 102], [110, 110], [...</td>
      <td>270</td>
      <td>[[7, 276]]</td>
      <td>269.180</td>
      <td>[[1, 4]]</td>
      <td>0</td>
      <td>[]</td>
      <td>276</td>
      <td>276</td>
      <td>[[1, 276]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((7, 276),)</td>
      <td>270</td>
      <td>0.088864</td>
      <td>0.094542</td>
      <td>2.650</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20190717</td>
      <td>20101013</td>
      <td>0.377358</td>
      <td>-66</td>
      <td>True</td>
      <td>2</td>
      <td>P21359-6</td>
      <td>NF1_HUMAN</td>
      <td>0.98</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[5,276]]</td>
      <td>[[1545,1816]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[5,276]]</td>
      <td>[[1545,1816]]</td>
      <td>{"44":"I"}</td>
      <td>[[44,44]]</td>
      <td>[[1584,1584]]</td>
      <td>2836</td>
      <td>23</td>
      <td>[[40, 42], [47, 47], [66, 66], [70, 70], [78, ...</td>
      <td>270</td>
      <td>[[7, 276]]</td>
      <td>267.845</td>
      <td>[[1, 4]]</td>
      <td>0</td>
      <td>[]</td>
      <td>276</td>
      <td>276</td>
      <td>[[1, 276]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((7, 276),)</td>
      <td>270</td>
      <td>0.085832</td>
      <td>0.093942</td>
      <td>-65</td>
      <td>False</td>
      <td>5</td>
      <td>True</td>
      <td>0.500000</td>
      <td>0.200000</td>
      <td>((1590, 1591), (1593, 1593), (1626, 1626), (16...</td>
      <td>((1590, 1591), (1593, 1593), (1626, 1626), (16...</td>
      <td>(P21359-2, P21359-6)</td>
      <td>False</td>
      <td>7</td>
    </tr>
    <tr>
      <th>28</th>
      <td>1</td>
      <td>B</td>
      <td>B</td>
      <td>B</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[1,24],[28,28],[30,61],[63,63],[65,134],[136,...</td>
      <td>[[31,32],[34,34],[67,67],[72,72],[148,149],[15...</td>
      <td>1</td>
      <td>A</td>
      <td>A</td>
      <td>A</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[1,24],[28,235],[237,238],[240,256]]</td>
      <td>[[31,32],[34,34],[67,67],[72,72],[148,149],[15...</td>
      <td>3pg7</td>
      <td>0</td>
      <td>4</td>
      <td>False</td>
      <td>P21359-2</td>
      <td>NF1_HUMAN</td>
      <td>1.00</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[1,256]]</td>
      <td>[[1560,1816]]</td>
      <td>P21359</td>
      <td>[1]</td>
      <td>Deletion</td>
      <td>False</td>
      <td>False</td>
      <td>1</td>
      <td>((1, 191), (192, 256))</td>
      <td>((1560, 1750), (1752, 1816))</td>
      <td>{"191":"K"}</td>
      <td>[[191,191]]</td>
      <td>[[1750,1750]]</td>
      <td>2818</td>
      <td>17</td>
      <td>[[61, 61], [73, 74], [76, 76], [82, 83], [91, ...</td>
      <td>256</td>
      <td>[[1, 256]]</td>
      <td>249.123</td>
      <td>[]</td>
      <td>0</td>
      <td>[]</td>
      <td>256</td>
      <td>256</td>
      <td>[[1, 256]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((1, 256),)</td>
      <td>256</td>
      <td>0.083171</td>
      <td>0.089204</td>
      <td>2.189</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20110713</td>
      <td>20101031</td>
      <td>0.456830</td>
      <td>-66</td>
      <td>False</td>
      <td>8</td>
      <td>P21359</td>
      <td>NF1_HUMAN</td>
      <td>1.00</td>
      <td>True</td>
      <td>NF1_HUMAN</td>
      <td>[[1,256]]</td>
      <td>[[1581,1837]]</td>
      <td>P21359</td>
      <td>[1]</td>
      <td>Deletion</td>
      <td>False</td>
      <td>False</td>
      <td>1</td>
      <td>((1, 191), (192, 256))</td>
      <td>((1581, 1771), (1773, 1837))</td>
      <td>{"191":"K"}</td>
      <td>[[191,191]]</td>
      <td>[[1771,1771]]</td>
      <td>2839</td>
      <td>15</td>
      <td>[[13, 13], [28, 28], [61, 61], [73, 73], [75, ...</td>
      <td>256</td>
      <td>[[1, 256]]</td>
      <td>247.929</td>
      <td>[]</td>
      <td>0</td>
      <td>[]</td>
      <td>256</td>
      <td>256</td>
      <td>[[1, 256]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((1, 256),)</td>
      <td>256</td>
      <td>0.083261</td>
      <td>0.088544</td>
      <td>-65</td>
      <td>False</td>
      <td>5</td>
      <td>False</td>
      <td>0.200000</td>
      <td>0.125000</td>
      <td>((1590, 1591), (1593, 1593), (1626, 1626), (16...</td>
      <td>((1611, 1612), (1614, 1614), (1647, 1647), (16...</td>
      <td>(P21359-2, P21359)</td>
      <td>False</td>
      <td>10</td>
    </tr>
    <tr>
      <th>29</th>
      <td>1</td>
      <td>A</td>
      <td>A</td>
      <td>A</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[1,24],[28,235],[237,238],[240,256]]</td>
      <td>[[31,32],[34,34],[67,67],[72,72],[148,149],[15...</td>
      <td>1</td>
      <td>B</td>
      <td>B</td>
      <td>B</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[1,24],[28,28],[30,61],[63,63],[65,134],[136,...</td>
      <td>[[31,32],[34,34],[67,67],[72,72],[148,149],[15...</td>
      <td>3pg7</td>
      <td>0</td>
      <td>4</td>
      <td>False</td>
      <td>P21359-2</td>
      <td>NF1_HUMAN</td>
      <td>1.00</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[1,256]]</td>
      <td>[[1560,1816]]</td>
      <td>P21359</td>
      <td>[1]</td>
      <td>Deletion</td>
      <td>False</td>
      <td>False</td>
      <td>1</td>
      <td>((1, 191), (192, 256))</td>
      <td>((1560, 1750), (1752, 1816))</td>
      <td>{"191":"K"}</td>
      <td>[[191,191]]</td>
      <td>[[1750,1750]]</td>
      <td>2818</td>
      <td>15</td>
      <td>[[13, 13], [28, 28], [61, 61], [73, 73], [75, ...</td>
      <td>256</td>
      <td>[[1, 256]]</td>
      <td>247.929</td>
      <td>[]</td>
      <td>0</td>
      <td>[]</td>
      <td>256</td>
      <td>256</td>
      <td>[[1, 256]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((1, 256),)</td>
      <td>256</td>
      <td>0.083881</td>
      <td>0.089204</td>
      <td>2.189</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20110713</td>
      <td>20101031</td>
      <td>0.456830</td>
      <td>-65</td>
      <td>False</td>
      <td>7</td>
      <td>P21359</td>
      <td>NF1_HUMAN</td>
      <td>1.00</td>
      <td>True</td>
      <td>NF1_HUMAN</td>
      <td>[[1,256]]</td>
      <td>[[1581,1837]]</td>
      <td>P21359</td>
      <td>[1]</td>
      <td>Deletion</td>
      <td>False</td>
      <td>False</td>
      <td>1</td>
      <td>((1, 191), (192, 256))</td>
      <td>((1581, 1771), (1773, 1837))</td>
      <td>{"191":"K"}</td>
      <td>[[191,191]]</td>
      <td>[[1771,1771]]</td>
      <td>2839</td>
      <td>17</td>
      <td>[[61, 61], [73, 74], [76, 76], [82, 83], [91, ...</td>
      <td>256</td>
      <td>[[1, 256]]</td>
      <td>249.123</td>
      <td>[]</td>
      <td>0</td>
      <td>[]</td>
      <td>256</td>
      <td>256</td>
      <td>[[1, 256]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((1, 256),)</td>
      <td>256</td>
      <td>0.082556</td>
      <td>0.088544</td>
      <td>-66</td>
      <td>False</td>
      <td>6</td>
      <td>False</td>
      <td>0.166667</td>
      <td>0.142857</td>
      <td>((1590, 1591), (1593, 1593), (1626, 1626), (16...</td>
      <td>((1611, 1612), (1614, 1614), (1647, 1647), (16...</td>
      <td>(P21359-2, P21359)</td>
      <td>False</td>
      <td>9</td>
    </tr>
    <tr>
      <th>30</th>
      <td>1</td>
      <td>A</td>
      <td>A</td>
      <td>A</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[1,24],[28,235],[237,238],[240,256]]</td>
      <td>[[31,32],[34,34],[67,67],[72,72],[148,149],[15...</td>
      <td>1</td>
      <td>B</td>
      <td>B</td>
      <td>B</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[1,24],[28,28],[30,61],[63,63],[65,134],[136,...</td>
      <td>[[31,32],[34,34],[67,67],[72,72],[148,149],[15...</td>
      <td>3pg7</td>
      <td>0</td>
      <td>4</td>
      <td>False</td>
      <td>P21359-2</td>
      <td>NF1_HUMAN</td>
      <td>1.00</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[1,256]]</td>
      <td>[[1560,1816]]</td>
      <td>P21359</td>
      <td>[1]</td>
      <td>Deletion</td>
      <td>False</td>
      <td>False</td>
      <td>1</td>
      <td>((1, 191), (192, 256))</td>
      <td>((1560, 1750), (1752, 1816))</td>
      <td>{"191":"K"}</td>
      <td>[[191,191]]</td>
      <td>[[1750,1750]]</td>
      <td>2818</td>
      <td>15</td>
      <td>[[13, 13], [28, 28], [61, 61], [73, 73], [75, ...</td>
      <td>256</td>
      <td>[[1, 256]]</td>
      <td>247.929</td>
      <td>[]</td>
      <td>0</td>
      <td>[]</td>
      <td>256</td>
      <td>256</td>
      <td>[[1, 256]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((1, 256),)</td>
      <td>256</td>
      <td>0.083881</td>
      <td>0.089204</td>
      <td>2.189</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20110713</td>
      <td>20101031</td>
      <td>0.456830</td>
      <td>-65</td>
      <td>False</td>
      <td>7</td>
      <td>P21359-4</td>
      <td>NF1_HUMAN</td>
      <td>0.91</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[1,11]]</td>
      <td>[[1581,1591]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[1,11]]</td>
      <td>[[1581,1591]]</td>
      <td>{"11":"T"}</td>
      <td>[[11,11]]</td>
      <td>[[1591,1591]]</td>
      <td>1598</td>
      <td>17</td>
      <td>[[61, 61], [73, 74], [76, 76], [82, 83], [91, ...</td>
      <td>256</td>
      <td>[[1, 256]]</td>
      <td>249.123</td>
      <td>[]</td>
      <td>0</td>
      <td>[]</td>
      <td>256</td>
      <td>256</td>
      <td>[[1, 256]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((1, 256),)</td>
      <td>256</td>
      <td>-0.153942</td>
      <td>-0.143304</td>
      <td>-66</td>
      <td>False</td>
      <td>-1</td>
      <td>False</td>
      <td>-1.000000</td>
      <td>0.142857</td>
      <td>((1590, 1591), (1593, 1593), (1626, 1626), (16...</td>
      <td>()</td>
      <td>(P21359-2, P21359-4)</td>
      <td>False</td>
      <td>-1</td>
    </tr>
    <tr>
      <th>31</th>
      <td>1</td>
      <td>A</td>
      <td>A</td>
      <td>A</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[1,24],[28,235],[237,238],[240,256]]</td>
      <td>[[31,32],[34,34],[67,67],[72,72],[148,149],[15...</td>
      <td>1</td>
      <td>B</td>
      <td>B</td>
      <td>B</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[1,24],[28,28],[30,61],[63,63],[65,134],[136,...</td>
      <td>[[31,32],[34,34],[67,67],[72,72],[148,149],[15...</td>
      <td>3pg7</td>
      <td>0</td>
      <td>4</td>
      <td>False</td>
      <td>P21359-2</td>
      <td>NF1_HUMAN</td>
      <td>1.00</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[1,256]]</td>
      <td>[[1560,1816]]</td>
      <td>P21359</td>
      <td>[1]</td>
      <td>Deletion</td>
      <td>False</td>
      <td>False</td>
      <td>1</td>
      <td>((1, 191), (192, 256))</td>
      <td>((1560, 1750), (1752, 1816))</td>
      <td>{"191":"K"}</td>
      <td>[[191,191]]</td>
      <td>[[1750,1750]]</td>
      <td>2818</td>
      <td>15</td>
      <td>[[13, 13], [28, 28], [61, 61], [73, 73], [75, ...</td>
      <td>256</td>
      <td>[[1, 256]]</td>
      <td>247.929</td>
      <td>[]</td>
      <td>0</td>
      <td>[]</td>
      <td>256</td>
      <td>256</td>
      <td>[[1, 256]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((1, 256),)</td>
      <td>256</td>
      <td>0.083881</td>
      <td>0.089204</td>
      <td>2.189</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20110713</td>
      <td>20101031</td>
      <td>0.456830</td>
      <td>-65</td>
      <td>False</td>
      <td>7</td>
      <td>P21359-6</td>
      <td>NF1_HUMAN</td>
      <td>1.00</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[1,256]]</td>
      <td>[[1560,1816]]</td>
      <td>P21359</td>
      <td>[1]</td>
      <td>Deletion</td>
      <td>False</td>
      <td>False</td>
      <td>1</td>
      <td>((1, 191), (192, 256))</td>
      <td>((1560, 1750), (1752, 1816))</td>
      <td>{"191":"K"}</td>
      <td>[[191,191]]</td>
      <td>[[1750,1750]]</td>
      <td>2836</td>
      <td>17</td>
      <td>[[61, 61], [73, 74], [76, 76], [82, 83], [91, ...</td>
      <td>256</td>
      <td>[[1, 256]]</td>
      <td>249.123</td>
      <td>[]</td>
      <td>0</td>
      <td>[]</td>
      <td>256</td>
      <td>256</td>
      <td>[[1, 256]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((1, 256),)</td>
      <td>256</td>
      <td>0.082643</td>
      <td>0.088638</td>
      <td>-66</td>
      <td>False</td>
      <td>8</td>
      <td>False</td>
      <td>0.142857</td>
      <td>0.125000</td>
      <td>((1590, 1591), (1593, 1593), (1626, 1626), (16...</td>
      <td>((1590, 1591), (1593, 1593), (1626, 1626), (16...</td>
      <td>(P21359-2, P21359-6)</td>
      <td>False</td>
      <td>9</td>
    </tr>
    <tr>
      <th>32</th>
      <td>1</td>
      <td>B</td>
      <td>B</td>
      <td>B</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[1,24],[28,28],[30,61],[63,63],[65,134],[136,...</td>
      <td>[[31,32],[34,34],[67,67],[72,72],[148,149],[15...</td>
      <td>1</td>
      <td>A</td>
      <td>A</td>
      <td>A</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[1,24],[28,235],[237,238],[240,256]]</td>
      <td>[[31,32],[34,34],[67,67],[72,72],[148,149],[15...</td>
      <td>3pg7</td>
      <td>0</td>
      <td>4</td>
      <td>False</td>
      <td>P21359-2</td>
      <td>NF1_HUMAN</td>
      <td>1.00</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[1,256]]</td>
      <td>[[1560,1816]]</td>
      <td>P21359</td>
      <td>[1]</td>
      <td>Deletion</td>
      <td>False</td>
      <td>False</td>
      <td>1</td>
      <td>((1, 191), (192, 256))</td>
      <td>((1560, 1750), (1752, 1816))</td>
      <td>{"191":"K"}</td>
      <td>[[191,191]]</td>
      <td>[[1750,1750]]</td>
      <td>2818</td>
      <td>17</td>
      <td>[[61, 61], [73, 74], [76, 76], [82, 83], [91, ...</td>
      <td>256</td>
      <td>[[1, 256]]</td>
      <td>249.123</td>
      <td>[]</td>
      <td>0</td>
      <td>[]</td>
      <td>256</td>
      <td>256</td>
      <td>[[1, 256]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((1, 256),)</td>
      <td>256</td>
      <td>0.083171</td>
      <td>0.089204</td>
      <td>2.189</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20110713</td>
      <td>20101031</td>
      <td>0.456830</td>
      <td>-66</td>
      <td>False</td>
      <td>8</td>
      <td>P21359-4</td>
      <td>NF1_HUMAN</td>
      <td>0.91</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[1,11]]</td>
      <td>[[1581,1591]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[1,11]]</td>
      <td>[[1581,1591]]</td>
      <td>{"11":"T"}</td>
      <td>[[11,11]]</td>
      <td>[[1591,1591]]</td>
      <td>1598</td>
      <td>15</td>
      <td>[[13, 13], [28, 28], [61, 61], [73, 73], [75, ...</td>
      <td>256</td>
      <td>[[1, 256]]</td>
      <td>247.929</td>
      <td>[]</td>
      <td>0</td>
      <td>[]</td>
      <td>256</td>
      <td>256</td>
      <td>[[1, 256]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((1, 256),)</td>
      <td>256</td>
      <td>-0.152691</td>
      <td>-0.143304</td>
      <td>-65</td>
      <td>False</td>
      <td>-1</td>
      <td>False</td>
      <td>-1.000000</td>
      <td>0.125000</td>
      <td>((1590, 1591), (1593, 1593), (1626, 1626), (16...</td>
      <td>()</td>
      <td>(P21359-2, P21359-4)</td>
      <td>False</td>
      <td>-1</td>
    </tr>
    <tr>
      <th>33</th>
      <td>1</td>
      <td>B</td>
      <td>B</td>
      <td>B</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[1,24],[28,28],[30,61],[63,63],[65,134],[136,...</td>
      <td>[[31,32],[34,34],[67,67],[72,72],[148,149],[15...</td>
      <td>1</td>
      <td>A</td>
      <td>A</td>
      <td>A</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[1,24],[28,235],[237,238],[240,256]]</td>
      <td>[[31,32],[34,34],[67,67],[72,72],[148,149],[15...</td>
      <td>3pg7</td>
      <td>0</td>
      <td>4</td>
      <td>False</td>
      <td>P21359-2</td>
      <td>NF1_HUMAN</td>
      <td>1.00</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[1,256]]</td>
      <td>[[1560,1816]]</td>
      <td>P21359</td>
      <td>[1]</td>
      <td>Deletion</td>
      <td>False</td>
      <td>False</td>
      <td>1</td>
      <td>((1, 191), (192, 256))</td>
      <td>((1560, 1750), (1752, 1816))</td>
      <td>{"191":"K"}</td>
      <td>[[191,191]]</td>
      <td>[[1750,1750]]</td>
      <td>2818</td>
      <td>17</td>
      <td>[[61, 61], [73, 74], [76, 76], [82, 83], [91, ...</td>
      <td>256</td>
      <td>[[1, 256]]</td>
      <td>249.123</td>
      <td>[]</td>
      <td>0</td>
      <td>[]</td>
      <td>256</td>
      <td>256</td>
      <td>[[1, 256]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((1, 256),)</td>
      <td>256</td>
      <td>0.083171</td>
      <td>0.089204</td>
      <td>2.189</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20110713</td>
      <td>20101031</td>
      <td>0.456830</td>
      <td>-66</td>
      <td>False</td>
      <td>8</td>
      <td>P21359-6</td>
      <td>NF1_HUMAN</td>
      <td>1.00</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[1,256]]</td>
      <td>[[1560,1816]]</td>
      <td>P21359</td>
      <td>[1]</td>
      <td>Deletion</td>
      <td>False</td>
      <td>False</td>
      <td>1</td>
      <td>((1, 191), (192, 256))</td>
      <td>((1560, 1750), (1752, 1816))</td>
      <td>{"191":"K"}</td>
      <td>[[191,191]]</td>
      <td>[[1750,1750]]</td>
      <td>2836</td>
      <td>15</td>
      <td>[[13, 13], [28, 28], [61, 61], [73, 73], [75, ...</td>
      <td>256</td>
      <td>[[1, 256]]</td>
      <td>247.929</td>
      <td>[]</td>
      <td>0</td>
      <td>[]</td>
      <td>256</td>
      <td>256</td>
      <td>[[1, 256]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((1, 256),)</td>
      <td>256</td>
      <td>0.083349</td>
      <td>0.088638</td>
      <td>-65</td>
      <td>False</td>
      <td>7</td>
      <td>False</td>
      <td>0.142857</td>
      <td>0.125000</td>
      <td>((1590, 1591), (1593, 1593), (1626, 1626), (16...</td>
      <td>((1590, 1591), (1593, 1593), (1626, 1626), (16...</td>
      <td>(P21359-2, P21359-6)</td>
      <td>False</td>
      <td>10</td>
    </tr>
    <tr>
      <th>34</th>
      <td>2</td>
      <td>D</td>
      <td>D</td>
      <td>D</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[12,53],[55,76],[78,80],[82,85],[87,100],[102...</td>
      <td>[[99,99],[194,194],[197,197],[199,201]]</td>
      <td>2</td>
      <td>B</td>
      <td>B</td>
      <td>B</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[12,48],[50,53],[55,76],[78,80],[82,85],[87,1...</td>
      <td>[[125,125],[231,231],[234,235],[237,238],[241,...</td>
      <td>6ob2</td>
      <td>0</td>
      <td>9</td>
      <td>False</td>
      <td>P21359-2</td>
      <td>NF1_HUMAN</td>
      <td>1.00</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2818</td>
      <td>0</td>
      <td>[]</td>
      <td>245</td>
      <td>[[12, 256]]</td>
      <td>239.938</td>
      <td>[[1, 1]]</td>
      <td>0</td>
      <td>[]</td>
      <td>256</td>
      <td>256</td>
      <td>[[1, 256]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((12, 256),)</td>
      <td>245</td>
      <td>0.080586</td>
      <td>0.080586</td>
      <td>2.845</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20191113</td>
      <td>20190319</td>
      <td>0.351494</td>
      <td>-68</td>
      <td>False</td>
      <td>9</td>
      <td>P21359</td>
      <td>NF1_HUMAN</td>
      <td>0.92</td>
      <td>True</td>
      <td>NF1_HUMAN</td>
      <td>[[2,256]]</td>
      <td>[[1209,1484]]</td>
      <td>P21359</td>
      <td>[21]</td>
      <td>Deletion</td>
      <td>False</td>
      <td>False</td>
      <td>21</td>
      <td>((2, 164), (165, 256))</td>
      <td>((1209, 1371), (1393, 1484))</td>
      <td>{"164":"A"}</td>
      <td>[[164,164]]</td>
      <td>[[1371,1371]]</td>
      <td>2839</td>
      <td>8</td>
      <td>[[18, 19], [22, 22], [191, 192], [202, 202], [...</td>
      <td>241</td>
      <td>[[12, 103], [107, 255]]</td>
      <td>236.933</td>
      <td>[[1, 1]]</td>
      <td>0</td>
      <td>[]</td>
      <td>256</td>
      <td>256</td>
      <td>[[1, 256]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((12, 103), (107, 255))</td>
      <td>241</td>
      <td>0.039043</td>
      <td>0.041861</td>
      <td>-66</td>
      <td>False</td>
      <td>14</td>
      <td>False</td>
      <td>0.111111</td>
      <td>0.071429</td>
      <td>((1306, 1306), (1401, 1401), (1404, 1404), (14...</td>
      <td>((1332, 1332), (1459, 1459), (1462, 1463), (14...</td>
      <td>(P21359-2, P21359)</td>
      <td>False</td>
      <td>18</td>
    </tr>
    <tr>
      <th>35</th>
      <td>2</td>
      <td>B</td>
      <td>B</td>
      <td>B</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[12,48],[50,53],[55,76],[78,80],[82,85],[87,1...</td>
      <td>[[125,125],[231,231],[234,235],[237,238],[241,...</td>
      <td>2</td>
      <td>D</td>
      <td>D</td>
      <td>D</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[12,53],[55,76],[78,80],[82,85],[87,100],[102...</td>
      <td>[[99,99],[194,194],[197,197],[199,201]]</td>
      <td>6ob2</td>
      <td>0</td>
      <td>9</td>
      <td>False</td>
      <td>P21359-2</td>
      <td>NF1_HUMAN</td>
      <td>1.00</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2818</td>
      <td>8</td>
      <td>[[18, 19], [22, 22], [191, 192], [202, 202], [...</td>
      <td>241</td>
      <td>[[12, 103], [107, 255]]</td>
      <td>236.933</td>
      <td>[[1, 1]]</td>
      <td>0</td>
      <td>[]</td>
      <td>256</td>
      <td>256</td>
      <td>[[1, 256]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((12, 103), (107, 255))</td>
      <td>241</td>
      <td>0.073786</td>
      <td>0.076625</td>
      <td>2.845</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20191113</td>
      <td>20190319</td>
      <td>0.351494</td>
      <td>-66</td>
      <td>False</td>
      <td>14</td>
      <td>P21359</td>
      <td>NF1_HUMAN</td>
      <td>0.92</td>
      <td>True</td>
      <td>NF1_HUMAN</td>
      <td>[[2,256]]</td>
      <td>[[1209,1484]]</td>
      <td>P21359</td>
      <td>[21]</td>
      <td>Deletion</td>
      <td>False</td>
      <td>False</td>
      <td>21</td>
      <td>((2, 164), (165, 256))</td>
      <td>((1209, 1371), (1393, 1484))</td>
      <td>{"164":"A"}</td>
      <td>[[164,164]]</td>
      <td>[[1371,1371]]</td>
      <td>2839</td>
      <td>0</td>
      <td>[]</td>
      <td>245</td>
      <td>[[12, 256]]</td>
      <td>239.938</td>
      <td>[[1, 1]]</td>
      <td>0</td>
      <td>[]</td>
      <td>256</td>
      <td>256</td>
      <td>[[1, 256]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((12, 256),)</td>
      <td>245</td>
      <td>0.045793</td>
      <td>0.045793</td>
      <td>-68</td>
      <td>False</td>
      <td>11</td>
      <td>False</td>
      <td>0.090909</td>
      <td>0.071429</td>
      <td>((1332, 1332), (1438, 1438), (1441, 1442), (14...</td>
      <td>((1306, 1306), (1422, 1422), (1425, 1425), (14...</td>
      <td>(P21359-2, P21359)</td>
      <td>False</td>
      <td>16</td>
    </tr>
    <tr>
      <th>36</th>
      <td>2</td>
      <td>B</td>
      <td>B</td>
      <td>B</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[12,48],[50,53],[55,76],[78,80],[82,85],[87,1...</td>
      <td>[[125,125],[231,231],[234,235],[237,238],[241,...</td>
      <td>2</td>
      <td>D</td>
      <td>D</td>
      <td>D</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[12,53],[55,76],[78,80],[82,85],[87,100],[102...</td>
      <td>[[99,99],[194,194],[197,197],[199,201]]</td>
      <td>6ob2</td>
      <td>0</td>
      <td>9</td>
      <td>False</td>
      <td>P21359-2</td>
      <td>NF1_HUMAN</td>
      <td>1.00</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2818</td>
      <td>8</td>
      <td>[[18, 19], [22, 22], [191, 192], [202, 202], [...</td>
      <td>241</td>
      <td>[[12, 103], [107, 255]]</td>
      <td>236.933</td>
      <td>[[1, 1]]</td>
      <td>0</td>
      <td>[]</td>
      <td>256</td>
      <td>256</td>
      <td>[[1, 256]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((12, 103), (107, 255))</td>
      <td>241</td>
      <td>0.073786</td>
      <td>0.076625</td>
      <td>2.845</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20191113</td>
      <td>20190319</td>
      <td>0.351494</td>
      <td>-66</td>
      <td>False</td>
      <td>14</td>
      <td>P21359-4</td>
      <td>NF1_HUMAN</td>
      <td>0.92</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[2,256]]</td>
      <td>[[1209,1484]]</td>
      <td>P21359</td>
      <td>[21]</td>
      <td>Deletion</td>
      <td>False</td>
      <td>False</td>
      <td>21</td>
      <td>((2, 164), (165, 256))</td>
      <td>((1209, 1371), (1393, 1484))</td>
      <td>{"164":"A"}</td>
      <td>[[164,164]]</td>
      <td>[[1371,1371]]</td>
      <td>1598</td>
      <td>0</td>
      <td>[]</td>
      <td>245</td>
      <td>[[12, 256]]</td>
      <td>239.938</td>
      <td>[[1, 1]]</td>
      <td>0</td>
      <td>[]</td>
      <td>256</td>
      <td>256</td>
      <td>[[1, 256]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((12, 256),)</td>
      <td>245</td>
      <td>0.081355</td>
      <td>0.081355</td>
      <td>-68</td>
      <td>False</td>
      <td>3</td>
      <td>False</td>
      <td>0.333333</td>
      <td>0.071429</td>
      <td>((1332, 1332), (1438, 1438), (1441, 1442), (14...</td>
      <td>((1306, 1306), (1422, 1422), (1425, 1425), (14...</td>
      <td>(P21359-2, P21359-4)</td>
      <td>False</td>
      <td>3</td>
    </tr>
    <tr>
      <th>37</th>
      <td>2</td>
      <td>B</td>
      <td>B</td>
      <td>B</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[12,48],[50,53],[55,76],[78,80],[82,85],[87,1...</td>
      <td>[[125,125],[231,231],[234,235],[237,238],[241,...</td>
      <td>2</td>
      <td>D</td>
      <td>D</td>
      <td>D</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[12,53],[55,76],[78,80],[82,85],[87,100],[102...</td>
      <td>[[99,99],[194,194],[197,197],[199,201]]</td>
      <td>6ob2</td>
      <td>0</td>
      <td>9</td>
      <td>False</td>
      <td>P21359-2</td>
      <td>NF1_HUMAN</td>
      <td>1.00</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2818</td>
      <td>8</td>
      <td>[[18, 19], [22, 22], [191, 192], [202, 202], [...</td>
      <td>241</td>
      <td>[[12, 103], [107, 255]]</td>
      <td>236.933</td>
      <td>[[1, 1]]</td>
      <td>0</td>
      <td>[]</td>
      <td>256</td>
      <td>256</td>
      <td>[[1, 256]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((12, 103), (107, 255))</td>
      <td>241</td>
      <td>0.073786</td>
      <td>0.076625</td>
      <td>2.845</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20191113</td>
      <td>20190319</td>
      <td>0.351494</td>
      <td>-66</td>
      <td>False</td>
      <td>14</td>
      <td>P21359-6</td>
      <td>NF1_HUMAN</td>
      <td>1.00</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2836</td>
      <td>0</td>
      <td>[]</td>
      <td>245</td>
      <td>[[12, 256]]</td>
      <td>239.938</td>
      <td>[[1, 1]]</td>
      <td>0</td>
      <td>[]</td>
      <td>256</td>
      <td>256</td>
      <td>[[1, 256]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((12, 256),)</td>
      <td>245</td>
      <td>0.080075</td>
      <td>0.080075</td>
      <td>-68</td>
      <td>False</td>
      <td>9</td>
      <td>False</td>
      <td>0.111111</td>
      <td>0.071429</td>
      <td>((1332, 1332), (1438, 1438), (1441, 1442), (14...</td>
      <td>((1306, 1306), (1401, 1401), (1404, 1404), (14...</td>
      <td>(P21359-2, P21359-6)</td>
      <td>False</td>
      <td>17</td>
    </tr>
    <tr>
      <th>38</th>
      <td>2</td>
      <td>D</td>
      <td>D</td>
      <td>D</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[12,53],[55,76],[78,80],[82,85],[87,100],[102...</td>
      <td>[[99,99],[194,194],[197,197],[199,201]]</td>
      <td>2</td>
      <td>B</td>
      <td>B</td>
      <td>B</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[12,48],[50,53],[55,76],[78,80],[82,85],[87,1...</td>
      <td>[[125,125],[231,231],[234,235],[237,238],[241,...</td>
      <td>6ob2</td>
      <td>0</td>
      <td>9</td>
      <td>False</td>
      <td>P21359-2</td>
      <td>NF1_HUMAN</td>
      <td>1.00</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2818</td>
      <td>0</td>
      <td>[]</td>
      <td>245</td>
      <td>[[12, 256]]</td>
      <td>239.938</td>
      <td>[[1, 1]]</td>
      <td>0</td>
      <td>[]</td>
      <td>256</td>
      <td>256</td>
      <td>[[1, 256]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((12, 256),)</td>
      <td>245</td>
      <td>0.080586</td>
      <td>0.080586</td>
      <td>2.845</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20191113</td>
      <td>20190319</td>
      <td>0.351494</td>
      <td>-68</td>
      <td>False</td>
      <td>9</td>
      <td>P21359-4</td>
      <td>NF1_HUMAN</td>
      <td>0.92</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[2,256]]</td>
      <td>[[1209,1484]]</td>
      <td>P21359</td>
      <td>[21]</td>
      <td>Deletion</td>
      <td>False</td>
      <td>False</td>
      <td>21</td>
      <td>((2, 164), (165, 256))</td>
      <td>((1209, 1371), (1393, 1484))</td>
      <td>{"164":"A"}</td>
      <td>[[164,164]]</td>
      <td>[[1371,1371]]</td>
      <td>1598</td>
      <td>8</td>
      <td>[[18, 19], [22, 22], [191, 192], [202, 202], [...</td>
      <td>241</td>
      <td>[[12, 103], [107, 255]]</td>
      <td>236.933</td>
      <td>[[1, 1]]</td>
      <td>0</td>
      <td>[]</td>
      <td>256</td>
      <td>256</td>
      <td>[[1, 256]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((12, 103), (107, 255))</td>
      <td>241</td>
      <td>0.069364</td>
      <td>0.074370</td>
      <td>-66</td>
      <td>False</td>
      <td>6</td>
      <td>False</td>
      <td>0.166667</td>
      <td>0.111111</td>
      <td>((1306, 1306), (1401, 1401), (1404, 1404), (14...</td>
      <td>((1332, 1332), (1459, 1459), (1462, 1463), (14...</td>
      <td>(P21359-2, P21359-4)</td>
      <td>False</td>
      <td>4</td>
    </tr>
    <tr>
      <th>39</th>
      <td>2</td>
      <td>D</td>
      <td>D</td>
      <td>D</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[12,53],[55,76],[78,80],[82,85],[87,100],[102...</td>
      <td>[[99,99],[194,194],[197,197],[199,201]]</td>
      <td>2</td>
      <td>B</td>
      <td>B</td>
      <td>B</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[12,48],[50,53],[55,76],[78,80],[82,85],[87,1...</td>
      <td>[[125,125],[231,231],[234,235],[237,238],[241,...</td>
      <td>6ob2</td>
      <td>0</td>
      <td>9</td>
      <td>False</td>
      <td>P21359-2</td>
      <td>NF1_HUMAN</td>
      <td>1.00</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2818</td>
      <td>0</td>
      <td>[]</td>
      <td>245</td>
      <td>[[12, 256]]</td>
      <td>239.938</td>
      <td>[[1, 1]]</td>
      <td>0</td>
      <td>[]</td>
      <td>256</td>
      <td>256</td>
      <td>[[1, 256]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((12, 256),)</td>
      <td>245</td>
      <td>0.080586</td>
      <td>0.080586</td>
      <td>2.845</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20191113</td>
      <td>20190319</td>
      <td>0.351494</td>
      <td>-68</td>
      <td>False</td>
      <td>9</td>
      <td>P21359-6</td>
      <td>NF1_HUMAN</td>
      <td>1.00</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2836</td>
      <td>8</td>
      <td>[[18, 19], [22, 22], [191, 192], [202, 202], [...</td>
      <td>241</td>
      <td>[[12, 103], [107, 255]]</td>
      <td>236.933</td>
      <td>[[1, 1]]</td>
      <td>0</td>
      <td>[]</td>
      <td>256</td>
      <td>256</td>
      <td>[[1, 256]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((12, 103), (107, 255))</td>
      <td>241</td>
      <td>0.073318</td>
      <td>0.076139</td>
      <td>-66</td>
      <td>False</td>
      <td>14</td>
      <td>False</td>
      <td>0.111111</td>
      <td>0.071429</td>
      <td>((1306, 1306), (1401, 1401), (1404, 1404), (14...</td>
      <td>((1332, 1332), (1438, 1438), (1441, 1442), (14...</td>
      <td>(P21359-2, P21359-6)</td>
      <td>False</td>
      <td>18</td>
    </tr>
    <tr>
      <th>40</th>
      <td>2</td>
      <td>D</td>
      <td>D</td>
      <td>D</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[10,48],[50,53],[55,76],[79,80],[82,85],[87,9...</td>
      <td>[[91,91],[95,95],[99,99],[194,195],[197,197],[...</td>
      <td>2</td>
      <td>B</td>
      <td>B</td>
      <td>B</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[12,48],[50,53],[55,73],[75,76],[78,80],[82,8...</td>
      <td>[[228,228],[231,232],[234,235],[237,238],[241,...</td>
      <td>6ob3</td>
      <td>0</td>
      <td>10</td>
      <td>False</td>
      <td>P21359-2</td>
      <td>NF1_HUMAN</td>
      <td>1.00</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2818</td>
      <td>7</td>
      <td>[[41, 41], [44, 44], [126, 126], [133, 133], [...</td>
      <td>247</td>
      <td>[[10, 256]]</td>
      <td>244.327</td>
      <td>[[1, 1]]</td>
      <td>0</td>
      <td>[]</td>
      <td>256</td>
      <td>256</td>
      <td>[[1, 256]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((10, 256),)</td>
      <td>247</td>
      <td>0.080083</td>
      <td>0.082567</td>
      <td>2.100</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20191113</td>
      <td>20190319</td>
      <td>0.476190</td>
      <td>-68</td>
      <td>False</td>
      <td>10</td>
      <td>P21359</td>
      <td>NF1_HUMAN</td>
      <td>0.92</td>
      <td>True</td>
      <td>NF1_HUMAN</td>
      <td>[[2,256]]</td>
      <td>[[1209,1484]]</td>
      <td>P21359</td>
      <td>[21]</td>
      <td>Deletion</td>
      <td>False</td>
      <td>False</td>
      <td>21</td>
      <td>((2, 164), (165, 256))</td>
      <td>((1209, 1371), (1393, 1484))</td>
      <td>{"164":"A"}</td>
      <td>[[164,164]]</td>
      <td>[[1371,1371]]</td>
      <td>2839</td>
      <td>10</td>
      <td>[[41, 41], [51, 51], [69, 69], [129, 130], [13...</td>
      <td>245</td>
      <td>[[12, 256]]</td>
      <td>241.495</td>
      <td>[[1, 1]]</td>
      <td>0</td>
      <td>[]</td>
      <td>256</td>
      <td>256</td>
      <td>[[1, 256]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((12, 256),)</td>
      <td>245</td>
      <td>0.042271</td>
      <td>0.045793</td>
      <td>-66</td>
      <td>False</td>
      <td>13</td>
      <td>False</td>
      <td>0.100000</td>
      <td>0.076923</td>
      <td>((1298, 1298), (1302, 1302), (1306, 1306), (14...</td>
      <td>((1456, 1456), (1459, 1460), (1462, 1463), (14...</td>
      <td>(P21359-2, P21359)</td>
      <td>True</td>
      <td>17</td>
    </tr>
    <tr>
      <th>41</th>
      <td>2</td>
      <td>B</td>
      <td>B</td>
      <td>B</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[12,48],[50,53],[55,73],[75,76],[78,80],[82,8...</td>
      <td>[[228,228],[231,232],[234,235],[237,238],[241,...</td>
      <td>2</td>
      <td>D</td>
      <td>D</td>
      <td>D</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[10,48],[50,53],[55,76],[79,80],[82,85],[87,9...</td>
      <td>[[91,91],[95,95],[99,99],[194,195],[197,197],[...</td>
      <td>6ob3</td>
      <td>0</td>
      <td>10</td>
      <td>False</td>
      <td>P21359-2</td>
      <td>NF1_HUMAN</td>
      <td>1.00</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2818</td>
      <td>10</td>
      <td>[[41, 41], [51, 51], [69, 69], [129, 130], [13...</td>
      <td>245</td>
      <td>[[12, 256]]</td>
      <td>241.495</td>
      <td>[[1, 1]]</td>
      <td>0</td>
      <td>[]</td>
      <td>256</td>
      <td>256</td>
      <td>[[1, 256]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((12, 256),)</td>
      <td>245</td>
      <td>0.077038</td>
      <td>0.080586</td>
      <td>2.100</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20191113</td>
      <td>20190319</td>
      <td>0.476190</td>
      <td>-66</td>
      <td>False</td>
      <td>11</td>
      <td>P21359</td>
      <td>NF1_HUMAN</td>
      <td>0.92</td>
      <td>True</td>
      <td>NF1_HUMAN</td>
      <td>[[2,256]]</td>
      <td>[[1209,1484]]</td>
      <td>P21359</td>
      <td>[21]</td>
      <td>Deletion</td>
      <td>False</td>
      <td>False</td>
      <td>21</td>
      <td>((2, 164), (165, 256))</td>
      <td>((1209, 1371), (1393, 1484))</td>
      <td>{"164":"A"}</td>
      <td>[[164,164]]</td>
      <td>[[1371,1371]]</td>
      <td>2839</td>
      <td>7</td>
      <td>[[41, 41], [44, 44], [126, 126], [133, 133], [...</td>
      <td>247</td>
      <td>[[10, 256]]</td>
      <td>244.327</td>
      <td>[[1, 1]]</td>
      <td>0</td>
      <td>[]</td>
      <td>256</td>
      <td>256</td>
      <td>[[1, 256]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((10, 256),)</td>
      <td>247</td>
      <td>0.045293</td>
      <td>0.047759</td>
      <td>-68</td>
      <td>False</td>
      <td>12</td>
      <td>False</td>
      <td>0.090909</td>
      <td>0.083333</td>
      <td>((1435, 1435), (1438, 1439), (1441, 1442), (14...</td>
      <td>((1298, 1298), (1302, 1302), (1306, 1306), (14...</td>
      <td>(P21359-2, P21359)</td>
      <td>True</td>
      <td>11</td>
    </tr>
    <tr>
      <th>42</th>
      <td>2</td>
      <td>B</td>
      <td>B</td>
      <td>B</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[12,48],[50,53],[55,73],[75,76],[78,80],[82,8...</td>
      <td>[[228,228],[231,232],[234,235],[237,238],[241,...</td>
      <td>2</td>
      <td>D</td>
      <td>D</td>
      <td>D</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[10,48],[50,53],[55,76],[79,80],[82,85],[87,9...</td>
      <td>[[91,91],[95,95],[99,99],[194,195],[197,197],[...</td>
      <td>6ob3</td>
      <td>0</td>
      <td>10</td>
      <td>False</td>
      <td>P21359-2</td>
      <td>NF1_HUMAN</td>
      <td>1.00</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2818</td>
      <td>10</td>
      <td>[[41, 41], [51, 51], [69, 69], [129, 130], [13...</td>
      <td>245</td>
      <td>[[12, 256]]</td>
      <td>241.495</td>
      <td>[[1, 1]]</td>
      <td>0</td>
      <td>[]</td>
      <td>256</td>
      <td>256</td>
      <td>[[1, 256]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((12, 256),)</td>
      <td>245</td>
      <td>0.077038</td>
      <td>0.080586</td>
      <td>2.100</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20191113</td>
      <td>20190319</td>
      <td>0.476190</td>
      <td>-66</td>
      <td>False</td>
      <td>11</td>
      <td>P21359-4</td>
      <td>NF1_HUMAN</td>
      <td>0.92</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[2,256]]</td>
      <td>[[1209,1484]]</td>
      <td>P21359</td>
      <td>[21]</td>
      <td>Deletion</td>
      <td>False</td>
      <td>False</td>
      <td>21</td>
      <td>((2, 164), (165, 256))</td>
      <td>((1209, 1371), (1393, 1484))</td>
      <td>{"164":"A"}</td>
      <td>[[164,164]]</td>
      <td>[[1371,1371]]</td>
      <td>1598</td>
      <td>7</td>
      <td>[[41, 41], [44, 44], [126, 126], [133, 133], [...</td>
      <td>247</td>
      <td>[[10, 256]]</td>
      <td>244.327</td>
      <td>[[1, 1]]</td>
      <td>0</td>
      <td>[]</td>
      <td>256</td>
      <td>256</td>
      <td>[[1, 256]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((10, 256),)</td>
      <td>247</td>
      <td>0.080468</td>
      <td>0.084848</td>
      <td>-68</td>
      <td>False</td>
      <td>4</td>
      <td>False</td>
      <td>0.250000</td>
      <td>0.090909</td>
      <td>((1435, 1435), (1438, 1439), (1441, 1442), (14...</td>
      <td>((1298, 1298), (1302, 1302), (1306, 1306), (14...</td>
      <td>(P21359-2, P21359-4)</td>
      <td>True</td>
      <td>1</td>
    </tr>
    <tr>
      <th>43</th>
      <td>2</td>
      <td>B</td>
      <td>B</td>
      <td>B</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[12,48],[50,53],[55,73],[75,76],[78,80],[82,8...</td>
      <td>[[228,228],[231,232],[234,235],[237,238],[241,...</td>
      <td>2</td>
      <td>D</td>
      <td>D</td>
      <td>D</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[10,48],[50,53],[55,76],[79,80],[82,85],[87,9...</td>
      <td>[[91,91],[95,95],[99,99],[194,195],[197,197],[...</td>
      <td>6ob3</td>
      <td>0</td>
      <td>10</td>
      <td>False</td>
      <td>P21359-2</td>
      <td>NF1_HUMAN</td>
      <td>1.00</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2818</td>
      <td>10</td>
      <td>[[41, 41], [51, 51], [69, 69], [129, 130], [13...</td>
      <td>245</td>
      <td>[[12, 256]]</td>
      <td>241.495</td>
      <td>[[1, 1]]</td>
      <td>0</td>
      <td>[]</td>
      <td>256</td>
      <td>256</td>
      <td>[[1, 256]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((12, 256),)</td>
      <td>245</td>
      <td>0.077038</td>
      <td>0.080586</td>
      <td>2.100</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20191113</td>
      <td>20190319</td>
      <td>0.476190</td>
      <td>-66</td>
      <td>False</td>
      <td>11</td>
      <td>P21359-6</td>
      <td>NF1_HUMAN</td>
      <td>1.00</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2836</td>
      <td>7</td>
      <td>[[41, 41], [44, 44], [126, 126], [133, 133], [...</td>
      <td>247</td>
      <td>[[10, 256]]</td>
      <td>244.327</td>
      <td>[[1, 1]]</td>
      <td>0</td>
      <td>[]</td>
      <td>256</td>
      <td>256</td>
      <td>[[1, 256]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((10, 256),)</td>
      <td>247</td>
      <td>0.079575</td>
      <td>0.082043</td>
      <td>-68</td>
      <td>False</td>
      <td>10</td>
      <td>False</td>
      <td>0.100000</td>
      <td>0.090909</td>
      <td>((1435, 1435), (1438, 1439), (1441, 1442), (14...</td>
      <td>((1298, 1298), (1302, 1302), (1306, 1306), (14...</td>
      <td>(P21359-2, P21359-6)</td>
      <td>True</td>
      <td>11</td>
    </tr>
    <tr>
      <th>44</th>
      <td>2</td>
      <td>D</td>
      <td>D</td>
      <td>D</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[10,48],[50,53],[55,76],[79,80],[82,85],[87,9...</td>
      <td>[[91,91],[95,95],[99,99],[194,195],[197,197],[...</td>
      <td>2</td>
      <td>B</td>
      <td>B</td>
      <td>B</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[12,48],[50,53],[55,73],[75,76],[78,80],[82,8...</td>
      <td>[[228,228],[231,232],[234,235],[237,238],[241,...</td>
      <td>6ob3</td>
      <td>0</td>
      <td>10</td>
      <td>False</td>
      <td>P21359-2</td>
      <td>NF1_HUMAN</td>
      <td>1.00</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2818</td>
      <td>7</td>
      <td>[[41, 41], [44, 44], [126, 126], [133, 133], [...</td>
      <td>247</td>
      <td>[[10, 256]]</td>
      <td>244.327</td>
      <td>[[1, 1]]</td>
      <td>0</td>
      <td>[]</td>
      <td>256</td>
      <td>256</td>
      <td>[[1, 256]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((10, 256),)</td>
      <td>247</td>
      <td>0.080083</td>
      <td>0.082567</td>
      <td>2.100</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20191113</td>
      <td>20190319</td>
      <td>0.476190</td>
      <td>-68</td>
      <td>False</td>
      <td>10</td>
      <td>P21359-4</td>
      <td>NF1_HUMAN</td>
      <td>0.92</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[2,256]]</td>
      <td>[[1209,1484]]</td>
      <td>P21359</td>
      <td>[21]</td>
      <td>Deletion</td>
      <td>False</td>
      <td>False</td>
      <td>21</td>
      <td>((2, 164), (165, 256))</td>
      <td>((1209, 1371), (1393, 1484))</td>
      <td>{"164":"A"}</td>
      <td>[[164,164]]</td>
      <td>[[1371,1371]]</td>
      <td>1598</td>
      <td>10</td>
      <td>[[41, 41], [51, 51], [69, 69], [129, 130], [13...</td>
      <td>245</td>
      <td>[[12, 256]]</td>
      <td>241.495</td>
      <td>[[1, 1]]</td>
      <td>0</td>
      <td>[]</td>
      <td>256</td>
      <td>256</td>
      <td>[[1, 256]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((12, 256),)</td>
      <td>245</td>
      <td>0.075098</td>
      <td>0.081355</td>
      <td>-66</td>
      <td>False</td>
      <td>5</td>
      <td>False</td>
      <td>0.200000</td>
      <td>0.100000</td>
      <td>((1298, 1298), (1302, 1302), (1306, 1306), (14...</td>
      <td>((1456, 1456), (1459, 1460), (1462, 1463), (14...</td>
      <td>(P21359-2, P21359-4)</td>
      <td>True</td>
      <td>2</td>
    </tr>
    <tr>
      <th>45</th>
      <td>2</td>
      <td>D</td>
      <td>D</td>
      <td>D</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[10,48],[50,53],[55,76],[79,80],[82,85],[87,9...</td>
      <td>[[91,91],[95,95],[99,99],[194,195],[197,197],[...</td>
      <td>2</td>
      <td>B</td>
      <td>B</td>
      <td>B</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[12,48],[50,53],[55,73],[75,76],[78,80],[82,8...</td>
      <td>[[228,228],[231,232],[234,235],[237,238],[241,...</td>
      <td>6ob3</td>
      <td>0</td>
      <td>10</td>
      <td>False</td>
      <td>P21359-2</td>
      <td>NF1_HUMAN</td>
      <td>1.00</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2818</td>
      <td>7</td>
      <td>[[41, 41], [44, 44], [126, 126], [133, 133], [...</td>
      <td>247</td>
      <td>[[10, 256]]</td>
      <td>244.327</td>
      <td>[[1, 1]]</td>
      <td>0</td>
      <td>[]</td>
      <td>256</td>
      <td>256</td>
      <td>[[1, 256]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((10, 256),)</td>
      <td>247</td>
      <td>0.080083</td>
      <td>0.082567</td>
      <td>2.100</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20191113</td>
      <td>20190319</td>
      <td>0.476190</td>
      <td>-68</td>
      <td>False</td>
      <td>10</td>
      <td>P21359-6</td>
      <td>NF1_HUMAN</td>
      <td>1.00</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2836</td>
      <td>10</td>
      <td>[[41, 41], [51, 51], [69, 69], [129, 130], [13...</td>
      <td>245</td>
      <td>[[12, 256]]</td>
      <td>241.495</td>
      <td>[[1, 1]]</td>
      <td>0</td>
      <td>[]</td>
      <td>256</td>
      <td>256</td>
      <td>[[1, 256]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((12, 256),)</td>
      <td>245</td>
      <td>0.076549</td>
      <td>0.080075</td>
      <td>-66</td>
      <td>False</td>
      <td>11</td>
      <td>False</td>
      <td>0.100000</td>
      <td>0.090909</td>
      <td>((1298, 1298), (1302, 1302), (1306, 1306), (14...</td>
      <td>((1435, 1435), (1438, 1439), (1441, 1442), (14...</td>
      <td>(P21359-2, P21359-6)</td>
      <td>True</td>
      <td>12</td>
    </tr>
  </tbody>
</table>

</details>

## 异聚体代表集结构选择

```python
df4 = sifts_demo.pipe_select_he(run_as_completed=True).result()
df4
```

<details>
<summary>Click to view dataframe</summary>

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
      <th>chain_id_2</th>
      <th>struct_asym_id_2</th>
      <th>struct_asym_id_in_assembly_2</th>
      <th>asym_id_rank_2</th>
      <th>model_id_2</th>
      <th>molecule_type_2</th>
      <th>surface_range_2</th>
      <th>interface_range_2</th>
      <th>pdb_id</th>
      <th>assembly_id</th>
      <th>interface_id</th>
      <th>use_au</th>
      <th>UniProt_1</th>
      <th>identifier_1</th>
      <th>identity_1</th>
      <th>is_canonical_1</th>
      <th>name_1</th>
      <th>pdb_range_1</th>
      <th>unp_range_1</th>
      <th>Entry_1</th>
      <th>range_diff_1</th>
      <th>sifts_range_tag_1</th>
      <th>repeated_1</th>
      <th>reversed_1</th>
      <th>InDel_sum_1</th>
      <th>new_pdb_range_1</th>
      <th>new_unp_range_1</th>
      <th>conflict_pdb_index_1</th>
      <th>conflict_pdb_range_1</th>
      <th>conflict_unp_range_1</th>
      <th>unp_len_1</th>
      <th>BINDING_LIGAND_COUNT_1</th>
      <th>BINDING_LIGAND_INDEX_1</th>
      <th>OBS_COUNT_1</th>
      <th>OBS_INDEX_1</th>
      <th>OBS_RATIO_SUM_1</th>
      <th>ARTIFACT_INDEX_1</th>
      <th>NON_COUNT_1</th>
      <th>NON_INDEX_1</th>
      <th>SEQRES_COUNT_1</th>
      <th>STD_COUNT_1</th>
      <th>STD_INDEX_1</th>
      <th>UNK_COUNT_1</th>
      <th>UNK_INDEX_1</th>
      <th>ca_p_only_1</th>
      <th>OBS_STD_INDEX_1</th>
      <th>OBS_STD_COUNT_1</th>
      <th>RAW_BS_1</th>
      <th>RAW_BS_IG3_1</th>
      <th>resolution</th>
      <th>experimental_method_class</th>
      <th>experimental_method</th>
      <th>multi_method</th>
      <th>revision_date</th>
      <th>deposition_date</th>
      <th>1/resolution</th>
      <th>id_score_1</th>
      <th>select_tag_1</th>
      <th>select_rank_1</th>
      <th>UniProt_2</th>
      <th>identifier_2</th>
      <th>identity_2</th>
      <th>is_canonical_2</th>
      <th>name_2</th>
      <th>pdb_range_2</th>
      <th>unp_range_2</th>
      <th>Entry_2</th>
      <th>range_diff_2</th>
      <th>sifts_range_tag_2</th>
      <th>repeated_2</th>
      <th>reversed_2</th>
      <th>InDel_sum_2</th>
      <th>new_pdb_range_2</th>
      <th>new_unp_range_2</th>
      <th>conflict_pdb_index_2</th>
      <th>conflict_pdb_range_2</th>
      <th>conflict_unp_range_2</th>
      <th>unp_len_2</th>
      <th>BINDING_LIGAND_COUNT_2</th>
      <th>BINDING_LIGAND_INDEX_2</th>
      <th>OBS_COUNT_2</th>
      <th>OBS_INDEX_2</th>
      <th>OBS_RATIO_SUM_2</th>
      <th>ARTIFACT_INDEX_2</th>
      <th>NON_COUNT_2</th>
      <th>NON_INDEX_2</th>
      <th>SEQRES_COUNT_2</th>
      <th>STD_COUNT_2</th>
      <th>STD_INDEX_2</th>
      <th>UNK_COUNT_2</th>
      <th>UNK_INDEX_2</th>
      <th>ca_p_only_2</th>
      <th>OBS_STD_INDEX_2</th>
      <th>OBS_STD_COUNT_2</th>
      <th>RAW_BS_2</th>
      <th>RAW_BS_IG3_2</th>
      <th>id_score_2</th>
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
      <th>0</th>
      <td>2</td>
      <td>B</td>
      <td>B</td>
      <td>B</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[4,22],[24,54],[56,59],[61,82],[84,86],[88,91...</td>
      <td>[[32,33],[36,36],[71,72],[75,77],[82,82],[85,8...</td>
      <td>3</td>
      <td>C</td>
      <td>C</td>
      <td>C</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[2,9],[11,51],[53,53],[55,55],[57,72],[74,77]...</td>
      <td>[[12,13],[18,18],[22,22],[26,26],[30,30],[32,4...</td>
      <td>6v6f</td>
      <td>0</td>
      <td>1</td>
      <td>False</td>
      <td>P21359-2</td>
      <td>NF1_HUMAN</td>
      <td>1.0</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[2,329]]</td>
      <td>[[1203,1530]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[2,329]]</td>
      <td>[[1203,1530]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2818</td>
      <td>1</td>
      <td>[[218, 218]]</td>
      <td>301</td>
      <td>[[4, 263], [276, 300], [312, 327]]</td>
      <td>294.205</td>
      <td>[[1, 1]]</td>
      <td>0</td>
      <td>[]</td>
      <td>329</td>
      <td>329</td>
      <td>[[1, 329]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((4, 263), (276, 300), (312, 327))</td>
      <td>301</td>
      <td>0.089301</td>
      <td>0.089656</td>
      <td>2.542</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20200805</td>
      <td>20191205</td>
      <td>0.393391</td>
      <td>-66</td>
      <td>True</td>
      <td>1</td>
      <td>P01116</td>
      <td>RASK_HUMAN</td>
      <td>0.96</td>
      <td>True</td>
      <td>RASK_HUMAN</td>
      <td>[[2,170]]</td>
      <td>[[1,169]]</td>
      <td>P01116</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[2,170]]</td>
      <td>[[1,169]]</td>
      <td>{"62":"Q","152":"R","154":"E","166":"Q","167":...</td>
      <td>[[62,62],[152,152],[154,154],[166,169]]</td>
      <td>[[61,61],[151,151],[153,153],[165,168]]</td>
      <td>189</td>
      <td>24</td>
      <td>[[14, 19], [29, 33], [35, 36], [58, 58], [61, ...</td>
      <td>168</td>
      <td>[[2, 169]]</td>
      <td>166.665</td>
      <td>[[1, 1]]</td>
      <td>0</td>
      <td>[]</td>
      <td>170</td>
      <td>170</td>
      <td>[[1, 170]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((2, 169),)</td>
      <td>168</td>
      <td>0.752430</td>
      <td>0.879414</td>
      <td>-67</td>
      <td>False</td>
      <td>4</td>
      <td>False</td>
      <td>1.000000</td>
      <td>0.250000</td>
      <td>((1233, 1234), (1237, 1237), (1272, 1273), (12...</td>
      <td>((11, 12), (17, 17), (21, 21), (25, 25), (29, ...</td>
      <td>(P21359-2, P01116)</td>
      <td>False</td>
      <td>11</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>B</td>
      <td>B</td>
      <td>B</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[4,22],[24,54],[56,59],[61,82],[84,86],[88,91...</td>
      <td>[[32,33],[36,36],[71,72],[75,77],[82,82],[85,8...</td>
      <td>3</td>
      <td>C</td>
      <td>C</td>
      <td>C</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[2,9],[11,51],[53,53],[55,55],[57,72],[74,77]...</td>
      <td>[[12,13],[18,18],[22,22],[26,26],[30,30],[32,4...</td>
      <td>6v6f</td>
      <td>0</td>
      <td>1</td>
      <td>False</td>
      <td>P21359-2</td>
      <td>NF1_HUMAN</td>
      <td>1.0</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[2,329]]</td>
      <td>[[1203,1530]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[2,329]]</td>
      <td>[[1203,1530]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2818</td>
      <td>1</td>
      <td>[[218, 218]]</td>
      <td>301</td>
      <td>[[4, 263], [276, 300], [312, 327]]</td>
      <td>294.205</td>
      <td>[[1, 1]]</td>
      <td>0</td>
      <td>[]</td>
      <td>329</td>
      <td>329</td>
      <td>[[1, 329]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((4, 263), (276, 300), (312, 327))</td>
      <td>301</td>
      <td>0.089301</td>
      <td>0.089656</td>
      <td>2.542</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20200805</td>
      <td>20191205</td>
      <td>0.393391</td>
      <td>-66</td>
      <td>True</td>
      <td>1</td>
      <td>P01116-2</td>
      <td>RASK_HUMAN</td>
      <td>0.99</td>
      <td>False</td>
      <td>RASK_HUMAN</td>
      <td>[[2,170]]</td>
      <td>[[1,169]]</td>
      <td>P01116</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[2,170]]</td>
      <td>[[1,169]]</td>
      <td>{"62":"Q"}</td>
      <td>[[62,62]]</td>
      <td>[[61,61]]</td>
      <td>188</td>
      <td>24</td>
      <td>[[14, 19], [29, 33], [35, 36], [58, 58], [61, ...</td>
      <td>168</td>
      <td>[[2, 169]]</td>
      <td>166.665</td>
      <td>[[1, 1]]</td>
      <td>0</td>
      <td>[]</td>
      <td>170</td>
      <td>170</td>
      <td>[[1, 170]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((2, 169),)</td>
      <td>168</td>
      <td>0.756432</td>
      <td>0.884092</td>
      <td>-67</td>
      <td>False</td>
      <td>4</td>
      <td>False</td>
      <td>1.000000</td>
      <td>0.250000</td>
      <td>((1233, 1234), (1237, 1237), (1272, 1273), (12...</td>
      <td>((11, 12), (17, 17), (21, 21), (25, 25), (29, ...</td>
      <td>(P21359-2, P01116-2)</td>
      <td>False</td>
      <td>11</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>B</td>
      <td>B</td>
      <td>B</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[4,22],[24,54],[56,59],[61,82],[84,86],[88,91...</td>
      <td>[[32,33],[36,36],[71,72],[75,77],[82,82],[85,8...</td>
      <td>3</td>
      <td>C</td>
      <td>C</td>
      <td>C</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[2,9],[11,51],[53,53],[55,55],[57,72],[74,77]...</td>
      <td>[[12,13],[18,18],[22,22],[26,26],[30,30],[32,4...</td>
      <td>6v6f</td>
      <td>1</td>
      <td>3</td>
      <td>False</td>
      <td>P21359-2</td>
      <td>NF1_HUMAN</td>
      <td>1.0</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[2,329]]</td>
      <td>[[1203,1530]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[2,329]]</td>
      <td>[[1203,1530]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2818</td>
      <td>1</td>
      <td>[[218, 218]]</td>
      <td>301</td>
      <td>[[4, 263], [276, 300], [312, 327]]</td>
      <td>294.205</td>
      <td>[[1, 1]]</td>
      <td>0</td>
      <td>[]</td>
      <td>329</td>
      <td>329</td>
      <td>[[1, 329]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((4, 263), (276, 300), (312, 327))</td>
      <td>301</td>
      <td>0.089301</td>
      <td>0.089656</td>
      <td>2.542</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20200805</td>
      <td>20191205</td>
      <td>0.393391</td>
      <td>-66</td>
      <td>True</td>
      <td>1</td>
      <td>P01116</td>
      <td>RASK_HUMAN</td>
      <td>0.96</td>
      <td>True</td>
      <td>RASK_HUMAN</td>
      <td>[[2,170]]</td>
      <td>[[1,169]]</td>
      <td>P01116</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[2,170]]</td>
      <td>[[1,169]]</td>
      <td>{"62":"Q","152":"R","154":"E","166":"Q","167":...</td>
      <td>[[62,62],[152,152],[154,154],[166,169]]</td>
      <td>[[61,61],[151,151],[153,153],[165,168]]</td>
      <td>189</td>
      <td>24</td>
      <td>[[14, 19], [29, 33], [35, 36], [58, 58], [61, ...</td>
      <td>168</td>
      <td>[[2, 169]]</td>
      <td>166.665</td>
      <td>[[1, 1]]</td>
      <td>0</td>
      <td>[]</td>
      <td>170</td>
      <td>170</td>
      <td>[[1, 170]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((2, 169),)</td>
      <td>168</td>
      <td>0.752430</td>
      <td>0.879414</td>
      <td>-67</td>
      <td>False</td>
      <td>4</td>
      <td>False</td>
      <td>1.000000</td>
      <td>0.250000</td>
      <td>((1233, 1234), (1237, 1237), (1272, 1273), (12...</td>
      <td>((11, 12), (17, 17), (21, 21), (25, 25), (29, ...</td>
      <td>(P21359-2, P01116)</td>
      <td>False</td>
      <td>12</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2</td>
      <td>B</td>
      <td>B</td>
      <td>B</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[4,22],[24,54],[56,59],[61,82],[84,86],[88,91...</td>
      <td>[[32,33],[36,36],[71,72],[75,77],[82,82],[85,8...</td>
      <td>3</td>
      <td>C</td>
      <td>C</td>
      <td>C</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[2,9],[11,51],[53,53],[55,55],[57,72],[74,77]...</td>
      <td>[[12,13],[18,18],[22,22],[26,26],[30,30],[32,4...</td>
      <td>6v6f</td>
      <td>1</td>
      <td>3</td>
      <td>False</td>
      <td>P21359-2</td>
      <td>NF1_HUMAN</td>
      <td>1.0</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[2,329]]</td>
      <td>[[1203,1530]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[2,329]]</td>
      <td>[[1203,1530]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2818</td>
      <td>1</td>
      <td>[[218, 218]]</td>
      <td>301</td>
      <td>[[4, 263], [276, 300], [312, 327]]</td>
      <td>294.205</td>
      <td>[[1, 1]]</td>
      <td>0</td>
      <td>[]</td>
      <td>329</td>
      <td>329</td>
      <td>[[1, 329]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((4, 263), (276, 300), (312, 327))</td>
      <td>301</td>
      <td>0.089301</td>
      <td>0.089656</td>
      <td>2.542</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20200805</td>
      <td>20191205</td>
      <td>0.393391</td>
      <td>-66</td>
      <td>True</td>
      <td>1</td>
      <td>P01116-2</td>
      <td>RASK_HUMAN</td>
      <td>0.99</td>
      <td>False</td>
      <td>RASK_HUMAN</td>
      <td>[[2,170]]</td>
      <td>[[1,169]]</td>
      <td>P01116</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[2,170]]</td>
      <td>[[1,169]]</td>
      <td>{"62":"Q"}</td>
      <td>[[62,62]]</td>
      <td>[[61,61]]</td>
      <td>188</td>
      <td>24</td>
      <td>[[14, 19], [29, 33], [35, 36], [58, 58], [61, ...</td>
      <td>168</td>
      <td>[[2, 169]]</td>
      <td>166.665</td>
      <td>[[1, 1]]</td>
      <td>0</td>
      <td>[]</td>
      <td>170</td>
      <td>170</td>
      <td>[[1, 170]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((2, 169),)</td>
      <td>168</td>
      <td>0.756432</td>
      <td>0.884092</td>
      <td>-67</td>
      <td>False</td>
      <td>4</td>
      <td>False</td>
      <td>1.000000</td>
      <td>0.250000</td>
      <td>((1233, 1234), (1237, 1237), (1272, 1273), (12...</td>
      <td>((11, 12), (17, 17), (21, 21), (25, 25), (29, ...</td>
      <td>(P21359-2, P01116-2)</td>
      <td>False</td>
      <td>12</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2</td>
      <td>B</td>
      <td>B</td>
      <td>B</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[4,22],[24,54],[56,59],[61,82],[84,86],[88,91...</td>
      <td>[[10,10],[12,19],[21,21],[49,51],[53,54],[57,5...</td>
      <td>1</td>
      <td>A</td>
      <td>A</td>
      <td>A</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[1,22],[25,47],[49,87],[89,99],[101,112]]</td>
      <td>[[8,8],[10,10],[12,21],[25,25],[27,27],[73,77]...</td>
      <td>6v6f</td>
      <td>0</td>
      <td>2</td>
      <td>False</td>
      <td>P21359-2</td>
      <td>NF1_HUMAN</td>
      <td>1.0</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[2,329]]</td>
      <td>[[1203,1530]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[2,329]]</td>
      <td>[[1203,1530]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2818</td>
      <td>1</td>
      <td>[[218, 218]]</td>
      <td>301</td>
      <td>[[4, 263], [276, 300], [312, 327]]</td>
      <td>294.205</td>
      <td>[[1, 1]]</td>
      <td>0</td>
      <td>[]</td>
      <td>329</td>
      <td>329</td>
      <td>[[1, 329]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((4, 263), (276, 300), (312, 327))</td>
      <td>301</td>
      <td>0.089301</td>
      <td>0.089656</td>
      <td>2.542</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20200805</td>
      <td>20191205</td>
      <td>0.393391</td>
      <td>-66</td>
      <td>True</td>
      <td>1</td>
      <td>Q7Z699</td>
      <td>SPRE1_HUMAN</td>
      <td>1.00</td>
      <td>True</td>
      <td>SPRE1_HUMAN</td>
      <td>[[1,113]]</td>
      <td>[[13,125]]</td>
      <td>Q7Z699</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[1,113]]</td>
      <td>[[13,125]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>444</td>
      <td>3</td>
      <td>[[37, 37], [43, 43], [98, 98]]</td>
      <td>110</td>
      <td>[[1, 22], [25, 112]]</td>
      <td>108.533</td>
      <td>[]</td>
      <td>0</td>
      <td>[]</td>
      <td>113</td>
      <td>113</td>
      <td>[[1, 113]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((1, 22), (25, 112))</td>
      <td>110</td>
      <td>0.228891</td>
      <td>0.235648</td>
      <td>-65</td>
      <td>False</td>
      <td>2</td>
      <td>False</td>
      <td>1.000000</td>
      <td>0.500000</td>
      <td>((1211, 1211), (1213, 1220), (1222, 1222), (12...</td>
      <td>((20, 20), (22, 22), (24, 33), (37, 37), (39, ...</td>
      <td>(P21359-2, Q7Z699)</td>
      <td>False</td>
      <td>3</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2</td>
      <td>B</td>
      <td>B</td>
      <td>B</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[4,22],[24,54],[56,59],[61,82],[84,86],[88,91...</td>
      <td>[[168,168],[177,178],[229,231],[247,247],[250,...</td>
      <td>1</td>
      <td>A</td>
      <td>A</td>
      <td>A</td>
      <td>1</td>
      <td>2</td>
      <td>polypeptide(L)</td>
      <td>[[1,22],[25,31],[33,47],[49,87],[89,99],[101,1...</td>
      <td>[[35,39],[43,45],[63,63],[65,66],[84,84],[111,...</td>
      <td>6v6f</td>
      <td>1</td>
      <td>8</td>
      <td>False</td>
      <td>P21359-2</td>
      <td>NF1_HUMAN</td>
      <td>1.0</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[2,329]]</td>
      <td>[[1203,1530]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[2,329]]</td>
      <td>[[1203,1530]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2818</td>
      <td>1</td>
      <td>[[218, 218]]</td>
      <td>301</td>
      <td>[[4, 263], [276, 300], [312, 327]]</td>
      <td>294.205</td>
      <td>[[1, 1]]</td>
      <td>0</td>
      <td>[]</td>
      <td>329</td>
      <td>329</td>
      <td>[[1, 329]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((4, 263), (276, 300), (312, 327))</td>
      <td>301</td>
      <td>0.089301</td>
      <td>0.089656</td>
      <td>2.542</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20200805</td>
      <td>20191205</td>
      <td>0.393391</td>
      <td>-66</td>
      <td>True</td>
      <td>1</td>
      <td>Q7Z699</td>
      <td>SPRE1_HUMAN</td>
      <td>1.00</td>
      <td>True</td>
      <td>SPRE1_HUMAN</td>
      <td>[[1,113]]</td>
      <td>[[13,125]]</td>
      <td>Q7Z699</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[1,113]]</td>
      <td>[[13,125]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>444</td>
      <td>3</td>
      <td>[[37, 37], [43, 43], [98, 98]]</td>
      <td>110</td>
      <td>[[1, 22], [25, 112]]</td>
      <td>108.533</td>
      <td>[]</td>
      <td>0</td>
      <td>[]</td>
      <td>113</td>
      <td>113</td>
      <td>[[1, 113]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((1, 22), (25, 112))</td>
      <td>110</td>
      <td>0.228891</td>
      <td>0.235648</td>
      <td>-65</td>
      <td>False</td>
      <td>2</td>
      <td>False</td>
      <td>1.000000</td>
      <td>0.500000</td>
      <td>((1369, 1369), (1378, 1379), (1430, 1432), (14...</td>
      <td>((47, 51), (55, 57), (75, 75), (77, 78), (96, ...</td>
      <td>(P21359-2, Q7Z699)</td>
      <td>False</td>
      <td>4</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2</td>
      <td>B</td>
      <td>B</td>
      <td>B</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[4,59],[61,83],[85,86],[88,91],[93,137],[139,...</td>
      <td>[[32,33],[35,35],[71,72],[75,77],[81,82],[85,8...</td>
      <td>3</td>
      <td>C</td>
      <td>C</td>
      <td>C</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[2,9],[11,51],[53,55],[57,72],[74,77],[80,81]...</td>
      <td>[[13,13],[18,18],[22,22],[26,26],[30,42],[55,5...</td>
      <td>6v65</td>
      <td>0</td>
      <td>1</td>
      <td>False</td>
      <td>P21359-2</td>
      <td>NF1_HUMAN</td>
      <td>1.0</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[2,329]]</td>
      <td>[[1203,1530]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[2,329]]</td>
      <td>[[1203,1530]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2818</td>
      <td>2</td>
      <td>[[240, 240], [243, 243]]</td>
      <td>300</td>
      <td>[[4, 263], [277, 300], [312, 327]]</td>
      <td>293.261</td>
      <td>[[1, 1]]</td>
      <td>0</td>
      <td>[]</td>
      <td>329</td>
      <td>329</td>
      <td>[[1, 329]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((4, 263), (277, 300), (312, 327))</td>
      <td>300</td>
      <td>0.087956</td>
      <td>0.088666</td>
      <td>2.763</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20200805</td>
      <td>20191204</td>
      <td>0.361925</td>
      <td>-66</td>
      <td>False</td>
      <td>3</td>
      <td>P01116</td>
      <td>RASK_HUMAN</td>
      <td>0.96</td>
      <td>True</td>
      <td>RASK_HUMAN</td>
      <td>[[2,170]]</td>
      <td>[[1,169]]</td>
      <td>P01116</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[2,170]]</td>
      <td>[[1,169]]</td>
      <td>{"152":"R","154":"E","166":"Q","167":"Y","168"...</td>
      <td>[[152,152],[154,154],[166,169]]</td>
      <td>[[151,151],[153,153],[165,168]]</td>
      <td>189</td>
      <td>20</td>
      <td>[[14, 14], [16, 19], [29, 32], [35, 36], [58, ...</td>
      <td>168</td>
      <td>[[2, 169]]</td>
      <td>166.776</td>
      <td>[[1, 1]]</td>
      <td>0</td>
      <td>[]</td>
      <td>170</td>
      <td>170</td>
      <td>[[1, 170]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((2, 169),)</td>
      <td>168</td>
      <td>0.773594</td>
      <td>0.879414</td>
      <td>-67</td>
      <td>False</td>
      <td>2</td>
      <td>False</td>
      <td>0.500000</td>
      <td>0.333333</td>
      <td>((1233, 1234), (1236, 1236), (1272, 1273), (12...</td>
      <td>((12, 12), (17, 17), (21, 21), (25, 25), (29, ...</td>
      <td>(P21359-2, P01116)</td>
      <td>False</td>
      <td>13</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2</td>
      <td>B</td>
      <td>B</td>
      <td>B</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[4,59],[61,83],[85,86],[88,91],[93,137],[139,...</td>
      <td>[[32,33],[35,35],[71,72],[75,77],[81,82],[85,8...</td>
      <td>3</td>
      <td>C</td>
      <td>C</td>
      <td>C</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[2,9],[11,51],[53,55],[57,72],[74,77],[80,81]...</td>
      <td>[[13,13],[18,18],[22,22],[26,26],[30,42],[55,5...</td>
      <td>6v65</td>
      <td>0</td>
      <td>1</td>
      <td>False</td>
      <td>P21359-2</td>
      <td>NF1_HUMAN</td>
      <td>1.0</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[2,329]]</td>
      <td>[[1203,1530]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[2,329]]</td>
      <td>[[1203,1530]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2818</td>
      <td>2</td>
      <td>[[240, 240], [243, 243]]</td>
      <td>300</td>
      <td>[[4, 263], [277, 300], [312, 327]]</td>
      <td>293.261</td>
      <td>[[1, 1]]</td>
      <td>0</td>
      <td>[]</td>
      <td>329</td>
      <td>329</td>
      <td>[[1, 329]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((4, 263), (277, 300), (312, 327))</td>
      <td>300</td>
      <td>0.087956</td>
      <td>0.088666</td>
      <td>2.763</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20200805</td>
      <td>20191204</td>
      <td>0.361925</td>
      <td>-66</td>
      <td>False</td>
      <td>3</td>
      <td>P01116-2</td>
      <td>RASK_HUMAN</td>
      <td>1.00</td>
      <td>False</td>
      <td>RASK_HUMAN</td>
      <td>[[2,170]]</td>
      <td>[[1,169]]</td>
      <td>P01116</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[2,170]]</td>
      <td>[[1,169]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>188</td>
      <td>20</td>
      <td>[[14, 14], [16, 19], [29, 32], [35, 36], [58, ...</td>
      <td>168</td>
      <td>[[2, 169]]</td>
      <td>166.776</td>
      <td>[[1, 1]]</td>
      <td>0</td>
      <td>[]</td>
      <td>170</td>
      <td>170</td>
      <td>[[1, 170]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((2, 169),)</td>
      <td>168</td>
      <td>0.777709</td>
      <td>0.884092</td>
      <td>-67</td>
      <td>False</td>
      <td>2</td>
      <td>False</td>
      <td>0.500000</td>
      <td>0.333333</td>
      <td>((1233, 1234), (1236, 1236), (1272, 1273), (12...</td>
      <td>((12, 12), (17, 17), (21, 21), (25, 25), (29, ...</td>
      <td>(P21359-2, P01116-2)</td>
      <td>False</td>
      <td>13</td>
    </tr>
    <tr>
      <th>8</th>
      <td>2</td>
      <td>B</td>
      <td>B</td>
      <td>B</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[4,59],[61,83],[85,86],[88,91],[93,137],[139,...</td>
      <td>[[32,33],[35,35],[71,72],[75,77],[81,82],[85,8...</td>
      <td>3</td>
      <td>C</td>
      <td>C</td>
      <td>C</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[2,9],[11,51],[53,55],[57,72],[74,77],[80,81]...</td>
      <td>[[13,13],[18,18],[22,22],[26,26],[30,42],[55,5...</td>
      <td>6v65</td>
      <td>1</td>
      <td>3</td>
      <td>False</td>
      <td>P21359-2</td>
      <td>NF1_HUMAN</td>
      <td>1.0</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[2,329]]</td>
      <td>[[1203,1530]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[2,329]]</td>
      <td>[[1203,1530]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2818</td>
      <td>2</td>
      <td>[[240, 240], [243, 243]]</td>
      <td>300</td>
      <td>[[4, 263], [277, 300], [312, 327]]</td>
      <td>293.261</td>
      <td>[[1, 1]]</td>
      <td>0</td>
      <td>[]</td>
      <td>329</td>
      <td>329</td>
      <td>[[1, 329]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((4, 263), (277, 300), (312, 327))</td>
      <td>300</td>
      <td>0.087956</td>
      <td>0.088666</td>
      <td>2.763</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20200805</td>
      <td>20191204</td>
      <td>0.361925</td>
      <td>-66</td>
      <td>False</td>
      <td>3</td>
      <td>P01116</td>
      <td>RASK_HUMAN</td>
      <td>0.96</td>
      <td>True</td>
      <td>RASK_HUMAN</td>
      <td>[[2,170]]</td>
      <td>[[1,169]]</td>
      <td>P01116</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[2,170]]</td>
      <td>[[1,169]]</td>
      <td>{"152":"R","154":"E","166":"Q","167":"Y","168"...</td>
      <td>[[152,152],[154,154],[166,169]]</td>
      <td>[[151,151],[153,153],[165,168]]</td>
      <td>189</td>
      <td>20</td>
      <td>[[14, 14], [16, 19], [29, 32], [35, 36], [58, ...</td>
      <td>168</td>
      <td>[[2, 169]]</td>
      <td>166.776</td>
      <td>[[1, 1]]</td>
      <td>0</td>
      <td>[]</td>
      <td>170</td>
      <td>170</td>
      <td>[[1, 170]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((2, 169),)</td>
      <td>168</td>
      <td>0.773594</td>
      <td>0.879414</td>
      <td>-67</td>
      <td>False</td>
      <td>2</td>
      <td>False</td>
      <td>0.500000</td>
      <td>0.333333</td>
      <td>((1233, 1234), (1236, 1236), (1272, 1273), (12...</td>
      <td>((12, 12), (17, 17), (21, 21), (25, 25), (29, ...</td>
      <td>(P21359-2, P01116)</td>
      <td>False</td>
      <td>14</td>
    </tr>
    <tr>
      <th>9</th>
      <td>2</td>
      <td>B</td>
      <td>B</td>
      <td>B</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[4,59],[61,83],[85,86],[88,91],[93,137],[139,...</td>
      <td>[[32,33],[35,35],[71,72],[75,77],[81,82],[85,8...</td>
      <td>3</td>
      <td>C</td>
      <td>C</td>
      <td>C</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[2,9],[11,51],[53,55],[57,72],[74,77],[80,81]...</td>
      <td>[[13,13],[18,18],[22,22],[26,26],[30,42],[55,5...</td>
      <td>6v65</td>
      <td>1</td>
      <td>3</td>
      <td>False</td>
      <td>P21359-2</td>
      <td>NF1_HUMAN</td>
      <td>1.0</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[2,329]]</td>
      <td>[[1203,1530]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[2,329]]</td>
      <td>[[1203,1530]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2818</td>
      <td>2</td>
      <td>[[240, 240], [243, 243]]</td>
      <td>300</td>
      <td>[[4, 263], [277, 300], [312, 327]]</td>
      <td>293.261</td>
      <td>[[1, 1]]</td>
      <td>0</td>
      <td>[]</td>
      <td>329</td>
      <td>329</td>
      <td>[[1, 329]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((4, 263), (277, 300), (312, 327))</td>
      <td>300</td>
      <td>0.087956</td>
      <td>0.088666</td>
      <td>2.763</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20200805</td>
      <td>20191204</td>
      <td>0.361925</td>
      <td>-66</td>
      <td>False</td>
      <td>3</td>
      <td>P01116-2</td>
      <td>RASK_HUMAN</td>
      <td>1.00</td>
      <td>False</td>
      <td>RASK_HUMAN</td>
      <td>[[2,170]]</td>
      <td>[[1,169]]</td>
      <td>P01116</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[2,170]]</td>
      <td>[[1,169]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>188</td>
      <td>20</td>
      <td>[[14, 14], [16, 19], [29, 32], [35, 36], [58, ...</td>
      <td>168</td>
      <td>[[2, 169]]</td>
      <td>166.776</td>
      <td>[[1, 1]]</td>
      <td>0</td>
      <td>[]</td>
      <td>170</td>
      <td>170</td>
      <td>[[1, 170]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((2, 169),)</td>
      <td>168</td>
      <td>0.777709</td>
      <td>0.884092</td>
      <td>-67</td>
      <td>False</td>
      <td>2</td>
      <td>False</td>
      <td>0.500000</td>
      <td>0.333333</td>
      <td>((1233, 1234), (1236, 1236), (1272, 1273), (12...</td>
      <td>((12, 12), (17, 17), (21, 21), (25, 25), (29, ...</td>
      <td>(P21359-2, P01116-2)</td>
      <td>False</td>
      <td>14</td>
    </tr>
    <tr>
      <th>10</th>
      <td>2</td>
      <td>B</td>
      <td>B</td>
      <td>B</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[4,59],[61,83],[85,86],[88,91],[93,137],[139,...</td>
      <td>[[9,10],[12,18],[49,51],[53,54],[57,58],[162,1...</td>
      <td>1</td>
      <td>A</td>
      <td>A</td>
      <td>A</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[1,22],[25,31],[33,87],[89,99],[101,106],[108...</td>
      <td>[[8,8],[10,10],[12,12],[14,21],[25,25],[27,27]...</td>
      <td>6v65</td>
      <td>0</td>
      <td>2</td>
      <td>False</td>
      <td>P21359-2</td>
      <td>NF1_HUMAN</td>
      <td>1.0</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[2,329]]</td>
      <td>[[1203,1530]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[2,329]]</td>
      <td>[[1203,1530]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2818</td>
      <td>2</td>
      <td>[[240, 240], [243, 243]]</td>
      <td>300</td>
      <td>[[4, 263], [277, 300], [312, 327]]</td>
      <td>293.261</td>
      <td>[[1, 1]]</td>
      <td>0</td>
      <td>[]</td>
      <td>329</td>
      <td>329</td>
      <td>[[1, 329]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((4, 263), (277, 300), (312, 327))</td>
      <td>300</td>
      <td>0.087956</td>
      <td>0.088666</td>
      <td>2.763</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20200805</td>
      <td>20191204</td>
      <td>0.361925</td>
      <td>-66</td>
      <td>False</td>
      <td>3</td>
      <td>Q7Z699</td>
      <td>SPRE1_HUMAN</td>
      <td>1.00</td>
      <td>True</td>
      <td>SPRE1_HUMAN</td>
      <td>[[1,113]]</td>
      <td>[[13,125]]</td>
      <td>Q7Z699</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[1,113]]</td>
      <td>[[13,125]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>444</td>
      <td>2</td>
      <td>[[37, 37], [43, 43]]</td>
      <td>110</td>
      <td>[[1, 22], [25, 112]]</td>
      <td>108.199</td>
      <td>[]</td>
      <td>0</td>
      <td>[]</td>
      <td>113</td>
      <td>113</td>
      <td>[[1, 113]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((1, 22), (25, 112))</td>
      <td>110</td>
      <td>0.231144</td>
      <td>0.235648</td>
      <td>-65</td>
      <td>True</td>
      <td>1</td>
      <td>False</td>
      <td>1.000000</td>
      <td>0.333333</td>
      <td>((1210, 1211), (1213, 1219), (1250, 1252), (12...</td>
      <td>((20, 20), (22, 22), (24, 24), (26, 33), (37, ...</td>
      <td>(P21359-2, Q7Z699)</td>
      <td>True</td>
      <td>1</td>
    </tr>
    <tr>
      <th>11</th>
      <td>2</td>
      <td>B</td>
      <td>B</td>
      <td>B</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[4,59],[61,83],[85,86],[88,91],[93,137],[139,...</td>
      <td>[[177,178],[229,231],[250,251],[254,255],[258,...</td>
      <td>1</td>
      <td>A</td>
      <td>A</td>
      <td>A</td>
      <td>1</td>
      <td>2</td>
      <td>polypeptide(L)</td>
      <td>[[1,22],[25,31],[33,87],[89,99],[101,106],[108...</td>
      <td>[[35,38],[40,40],[43,45],[63,63],[66,66],[111,...</td>
      <td>6v65</td>
      <td>1</td>
      <td>8</td>
      <td>False</td>
      <td>P21359-2</td>
      <td>NF1_HUMAN</td>
      <td>1.0</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[2,329]]</td>
      <td>[[1203,1530]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[2,329]]</td>
      <td>[[1203,1530]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2818</td>
      <td>2</td>
      <td>[[240, 240], [243, 243]]</td>
      <td>300</td>
      <td>[[4, 263], [277, 300], [312, 327]]</td>
      <td>293.261</td>
      <td>[[1, 1]]</td>
      <td>0</td>
      <td>[]</td>
      <td>329</td>
      <td>329</td>
      <td>[[1, 329]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((4, 263), (277, 300), (312, 327))</td>
      <td>300</td>
      <td>0.087956</td>
      <td>0.088666</td>
      <td>2.763</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20200805</td>
      <td>20191204</td>
      <td>0.361925</td>
      <td>-66</td>
      <td>False</td>
      <td>3</td>
      <td>Q7Z699</td>
      <td>SPRE1_HUMAN</td>
      <td>1.00</td>
      <td>True</td>
      <td>SPRE1_HUMAN</td>
      <td>[[1,113]]</td>
      <td>[[13,125]]</td>
      <td>Q7Z699</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[1,113]]</td>
      <td>[[13,125]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>444</td>
      <td>2</td>
      <td>[[37, 37], [43, 43]]</td>
      <td>110</td>
      <td>[[1, 22], [25, 112]]</td>
      <td>108.199</td>
      <td>[]</td>
      <td>0</td>
      <td>[]</td>
      <td>113</td>
      <td>113</td>
      <td>[[1, 113]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((1, 22), (25, 112))</td>
      <td>110</td>
      <td>0.231144</td>
      <td>0.235648</td>
      <td>-65</td>
      <td>True</td>
      <td>1</td>
      <td>False</td>
      <td>1.000000</td>
      <td>0.333333</td>
      <td>((1378, 1379), (1430, 1432), (1451, 1452), (14...</td>
      <td>((47, 50), (52, 52), (55, 57), (75, 75), (78, ...</td>
      <td>(P21359-2, Q7Z699)</td>
      <td>True</td>
      <td>2</td>
    </tr>
    <tr>
      <th>12</th>
      <td>2</td>
      <td>B</td>
      <td>B</td>
      <td>B</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[12,48],[50,53],[55,73],[75,76],[78,80],[82,8...</td>
      <td>[[25,27],[30,30],[64,71],[76,76],[79,79],[115,...</td>
      <td>1</td>
      <td>A</td>
      <td>A</td>
      <td>A</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[1,8],[11,20],[22,53],[55,55],[57,72],[74,77]...</td>
      <td>[[13,14],[18,18],[22,22],[25,26],[31,42],[55,5...</td>
      <td>6ob3</td>
      <td>0</td>
      <td>1</td>
      <td>False</td>
      <td>P21359-2</td>
      <td>NF1_HUMAN</td>
      <td>1.0</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2818</td>
      <td>10</td>
      <td>[[41, 41], [51, 51], [69, 69], [129, 130], [13...</td>
      <td>245</td>
      <td>[[12, 256]]</td>
      <td>241.495</td>
      <td>[[1, 1]]</td>
      <td>0</td>
      <td>[]</td>
      <td>256</td>
      <td>256</td>
      <td>[[1, 256]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((12, 256),)</td>
      <td>245</td>
      <td>0.077038</td>
      <td>0.080586</td>
      <td>2.100</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20191113</td>
      <td>20190319</td>
      <td>0.476190</td>
      <td>-66</td>
      <td>False</td>
      <td>11</td>
      <td>P01116</td>
      <td>RASK_HUMAN</td>
      <td>0.96</td>
      <td>True</td>
      <td>RASK_HUMAN</td>
      <td>[[2,170]]</td>
      <td>[[1,169]]</td>
      <td>P01116</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[2,170]]</td>
      <td>[[1,169]]</td>
      <td>{"14":"G","152":"R","154":"E","166":"Q","167":...</td>
      <td>[[14,14],[152,152],[154,154],[166,169]]</td>
      <td>[[13,13],[151,151],[153,153],[165,168]]</td>
      <td>189</td>
      <td>22</td>
      <td>[[13, 19], [23, 23], [29, 31], [35, 36], [61, ...</td>
      <td>170</td>
      <td>[[1, 170]]</td>
      <td>169.566</td>
      <td>[[1, 1]]</td>
      <td>0</td>
      <td>[]</td>
      <td>170</td>
      <td>170</td>
      <td>[[1, 170]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((1, 170),)</td>
      <td>170</td>
      <td>0.777778</td>
      <td>0.894180</td>
      <td>-65</td>
      <td>True</td>
      <td>1</td>
      <td>False</td>
      <td>1.000000</td>
      <td>0.090909</td>
      <td>((1232, 1234), (1237, 1237), (1271, 1278), (12...</td>
      <td>((12, 13), (17, 17), (21, 21), (24, 25), (30, ...</td>
      <td>(P21359-2, P01116)</td>
      <td>False</td>
      <td>3</td>
    </tr>
    <tr>
      <th>13</th>
      <td>2</td>
      <td>B</td>
      <td>B</td>
      <td>B</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[12,48],[50,53],[55,73],[75,76],[78,80],[82,8...</td>
      <td>[[25,27],[30,30],[64,71],[76,76],[79,79],[115,...</td>
      <td>1</td>
      <td>A</td>
      <td>A</td>
      <td>A</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[1,8],[11,20],[22,53],[55,55],[57,72],[74,77]...</td>
      <td>[[13,14],[18,18],[22,22],[25,26],[31,42],[55,5...</td>
      <td>6ob3</td>
      <td>0</td>
      <td>1</td>
      <td>False</td>
      <td>P21359-2</td>
      <td>NF1_HUMAN</td>
      <td>1.0</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2818</td>
      <td>10</td>
      <td>[[41, 41], [51, 51], [69, 69], [129, 130], [13...</td>
      <td>245</td>
      <td>[[12, 256]]</td>
      <td>241.495</td>
      <td>[[1, 1]]</td>
      <td>0</td>
      <td>[]</td>
      <td>256</td>
      <td>256</td>
      <td>[[1, 256]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((12, 256),)</td>
      <td>245</td>
      <td>0.077038</td>
      <td>0.080586</td>
      <td>2.100</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20191113</td>
      <td>20190319</td>
      <td>0.476190</td>
      <td>-66</td>
      <td>False</td>
      <td>11</td>
      <td>P01116-2</td>
      <td>RASK_HUMAN</td>
      <td>0.99</td>
      <td>False</td>
      <td>RASK_HUMAN</td>
      <td>[[2,170]]</td>
      <td>[[1,169]]</td>
      <td>P01116</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[2,170]]</td>
      <td>[[1,169]]</td>
      <td>{"14":"G"}</td>
      <td>[[14,14]]</td>
      <td>[[13,13]]</td>
      <td>188</td>
      <td>22</td>
      <td>[[13, 19], [23, 23], [29, 31], [35, 36], [61, ...</td>
      <td>170</td>
      <td>[[1, 170]]</td>
      <td>169.566</td>
      <td>[[1, 1]]</td>
      <td>0</td>
      <td>[]</td>
      <td>170</td>
      <td>170</td>
      <td>[[1, 170]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((1, 170),)</td>
      <td>170</td>
      <td>0.781915</td>
      <td>0.898936</td>
      <td>-65</td>
      <td>True</td>
      <td>1</td>
      <td>False</td>
      <td>1.000000</td>
      <td>0.090909</td>
      <td>((1232, 1234), (1237, 1237), (1271, 1278), (12...</td>
      <td>((12, 13), (17, 17), (21, 21), (24, 25), (30, ...</td>
      <td>(P21359-2, P01116-2)</td>
      <td>False</td>
      <td>3</td>
    </tr>
    <tr>
      <th>14</th>
      <td>2</td>
      <td>B</td>
      <td>B</td>
      <td>B</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[12,48],[50,53],[55,73],[75,76],[78,80],[82,8...</td>
      <td>[[25,27],[30,30],[64,71],[76,76],[79,79],[115,...</td>
      <td>1</td>
      <td>A</td>
      <td>A</td>
      <td>A</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[1,8],[11,20],[22,53],[55,55],[57,72],[74,77]...</td>
      <td>[[13,14],[18,18],[22,22],[25,26],[31,42],[55,5...</td>
      <td>6ob3</td>
      <td>1</td>
      <td>1</td>
      <td>True</td>
      <td>P21359-2</td>
      <td>NF1_HUMAN</td>
      <td>1.0</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2818</td>
      <td>10</td>
      <td>[[41, 41], [51, 51], [69, 69], [129, 130], [13...</td>
      <td>245</td>
      <td>[[12, 256]]</td>
      <td>241.495</td>
      <td>[[1, 1]]</td>
      <td>0</td>
      <td>[]</td>
      <td>256</td>
      <td>256</td>
      <td>[[1, 256]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((12, 256),)</td>
      <td>245</td>
      <td>0.077038</td>
      <td>0.080586</td>
      <td>2.100</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20191113</td>
      <td>20190319</td>
      <td>0.476190</td>
      <td>-66</td>
      <td>False</td>
      <td>11</td>
      <td>P01116</td>
      <td>RASK_HUMAN</td>
      <td>0.96</td>
      <td>True</td>
      <td>RASK_HUMAN</td>
      <td>[[2,170]]</td>
      <td>[[1,169]]</td>
      <td>P01116</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[2,170]]</td>
      <td>[[1,169]]</td>
      <td>{"14":"G","152":"R","154":"E","166":"Q","167":...</td>
      <td>[[14,14],[152,152],[154,154],[166,169]]</td>
      <td>[[13,13],[151,151],[153,153],[165,168]]</td>
      <td>189</td>
      <td>22</td>
      <td>[[13, 19], [23, 23], [29, 31], [35, 36], [61, ...</td>
      <td>170</td>
      <td>[[1, 170]]</td>
      <td>169.566</td>
      <td>[[1, 1]]</td>
      <td>0</td>
      <td>[]</td>
      <td>170</td>
      <td>170</td>
      <td>[[1, 170]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((1, 170),)</td>
      <td>170</td>
      <td>0.777778</td>
      <td>0.894180</td>
      <td>-65</td>
      <td>True</td>
      <td>1</td>
      <td>True</td>
      <td>1.000000</td>
      <td>0.090909</td>
      <td>((1232, 1234), (1237, 1237), (1271, 1278), (12...</td>
      <td>((12, 13), (17, 17), (21, 21), (24, 25), (30, ...</td>
      <td>(P21359-2, P01116)</td>
      <td>True</td>
      <td>2</td>
    </tr>
    <tr>
      <th>15</th>
      <td>2</td>
      <td>B</td>
      <td>B</td>
      <td>B</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[12,48],[50,53],[55,73],[75,76],[78,80],[82,8...</td>
      <td>[[25,27],[30,30],[64,71],[76,76],[79,79],[115,...</td>
      <td>1</td>
      <td>A</td>
      <td>A</td>
      <td>A</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[1,8],[11,20],[22,53],[55,55],[57,72],[74,77]...</td>
      <td>[[13,14],[18,18],[22,22],[25,26],[31,42],[55,5...</td>
      <td>6ob3</td>
      <td>1</td>
      <td>1</td>
      <td>True</td>
      <td>P21359-2</td>
      <td>NF1_HUMAN</td>
      <td>1.0</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2818</td>
      <td>10</td>
      <td>[[41, 41], [51, 51], [69, 69], [129, 130], [13...</td>
      <td>245</td>
      <td>[[12, 256]]</td>
      <td>241.495</td>
      <td>[[1, 1]]</td>
      <td>0</td>
      <td>[]</td>
      <td>256</td>
      <td>256</td>
      <td>[[1, 256]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((12, 256),)</td>
      <td>245</td>
      <td>0.077038</td>
      <td>0.080586</td>
      <td>2.100</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20191113</td>
      <td>20190319</td>
      <td>0.476190</td>
      <td>-66</td>
      <td>False</td>
      <td>11</td>
      <td>P01116-2</td>
      <td>RASK_HUMAN</td>
      <td>0.99</td>
      <td>False</td>
      <td>RASK_HUMAN</td>
      <td>[[2,170]]</td>
      <td>[[1,169]]</td>
      <td>P01116</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[2,170]]</td>
      <td>[[1,169]]</td>
      <td>{"14":"G"}</td>
      <td>[[14,14]]</td>
      <td>[[13,13]]</td>
      <td>188</td>
      <td>22</td>
      <td>[[13, 19], [23, 23], [29, 31], [35, 36], [61, ...</td>
      <td>170</td>
      <td>[[1, 170]]</td>
      <td>169.566</td>
      <td>[[1, 1]]</td>
      <td>0</td>
      <td>[]</td>
      <td>170</td>
      <td>170</td>
      <td>[[1, 170]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((1, 170),)</td>
      <td>170</td>
      <td>0.781915</td>
      <td>0.898936</td>
      <td>-65</td>
      <td>True</td>
      <td>1</td>
      <td>True</td>
      <td>1.000000</td>
      <td>0.090909</td>
      <td>((1232, 1234), (1237, 1237), (1271, 1278), (12...</td>
      <td>((12, 13), (17, 17), (21, 21), (24, 25), (30, ...</td>
      <td>(P21359-2, P01116-2)</td>
      <td>True</td>
      <td>2</td>
    </tr>
    <tr>
      <th>16</th>
      <td>2</td>
      <td>D</td>
      <td>D</td>
      <td>D</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[10,48],[50,53],[55,76],[79,80],[82,85],[87,9...</td>
      <td>[[28,28],[31,31],[34,35],[38,38],[42,42],[80,8...</td>
      <td>1</td>
      <td>A</td>
      <td>A</td>
      <td>A</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[1,8],[11,20],[22,53],[55,55],[57,72],[74,77]...</td>
      <td>[[24,24],[26,28],[43,46],[51,51],[149,150],[15...</td>
      <td>6ob3</td>
      <td>0</td>
      <td>9</td>
      <td>False</td>
      <td>P21359-2</td>
      <td>NF1_HUMAN</td>
      <td>1.0</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2818</td>
      <td>7</td>
      <td>[[41, 41], [44, 44], [126, 126], [133, 133], [...</td>
      <td>247</td>
      <td>[[10, 256]]</td>
      <td>244.327</td>
      <td>[[1, 1]]</td>
      <td>0</td>
      <td>[]</td>
      <td>256</td>
      <td>256</td>
      <td>[[1, 256]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((10, 256),)</td>
      <td>247</td>
      <td>0.080083</td>
      <td>0.082567</td>
      <td>2.100</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20191113</td>
      <td>20190319</td>
      <td>0.476190</td>
      <td>-68</td>
      <td>False</td>
      <td>10</td>
      <td>P01116</td>
      <td>RASK_HUMAN</td>
      <td>0.96</td>
      <td>True</td>
      <td>RASK_HUMAN</td>
      <td>[[2,170]]</td>
      <td>[[1,169]]</td>
      <td>P01116</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[2,170]]</td>
      <td>[[1,169]]</td>
      <td>{"14":"G","152":"R","154":"E","166":"Q","167":...</td>
      <td>[[14,14],[152,152],[154,154],[166,169]]</td>
      <td>[[13,13],[151,151],[153,153],[165,168]]</td>
      <td>189</td>
      <td>22</td>
      <td>[[13, 19], [23, 23], [29, 31], [35, 36], [61, ...</td>
      <td>170</td>
      <td>[[1, 170]]</td>
      <td>169.566</td>
      <td>[[1, 1]]</td>
      <td>0</td>
      <td>[]</td>
      <td>170</td>
      <td>170</td>
      <td>[[1, 170]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((1, 170),)</td>
      <td>170</td>
      <td>0.777778</td>
      <td>0.894180</td>
      <td>-65</td>
      <td>True</td>
      <td>1</td>
      <td>False</td>
      <td>1.000000</td>
      <td>0.100000</td>
      <td>((1235, 1235), (1238, 1238), (1241, 1242), (12...</td>
      <td>((23, 23), (25, 27), (42, 45), (50, 50), (148,...</td>
      <td>(P21359-2, P01116)</td>
      <td>True</td>
      <td>1</td>
    </tr>
    <tr>
      <th>17</th>
      <td>2</td>
      <td>D</td>
      <td>D</td>
      <td>D</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[10,48],[50,53],[55,76],[79,80],[82,85],[87,9...</td>
      <td>[[28,28],[31,31],[34,35],[38,38],[42,42],[80,8...</td>
      <td>1</td>
      <td>A</td>
      <td>A</td>
      <td>A</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[1,8],[11,20],[22,53],[55,55],[57,72],[74,77]...</td>
      <td>[[24,24],[26,28],[43,46],[51,51],[149,150],[15...</td>
      <td>6ob3</td>
      <td>0</td>
      <td>9</td>
      <td>False</td>
      <td>P21359-2</td>
      <td>NF1_HUMAN</td>
      <td>1.0</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2818</td>
      <td>7</td>
      <td>[[41, 41], [44, 44], [126, 126], [133, 133], [...</td>
      <td>247</td>
      <td>[[10, 256]]</td>
      <td>244.327</td>
      <td>[[1, 1]]</td>
      <td>0</td>
      <td>[]</td>
      <td>256</td>
      <td>256</td>
      <td>[[1, 256]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((10, 256),)</td>
      <td>247</td>
      <td>0.080083</td>
      <td>0.082567</td>
      <td>2.100</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20191113</td>
      <td>20190319</td>
      <td>0.476190</td>
      <td>-68</td>
      <td>False</td>
      <td>10</td>
      <td>P01116-2</td>
      <td>RASK_HUMAN</td>
      <td>0.99</td>
      <td>False</td>
      <td>RASK_HUMAN</td>
      <td>[[2,170]]</td>
      <td>[[1,169]]</td>
      <td>P01116</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[2,170]]</td>
      <td>[[1,169]]</td>
      <td>{"14":"G"}</td>
      <td>[[14,14]]</td>
      <td>[[13,13]]</td>
      <td>188</td>
      <td>22</td>
      <td>[[13, 19], [23, 23], [29, 31], [35, 36], [61, ...</td>
      <td>170</td>
      <td>[[1, 170]]</td>
      <td>169.566</td>
      <td>[[1, 1]]</td>
      <td>0</td>
      <td>[]</td>
      <td>170</td>
      <td>170</td>
      <td>[[1, 170]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((1, 170),)</td>
      <td>170</td>
      <td>0.781915</td>
      <td>0.898936</td>
      <td>-65</td>
      <td>True</td>
      <td>1</td>
      <td>False</td>
      <td>1.000000</td>
      <td>0.100000</td>
      <td>((1235, 1235), (1238, 1238), (1241, 1242), (12...</td>
      <td>((23, 23), (25, 27), (42, 45), (50, 50), (148,...</td>
      <td>(P21359-2, P01116-2)</td>
      <td>True</td>
      <td>1</td>
    </tr>
    <tr>
      <th>18</th>
      <td>2</td>
      <td>D</td>
      <td>D</td>
      <td>D</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[10,48],[50,53],[55,76],[79,80],[82,85],[87,9...</td>
      <td>[[26,27],[29,30],[65,71],[75,76],[79,79],[83,8...</td>
      <td>1</td>
      <td>C</td>
      <td>C</td>
      <td>C</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[2,20],[22,23],[25,51],[53,53],[55,55],[57,72...</td>
      <td>[[12,14],[18,18],[22,22],[26,26],[28,28],[30,3...</td>
      <td>6ob3</td>
      <td>0</td>
      <td>2</td>
      <td>False</td>
      <td>P21359-2</td>
      <td>NF1_HUMAN</td>
      <td>1.0</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2818</td>
      <td>7</td>
      <td>[[41, 41], [44, 44], [126, 126], [133, 133], [...</td>
      <td>247</td>
      <td>[[10, 256]]</td>
      <td>244.327</td>
      <td>[[1, 1]]</td>
      <td>0</td>
      <td>[]</td>
      <td>256</td>
      <td>256</td>
      <td>[[1, 256]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((10, 256),)</td>
      <td>247</td>
      <td>0.080083</td>
      <td>0.082567</td>
      <td>2.100</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20191113</td>
      <td>20190319</td>
      <td>0.476190</td>
      <td>-68</td>
      <td>False</td>
      <td>10</td>
      <td>P01116</td>
      <td>RASK_HUMAN</td>
      <td>0.96</td>
      <td>True</td>
      <td>RASK_HUMAN</td>
      <td>[[2,170]]</td>
      <td>[[1,169]]</td>
      <td>P01116</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[2,170]]</td>
      <td>[[1,169]]</td>
      <td>{"14":"G","152":"R","154":"E","166":"Q","167":...</td>
      <td>[[14,14],[152,152],[154,154],[166,169]]</td>
      <td>[[13,13],[151,151],[153,153],[165,168]]</td>
      <td>189</td>
      <td>21</td>
      <td>[[13, 19], [29, 31], [35, 36], [61, 61], [69, ...</td>
      <td>166</td>
      <td>[[2, 167]]</td>
      <td>164.220</td>
      <td>[[1, 1]]</td>
      <td>0</td>
      <td>[]</td>
      <td>170</td>
      <td>170</td>
      <td>[[1, 170]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((2, 167),)</td>
      <td>166</td>
      <td>0.738772</td>
      <td>0.849883</td>
      <td>-67</td>
      <td>False</td>
      <td>5</td>
      <td>False</td>
      <td>0.200000</td>
      <td>0.100000</td>
      <td>((1233, 1234), (1236, 1237), (1272, 1278), (12...</td>
      <td>((11, 13), (17, 17), (21, 21), (25, 25), (27, ...</td>
      <td>(P21359-2, P01116)</td>
      <td>False</td>
      <td>8</td>
    </tr>
    <tr>
      <th>19</th>
      <td>2</td>
      <td>D</td>
      <td>D</td>
      <td>D</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[10,48],[50,53],[55,76],[79,80],[82,85],[87,9...</td>
      <td>[[26,27],[29,30],[65,71],[75,76],[79,79],[83,8...</td>
      <td>1</td>
      <td>C</td>
      <td>C</td>
      <td>C</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[2,20],[22,23],[25,51],[53,53],[55,55],[57,72...</td>
      <td>[[12,14],[18,18],[22,22],[26,26],[28,28],[30,3...</td>
      <td>6ob3</td>
      <td>0</td>
      <td>2</td>
      <td>False</td>
      <td>P21359-2</td>
      <td>NF1_HUMAN</td>
      <td>1.0</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2818</td>
      <td>7</td>
      <td>[[41, 41], [44, 44], [126, 126], [133, 133], [...</td>
      <td>247</td>
      <td>[[10, 256]]</td>
      <td>244.327</td>
      <td>[[1, 1]]</td>
      <td>0</td>
      <td>[]</td>
      <td>256</td>
      <td>256</td>
      <td>[[1, 256]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((10, 256),)</td>
      <td>247</td>
      <td>0.080083</td>
      <td>0.082567</td>
      <td>2.100</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20191113</td>
      <td>20190319</td>
      <td>0.476190</td>
      <td>-68</td>
      <td>False</td>
      <td>10</td>
      <td>P01116-2</td>
      <td>RASK_HUMAN</td>
      <td>0.99</td>
      <td>False</td>
      <td>RASK_HUMAN</td>
      <td>[[2,170]]</td>
      <td>[[1,169]]</td>
      <td>P01116</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[2,170]]</td>
      <td>[[1,169]]</td>
      <td>{"14":"G"}</td>
      <td>[[14,14]]</td>
      <td>[[13,13]]</td>
      <td>188</td>
      <td>21</td>
      <td>[[13, 19], [29, 31], [35, 36], [61, 61], [69, ...</td>
      <td>166</td>
      <td>[[2, 167]]</td>
      <td>164.220</td>
      <td>[[1, 1]]</td>
      <td>0</td>
      <td>[]</td>
      <td>170</td>
      <td>170</td>
      <td>[[1, 170]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((2, 167),)</td>
      <td>166</td>
      <td>0.742701</td>
      <td>0.854403</td>
      <td>-67</td>
      <td>False</td>
      <td>5</td>
      <td>False</td>
      <td>0.200000</td>
      <td>0.100000</td>
      <td>((1233, 1234), (1236, 1237), (1272, 1278), (12...</td>
      <td>((11, 13), (17, 17), (21, 21), (25, 25), (27, ...</td>
      <td>(P21359-2, P01116-2)</td>
      <td>False</td>
      <td>8</td>
    </tr>
    <tr>
      <th>20</th>
      <td>2</td>
      <td>D</td>
      <td>D</td>
      <td>D</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[10,48],[50,53],[55,76],[79,80],[82,85],[87,9...</td>
      <td>[[26,27],[29,30],[65,71],[75,76],[79,79],[83,8...</td>
      <td>1</td>
      <td>C</td>
      <td>C</td>
      <td>C</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[2,20],[22,23],[25,51],[53,53],[55,55],[57,72...</td>
      <td>[[12,14],[18,18],[22,22],[26,26],[28,28],[30,3...</td>
      <td>6ob3</td>
      <td>2</td>
      <td>2</td>
      <td>True</td>
      <td>P21359-2</td>
      <td>NF1_HUMAN</td>
      <td>1.0</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2818</td>
      <td>7</td>
      <td>[[41, 41], [44, 44], [126, 126], [133, 133], [...</td>
      <td>247</td>
      <td>[[10, 256]]</td>
      <td>244.327</td>
      <td>[[1, 1]]</td>
      <td>0</td>
      <td>[]</td>
      <td>256</td>
      <td>256</td>
      <td>[[1, 256]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((10, 256),)</td>
      <td>247</td>
      <td>0.080083</td>
      <td>0.082567</td>
      <td>2.100</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20191113</td>
      <td>20190319</td>
      <td>0.476190</td>
      <td>-68</td>
      <td>False</td>
      <td>10</td>
      <td>P01116</td>
      <td>RASK_HUMAN</td>
      <td>0.96</td>
      <td>True</td>
      <td>RASK_HUMAN</td>
      <td>[[2,170]]</td>
      <td>[[1,169]]</td>
      <td>P01116</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[2,170]]</td>
      <td>[[1,169]]</td>
      <td>{"14":"G","152":"R","154":"E","166":"Q","167":...</td>
      <td>[[14,14],[152,152],[154,154],[166,169]]</td>
      <td>[[13,13],[151,151],[153,153],[165,168]]</td>
      <td>189</td>
      <td>21</td>
      <td>[[13, 19], [29, 31], [35, 36], [61, 61], [69, ...</td>
      <td>166</td>
      <td>[[2, 167]]</td>
      <td>164.220</td>
      <td>[[1, 1]]</td>
      <td>0</td>
      <td>[]</td>
      <td>170</td>
      <td>170</td>
      <td>[[1, 170]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((2, 167),)</td>
      <td>166</td>
      <td>0.738772</td>
      <td>0.849883</td>
      <td>-67</td>
      <td>False</td>
      <td>5</td>
      <td>True</td>
      <td>0.200000</td>
      <td>0.100000</td>
      <td>((1233, 1234), (1236, 1237), (1272, 1278), (12...</td>
      <td>((11, 13), (17, 17), (21, 21), (25, 25), (27, ...</td>
      <td>(P21359-2, P01116)</td>
      <td>False</td>
      <td>7</td>
    </tr>
    <tr>
      <th>21</th>
      <td>2</td>
      <td>D</td>
      <td>D</td>
      <td>D</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[10,48],[50,53],[55,76],[79,80],[82,85],[87,9...</td>
      <td>[[26,27],[29,30],[65,71],[75,76],[79,79],[83,8...</td>
      <td>1</td>
      <td>C</td>
      <td>C</td>
      <td>C</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[2,20],[22,23],[25,51],[53,53],[55,55],[57,72...</td>
      <td>[[12,14],[18,18],[22,22],[26,26],[28,28],[30,3...</td>
      <td>6ob3</td>
      <td>2</td>
      <td>2</td>
      <td>True</td>
      <td>P21359-2</td>
      <td>NF1_HUMAN</td>
      <td>1.0</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2818</td>
      <td>7</td>
      <td>[[41, 41], [44, 44], [126, 126], [133, 133], [...</td>
      <td>247</td>
      <td>[[10, 256]]</td>
      <td>244.327</td>
      <td>[[1, 1]]</td>
      <td>0</td>
      <td>[]</td>
      <td>256</td>
      <td>256</td>
      <td>[[1, 256]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((10, 256),)</td>
      <td>247</td>
      <td>0.080083</td>
      <td>0.082567</td>
      <td>2.100</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20191113</td>
      <td>20190319</td>
      <td>0.476190</td>
      <td>-68</td>
      <td>False</td>
      <td>10</td>
      <td>P01116-2</td>
      <td>RASK_HUMAN</td>
      <td>0.99</td>
      <td>False</td>
      <td>RASK_HUMAN</td>
      <td>[[2,170]]</td>
      <td>[[1,169]]</td>
      <td>P01116</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[2,170]]</td>
      <td>[[1,169]]</td>
      <td>{"14":"G"}</td>
      <td>[[14,14]]</td>
      <td>[[13,13]]</td>
      <td>188</td>
      <td>21</td>
      <td>[[13, 19], [29, 31], [35, 36], [61, 61], [69, ...</td>
      <td>166</td>
      <td>[[2, 167]]</td>
      <td>164.220</td>
      <td>[[1, 1]]</td>
      <td>0</td>
      <td>[]</td>
      <td>170</td>
      <td>170</td>
      <td>[[1, 170]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((2, 167),)</td>
      <td>166</td>
      <td>0.742701</td>
      <td>0.854403</td>
      <td>-67</td>
      <td>False</td>
      <td>5</td>
      <td>True</td>
      <td>0.200000</td>
      <td>0.100000</td>
      <td>((1233, 1234), (1236, 1237), (1272, 1278), (12...</td>
      <td>((11, 13), (17, 17), (21, 21), (25, 25), (27, ...</td>
      <td>(P21359-2, P01116-2)</td>
      <td>False</td>
      <td>7</td>
    </tr>
    <tr>
      <th>22</th>
      <td>2</td>
      <td>B</td>
      <td>B</td>
      <td>B</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[12,48],[50,53],[55,76],[78,80],[82,85],[87,1...</td>
      <td>[[26,27],[29,30],[65,66],[69,71],[76,76],[79,7...</td>
      <td>1</td>
      <td>A</td>
      <td>A</td>
      <td>A</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[2,8],[10,51],[53,55],[57,77],[80,112],[114,1...</td>
      <td>[[13,13],[18,18],[22,22],[26,26],[30,42],[58,5...</td>
      <td>6ob2</td>
      <td>0</td>
      <td>1</td>
      <td>False</td>
      <td>P21359-2</td>
      <td>NF1_HUMAN</td>
      <td>1.0</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2818</td>
      <td>8</td>
      <td>[[18, 19], [22, 22], [191, 192], [202, 202], [...</td>
      <td>241</td>
      <td>[[12, 103], [107, 255]]</td>
      <td>236.933</td>
      <td>[[1, 1]]</td>
      <td>0</td>
      <td>[]</td>
      <td>256</td>
      <td>256</td>
      <td>[[1, 256]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((12, 103), (107, 255))</td>
      <td>241</td>
      <td>0.073786</td>
      <td>0.076625</td>
      <td>2.845</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20191113</td>
      <td>20190319</td>
      <td>0.351494</td>
      <td>-66</td>
      <td>False</td>
      <td>14</td>
      <td>P01116</td>
      <td>RASK_HUMAN</td>
      <td>0.96</td>
      <td>True</td>
      <td>RASK_HUMAN</td>
      <td>[[2,170]]</td>
      <td>[[1,169]]</td>
      <td>P01116</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[2,170]]</td>
      <td>[[1,169]]</td>
      <td>{"152":"R","154":"E","166":"Q","167":"Y","168"...</td>
      <td>[[152,152],[154,154],[166,169]]</td>
      <td>[[151,151],[153,153],[165,168]]</td>
      <td>189</td>
      <td>25</td>
      <td>[[13, 19], [29, 32], [35, 36], [61, 61], [68, ...</td>
      <td>169</td>
      <td>[[2, 170]]</td>
      <td>166.890</td>
      <td>[[1, 1]]</td>
      <td>0</td>
      <td>[]</td>
      <td>170</td>
      <td>170</td>
      <td>[[1, 170]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((2, 170),)</td>
      <td>169</td>
      <td>0.761905</td>
      <td>0.894180</td>
      <td>-65</td>
      <td>False</td>
      <td>3</td>
      <td>False</td>
      <td>0.333333</td>
      <td>0.071429</td>
      <td>((1233, 1234), (1236, 1237), (1272, 1273), (12...</td>
      <td>((12, 12), (17, 17), (21, 21), (25, 25), (29, ...</td>
      <td>(P21359-2, P01116)</td>
      <td>False</td>
      <td>6</td>
    </tr>
    <tr>
      <th>23</th>
      <td>2</td>
      <td>B</td>
      <td>B</td>
      <td>B</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[12,48],[50,53],[55,76],[78,80],[82,85],[87,1...</td>
      <td>[[26,27],[29,30],[65,66],[69,71],[76,76],[79,7...</td>
      <td>1</td>
      <td>A</td>
      <td>A</td>
      <td>A</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[2,8],[10,51],[53,55],[57,77],[80,112],[114,1...</td>
      <td>[[13,13],[18,18],[22,22],[26,26],[30,42],[58,5...</td>
      <td>6ob2</td>
      <td>0</td>
      <td>1</td>
      <td>False</td>
      <td>P21359-2</td>
      <td>NF1_HUMAN</td>
      <td>1.0</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2818</td>
      <td>8</td>
      <td>[[18, 19], [22, 22], [191, 192], [202, 202], [...</td>
      <td>241</td>
      <td>[[12, 103], [107, 255]]</td>
      <td>236.933</td>
      <td>[[1, 1]]</td>
      <td>0</td>
      <td>[]</td>
      <td>256</td>
      <td>256</td>
      <td>[[1, 256]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((12, 103), (107, 255))</td>
      <td>241</td>
      <td>0.073786</td>
      <td>0.076625</td>
      <td>2.845</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20191113</td>
      <td>20190319</td>
      <td>0.351494</td>
      <td>-66</td>
      <td>False</td>
      <td>14</td>
      <td>P01116-2</td>
      <td>RASK_HUMAN</td>
      <td>1.00</td>
      <td>False</td>
      <td>RASK_HUMAN</td>
      <td>[[2,170]]</td>
      <td>[[1,169]]</td>
      <td>P01116</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[2,170]]</td>
      <td>[[1,169]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>188</td>
      <td>25</td>
      <td>[[13, 19], [29, 32], [35, 36], [61, 61], [68, ...</td>
      <td>169</td>
      <td>[[2, 170]]</td>
      <td>166.890</td>
      <td>[[1, 1]]</td>
      <td>0</td>
      <td>[]</td>
      <td>170</td>
      <td>170</td>
      <td>[[1, 170]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((2, 170),)</td>
      <td>169</td>
      <td>0.765957</td>
      <td>0.898936</td>
      <td>-65</td>
      <td>False</td>
      <td>3</td>
      <td>False</td>
      <td>0.333333</td>
      <td>0.071429</td>
      <td>((1233, 1234), (1236, 1237), (1272, 1273), (12...</td>
      <td>((12, 12), (17, 17), (21, 21), (25, 25), (29, ...</td>
      <td>(P21359-2, P01116-2)</td>
      <td>False</td>
      <td>6</td>
    </tr>
    <tr>
      <th>24</th>
      <td>2</td>
      <td>B</td>
      <td>B</td>
      <td>B</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[12,48],[50,53],[55,76],[78,80],[82,85],[87,1...</td>
      <td>[[26,27],[29,30],[65,66],[69,71],[76,76],[79,7...</td>
      <td>1</td>
      <td>A</td>
      <td>A</td>
      <td>A</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[2,8],[10,51],[53,55],[57,77],[80,112],[114,1...</td>
      <td>[[13,13],[18,18],[22,22],[26,26],[30,42],[58,5...</td>
      <td>6ob2</td>
      <td>1</td>
      <td>1</td>
      <td>True</td>
      <td>P21359-2</td>
      <td>NF1_HUMAN</td>
      <td>1.0</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2818</td>
      <td>8</td>
      <td>[[18, 19], [22, 22], [191, 192], [202, 202], [...</td>
      <td>241</td>
      <td>[[12, 103], [107, 255]]</td>
      <td>236.933</td>
      <td>[[1, 1]]</td>
      <td>0</td>
      <td>[]</td>
      <td>256</td>
      <td>256</td>
      <td>[[1, 256]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((12, 103), (107, 255))</td>
      <td>241</td>
      <td>0.073786</td>
      <td>0.076625</td>
      <td>2.845</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20191113</td>
      <td>20190319</td>
      <td>0.351494</td>
      <td>-66</td>
      <td>False</td>
      <td>14</td>
      <td>P01116</td>
      <td>RASK_HUMAN</td>
      <td>0.96</td>
      <td>True</td>
      <td>RASK_HUMAN</td>
      <td>[[2,170]]</td>
      <td>[[1,169]]</td>
      <td>P01116</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[2,170]]</td>
      <td>[[1,169]]</td>
      <td>{"152":"R","154":"E","166":"Q","167":"Y","168"...</td>
      <td>[[152,152],[154,154],[166,169]]</td>
      <td>[[151,151],[153,153],[165,168]]</td>
      <td>189</td>
      <td>25</td>
      <td>[[13, 19], [29, 32], [35, 36], [61, 61], [68, ...</td>
      <td>169</td>
      <td>[[2, 170]]</td>
      <td>166.890</td>
      <td>[[1, 1]]</td>
      <td>0</td>
      <td>[]</td>
      <td>170</td>
      <td>170</td>
      <td>[[1, 170]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((2, 170),)</td>
      <td>169</td>
      <td>0.761905</td>
      <td>0.894180</td>
      <td>-65</td>
      <td>False</td>
      <td>3</td>
      <td>True</td>
      <td>0.333333</td>
      <td>0.071429</td>
      <td>((1233, 1234), (1236, 1237), (1272, 1273), (12...</td>
      <td>((12, 12), (17, 17), (21, 21), (25, 25), (29, ...</td>
      <td>(P21359-2, P01116)</td>
      <td>False</td>
      <td>5</td>
    </tr>
    <tr>
      <th>25</th>
      <td>2</td>
      <td>B</td>
      <td>B</td>
      <td>B</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[12,48],[50,53],[55,76],[78,80],[82,85],[87,1...</td>
      <td>[[26,27],[29,30],[65,66],[69,71],[76,76],[79,7...</td>
      <td>1</td>
      <td>A</td>
      <td>A</td>
      <td>A</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[2,8],[10,51],[53,55],[57,77],[80,112],[114,1...</td>
      <td>[[13,13],[18,18],[22,22],[26,26],[30,42],[58,5...</td>
      <td>6ob2</td>
      <td>1</td>
      <td>1</td>
      <td>True</td>
      <td>P21359-2</td>
      <td>NF1_HUMAN</td>
      <td>1.0</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2818</td>
      <td>8</td>
      <td>[[18, 19], [22, 22], [191, 192], [202, 202], [...</td>
      <td>241</td>
      <td>[[12, 103], [107, 255]]</td>
      <td>236.933</td>
      <td>[[1, 1]]</td>
      <td>0</td>
      <td>[]</td>
      <td>256</td>
      <td>256</td>
      <td>[[1, 256]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((12, 103), (107, 255))</td>
      <td>241</td>
      <td>0.073786</td>
      <td>0.076625</td>
      <td>2.845</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20191113</td>
      <td>20190319</td>
      <td>0.351494</td>
      <td>-66</td>
      <td>False</td>
      <td>14</td>
      <td>P01116-2</td>
      <td>RASK_HUMAN</td>
      <td>1.00</td>
      <td>False</td>
      <td>RASK_HUMAN</td>
      <td>[[2,170]]</td>
      <td>[[1,169]]</td>
      <td>P01116</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[2,170]]</td>
      <td>[[1,169]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>188</td>
      <td>25</td>
      <td>[[13, 19], [29, 32], [35, 36], [61, 61], [68, ...</td>
      <td>169</td>
      <td>[[2, 170]]</td>
      <td>166.890</td>
      <td>[[1, 1]]</td>
      <td>0</td>
      <td>[]</td>
      <td>170</td>
      <td>170</td>
      <td>[[1, 170]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((2, 170),)</td>
      <td>169</td>
      <td>0.765957</td>
      <td>0.898936</td>
      <td>-65</td>
      <td>False</td>
      <td>3</td>
      <td>True</td>
      <td>0.333333</td>
      <td>0.071429</td>
      <td>((1233, 1234), (1236, 1237), (1272, 1273), (12...</td>
      <td>((12, 12), (17, 17), (21, 21), (25, 25), (29, ...</td>
      <td>(P21359-2, P01116-2)</td>
      <td>False</td>
      <td>5</td>
    </tr>
    <tr>
      <th>26</th>
      <td>2</td>
      <td>D</td>
      <td>D</td>
      <td>D</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[12,53],[55,76],[78,80],[82,85],[87,100],[102...</td>
      <td>[[28,28],[31,31],[34,35],[38,38],[42,42],[80,8...</td>
      <td>1</td>
      <td>A</td>
      <td>A</td>
      <td>A</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[2,8],[10,51],[53,55],[57,77],[80,112],[114,1...</td>
      <td>[[24,24],[26,28],[43,46],[49,49],[51,51],[149,...</td>
      <td>6ob2</td>
      <td>0</td>
      <td>7</td>
      <td>False</td>
      <td>P21359-2</td>
      <td>NF1_HUMAN</td>
      <td>1.0</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2818</td>
      <td>0</td>
      <td>[]</td>
      <td>245</td>
      <td>[[12, 256]]</td>
      <td>239.938</td>
      <td>[[1, 1]]</td>
      <td>0</td>
      <td>[]</td>
      <td>256</td>
      <td>256</td>
      <td>[[1, 256]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((12, 256),)</td>
      <td>245</td>
      <td>0.080586</td>
      <td>0.080586</td>
      <td>2.845</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20191113</td>
      <td>20190319</td>
      <td>0.351494</td>
      <td>-68</td>
      <td>False</td>
      <td>9</td>
      <td>P01116</td>
      <td>RASK_HUMAN</td>
      <td>0.96</td>
      <td>True</td>
      <td>RASK_HUMAN</td>
      <td>[[2,170]]</td>
      <td>[[1,169]]</td>
      <td>P01116</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[2,170]]</td>
      <td>[[1,169]]</td>
      <td>{"152":"R","154":"E","166":"Q","167":"Y","168"...</td>
      <td>[[152,152],[154,154],[166,169]]</td>
      <td>[[151,151],[153,153],[165,168]]</td>
      <td>189</td>
      <td>25</td>
      <td>[[13, 19], [29, 32], [35, 36], [61, 61], [68, ...</td>
      <td>169</td>
      <td>[[2, 170]]</td>
      <td>166.890</td>
      <td>[[1, 1]]</td>
      <td>0</td>
      <td>[]</td>
      <td>170</td>
      <td>170</td>
      <td>[[1, 170]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((2, 170),)</td>
      <td>169</td>
      <td>0.761905</td>
      <td>0.894180</td>
      <td>-65</td>
      <td>False</td>
      <td>3</td>
      <td>False</td>
      <td>0.333333</td>
      <td>0.111111</td>
      <td>((1235, 1235), (1238, 1238), (1241, 1242), (12...</td>
      <td>((23, 23), (25, 27), (42, 45), (48, 48), (50, ...</td>
      <td>(P21359-2, P01116)</td>
      <td>False</td>
      <td>4</td>
    </tr>
    <tr>
      <th>27</th>
      <td>2</td>
      <td>D</td>
      <td>D</td>
      <td>D</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[12,53],[55,76],[78,80],[82,85],[87,100],[102...</td>
      <td>[[28,28],[31,31],[34,35],[38,38],[42,42],[80,8...</td>
      <td>1</td>
      <td>A</td>
      <td>A</td>
      <td>A</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[2,8],[10,51],[53,55],[57,77],[80,112],[114,1...</td>
      <td>[[24,24],[26,28],[43,46],[49,49],[51,51],[149,...</td>
      <td>6ob2</td>
      <td>0</td>
      <td>7</td>
      <td>False</td>
      <td>P21359-2</td>
      <td>NF1_HUMAN</td>
      <td>1.0</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2818</td>
      <td>0</td>
      <td>[]</td>
      <td>245</td>
      <td>[[12, 256]]</td>
      <td>239.938</td>
      <td>[[1, 1]]</td>
      <td>0</td>
      <td>[]</td>
      <td>256</td>
      <td>256</td>
      <td>[[1, 256]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((12, 256),)</td>
      <td>245</td>
      <td>0.080586</td>
      <td>0.080586</td>
      <td>2.845</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20191113</td>
      <td>20190319</td>
      <td>0.351494</td>
      <td>-68</td>
      <td>False</td>
      <td>9</td>
      <td>P01116-2</td>
      <td>RASK_HUMAN</td>
      <td>1.00</td>
      <td>False</td>
      <td>RASK_HUMAN</td>
      <td>[[2,170]]</td>
      <td>[[1,169]]</td>
      <td>P01116</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[2,170]]</td>
      <td>[[1,169]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>188</td>
      <td>25</td>
      <td>[[13, 19], [29, 32], [35, 36], [61, 61], [68, ...</td>
      <td>169</td>
      <td>[[2, 170]]</td>
      <td>166.890</td>
      <td>[[1, 1]]</td>
      <td>0</td>
      <td>[]</td>
      <td>170</td>
      <td>170</td>
      <td>[[1, 170]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((2, 170),)</td>
      <td>169</td>
      <td>0.765957</td>
      <td>0.898936</td>
      <td>-65</td>
      <td>False</td>
      <td>3</td>
      <td>False</td>
      <td>0.333333</td>
      <td>0.111111</td>
      <td>((1235, 1235), (1238, 1238), (1241, 1242), (12...</td>
      <td>((23, 23), (25, 27), (42, 45), (48, 48), (50, ...</td>
      <td>(P21359-2, P01116-2)</td>
      <td>False</td>
      <td>4</td>
    </tr>
    <tr>
      <th>28</th>
      <td>2</td>
      <td>D</td>
      <td>D</td>
      <td>D</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[12,53],[55,76],[78,80],[82,85],[87,100],[102...</td>
      <td>[[26,26],[65,66],[69,71],[76,76],[79,79],[83,8...</td>
      <td>1</td>
      <td>C</td>
      <td>C</td>
      <td>C</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[2,20],[22,166]]</td>
      <td>[[12,13],[18,18],[22,22],[30,42],[55,55],[57,5...</td>
      <td>6ob2</td>
      <td>0</td>
      <td>2</td>
      <td>False</td>
      <td>P21359-2</td>
      <td>NF1_HUMAN</td>
      <td>1.0</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2818</td>
      <td>0</td>
      <td>[]</td>
      <td>245</td>
      <td>[[12, 256]]</td>
      <td>239.938</td>
      <td>[[1, 1]]</td>
      <td>0</td>
      <td>[]</td>
      <td>256</td>
      <td>256</td>
      <td>[[1, 256]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((12, 256),)</td>
      <td>245</td>
      <td>0.080586</td>
      <td>0.080586</td>
      <td>2.845</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20191113</td>
      <td>20190319</td>
      <td>0.351494</td>
      <td>-68</td>
      <td>False</td>
      <td>9</td>
      <td>P01116</td>
      <td>RASK_HUMAN</td>
      <td>0.96</td>
      <td>True</td>
      <td>RASK_HUMAN</td>
      <td>[[2,170]]</td>
      <td>[[1,169]]</td>
      <td>P01116</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[2,170]]</td>
      <td>[[1,169]]</td>
      <td>{"152":"R","154":"E","166":"Q","167":"Y","168"...</td>
      <td>[[152,152],[154,154],[166,169]]</td>
      <td>[[151,151],[153,153],[165,168]]</td>
      <td>189</td>
      <td>19</td>
      <td>[[13, 19], [29, 31], [35, 36], [61, 61], [117,...</td>
      <td>165</td>
      <td>[[2, 166]]</td>
      <td>143.555</td>
      <td>[[1, 1]]</td>
      <td>0</td>
      <td>[]</td>
      <td>170</td>
      <td>170</td>
      <td>[[1, 170]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((2, 166),)</td>
      <td>165</td>
      <td>0.734588</td>
      <td>0.835117</td>
      <td>-67</td>
      <td>False</td>
      <td>6</td>
      <td>False</td>
      <td>0.166667</td>
      <td>0.111111</td>
      <td>((1233, 1233), (1272, 1273), (1276, 1278), (12...</td>
      <td>((11, 12), (17, 17), (21, 21), (29, 41), (54, ...</td>
      <td>(P21359-2, P01116)</td>
      <td>False</td>
      <td>10</td>
    </tr>
    <tr>
      <th>29</th>
      <td>2</td>
      <td>D</td>
      <td>D</td>
      <td>D</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[12,53],[55,76],[78,80],[82,85],[87,100],[102...</td>
      <td>[[26,26],[65,66],[69,71],[76,76],[79,79],[83,8...</td>
      <td>1</td>
      <td>C</td>
      <td>C</td>
      <td>C</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[2,20],[22,166]]</td>
      <td>[[12,13],[18,18],[22,22],[30,42],[55,55],[57,5...</td>
      <td>6ob2</td>
      <td>0</td>
      <td>2</td>
      <td>False</td>
      <td>P21359-2</td>
      <td>NF1_HUMAN</td>
      <td>1.0</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2818</td>
      <td>0</td>
      <td>[]</td>
      <td>245</td>
      <td>[[12, 256]]</td>
      <td>239.938</td>
      <td>[[1, 1]]</td>
      <td>0</td>
      <td>[]</td>
      <td>256</td>
      <td>256</td>
      <td>[[1, 256]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((12, 256),)</td>
      <td>245</td>
      <td>0.080586</td>
      <td>0.080586</td>
      <td>2.845</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20191113</td>
      <td>20190319</td>
      <td>0.351494</td>
      <td>-68</td>
      <td>False</td>
      <td>9</td>
      <td>P01116-2</td>
      <td>RASK_HUMAN</td>
      <td>1.00</td>
      <td>False</td>
      <td>RASK_HUMAN</td>
      <td>[[2,170]]</td>
      <td>[[1,169]]</td>
      <td>P01116</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[2,170]]</td>
      <td>[[1,169]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>188</td>
      <td>19</td>
      <td>[[13, 19], [29, 31], [35, 36], [61, 61], [117,...</td>
      <td>165</td>
      <td>[[2, 166]]</td>
      <td>143.555</td>
      <td>[[1, 1]]</td>
      <td>0</td>
      <td>[]</td>
      <td>170</td>
      <td>170</td>
      <td>[[1, 170]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((2, 166),)</td>
      <td>165</td>
      <td>0.738495</td>
      <td>0.839559</td>
      <td>-67</td>
      <td>False</td>
      <td>6</td>
      <td>False</td>
      <td>0.166667</td>
      <td>0.111111</td>
      <td>((1233, 1233), (1272, 1273), (1276, 1278), (12...</td>
      <td>((11, 12), (17, 17), (21, 21), (29, 41), (54, ...</td>
      <td>(P21359-2, P01116-2)</td>
      <td>False</td>
      <td>10</td>
    </tr>
    <tr>
      <th>30</th>
      <td>2</td>
      <td>D</td>
      <td>D</td>
      <td>D</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[12,53],[55,76],[78,80],[82,85],[87,100],[102...</td>
      <td>[[26,26],[65,66],[69,71],[76,76],[79,79],[83,8...</td>
      <td>1</td>
      <td>C</td>
      <td>C</td>
      <td>C</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[2,20],[22,166]]</td>
      <td>[[12,13],[18,18],[22,22],[30,42],[55,55],[57,5...</td>
      <td>6ob2</td>
      <td>2</td>
      <td>2</td>
      <td>True</td>
      <td>P21359-2</td>
      <td>NF1_HUMAN</td>
      <td>1.0</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2818</td>
      <td>0</td>
      <td>[]</td>
      <td>245</td>
      <td>[[12, 256]]</td>
      <td>239.938</td>
      <td>[[1, 1]]</td>
      <td>0</td>
      <td>[]</td>
      <td>256</td>
      <td>256</td>
      <td>[[1, 256]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((12, 256),)</td>
      <td>245</td>
      <td>0.080586</td>
      <td>0.080586</td>
      <td>2.845</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20191113</td>
      <td>20190319</td>
      <td>0.351494</td>
      <td>-68</td>
      <td>False</td>
      <td>9</td>
      <td>P01116</td>
      <td>RASK_HUMAN</td>
      <td>0.96</td>
      <td>True</td>
      <td>RASK_HUMAN</td>
      <td>[[2,170]]</td>
      <td>[[1,169]]</td>
      <td>P01116</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[2,170]]</td>
      <td>[[1,169]]</td>
      <td>{"152":"R","154":"E","166":"Q","167":"Y","168"...</td>
      <td>[[152,152],[154,154],[166,169]]</td>
      <td>[[151,151],[153,153],[165,168]]</td>
      <td>189</td>
      <td>19</td>
      <td>[[13, 19], [29, 31], [35, 36], [61, 61], [117,...</td>
      <td>165</td>
      <td>[[2, 166]]</td>
      <td>143.555</td>
      <td>[[1, 1]]</td>
      <td>0</td>
      <td>[]</td>
      <td>170</td>
      <td>170</td>
      <td>[[1, 170]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((2, 166),)</td>
      <td>165</td>
      <td>0.734588</td>
      <td>0.835117</td>
      <td>-67</td>
      <td>False</td>
      <td>6</td>
      <td>True</td>
      <td>0.166667</td>
      <td>0.111111</td>
      <td>((1233, 1233), (1272, 1273), (1276, 1278), (12...</td>
      <td>((11, 12), (17, 17), (21, 21), (29, 41), (54, ...</td>
      <td>(P21359-2, P01116)</td>
      <td>False</td>
      <td>9</td>
    </tr>
    <tr>
      <th>31</th>
      <td>2</td>
      <td>D</td>
      <td>D</td>
      <td>D</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[12,53],[55,76],[78,80],[82,85],[87,100],[102...</td>
      <td>[[26,26],[65,66],[69,71],[76,76],[79,79],[83,8...</td>
      <td>1</td>
      <td>C</td>
      <td>C</td>
      <td>C</td>
      <td>1</td>
      <td>1</td>
      <td>polypeptide(L)</td>
      <td>[[2,20],[22,166]]</td>
      <td>[[12,13],[18,18],[22,22],[30,42],[55,55],[57,5...</td>
      <td>6ob2</td>
      <td>2</td>
      <td>2</td>
      <td>True</td>
      <td>P21359-2</td>
      <td>NF1_HUMAN</td>
      <td>1.0</td>
      <td>False</td>
      <td>NF1_HUMAN</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>P21359</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[2,256]]</td>
      <td>[[1209,1463]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>2818</td>
      <td>0</td>
      <td>[]</td>
      <td>245</td>
      <td>[[12, 256]]</td>
      <td>239.938</td>
      <td>[[1, 1]]</td>
      <td>0</td>
      <td>[]</td>
      <td>256</td>
      <td>256</td>
      <td>[[1, 256]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((12, 256),)</td>
      <td>245</td>
      <td>0.080586</td>
      <td>0.080586</td>
      <td>2.845</td>
      <td>x-ray</td>
      <td>X-ray diffraction</td>
      <td>False</td>
      <td>20191113</td>
      <td>20190319</td>
      <td>0.351494</td>
      <td>-68</td>
      <td>False</td>
      <td>9</td>
      <td>P01116-2</td>
      <td>RASK_HUMAN</td>
      <td>1.00</td>
      <td>False</td>
      <td>RASK_HUMAN</td>
      <td>[[2,170]]</td>
      <td>[[1,169]]</td>
      <td>P01116</td>
      <td>[0]</td>
      <td>Safe</td>
      <td>False</td>
      <td>False</td>
      <td>0</td>
      <td>[[2,170]]</td>
      <td>[[1,169]]</td>
      <td>{}</td>
      <td>[]</td>
      <td>[]</td>
      <td>188</td>
      <td>19</td>
      <td>[[13, 19], [29, 31], [35, 36], [61, 61], [117,...</td>
      <td>165</td>
      <td>[[2, 166]]</td>
      <td>143.555</td>
      <td>[[1, 1]]</td>
      <td>0</td>
      <td>[]</td>
      <td>170</td>
      <td>170</td>
      <td>[[1, 170]]</td>
      <td>0</td>
      <td>[]</td>
      <td>False</td>
      <td>((2, 166),)</td>
      <td>165</td>
      <td>0.738495</td>
      <td>0.839559</td>
      <td>-67</td>
      <td>False</td>
      <td>6</td>
      <td>True</td>
      <td>0.166667</td>
      <td>0.111111</td>
      <td>((1233, 1233), (1272, 1273), (1276, 1278), (12...</td>
      <td>((11, 12), (17, 17), (21, 21), (29, 41), (54, ...</td>
      <td>(P21359-2, P01116-2)</td>
      <td>False</td>
      <td>9</td>
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
      <th>UniProt</th>
      <th>chains</th>
      <th>coordinates</th>
      <th>coverage</th>
      <th>created_date</th>
      <th>found_by</th>
      <th>gmqe</th>
      <th>identifier</th>
      <th>identity</th>
      <th>isoid</th>
      <th>ligand_chains</th>
      <th>md5</th>
      <th>method</th>
      <th>oligo-state</th>
      <th>provider</th>
      <th>unp_len</th>
      <th>similarity</th>
      <th>template</th>
      <th>unp_range</th>
      <th>acc_agreement_norm_score</th>
      <th>acc_agreement_z_score</th>
      <th>avg_local_score</th>
      <th>avg_local_score_error</th>
      <th>cbeta_norm_score</th>
      <th>cbeta_z_score</th>
      <th>interaction_norm_score</th>
      <th>interaction_z_score</th>
      <th>packing_norm_score</th>
      <th>packing_z_score</th>
      <th>qmean4_norm_score</th>
      <th>qmean4_z_score</th>
      <th>qmean6_norm_score</th>
      <th>qmean6_z_score</th>
      <th>ss_agreement_norm_score</th>
      <th>ss_agreement_z_score</th>
      <th>torsion_norm_score</th>
      <th>torsion_z_score</th>
      <th>select_rank</th>
      <th>select_tag</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>P21359-2</td>
      <td>[{"id":"A","segments":[{"smtl":{"aligned_seque...</td>
      <td>https://swissmodel.expasy.org/repository/unipr...</td>
      <td>0.095813</td>
      <td>2020-11-01T18:53:29.485000+00:00</td>
      <td>BLAST</td>
      <td>0.0</td>
      <td>NF1_HUMAN</td>
      <td>0.996324</td>
      <td>2</td>
      <td>[{"count":1,"ligands":[{"description":"(1S)-2-...</td>
      <td>fc83f587346226e60cc701448008f89f</td>
      <td>HOMOLOGY MODELLING</td>
      <td>monomer</td>
      <td>SWISSMODEL</td>
      <td>2818</td>
      <td>0.615442</td>
      <td>3p7z.1.A</td>
      <td>[[1547,1816]]</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.716453</td>
      <td>0.051</td>
      <td>-0.011142</td>
      <td>-0.509795</td>
      <td>-0.020118</td>
      <td>-0.777705</td>
      <td>-0.389243</td>
      <td>0.302031</td>
      <td>0.767440</td>
      <td>-0.164094</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.597907</td>
      <td>-0.394816</td>
      <td>-0.304895</td>
      <td>-0.147987</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>1</th>
      <td>P21359-2</td>
      <td>[{"id":"A","segments":[{"smtl":{"aligned_seque...</td>
      <td>https://swissmodel.expasy.org/repository/unipr...</td>
      <td>0.114975</td>
      <td>2020-11-01T18:53:29.436000+00:00</td>
      <td>HHblits</td>
      <td>0.0</td>
      <td>NF1_HUMAN</td>
      <td>1.000000</td>
      <td>2</td>
      <td>NaN</td>
      <td>fc83f587346226e60cc701448008f89f</td>
      <td>HOMOLOGY MODELLING</td>
      <td>monomer</td>
      <td>SWISSMODEL</td>
      <td>2818</td>
      <td>0.612197</td>
      <td>6v6f.1.A</td>
      <td>[[1205,1528]]</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.725275</td>
      <td>0.052</td>
      <td>-0.012087</td>
      <td>-0.252126</td>
      <td>-0.023037</td>
      <td>0.008588</td>
      <td>-0.400769</td>
      <td>0.585791</td>
      <td>0.708347</td>
      <td>-1.885406</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.590228</td>
      <td>-0.466057</td>
      <td>-0.112651</td>
      <td>-2.133139</td>
      <td>2</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2</th>
      <td>P21359-2</td>
      <td>[{"id":"A","segments":[{"smtl":{"aligned_seque...</td>
      <td>https://swissmodel.expasy.org/repository/unipr...</td>
      <td>0.048971</td>
      <td>2020-11-01T18:53:29.457000+00:00</td>
      <td>HHblits</td>
      <td>0.0</td>
      <td>NF1_HUMAN</td>
      <td>0.159420</td>
      <td>2</td>
      <td>NaN</td>
      <td>fc83f587346226e60cc701448008f89f</td>
      <td>HOMOLOGY MODELLING</td>
      <td>monomer</td>
      <td>SWISSMODEL</td>
      <td>2818</td>
      <td>0.284541</td>
      <td>5owu.1.A</td>
      <td>[[2221,2358]]</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.508763</td>
      <td>0.071</td>
      <td>0.007388</td>
      <td>-3.787026</td>
      <td>-0.016512</td>
      <td>-1.403135</td>
      <td>-0.270749</td>
      <td>-1.332674</td>
      <td>0.591839</td>
      <td>-3.581241</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.338587</td>
      <td>-2.294993</td>
      <td>0.027482</td>
      <td>-2.451582</td>
      <td>3</td>
      <td>True</td>
    </tr>
    <tr>
      <th>3</th>
      <td>P21359-2</td>
      <td>[{"id":"A","segments":[{"smtl":{"aligned_seque...</td>
      <td>https://swissmodel.expasy.org/repository/unipr...</td>
      <td>0.046842</td>
      <td>2020-11-01T18:53:29.405000+00:00</td>
      <td>HHblits</td>
      <td>0.0</td>
      <td>NF1_HUMAN</td>
      <td>0.106870</td>
      <td>2</td>
      <td>NaN</td>
      <td>fc83f587346226e60cc701448008f89f</td>
      <td>HOMOLOGY MODELLING</td>
      <td>monomer</td>
      <td>SWISSMODEL</td>
      <td>2818</td>
      <td>0.254453</td>
      <td>3woy.1.A</td>
      <td>[[2268,2399]]</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.423608</td>
      <td>0.072</td>
      <td>0.011488</td>
      <td>-4.452434</td>
      <td>-0.014163</td>
      <td>-1.706403</td>
      <td>-0.299886</td>
      <td>-0.922307</td>
      <td>0.589486</td>
      <td>-3.592260</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.236340</td>
      <td>-2.872675</td>
      <td>0.028206</td>
      <td>-2.441966</td>
      <td>4</td>
      <td>False</td>
    </tr>
    <tr>
      <th>4</th>
      <td>P21359-2</td>
      <td>[{"id":"L","segments":[{"smtl":{"aligned_seque...</td>
      <td>https://swissmodel.expasy.org/repository/unipr...</td>
      <td>0.049326</td>
      <td>2020-11-01T18:53:29.362000+00:00</td>
      <td>HHblits</td>
      <td>0.0</td>
      <td>NF1_HUMAN</td>
      <td>0.214815</td>
      <td>2</td>
      <td>NaN</td>
      <td>fc83f587346226e60cc701448008f89f</td>
      <td>HOMOLOGY MODELLING</td>
      <td>monomer</td>
      <td>SWISSMODEL</td>
      <td>2818</td>
      <td>0.299259</td>
      <td>6ltj.1.L</td>
      <td>[[1074,1212]]</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.414444</td>
      <td>0.071</td>
      <td>-0.003353</td>
      <td>-1.860656</td>
      <td>-0.016426</td>
      <td>-1.423716</td>
      <td>-0.347270</td>
      <td>-0.361593</td>
      <td>0.588397</td>
      <td>-3.625870</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.129832</td>
      <td>-3.591374</td>
      <td>0.151137</td>
      <td>-3.256164</td>
      <td>5</td>
      <td>True</td>
    </tr>
    <tr>
      <th>5</th>
      <td>P21359-2</td>
      <td>[{"id":"A","segments":[{"smtl":{"aligned_seque...</td>
      <td>https://swissmodel.expasy.org/repository/unipr...</td>
      <td>0.053229</td>
      <td>2020-11-01T18:53:29.384000+00:00</td>
      <td>HHblits</td>
      <td>0.0</td>
      <td>NF1_HUMAN</td>
      <td>0.111940</td>
      <td>2</td>
      <td>NaN</td>
      <td>fc83f587346226e60cc701448008f89f</td>
      <td>HOMOLOGY MODELLING</td>
      <td>monomer</td>
      <td>SWISSMODEL</td>
      <td>2818</td>
      <td>0.260199</td>
      <td>1h2t.1.A</td>
      <td>[[1986,2135]]</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.409797</td>
      <td>0.067</td>
      <td>0.008711</td>
      <td>-4.268426</td>
      <td>-0.012236</td>
      <td>-2.127937</td>
      <td>-0.346139</td>
      <td>-0.413069</td>
      <td>0.582163</td>
      <td>-4.048233</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.350606</td>
      <td>-2.199805</td>
      <td>0.095252</td>
      <td>-3.054075</td>
      <td>6</td>
      <td>True</td>
    </tr>
  </tbody>
</table>

</details>

`pipe_select_smr_mo`会根据传入的SIFTS单体选择结果结合SMR提供的model的覆盖范围来判断可用选择哪些模型结构作为补充。

## 位点映射

以P00734与3sqh(chain_id: E)的映射关系为例:

{{% callout note %}}
下面两个函数的`conflict_pdb_index`参数是可选的，不一定需要传入，当您对映射位点上是否存在残基冲突(即PDB链上残基与UniProt Isoform上残基不一致)感兴趣时,才需要传入。
{{% /callout %}}

```python
df1 = SIFTS('P00734').pipe_select_mo().result()
record = df1[df1.pdb_id.eq('3sqh')].iloc[0]  # df1[df1.select_tag.eq(True)].iloc[0]
record
'''
UniProt                                      P00734
chain_id                                          E
entity_id                                         1
identity                                          1
is_canonical                                   True
pdb_id                                         3sqh
struct_asym_id                                    A
pdb_range                                 [[1,290]]
unp_range                               [[333,622]]
Entry                                        P00734
range_diff                                      [0]
sifts_range_tag                                Safe
repeated                                      False
reversed                                      False
InDel_sum                                         0
new_pdb_range                             [[1,290]]
new_unp_range                           [[333,622]]
conflict_pdb_index                      {"236":"S"}
conflict_pdb_range                      [[236,236]]
conflict_unp_range                      [[568,568]]
unp_len                                         622
OBS_INDEX                    ((1, 181), (188, 290))
OBS_COUNT                                       284
OBS_RATIO_SUM                                 283.9
BINDING_LIGAND_INDEX                             ()
BINDING_LIGAND_COUNT                              0
molecule_type                        polypeptide(L)
ca_p_only                                     False
SEQRES_COUNT                                    290
STD_INDEX                               ((1, 290),)
STD_COUNT                                       290
NON_INDEX                                        ()
NON_COUNT                                         0
UNK_INDEX                                        ()
UNK_COUNT                                         0
ARTIFACT_INDEX                                   ()
OBS_STD_INDEX                ((1, 181), (188, 290))
OBS_STD_COUNT                                   284
RAW_BS                                     0.439318
RAW_BS_IG3                                 0.439318
resolution                                      2.2
experimental_method_class                     x-ray
experimental_method               X-ray diffraction
multi_method                                  False
revision_date                              20120523
deposition_date                            20110705
1/resolution                               0.454545
id_score                                        -69
select_tag                                    False
select_rank                                       8
'''
```

通过下面代码来得到匹配区间的所有位点映射关系:

```python
PDB(record['pdb_id']).get_expanded_map_res_df(
    record['UniProt'],
    record['new_unp_range'],
    record['new_pdb_range'],
    conflict_pdb_index=record['conflict_pdb_index'],
    struct_asym_id=record['struct_asym_id']).result()
```

<details><summary>Click to view dataframe</summary>

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
      <th>conflict_code</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>333</td>
      <td>1</td>
      <td>P00734</td>
      <td>C</td>
      <td>1</td>
      <td>E</td>
      <td>1</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>3sqh</td>
      <td>GLU</td>
      <td>A</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>334</td>
      <td>2</td>
      <td>P00734</td>
      <td>B</td>
      <td>1</td>
      <td>E</td>
      <td>1</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>3sqh</td>
      <td>ALA</td>
      <td>A</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>335</td>
      <td>3</td>
      <td>P00734</td>
      <td>A</td>
      <td>1</td>
      <td>E</td>
      <td>1</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>3sqh</td>
      <td>ASP</td>
      <td>A</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>336</td>
      <td>4</td>
      <td>P00734</td>
      <td></td>
      <td>1</td>
      <td>E</td>
      <td>1</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>3sqh</td>
      <td>CYS</td>
      <td>A</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>337</td>
      <td>5</td>
      <td>P00734</td>
      <td></td>
      <td>2</td>
      <td>E</td>
      <td>1</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>3sqh</td>
      <td>GLY</td>
      <td>A</td>
      <td>NaN</td>
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
    </tr>
    <tr>
      <th>285</th>
      <td>618</td>
      <td>286</td>
      <td>P00734</td>
      <td></td>
      <td>243</td>
      <td>E</td>
      <td>1</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>3sqh</td>
      <td>ASP</td>
      <td>A</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>286</th>
      <td>619</td>
      <td>287</td>
      <td>P00734</td>
      <td></td>
      <td>244</td>
      <td>E</td>
      <td>1</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>3sqh</td>
      <td>GLN</td>
      <td>A</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>287</th>
      <td>620</td>
      <td>288</td>
      <td>P00734</td>
      <td></td>
      <td>245</td>
      <td>E</td>
      <td>1</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>3sqh</td>
      <td>PHE</td>
      <td>A</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>288</th>
      <td>621</td>
      <td>289</td>
      <td>P00734</td>
      <td></td>
      <td>246</td>
      <td>E</td>
      <td>1</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>3sqh</td>
      <td>GLY</td>
      <td>A</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>289</th>
      <td>622</td>
      <td>290</td>
      <td>P00734</td>
      <td></td>
      <td>247</td>
      <td>E</td>
      <td>1</td>
      <td>NaN</td>
      <td>0.9</td>
      <td>3sqh</td>
      <td>GLU</td>
      <td>A</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>

</details>

或者通过如下代码来指定映射位点的映射关系:


```python
PDB(record['pdb_id']).get_map_res_df(
    record['UniProt'],
    record['new_unp_range'],
    record['new_pdb_range'],
    your_sites=(336, 353, 568, 362),
    conflict_pdb_index=record['conflict_pdb_index'],
    struct_asym_id=record['struct_asym_id']).result()
```

<details><summary>Click to view dataframe</summary>

<table class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>author_insertion_code</th>
      <th>author_residue_number</th>
      <th>chain_id</th>
      <th>entity_id</th>
      <th>multiple_conformers</th>
      <th>observed_ratio</th>
      <th>pdb_id</th>
      <th>residue_name</th>
      <th>residue_number</th>
      <th>struct_asym_id</th>
      <th>unp_residue_number</th>
      <th>UniProt</th>
      <th>conflict_code</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td></td>
      <td>1</td>
      <td>E</td>
      <td>1</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>3sqh</td>
      <td>CYS</td>
      <td>4</td>
      <td>A</td>
      <td>336</td>
      <td>P00734</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>D</td>
      <td>14</td>
      <td>E</td>
      <td>1</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>3sqh</td>
      <td>ARG</td>
      <td>21</td>
      <td>A</td>
      <td>353</td>
      <td>P00734</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>M</td>
      <td>14</td>
      <td>E</td>
      <td>1</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>3sqh</td>
      <td>GLY</td>
      <td>30</td>
      <td>A</td>
      <td>362</td>
      <td>P00734</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td></td>
      <td>195</td>
      <td>E</td>
      <td>1</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>3sqh</td>
      <td>ALA</td>
      <td>236</td>
      <td>A</td>
      <td>568</td>
      <td>P00734</td>
      <td>S</td>
    </tr>
  </tbody>
</table>

</details>

{{% callout note %}}
`get_map_res_df`有一个`unp2pdb`参数默认为True,表示此函数将把`your_sites`传入的参数认定为UniProt Isoform上的位点，进而映射至PDB链上。若要让此函数将`your_sites`传入的参数认定为PDB链上的位点，进而映射至UniProt Isoform上，请设置`unp2pdb=False`:
{{% /callout %}}

```python
PDB(record['pdb_id']).get_map_res_df(
    record['UniProt'],
    record['new_unp_range'],
    record['new_pdb_range'],
    your_sites=(22, 31, 5, 237),
    conflict_pdb_index=record['conflict_pdb_index'],
    unp2pdb=False,
    struct_asym_id=record['struct_asym_id']).result()
```

<details><summary>Click to view dataframe</summary>

<table class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>author_insertion_code</th>
      <th>author_residue_number</th>
      <th>chain_id</th>
      <th>entity_id</th>
      <th>multiple_conformers</th>
      <th>observed_ratio</th>
      <th>pdb_id</th>
      <th>residue_name</th>
      <th>residue_number</th>
      <th>struct_asym_id</th>
      <th>unp_residue_number</th>
      <th>UniProt</th>
      <th>conflict_code</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td></td>
      <td>2</td>
      <td>E</td>
      <td>1</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>3sqh</td>
      <td>GLY</td>
      <td>5</td>
      <td>A</td>
      <td>337</td>
      <td>P00734</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>E</td>
      <td>14</td>
      <td>E</td>
      <td>1</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>3sqh</td>
      <td>GLU</td>
      <td>22</td>
      <td>A</td>
      <td>354</td>
      <td>P00734</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td></td>
      <td>15</td>
      <td>E</td>
      <td>1</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>3sqh</td>
      <td>ARG</td>
      <td>31</td>
      <td>A</td>
      <td>363</td>
      <td>P00734</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td></td>
      <td>196</td>
      <td>E</td>
      <td>1</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>3sqh</td>
      <td>GLY</td>
      <td>237</td>
      <td>A</td>
      <td>569</td>
      <td>P00734</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>

</details>

{{% callout note %}}
若设置了`unp2pdb=False`且传入的`your_sites`中位点是`author_residue_number`+`author_insertion_code`,请传入参数`author_site=True`:
{{% /callout %}}

```python
PDB(record['pdb_id']).get_map_res_df(
    record['UniProt'],
    record['new_unp_range'],
    record['new_pdb_range'],
    your_sites=('14E', '2', '14A', '195'),
    conflict_pdb_index=record['conflict_pdb_index'],
    unp2pdb=False,
    author_site=True,
    struct_asym_id=record['struct_asym_id']).result()
```

<details><summary>Click to view dataframe</summary>

<table class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>author_insertion_code</th>
      <th>author_residue_number</th>
      <th>chain_id</th>
      <th>entity_id</th>
      <th>multiple_conformers</th>
      <th>observed_ratio</th>
      <th>pdb_id</th>
      <th>residue_name</th>
      <th>residue_number</th>
      <th>struct_asym_id</th>
      <th>UniProt</th>
      <th>unp_residue_number</th>
      <th>conflict_code</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td></td>
      <td>2</td>
      <td>E</td>
      <td>1</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>3sqh</td>
      <td>GLY</td>
      <td>5</td>
      <td>A</td>
      <td>P00734</td>
      <td>337</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>A</td>
      <td>14</td>
      <td>E</td>
      <td>1</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>3sqh</td>
      <td>LYS</td>
      <td>18</td>
      <td>A</td>
      <td>P00734</td>
      <td>350</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>E</td>
      <td>14</td>
      <td>E</td>
      <td>1</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>3sqh</td>
      <td>GLU</td>
      <td>22</td>
      <td>A</td>
      <td>P00734</td>
      <td>354</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td></td>
      <td>195</td>
      <td>E</td>
      <td>1</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>3sqh</td>
      <td>ALA</td>
      <td>236</td>
      <td>A</td>
      <td>P00734</td>
      <td>568</td>
      <td>S</td>
    </tr>
  </tbody>
</table>

</details>

按照如上教程，您应该已经可以利用`pdb-profiling`完成不少任务了。若想了解更多其中的编程逻辑、处理逻辑与数据解释，可以继续阅读文档的剩余部分，在那里将会有更为详细的说明。