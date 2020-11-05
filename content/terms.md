---
title: "pdb-profiling: 助力ProteinDataBank数据批量分析"
date: 2020-11-05T09:14:05.782Z
summary: ""
draft: false
---
[![Build](https://img.shields.io/travis/naturegeorge/pdb-profiling?style=flat-square&logo=travis)](https://github.com/naturegeorge/pdb-profiling)
[![SupportPythonVersion](https://img.shields.io/pypi/pyversions/pdb-profiling.svg?style=flat-square&logo=python)](https://pypi.org/project/pdb-profiling/)
[![Version](https://img.shields.io/pypi/v/pdb-profiling?style=flat-square&logo=PYPI)](https://github.com/naturegeorge/pdb-profiling/blob/master/pdb_profiling/__init__.py)
[![Dependencies](https://img.shields.io/librariesio/github/NatureGeorge/pdb-profiling?style=flat-square&logo=PYPI)](https://github.com/naturegeorge/pdb-profiling/blob/master/setup.py)
[![PyPIDownloads](https://img.shields.io/pypi/dm/pdb-profiling.svg?style=flat-square&logo=PYPI)](https://pypi.org/project/pdb-profiling/)
[![License](https://img.shields.io/badge/License-MIT-blue.svg?style=flat-square&logo=github)](https://github.com/naturegeorge/pdb-profiling/blob/master/LICENSE)
[![GitHubDownloads](https://img.shields.io/github/downloads/NatureGeorge/pdb-profiling/total?style=flat-square&logo=github)](https://github.com/NatureGeorge/pdb-profiling/releases/)
[![Coverage Status](https://img.shields.io/coveralls/github/NatureGeorge/pdb-profiling?style=flat-square&logo=coveralls)](https://coveralls.io/github/NatureGeorge/pdb-profiling?branch=master)

## Introduction

### The problem it solves

随着PDB条目数据的增长，对PDB元数据(metadata)批量处理的需求也在逐渐增加。同时，处理PDB数据本身也有着如下特点a) 不少PDB条目会在更新中会被弃用(obsolete);b) 部分PDB条目的内容会进行更新，其中包括对biological assembly的重新定义(i.e. 2wc8)、配体链的重命名(i.e. 1wdq)等;c) 解析PDB完整文件需要大量存储空间与下载/计算时间，为获取相关元数据而对完整PDB文件进行处理有些南辕北辙;d)解析各种PDB文件格式(.pdb, .cif, .mmtf etc.)在具有相关现成parser函数的情况下仍具有较高编程成本且存在各种边缘异常情况。所幸，EBI提供的PDBe RESTful API等服务能够很好的解决获取元数据的便捷性问题。面对上述问题，pdb-profiling应用了PDBe的Entry-Based API与Aggregated API(PDBe Graph API)。利用Entry-Based API能够实时地获取最新的PDB在Entry-Assembly/Model-Entity-Chain-Residue水平的元数据信息，进型相关信息的批量检索与收集。此外，这些信息也为.pdb与.cif及其他格式之间的数据标识符转化提供了足够信息，能够做到向前兼容一些较为早期的(old history)软件所需的标识符格式信息。且不单单应对asymmetric unit，同时处理好biological assembly。利用Entry-Based API中的SIFTS API能够做到最新版本下UniProt Isofrom与对应PDB在chain-level以及residue-level的高效映射，结合EBI's Proteins API能够实现突变信息在转录本与对应PDB Chain Instance的残基的双向映射。PDBe的Aggregated API与Entry-Based API还一同提供了chain-level和residue-level的丰富注释信息，能够获取结构域、二级结构、残基保守性、配体结合倾向等大量且丰富的预先计算好的特征。

此外，在UniProt视角下，不少UniProt对应的PDB晶体结构在对UniProt序列的覆盖度上有着较大的冗余度，对特定参考序列下(如UniProt)进行蛋白质晶体结构的代表集结构确定是个由来已久的需求。且考虑到a) 不少PDB结构依照具有一定局限性的序列匹配算法被错误对应上，这其中包括Insertion,Deletion,InDel,repeated mapping,reversed mapping,mapped out (head and tail) segment,residue conflict;b) PDB结构中存在着missing residue,UNK residue,modified residue,ligand binding residue,ca_p_only chain等。这使得确定一个严谨准确的蛋白质结构代表集流程对科学研究有着相当的重要性。同时，对于二元相互作用(同聚体相互作用、异聚体相互作用)，进行代表集相互作用结构筛选时有必要考虑到a) 是否具有UniProt binary interaction的生物学意义/crystal interaction是否具有意义;b) 同一对binary interaction下the residues of interacting interface的区别。pdb-profiling在SIFTS API等提供的数据的基础上，自主探查出a) UniProt Isoform与PDB Chain的对应关系中的Deletion、InDel区域情况，并对匹配区域进型修正;b) mapped out segment(have removed artifact residues)情况; c) repeated mapping与reversed mapping情况;d) 匹配区域中的残基坐标缺失情况; e) 匹配区域中的残基冲突与修饰残基情况。并依据这些信息对UniProt Isoform与PDB Chain的对应关系进行打分，即得到固定UniProt Isoform下其对应的多条PDB Chain的符合度指标，并进行排序。对于单体蛋白结构代表集选择即利用贪婪算法与overlap similarity coefficient metric来选择出排名靠前的且覆盖UniProt Isoform范围有足够差异的PDB Chain。对与同聚体与异聚体蛋白结构代表集选择，pdb-profiling同时整合了Interactome3D与PISA的相互作用信息，给出asymmetric unit与biological assembly层面的chain-level binary interaction；并考虑到两条链的打分排名情况依照映射回UniProt Isoform的interface residues利用贪婪算法分别在wasserstein distance与dice similarity coefficient metric下选择出排名较好的、interface region有足够差异的相互作用。为了弥补部分UniProt Isoform的部分区域无法被现有晶体结构覆盖的问题，pdb-profiling也应用了SWISS-MODEL Repository API来获取最新的相应UniProt Isoform的可用同源建模模型相关元数据，可自动根据建模区域判断其是否覆盖于晶体结构无法覆盖到的部分。

<table>
  <tr>
    <td>
      <img src="https://naturegeorge.github.io/eigenblog/assets/img/unp_map_pdb.drawio.svg">
    </td>
    <td>
      <img src="https://naturegeorge.github.io/eigenblog/assets/img/unp_map_pdb_insertion.drawio.svg">
    </td>
  </tr>
  <tr>
    <td>
      P68871 mapped with 1a01 Chain B
    </td>
    <td>
      Insertion: P30038-3 mapped with 4oe5 Chain D
    </td>
  </tr>
  <tr>
    <td>
      <img src="https://naturegeorge.github.io/eigenblog/assets/img/unp_map_pdb_deletion.drawio.svg">
    </td>
    <td>
      <img src="https://naturegeorge.github.io/eigenblog/assets/img/unp_map_pdb_indel.drawio.svg">
    </td>
  </tr>
  <tr>
    <td>
      Deletion: Q13303-3 mapped with 1zsx Chain A
    </td>
    <td>
      InDel: Q01780 mapped with 6d6q Chain J
    </td>
  </tr>
  <tr>
    <td>
      <img src="https://raw.githubusercontent.com/NatureGeorge/pdb-profiling/a7841d4033b3d5be6d17d225133e40912cf000ea/docs/figs/sifts_reversed_mapping.drawio.svg">
    </td>
    <td>
      <img src="https://raw.githubusercontent.com/NatureGeorge/pdb-profiling/a7841d4033b3d5be6d17d225133e40912cf000ea/docs/figs/sifts_repeated_mapping.drawio.svg">
    </td>
  </tr>
  <tr>
    <td>
      Reversed Mapping: P00441 mapped with 5j0c Chain A
    </td>
    <td>
      Repeated Mapping: Q7KZ85-3 mapped with 6gmh Chain M
    </td>
  </tr>
  <tr>
    <td>
      <img src="https://raw.githubusercontent.com/NatureGeorge/pdb-profiling/a7841d4033b3d5be6d17d225133e40912cf000ea/docs/figs/sifts_mapped_out_1.drawio.svg">
    </td>
    <td>
      <img src="https://raw.githubusercontent.com/NatureGeorge/pdb-profiling/a7841d4033b3d5be6d17d225133e40912cf000ea/docs/figs/sifts_mapped_out_2.drawio.svg">
    </td>
  </tr>
  <tr>
    <td>
      Mapped Out Situation: P14647 mapped with 3agp Chain A
    </td>
    <td>
      Mapped Out Situation: Q16611 mapped with 4u2v Chain C
    </td>
  </tr>
</table>

for Mo: Overlap Similarity Coefficient:

$$
\text{OSC} = \cfrac{|\text{unp\_mapped\_res1}\cap\text{unp\_mapped\_res2}|}{\min(|\text{unp\_mapped\_res1}|, |\text{unp\_mapped\_res2}|)}
$$

for He: Dice Similarity Coefficient:

$$
\text{DSC} = \cfrac{2|\text{interface\_res1}\cap\text{interface\_res2}|}{|\text{interface\_res1}| + |\text{interface\_res2}|}
$$

for Ho: Wasserstein Distance:

$$
\text{WD} = \text{wasserstein\_distance}(\text{interface\_res1\_distribution}, \text{interface\_res2\_distribution})
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

pdb-profiling为上述各种API的调用与数据获取以及后续的数据处理提供了较为同一的调用接口与返回数据形式；为PDB残基位置映射、为UniProt Isoform与PDB Chain的映射关系打分以及单体/同聚体/异聚体的代表集结构筛选提供了相应的函数接口。

结合面对对象编程与函数式编程，只需少数代码即可完成众多流程，下面展示简单应用。首先是导入模块与设置工作目录:

```py
from pdb_profiling import default_config
from pdb_profiling.processors import PDB, SIFTS, SIFTSs
default_config(your_output_folder)
```

调用PDBe RESTful API等:

```py
PDB('3hl2').fetch_from_web_api('api/pdb/entry/molecules/', PDB.to_dataframe).result()
```

对特定UniProt Isoform进行单体/同聚体/异聚体层面的代表集结构筛选:

```py
unp_demo = SIFTS('Q5VST9')
unp_demo.pipe_select_mo().result()
unp_demo.pipe_select_ho(run_as_completed=True).result()
unp_demo.pipe_select_he(run_as_completed=True).result()
```

批量检索:

```py
SIFTSs(('P21359', 'Q5VST9', 'P21359-5')).fetch('pipe_select_mo').run().result()
```

值得一提的是，pdb-profiling基于python，应用python的协程，在asyncio,aiohttp, unsync等框架的加持下能够高效解决大规模请求问题，规避python阻塞访问造成的性能问题，实现好大规模处理，且控制好信号量做到对server端足够友好而不占用过多资源造成dos(or ddos)攻击。

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
