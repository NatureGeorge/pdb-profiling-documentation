---
# Title, summary, and page position.
linktitle: Reference
summary: Information-Oriented
weight: 5
icon: book-reader
icon_pack: fas

# Page metadata.
title: Reference
date: "2020-11-05T00:00:00Z"
type: book  # Do not modify.
---

## RESTful API Reference

* Apply mature and robust API to collect well-organized data
  * PDBe REST API
    * <https://www.ebi.ac.uk/pdbe/api/doc/pdb.html>
    * <https://www.ebi.ac.uk/pdbe/api/doc/pisa.html>
    * <https://www.ebi.ac.uk/pdbe/api/doc/sifts.html>
  * PDBe Graph API (Neo4j Graph DataBase)
    * <https://www.ebi.ac.uk/pdbe/graph-api/pdbe_doc/>
  * PDBe CoordinateServer API
    * <https://www.ebi.ac.uk/pdbe/coordinates/index.html>
    * <https://cs.litemol.org/>
  * ModelServer API
    * `PDBe`: <https://www.ebi.ac.uk/pdbe/model-server/>
    * `RCSB`: <https://models.rcsb.org/>
  * PDBe DensityServer API
    * <https://ds.litemol.org/>
  * PDBe VolumeServer API
    * <https://www.ebi.ac.uk/pdbe/volume-server/>
  * SWISS-MODEL Repository API
    * <https://swissmodel.expasy.org/docs/smr_openapi>
  * EBI Proteins API
    * <https://www.ebi.ac.uk/proteins/api/doc/>
  * UniProt API
    * <https://www.uniprot.org/uploadlists/>
    * <https://www.uniprot.org/uniprot/*.fasta>
  * Interactome3D API
    * <https://interactome3d.irbbarcelona.org/>
  * Ensembl REST API
    * <https://rest.ensembl.org/documentation>
    * <https://rest.ensembl.org/documentation/info/sequence_id>
    * <https://rest.ensembl.org/documentation/info/archive_id_get>
  * Eutils API
    * <https://eutils.ncbi.nlm.nih.gov/entrez/eutils/>
    * NOTE: currently only support minimum use
* Download data from PDB Archive against unexpected needs
  * wwPDB&RCSB: <https://ftp.wwpdb.org/pub/pdb/data/structures/>
  * EBI: <http://ftp.ebi.ac.uk/pub/databases/pdb/data/structures/>
  * wwPDB Versioned: <http://ftp-versioned.wwpdb.org/pdb_versioned/data/entries/>

## Package Method API Reference

building...

## Column Name Reference

* `pdb_id`: PDB Entry ID
* `entity_id`: the entity identifier of a PDB Entity; for *what is PDB Entity?* please look at [this link](https://pdb101.rcsb.org/learn/guide-to-understanding-pdb-data/beginner%E2%80%99s-guide-to-pdb-structures-and-the-pdbx-mmcif-format)
* `molecule_type`
* `ca_p_only`: whether the PDB Entity only contains C-alpha atom for each observed residue
* `chain_id`: the chain identifier of a PDB Chain
* `struct_asym_id`: the chain identifier of a PDB Chain (unique across all PDB Entity)
* `Entry`: UniProt Entry ID
* `UniProt`: UniProt Isoform ID
* `is_canonical`: whether the UniProt Isoform is the canonical isoform defined by UniProt-KB
* `identity`: provided by SIFTS: sequence identity of PDB Entity SEQRES with UniProt Isoform (0-1)
* `unp_range`: mapped range of the UniProt Isoform's Sequence with its corresponding PDB Chain's Sequence (Index from 1)
* `pdb_range`: mapped range of the PDB Chain's Sequence Sequence with its corresponding UniProt Isoform's (Index from 1)
* `new_unp_range`: fixed(deal with InDel) mapped range of the UniProt Isoform's Sequence with its corresponding PDB Chain's Sequence (Index from 1)
* `new_pdb_range`: fixed(deal with InDel) mapped range of the PDB Chain's Sequence Sequence with its corresponding UniProt Isoform's (Index from 1)
* `conflict_pdb_range`: the chain's residue index of residue confilct with UniProt isoform sequence in the mapped range(Index from 1)
* `select_tag`: whether in the recommanded representative set
* `select_rank`: the rank among all the chains (1st denoted as the best)
* `RAW_BS`
* `RAW_BS_IG3`

* `sifts_range_tag`
  * ([example](https://naturegeorge.github.io/eigenblog/posts/introduce-pdb-profiling/#about-mapped-range-reformated-by-pdb-profiling))
  * `Safe`
  * `Insertion`
  * `Deletion`
  * `InDel`
* `reversed`
  * whether there is reversed mapped range in the aspect of UniProt Isoform Sequence ([P00441 5j0c A](https://naturegeorge.github.io/eigenblog/posts/introduce-pdb-profiling/#about-mapped-range-reformated-by-pdb-profiling))
  * SIFTS是以PDB Chain Sequence的视角来匹配序列片段，少数情况会有把部分unp序列反向匹配
  * "5j0c - it the circular permutant structure where authors have swapped the few chunk protein from front and back -(figure 2 in <https://pubs.acs.org/doi/pdf/10.1021/jacs.6b05151>). That's why you see "the head of the UniProt sequence is mapped with the tail of the PDB-Chain sequence" -- from Preeti Choudhary
* `repeated`
  * whether there is repeated mapped range in the aspect of UniProt Isoform Sequence ([i.e. Q7KZ85-3 6gmh M](https://naturegeorge.github.io/eigenblog/posts/introduce-pdb-profiling/#about-mapped-range-reformated-by-pdb-profiling))
  * "In SIFTS, the segment generation is done from PDB point of view, that's why you will see continuous pdb ranges. Seldom, in protein structures, you may see a same protein (uniprot accession) is present in copies/or is repeated" -- from Preeti Choudhary

* `_1`: denoted as the partner chain 1
* `_2`: denoted as the partner chain 2
* `assembly_id`
    * 0 stands for asymmetric unit
    * 1 stands for biological assembly 1 
    * 2 stands for biological assembly 2
    * and so on
    * for *what is asymmetric unit & biological assembly?* please [click the link](https://pdb101.rcsb.org/learn/guide-to-understanding-pdb-data/biological-assemblies)
* `model_id`: the model ID of the chain in the corresponding biological assembly PDB format file
    * 0 denoted as the first model
* `asym_id_rank`
* `struct_asym_id_in_assembly`
* `interface_id`
* `unp_range_DSC`: the Dice Similarity Coefficient of `new_unp_range_1` & `new_unp_range_2`
* `interface_range_1`: the range of the interaction's interface in the aspect of partner1 chain (Index from 1)
* `interface_range_2`: the range of the interaction's interface in the aspect of partner2 chain (Index from 1)
* `unp_interface_range_1`: the range of the interaction's interface in the aspect of partner1 chain (mapped to the UniProt Isoforom)
* `unp_interface_range_2`: the range of the interaction's interface in the aspect of partner2 chain (mapped to the UniProt Isoforom)
* `i_select_tag`: whether in the recommanded interaction representative set
* `i_select_rank`: the rank among all the interacting-chains (1st denoted as the best)
* `i_group`: the Interaction Group
* `in_i3d`: 判断这一PPI是否在`Interactome3D`数据集中(UniProt Entry相互作用以及对应biological assembly、model的PDB Chain相互作用都在数据集中才为True)

* `unp_residue_number`: residue index in the aspect of the UniProt Isoform's Sequence (Index from 1)
* `residue_number`: residue index in the aspect of the PDB Chain's Sequence (SEQRES, Index from 1)
* `author_residue_number`: residue index in the aspect of the PDB Chain's Sequence but assigned by the author of this PDB Entry
* `author_insertion_code`
* `multiple_conformers`

* `SEQRES_COUNT`: the count of the residues in SEQRES
* `OBS_INDEX`: the index of observed/modelled (with coordinates) residues of the PDB Chain Instance
* `OBS_COUNT`: the count of observed/modelled (with coordinates) residues of the PDB Chain Instance
* `OBS_RATIO_SUM`: the sum of the observed/modelled (with coordinates) residues's ratio of the PDB Chain Instance
* `BINDING_LIGAND_INDEX`: the residues that binding to ligands(including carbohydrate polymer) of the PDB Chain Instance
* `BINDING_LIGAND_COUNT`: the count of residues that binding to ligands(including carbohydrate polymer) of the PDB Chain Instance
* `STD_INDEX`: the index of the standard residues of the PDB Entity
* `STD_COUNT`: the count of the standard residues of the PDB Entity
* `OBS_STD_INDEX`: the index of the standard residues of the PDB Entity
* `OBS_STD_COUNT`: the count of the observed standard residues of the PDB Chain Instance
* `NON_INDEX`: the index of non-standard residues of the PDB Entity (including UNK)
* `NON_COUNT`: the count of non-standard residues of the PDB Entity (including UNK)
* `UNK_INDEX`: the index of the UNK residues of the PDB Entity
* `UNK_COUNT`: the count of the UNK residues of the PDB Entity
* `dNTP_INDEX`: the index (in SEQRES) of DA|DT|DC|DG|DI in that PDB Entity
* `dNTP_COUNT`: the count of DA|DT|DC|DG|DI in that PDB Entity
* `NTP_INDEX`: the index (in SEQRES) of A|U|C|G|I in that PDB Entity
* `NTP_COUNT`: the count of A|U|C|G|I in that PDB Entity
* `ARTIFACT_INDEX`
* `conflict_pdb_index`
* `conflict_pdb_range`
* `conflict_unp_range`
* `unp_len`: the length of the UniProt Isoform Sequence
* `InDel_sum`: SEQRES residues that fall into the range of Insertion or Deletion or InDel of the PDB Chain Instance

* `resolution`: ([pdb-101-explanation](http://pdb101.rcsb.org/learn/guide-to-understanding-pdb-data/resolution))
* `experimental_method_class`: ([pdb-101-explanation](https://pdb101.rcsb.org/learn/guide-to-understanding-pdb-data/methods-for-determining-structure))
* `experimental_method`: x-ray, nmr, em, other
* `multi_method`: whether the PDB entry was determined by multiple method
* `revision_date`: as name said
* `deposition_date`: as name said