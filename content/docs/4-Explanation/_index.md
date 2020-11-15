---
# Title, summary, and page position.
linktitle: Explanation
summary: Understanding-Oriented
weight: 4
icon: book-reader
icon_pack: fas

# Page metadata.
title: Explanation
date: "2020-11-05T00:00:00Z"
type: book  # Do not modify.
authors:
  - admin
---

## `RAW_BS` Score

This section explains how does `pdb-profiling` define a weighted score that measure the correspondence between the UniProt Isoform and the PDB chain instance (apo-state) in the sequence-level.

## UniProt Isoform

This section explains why does `pdb-profiling` implement SIFTS's `api/mappings/all_isoforms/` API that mapped with all the available alternative products of a UniProt Entry in the `Selection` pipeline.

* From the point of transcript mapping
* From the point of the best-mapped isoform of a PDB Entity

## UniProt Isoform Interaction

This section explains why does `pdb-profiling` includes isoform-level interaction instead of just focuses on canonical interaction.

## Asymmetric Unit & Biological Unit

This section explains why does `pdb-profiling` not only includes interaction data from asymmetric unit but also from those author/software defined biological assembly. Besides, this section also shows the barriers that `pdb-profiling` overcame in the process of integrating biological assembly information.

## Metrics that measure the similarity/distance between two ranges

This section explains:

1. the ranges/intervals-format that `pdb-profiling` implements for the representation of sequence coverage range on a reference sequence
2. which metric `pdb-profiling` apply to measure the similarity/distance between two ranges in different situation and why

## Selection Algorithm

This section explains the greedy algorithm that `pdb-profiling` implements to yield a non-redundant set of coverage ranges, which can be used to define the representative set of protein structures in different polymer forms.


## Programming Details

This section explains the key points of `pdb-profiling`'s programming design and architecture, including:

1. Implement Coroutine & Asynchronous Programming
2. Take both of the advantages of file system and database system

## Comparison

This section compares `pdb-profiling` with previous similar works and emphasis on how `pdb-profiling` overcoming their short-comings.