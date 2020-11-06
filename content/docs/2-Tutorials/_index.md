---
# Title, summary, and page position.
linktitle: Tutotials
summary: Learning-Oriented
weight: 2
icon: book-reader
icon_pack: fas

# Page metadata.
title: Tutotials
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

```python
pdb_object = PDB('3hl2')

dfrm = pdb_object.fetch_from_web_api('api/pdb/entry/molecules/', PDB.to_dataframe).result()
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
<table border="1" class="dataframe">
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
</div>