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
authors:
  - admin
---

> The problem it solves

在自然生物体内，一生物功能的实现，往往需要具有生物学效应的蛋白质参与实施。对蛋白质结构本身、蛋白-蛋白相互作用(PPI)等层面的研究火热进行中。在繁复多样的数据中，**P**rotein **D**ata **B**ank(PDB)无疑是公认的重要资源，其与UniProt-KB等资源的整合能够很好地将生物学意义落实到具体的功能结构上。但是，处理PDB以及相关数据的相关工作还存在不少gap需要跨越。`pdb-profiling`为此而生。

## PDB元数据获取层面的相关问题

随着PDB条目数据的增长，对PDB元数据(metadata)批量处理的需求也在逐渐增加。同时，处理PDB数据本身也有着如下特点:

* 不少PDB条目会在更新中会被弃用(`obsolete`)
* 部分PDB条目的内容会进行更新，其中包括对`biological assembly`的重新定义(i.e. `2wc8`)、配体链的重命名(i.e. `1wdq`)等
* 解析PDB完整文件需要大量存储空间与下载/计算时间，为获取相关元数据而对完整PDB文件进行处理有些南辕北辙
* 解析各种PDB文件格式(`.pdb`, `.cif`, `.mmtf` etc.)在具有相关现成parser函数的情况下仍具有较高编程成本且存在各种边缘异常情况

所幸，`EBI`提供的`PDBe RESTful API`等[^1][^2]服务能够很好的解决获取元数据的便捷性问题。面对上述问题，`pdb-profiling`应用了`PDBe`的`Entry-Based API`[^1]与`Aggregated API`(`PDBe Graph API`)[^2]。利用`Entry-Based API`能够实时地获取最新的PDB在`Entry-Assembly/Model-Entity-Chain-Residue`水平的元数据信息，进行相关信息的批量检索与收集。此外，这些信息也为`.pdb`与`.cif`及其他格式之间的数据标识符转化提供了足够信息，能够做到向前兼容一些较为早期的(old history)软件所需的标识符格式信息。且不单单应对`asymmetric unit`，同时处理好`biological assembly`。利用`Entry-Based API`中的`SIFTS API`[^3]能够做到最新版本下`UniProt isoform`与对应PDB在`chain-level`以及`residue-level`的高效映射，结合`EBI's Proteins API`[^4]能够实现突变信息在转录本与对应`PDB Chain Instance`的残基的双向映射。`PDBe`的`Aggregated API`与`Entry-Based API`还一同提供了`chain-level`和`residue-level`的丰富注释信息，能够获取结构域、二级结构、残基保守性、配体结合倾向等大量且丰富的预先计算好的特征[^2]。

## 与`UniProt-KB`数据资源在整合时的问题

此外，在`UniProt`视角下，不少`UniProt`对应的PDB晶体结构在对`UniProt`序列的覆盖度上有着较大的冗余度，对特定参考序列下进行蛋白质晶体结构的代表集结构确定是个由来已久的需求。且考虑到:

* PDB结构与UniProt Isoform的匹配采用SIFTS资源，而SIFTS的匹配结果是以PDB的SEQRES序列为参考序列利用BLAST算法进行匹配产生的[^3]，这就使得以UniProt Isoform为参考序列来选择PDB结构时需要注意如下情况:
  * Insertion: 部分匹配上的PDB链的序列在匹配区域中间存在一段或多段参考序列上不具有的序列片段
  * Deletion: 部分匹配上的PDB链的序列在匹配区域中间缺失一段或多段参考序列上本来具有的序列片段
  * InDel: 部分匹配上的PDB链的序列在匹配区域中间与参考序列的部分片段存在较大差异
  * repeated mapping: 部分UniProt Isoform序列片段被多次匹配上PDB链的序列片段
  * reversed mapping: 部分UniProt Isoform序列片段被倒序匹配于PDB链的某序列片段
  * mapped out (head and tail) segment: PDB链在除了匹配上对应UniProt Isoform的片段之外在C/N端还具有其他较大的序列片段
  * residue conflict: 在匹配区域中，PDB链的序列与参考序列存在个别残基差异
* PDB结构中存在着
  * missing residues (unmodelled residues): 晶体结构在解析时并不一定能够解析出SEQRES所有残基的空间结构，存在部分残基未被建模出来
  * UNK residues: 晶体结构中由于实验方法的限制，有时候不能确定解析出的残基的氨基酸种类
  * modified residues: 晶体结构中有时会有部分残基被化学修饰，氨基酸的侧链发生改变使得其为非标准氨基酸
  * ligand binding residues: 晶体结构中会有部分残基与配体相结合
  * ca_p_only chain: 由于实验方法的限制，有时解析出的整条多肽链都只有C-alpha而无侧链原子
* UniProt数据本身也会随着版本更新而对条目数据进行变化，包括条目的增删改、canonical isoform的重新界定等

这使得确定一个严谨准确的蛋白质结构代表集流程对科学研究有着相当的重要性。

{{< figure library="true" src="unp_map_pdb.drawio.svg" title="P68871 mapped with 1a01 Chain B" >}}

{{< figure library="true" src="unp_map_pdb_insertion.drawio.svg" title="Insertion: P30038-3 mapped with 4oe5 Chain D" >}}

{{< figure library="true" src="unp_map_pdb_deletion.drawio.svg" title="Deletion: Q13303-3 mapped with 1zsx Chain A" >}}

{{< figure library="true" src="unp_map_pdb_indel.drawio.svg" title="InDel: Q01780 mapped with 6d6q Chain J" >}}

{{< figure library="true" src="sifts_reversed_mapping.drawio.svg" title="Reversed Mapping: P00441 mapped with 5j0c Chain A" >}}

{{< figure library="true" src="sifts_repeated_mapping.drawio.svg" title="Repeated Mapping: Q7KZ85-3 mapped with 6gmh Chain M" >}}

{{< figure library="true" src="sifts_repeated_mapping.drawio.svg" title="Repeated Mapping: Q7KZ85-3 mapped with 6gmh Chain M" >}}

{{< figure library="true" src="sifts_mapped_out_1.drawio.svg" title="Mapped Out Situation: P14647 mapped with 3agp Chain A" >}}

{{< figure library="true" src="sifts_mapped_out_2.drawio.svg" title="Mapped Out Situation: Q16611 mapped with 4u2v Chain C" >}}

## 与二元相互作用数据资源在整合时的问题

同时，对于二元相互作用(同聚体相互作用、异聚体相互作用)，进行代表集相互作用结构筛选时有必要考虑到

* UniProt binary interaction是否具有生物学意义
* crystal interaction是否具有意义，是单纯的crystal patch还是说确实在分子表型层面其能够形成相互作用
* 同一对binary interaction下the residues of interacting interface的区别

## 代表集结构的确定问题

`pdb-profiling`在`SIFTS API`等提供的数据的基础上，自主探查出

* UniProt Isoform与PDB Chain的对应关系中的Deletion、InDel区域情况，并对匹配区域进行修正
* mapped out segment(have removed artifact residues)情况
* repeated mapping与reversed mapping情况
* 匹配区域中的残基坐标缺失情况
* 匹配区域中的残基冲突与修饰残基情况

并依据这些信息结合相关Entry-Based API获取来的信息对`UniProt Isoform`与`PDB Chain`的对应关系进行打分，即得到固定`UniProt Isoform`下其对应的多条`PDB Chain`的符合度指标，并进行排序。

### How it score

1. $s_1$: the number of residues that observed & mapped & standard
2. $s_2$: the number of residues out of mapped ranges while ignoring artifact residues
3. $s_3$: the number of residues that binds ligands
4. $s_4$: the number of residues that missing in the tertiary structure
5. $s_5$: the number of residues that observed & mapped & (conflict | modified)
6. $s_6$: the number of residues that fall into the ranges of Indel region

$$
W = [1, -1, -1, -1.79072623, -2.95685934, -4.6231746]
$$

$$
\text{Score}=\cfrac{\sum_{i=1}^{n=6}w_i\cdot s_i}{\text{length of UniProt Isoform Seq}}
$$

分值最佳为1，取值范围为$(-\infty, 1]$

### Coverage Metric

对于单体蛋白结构代表集选择即利用贪婪算法与`overlap similarity coefficient` metric来选择出排名靠前的且覆盖`UniProt Isoform`范围有足够差异的`PDB Chain`。

$$
\text{OSC}_{\text{mo}} = \cfrac{|\text{unp\_mapped\_res1}\cap\text{unp\_mapped\_res2}|}{\min(|\text{unp\_mapped\_res1}|, |\text{unp\_mapped\_res2}|)}
$$

对与同聚体与异聚体蛋白结构代表集选择，`pdb-profiling`同时整合了`PISA`[^5]与`Interactome3D`[^6]的相互作用信息，给出`asymmetric unit`与`biological assembly`层面的`chain-level binary interaction`。并考虑到两条链的打分排名情况依照映射回`UniProt Isoform`的`interface residues`利用贪婪算法分别在`wasserstein distance`与`dice similarity coefficient` metric下选择出排名较好的、`interface region`有足够差异的相互作用。

$$
\text{DSC}_{\text{he}} = \cfrac{2|\text{interface\_res1}\cap\text{interface\_res2}|}{|\text{interface\_res1}| + |\text{interface\_res2}|}
$$

$$
\text{WD}_{\text{ho}} = \text{wasserstein\_distance}(\text{interface\_res1\_distribution}, \text{interface\_res2\_distribution})
$$

### Selection Algorithm

{{< figure library="true" src="greedy_algorithm.drawio.svg" title="Selection Algorithm" >}}

## 模型结构

为了弥补部分`UniProt Isoform`的部分区域无法被现有晶体结构覆盖的问题，`pdb-profiling`也应用了`SWISS-MODEL Repository API`[^7]来获取最新的相应`UniProt Isoform`的可用同源建模模型相关元数据，可自动根据建模区域判断其是否覆盖于晶体结构无法覆盖到的部分。

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

## Reference

[^1]: Mir S, Alhroub Y, Anyango S, Armstrong DR, Berrisford JM, Clark AR, Conroy MJ, Dana JM, Deshpande M, Gupta D, Gutmanas A, Haslam P, Mak L, Mukhopadhyay A, Nadzirin N, Paysan-Lafosse T, Sehnal D, Sen S, Smart OS, Varadi M, Kleywegt GJ, Velankar S. PDBe: towards reusable data delivery infrastructure at protein data bank in Europe. Nucleic Acids Res. 2018 Jan 4;46(D1):D486-D492. doi: 10.1093/nar/gkx1070. PMID: 29126160; PMCID: PMC5753225.
[^2]: PDBe-KB consortium. PDBe-KB: a community-driven resource for structural and functional annotations. Nucleic Acids Res. 2020 Jan 8;48(D1):D344-D353. doi: 10.1093/nar/gkz853. PMID: 31584092; PMCID: PMC6943075.
[^3]: Dana JM, Gutmanas A, Tyagi N, Qi G, O'Donovan C, Martin M, Velankar S. SIFTS: updated Structure Integration with Function, Taxonomy and Sequences resource allows 40-fold increase in coverage of structure-based annotations for proteins. Nucleic Acids Res. 2019 Jan 8;47(D1):D482-D489. doi: 10.1093/nar/gky1114. PMID: 30445541; PMCID: PMC6324003.
[^4]: Andrew Nightingale, Ricardo Antunes, Emanuele Alpi, Borisas Bursteinas, Leonardo Gonzales, Wudong Liu, Jie Luo, Guoying Qi, Edd Turner, Maria Martin, The Proteins API: accessing key integrated protein and genome information, Nucleic Acids Research, Volume 45, Issue W1, 3 July 2017, Pages W539–W544, https://doi.org/10.1093/nar/gkx237
[^5]: Protein interfaces, surfaces and assemblies' service PISA at the European Bioinformatics Institute. (http://www.ebi.ac.uk/pdbe/prot_int/pistart.html), paper E. Krissinel and K. Henrick (2007). 'Inference of macromolecular assemblies from crystalline state.'. J. Mol. Biol. 372, 774--797.
[^6]: Mosca R, Céol A, Aloy P. Interactome3D: adding structural details to protein networks. Nat Methods. 2013 Jan;10(1):47-53. doi: 10.1038/nmeth.2289. Epub 2012 Dec 16. PMID: 23399932.
[^7]: Stefan Bienert, Andrew Waterhouse, Tjaart A. P. de Beer, Gerardo Tauriello, Gabriel Studer, Lorenza Bordoli, Torsten Schwede, The SWISS-MODEL Repository—new features and functionality, Nucleic Acids Research, Volume 45, Issue D1, January 2017, Pages D313–D319, https://doi.org/10.1093/nar/gkw1132
