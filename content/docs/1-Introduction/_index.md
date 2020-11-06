---
# Title, summary, and page position.
linktitle: Introduction
summary: A brife summary of the problems it solves and some background information.
weight: 1
icon: book
icon_pack: fas

# Page metadata.
title: Introduction
date: "2020-11-05T00:00:00Z"
type: book  # Do not modify.
---

> The problem it solves

## PDB元数据获取层面的相关问题

随着PDB条目数据的增长，对PDB元数据(metadata)批量处理的需求也在逐渐增加。同时，处理PDB数据本身也有着如下特点:

* 不少PDB条目会在更新中会被弃用(`obsolete`)
* 部分PDB条目的内容会进行更新，其中包括对`biological assembly`的重新定义(i.e. `2wc8`)、配体链的重命名(i.e. `1wdq`)等
* 解析PDB完整文件需要大量存储空间与下载/计算时间，为获取相关元数据而对完整PDB文件进行处理有些南辕北辙
* 解析各种PDB文件格式(`.pdb`, `.cif`, `.mmtf` etc.)在具有相关现成parser函数的情况下仍具有较高编程成本且存在各种边缘异常情况

所幸，`EBI`提供的`PDBe RESTful API`等服务能够很好的解决获取元数据的便捷性问题。面对上述问题，`pdb-profiling`应用了`PDBe`的`Entry-Based API`与`Aggregated API`(`PDBe Graph API`)。利用`Entry-Based API`能够实时地获取最新的PDB在`Entry-Assembly/Model-Entity-Chain-Residue`水平的元数据信息，进行相关信息的批量检索与收集。此外，这些信息也为.pdb与.cif及其他格式之间的数据标识符转化提供了足够信息，能够做到向前兼容一些较为早期的(old history)软件所需的标识符格式信息。且不单单应对`asymmetric unit`，同时处理好`biological assembly`。利用`Entry-Based API`中的`SIFTS API`能够做到最新版本下`UniProt Isofrom`与对应PDB在`chain-level`以及`residue-level`的高效映射，结合`EBI's Proteins API`能够实现突变信息在转录本与对应`PDB Chain Instance`的残基的双向映射。`PDBe`的`Aggregated API`与`Entry-Based API`还一同提供了`chain-level`和`residue-level`的丰富注释信息，能够获取结构域、二级结构、残基保守性、配体结合倾向等大量且丰富的预先计算好的特征。

## 与`UniProt-KB`数据资源在整合时的问题

此外，在`UniProt`视角下，不少`UniProt`对应的PDB晶体结构在对`UniProt`序列的覆盖度上有着较大的冗余度，对特定参考序列下进行蛋白质晶体结构的代表集结构确定是个由来已久的需求。且考虑到:

* 不少PDB结构依照具有一定局限性的序列匹配算法被错误对应上，这其中包括
  * Insertion
  * Deletion
  * InDel
  * repeated mapping
  * reversed mapping
  * mapped out (head and tail) segment
  * residue conflict
* PDB结构中存在着
  * missing residue
  * UNK residue
  * modified residue
  * ligand binding residue
  * ca_p_only chain

这使得确定一个严谨准确的蛋白质结构代表集流程对科学研究有着相当的重要性。

<table>
  <tr>
    <td>
      <img src="https://naturegeorge.github.io/eigenblog/assets/img/unp_map_pdb.drawio.svg">
    </td>
  </tr>
  <tr>
    <td>
      P68871 mapped with 1a01 Chain B
    </td>
  </tr>
  <tr>
    <td>
      <img src="https://naturegeorge.github.io/eigenblog/assets/img/unp_map_pdb_insertion.drawio.svg">
    </td>
  </tr>
  <tr>
    <td>
      Insertion: P30038-3 mapped with 4oe5 Chain D
    </td>
  </tr>
  <tr>
    <td>
      <img src="https://naturegeorge.github.io/eigenblog/assets/img/unp_map_pdb_deletion.drawio.svg">
    </td>
  </tr>
  <tr>
    <td>
      Deletion: Q13303-3 mapped with 1zsx Chain A
    </td>
  </tr>
  <tr>
    <td>
      <img src="https://naturegeorge.github.io/eigenblog/assets/img/unp_map_pdb_indel.drawio.svg">
    </td>
  </tr>
  <tr>
    <td>
      InDel: Q01780 mapped with 6d6q Chain J
    </td>
  </tr>
  <tr>
    <td>
      <img src="https://raw.githubusercontent.com/NatureGeorge/pdb-profiling/a7841d4033b3d5be6d17d225133e40912cf000ea/docs/figs/sifts_reversed_mapping.drawio.svg">
    </td>
  </tr>
  <tr>
    <td>
      Reversed Mapping: P00441 mapped with 5j0c Chain A
    </td>
  </tr>
  <tr>
    <td>
      <img src="https://raw.githubusercontent.com/NatureGeorge/pdb-profiling/a7841d4033b3d5be6d17d225133e40912cf000ea/docs/figs/sifts_repeated_mapping.drawio.svg">
    </td>
  </tr>
  <tr>
    <td>
      Repeated Mapping: Q7KZ85-3 mapped with 6gmh Chain M
    </td>
  </tr>
  <tr>
    <td>
      <img src="https://raw.githubusercontent.com/NatureGeorge/pdb-profiling/a7841d4033b3d5be6d17d225133e40912cf000ea/docs/figs/sifts_mapped_out_1.drawio.svg">
    </td>
  </tr>
  <tr>
    <td>
      Mapped Out Situation: P14647 mapped with 3agp Chain A
    </td>
  </tr>
  <tr>
    <td>
      <img src="https://raw.githubusercontent.com/NatureGeorge/pdb-profiling/a7841d4033b3d5be6d17d225133e40912cf000ea/docs/figs/sifts_mapped_out_2.drawio.svg">
    </td>
  </tr>
  <tr>
    <td>
      Mapped Out Situation: Q16611 mapped with 4u2v Chain C
    </td>
  </tr>
</table>

## 与二元相互作用数据资源在整合时的问题

同时，对于二元相互作用(同聚体相互作用、异聚体相互作用)，进行代表集相互作用结构筛选时有必要考虑到

* UniProt binary interaction是否具有生物学意义
* crystal interaction是否具有意义
* 同一对binary interaction下the residues of interacting interface的区别

## 代表集结构的确定问题

`pdb-profiling`在`SIFTS API`等提供的数据的基础上，自主探查出

* UniProt Isoform与PDB Chain的对应关系中的Deletion、InDel区域情况，并对匹配区域进行修正
* mapped out segment(have removed artifact residues)情况
* repeated mapping与reversed mapping情况
* 匹配区域中的残基坐标缺失情况
* 匹配区域中的残基冲突与修饰残基情况

并依据这些信息结合相关Entry-Based API获取来的信息对`UniProt Isoform`与`PDB Chain`的对应关系进行打分，即得到固定`UniProt Isoform`下其对应的多条`PDB Chain`的符合度指标，并进行排序。

对于单体蛋白结构代表集选择即利用贪婪算法与`overlap similarity coefficient` metric来选择出排名靠前的且覆盖`UniProt Isoform`范围有足够差异的`PDB Chain`。

$$
\text{OSC}_{\text{mo}} = \cfrac{|\text{unp\_mapped\_res1}\cap\text{unp\_mapped\_res2}|}{\min(|\text{unp\_mapped\_res1}|, |\text{unp\_mapped\_res2}|)}
$$

对与同聚体与异聚体蛋白结构代表集选择，`pdb-profiling`同时整合了`Interactome3D`与`PISA`的相互作用信息，给出`asymmetric unit`与`biological assembly`层面的`chain-level binary interaction`。并考虑到两条链的打分排名情况依照映射回`UniProt Isoform`的`interface residues`利用贪婪算法分别在`wasserstein distance`与`dice similarity coefficient` metric下选择出排名较好的、`interface region`有足够差异的相互作用。

$$
\text{DSC}_{\text{he}} = \cfrac{2|\text{interface\_res1}\cap\text{interface\_res2}|}{|\text{interface\_res1}| + |\text{interface\_res2}|}
$$

$$
\text{WD}_{\text{ho}} = \text{wasserstein\_distance}(\text{interface\_res1\_distribution}, \text{interface\_res2\_distribution})
$$

<table>
  <tr>
    <td>
      <img src="https://raw.githubusercontent.com/NatureGeorge/pdb-profiling/a7841d4033b3d5be6d17d225133e40912cf000ea/docs/figs/greedy_algorithm.drawio.svg">
    </td>
  </tr>
  <tr>
    <td>
      Selection Algorithm
    </td>
  </tr>
</table>

## 模型结构

为了弥补部分`UniProt Isoform`的部分区域无法被现有晶体结构覆盖的问题，`pdb-profiling`也应用了`SWISS-MODEL Repository API`来获取最新的相应`UniProt Isoform`的可用同源建模模型相关元数据，可自动根据建模区域判断其是否覆盖于晶体结构无法覆盖到的部分。

## 函数接口

pdb-profiling为上述各种API的调用与数据获取以及后续的数据处理提供了较为同一的调用接口与返回数据形式；为PDB残基位置映射、为UniProt Isoform与PDB Chain的映射关系打分以及单体/同聚体/异聚体的代表集结构筛选提供了相应的函数接口。

### 导入模块与设置工作目录

结合面对对象编程与函数式编程，只需少数代码即可完成众多流程，下面展示简单应用。首先是导入模块与设置工作目录:

```python
from pdb_profiling import default_config
from pdb_profiling.processors import PDB, SIFTS, SIFTSs
default_config(your_output_folder)
```

### 调用API

调用PDBe RESTful API等:

```python
PDB('3hl2').fetch_from_web_api('api/pdb/entry/molecules/', PDB.to_dataframe).result()
```

### 结构代表集的确定

对特定UniProt Isoform进行单体/同聚体/异聚体层面的代表集结构筛选:

```python
unp_demo = SIFTS('Q5VST9')
unp_demo.pipe_select_mo().result()
unp_demo.pipe_select_ho(run_as_completed=True).result()
unp_demo.pipe_select_he(run_as_completed=True).result()
```

### 批量检索

```python
SIFTSs(('P21359', 'Q5VST9', 'P21359-5')).fetch('pipe_select_mo').run().result()
```

### 程序设计

值得一提的是，pdb-profiling基于python，应用python的协程，在asyncio,aiohttp, unsync等框架的加持下能够高效解决大规模请求问题，规避python阻塞访问造成的性能问题，实现好大规模处理，且控制好信号量做到对server端足够友好而不占用过多资源造成dos(or ddos)攻击。

### API Reference

除了上述提及的API，pdb-profiling为了更好实现相关功能还其他API资源，完整API资源使用情况参见下表:

<table>
    <tr>
        <td>
            API Name
        </td>
        <td>
            Reference
        </td>
    </tr>
    <tr>
        <td>
            PDBe Entry-Based API
        </td>
        <td>
            <p>https://www.ebi.ac.uk/pdbe/api/doc/pdb.html</p>
            <p>https://www.ebi.ac.uk/pdbe/api/doc/pisa.html</p>
            <p>https://www.ebi.ac.uk/pdbe/api/doc/sifts.html</p>
        </td>
    </tr>
    <tr>
        <td>
            PDBe Aggregated API/PDBe Graph API
        </td>
        <td>
            <p>https://www.ebi.ac.uk/pdbe/graph-api/pdbe_doc/</p>
        </td>
    </tr>
    <tr>
        <td>
            PDBe ModelServer API
        </td>
        <td>
            <p>https://www.ebi.ac.uk/pdbe/model-server/</p>
        </td>
    </tr>
    <tr>
        <td>
            SWISS-MODEL Repository API
        </td>
        <td>
            <p>https://swissmodel.expasy.org/docs/smr_openapi</p>
        </td>
    </tr>
    <tr>
        <td>
            EBI Proteins API
        </td>
        <td>
            <p>https://www.ebi.ac.uk/proteins/api/doc/</p>
        </td>
    </tr>
    <tr>
        <td>
            UniProt API
        </td>
        <td>
            <p>https://www.uniprot.org/uploadlists/</p>
        </td>
    </tr>
    <tr>
        <td>
            Interactome3D API
        </td>
        <td>
            <p>https://interactome3d.irbbarcelona.org/</p>
        </td>
    </tr>
    <tr>
        <td>
            Ensembl REST API
        </td>
        <td>
            <p>https://rest.ensembl.org/documentation</p>
        </td>
    </tr>
    <tr>
        <td>
            Eutils API
        </td>
        <td>
            <p>https://eutils.ncbi.nlm.nih.gov/entrez/eutils/</p>
            <p>currently only support minimum use</p>
        </td>
    </tr>
    <tr>
        <td>
            Download data from PDB Archive against unexpected needs
        </td>
        <td>
            <p>http://www.ebi.ac.uk/pdbe/static/entry/download/</p>
            <p>http://ftp.ebi.ac.uk/pub/databases/pdb/data/structures/</p>
            <p>http://ftp-versioned.wwpdb.org/pdb_versioned/data/entries/</p>
        </td>
    </tr>
</table>
