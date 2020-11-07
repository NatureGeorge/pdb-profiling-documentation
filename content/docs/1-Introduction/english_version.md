---
title: Introduction (English Version)
linktitle: Introduction (English Version)
type: book
date: "2020-11-05T00:00:00+01:00"
# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 2
---

> The problem it solves

## Issues related to PDB metadata acquisition

With the increase of PDB entry data, the demand for batch processing of PDB metadata is increasing. At the same time, processing PDB data itself has the following characteristics:

* Many PDB entries will be discarded in the update
* Some PDB entries will be updated, including redefining biological assembly (i.e. 2wc8), renaming ligand chains (i.e. 1wdq), etc
* It takes a lot of storage space and download / calculation time to parse the PDB complete file. It is quite heavy to deal with the complete pdb file in order to obtain the relevant metadata
* Parsing various pdb file formats (`.pdb`,`.cif`,`.mmtf` etc.) still has high programming cost and various edge exceptions when there is a related off the shelf parser function

Fortunately, the `PDBe RESTful API` and other services provided by EBI can solve the problem of convenient access to metadata. To solve these problems, `pdb-profiling` applies the `Entry-Based API` and `Aggregated API` (pdbe graph API) of pdbe. Using the `Entry-Based API`, we can get the latest PDB metadata information at the `Entry-Assembly/Model-Entity-Chain-Residue level` in real time, and retrieve and collect the relevant information in batch. In addition, this information also provides enough information for the data identifier transformation between `.pdb` and `.cif` and other formats, which can be compatible with some earlier (old history) software identifier format information. We not only deal with asymmetric unit, but also deal with biological assembly. Using the sifts API of `Entry-Based API`, we can achieve the efficient mapping of UniProt isoform and corresponding PDB at chain level and residue level under the latest version. In combination with EBI's proteins API, we can realize bidirectional mapping of mutation information between transcripts and corresponding PDB chain instance residues. Pdbe's `Aggregated API` and `Entry-Based API` also provide rich chain-level and residue-level annotation, which can obtain a large number of pre calculated features such as domain, secondary structure, residue conservation, ligand binding tendency, etc.

## Problems in integration with `UniProt-KB` data resources

In addition, from the perspective of UniProt, many of the PDB crystal structures corresponding to a particular UniProt Isoform have large redundancy on the coverage of UniProt Isoform sequences. It is a long-standing requirement to determine the representative set structure of protein crystal structure under specific reference sequences. And consider the following:

* Many PDB structures are wrongly mapped according to the sequence matching algorithm with certain limitations, including
  * Insertion
  * Deletion
  * InDel
  * repeated mapping
  * reversed mapping
  * mapped out (head and tail) segment
  * residue conflict
* PDB structure exists
  * missing residue
  * UNK residue
  * modified residue
  * ligand binding residue
  * ca_p_only chain

This makes it crucial to determine a rigorous and accurate protein structure representative set process for scientific research.

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

## The problem of data resource integration with binary interaction resource

At the same time, for binary interaction (homopolymer interaction, heteropolymer interaction), it is necessary to consider the following conditions when selecting representative set interaction structure:

* Is UniProt binary interaction of biological significance
* Does crystal interaction make sense
* The differences of the residues of interacting interfaces under the same pair of binary interactions

## The problem of determining the representative structure set

On the basis of the data provided by `SIFTS API`, `pdb-profiling` independently detects the following situations:

* UniProt Isoform与PDB Chain的对应关系中的Deletion、InDel区域情况，并对匹配区域进型修正
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

调用`PDBe RESTful API`等:

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
            PDBe `Aggregated API`/PDBe Graph API
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
