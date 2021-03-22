---
title: Command Line Tutorial
linktitle: Command Line Tutorial
type: book
date: "2020-12-09T00:00:00+01:00"
weight: 3
authors:
  - admin
---

## Map from transcript/protein identifier to UniProt Isoform

> for canonical isoform, the isoform suffix would be dropped

```bash
pdb_profiling --folder $your_output_folder id-mapping --input $id_file
```

> `--folder $your_output_folder` can be ignored and the default value is the current path

### Demo content for `$id_file`

```tsv
ENSP00000491589
ENST00000379268
ENSP00000427757
ENSP00000266732
NP_001291289.1
ENST00000335295
NP_001165602.1
P21359-3
ENST00000402254
ENST00000371100
NM_000267.3
P68871
```

The mapping results are stored in the`$your_output_folder/local/CustomDB.db`'s IDMapping Table.

If your `$id_file` has column name(s), you can add `--column $column_name`, and the command becomes this:

```bash
pdb_profiling --folder $your_output_folder id-mapping --input $id_file --column $column_name
```

## Map from UniProt Isoform to available PDB Chain instance

```bash
pdb_profiling --folder $your_output_folder sifts-mapping --func pipe_base --output $output_file
```

By default, this command would load UniProt Isoforms from the `$your_output_folder/local/CustomDB.db`'s IDMapping Table and perform the SIFTS mapping procedure.

Noted that if you start a new task in the same folder, you should delete `$your_output_folder/local/CustomDB.db`'s IDMapping Table or the complete DB file.

### Load External File to process

If you already have a file containing UniProt Isoform identifiers, you can directly run the `sifts-mapping` command without running the `id-mapping` command:

```bash
pdb_profiling --folder $your_output_folder sifts-mapping --input $id_file --func pipe_base --output $output_file
```

Still, if you have column name(s) in your `$id_file`, you can add `--column $column_name`.

Noted that you should drop duplicate identifiers by yourself.

### Perform Selection

|  Type   | Args  |
|  ----  | ----  |
| Monomer  | `sifts-mapping --func pipe_select_mo` (default) |
| Homodimer | `sifts-mapping --func pipe_select_ho` |
| Heterodimer | `sifts-mapping --func pipe_select_he` |
| Protein-Ligand Interaction Pair | `sifts-mapping --func pipe_select_else --kwargs '{"func": "pipe_protein_ligand_interface", "focus_assembly_ids": (0,)}'` |
| Protein-Nucleotide Interaction Pair | `sifts-mapping --func pipe_select_else --kwargs '{"func": "pipe_protein_nucleotide_interface"}'` |

## Retrieve SMR Data

```bash
pdb_profiling --folder $your_output_folder sifts-mapping --input $id_file --output $output_file --func pipe_select_smr_mo
```

## Map from PDB to UniProt Isoform

```bash
pdb_profiling --folder $your_output_folder sifts-mapping --input $id_file --output $output_file --func pipe_base --column pdb
```

### Demo content for `$id_file`

```tsv
pdb
1a01
2xyn
3hl2
4hho
```

## Residue Mapping expanded from SIFTS mapping results

```bash
pdb_profiling --folder $your_output_folder residue-mapping --input $sifts_file --output $output_file
```

Noted that the default separator is `\t`, if your input file has another separator, you can add `--sep $your_sep`

### Demo content for `$sifts_file`

<table>
	<thead>
		<tr>
			<td>UniProt</td>
			<td>pdb_id</td>
			<td>struct_asym_id</td>
			<td>new_pdb_range</td>
			<td>new_unp_range</td>
			<td>conflict_pdb_index</td>
		</tr>
	</thead>
	<tr>
		<td>P16144</td>
		<td>3f7p</td>
		<td>C</td>
		<td>[[4,247]]</td>
		<td>[[1126,1369]]</td>
		<td>{}</td>
	</tr>
	<tr>
		<td>P49366</td>
		<td>6wkz</td>
		<td>A</td>
		<td>[[4,372]]</td>
		<td>[[1,369]]</td>
		<td>{}</td>
	</tr>
	<tr>
		<td>Q96RI1-4</td>
		<td>5q1b</td>
		<td>A</td>
		<td>[[5,233]]</td>
		<td>[[254,482]]</td>
		<td>{"38":"E","111":"E"}</td>
	</tr>
	<tr>
		<td>P49366</td>
		<td>6xxh</td>
		<td>A</td>
		<td>[[1,369]]</td>
		<td>[[1,369]]</td>
		<td>{}</td>
	</tr>
	<tr>
		<td>O14558</td>
		<td>4jus</td>
		<td>A</td>
		<td>[[1,104]]</td>
		<td>[[57,160]]</td>
		<td>{}</td>
	</tr>
</table>

## Download Complete PDB Structure from PDB Archive

### `.pdb` format

```bash
pdb_profiling --folder $your_output_folder sifts-mapping --input $id_file --func fetch_from_PDBArchive --kwargs 'dict(api_suffix=\"divided/pdb/\")'
```

By default, the file suffix would be `.ent.gz`. You can specify the file suffix you want.

```bash
pdb_profiling --folder $your_output_folder sifts-mapping --input $id_file --func fetch_from_PDBArchive --kwargs 'dict(api_suffix=\"divided/pdb/\", file_suffix=\".pdb.gz\")'
```

### `.cif` format

```bash
pdb_profiling --folder $your_output_folder sifts-mapping --input $id_file --func fetch_from_PDBArchive --kwargs 'dict(api_suffix=\"divided/mmCIF/\")'
```

--- 

## Collect PDB-Based Annotations

### From SIFTS Resources

#### Sequence Domain

> `api/mappings/sequence_domains/` (interpro & pfam)

* interpro: `api/mappings/interpro/`
* pfam: `api/mappings/pfam/`

#### Structrual Domain

> `api/mappings/structural_domains/` (scop & cath)

* `api/mappings/scop/`
* `api/mappings/cath/`
* `api/mappings/cath_b/`

#### Others

* `api/mappings/go/`
* `api/mappings/ec/`
* `api/mappings/hmmer/`
* `api/pdb/entry/secondary_structure/`

### From PDBe Graph Database (PDBe Graph API/Aggregated API)

#### FunPDBe Resources

* `graph-api/pdb/funpdbe_annotation/`
  * `graph-api/pdb/funpdbe_annotation/depth/`,
  * `graph-api/pdb/funpdbe_annotation/cath-funsites/`,
  * `graph-api/pdb/funpdbe_annotation/3Dcomplex/`,
  * `graph-api/pdb/funpdbe_annotation/akid/`,
  * `graph-api/pdb/funpdbe_annotation/3dligandsite/`,
  * `graph-api/pdb/funpdbe_annotation/camkinet/`,
  * `graph-api/pdb/funpdbe_annotation/canSAR/`,
  * `graph-api/pdb/funpdbe_annotation/ChannelsDB/`,
  * `graph-api/pdb/funpdbe_annotation/dynamine/`,
  * `graph-api/pdb/funpdbe_annotation/FoldX/`,
  * `graph-api/pdb/funpdbe_annotation/MetalPDB/`,
  * `graph-api/pdb/funpdbe_annotation/M-CSA/`,
  * `graph-api/pdb/funpdbe_annotation/p2rank/`,
  * `graph-api/pdb/funpdbe_annotation/Missense3D/`,
  * `graph-api/pdb/funpdbe_annotation/POPScomp_PDBML/`,
  * `graph-api/pdb/funpdbe_annotation/ProKinO/`,
  * `graph-api/pdb/funpdbe_annotation/14-3-3-pred/`

#### Others

* `graph-api/pdb/bound_molecules/`
* `graph-api/pdb/bound_molecule_interactions`
* `graph-api/pdb/sequence_conservation/`
* `graph-api/uniprot/sequence_conservation/`
* `graph-api/uniprot/annotations/`
* ...

Code:

```python
PDB('1a01').fetch_from_pdbe_api('api/mappings/sequence_domains/').result()
PDB(['1a01', '3hl2']).fetch('fetch_from_pdbe_api', api_suffix='api/mappings/structural_domains/').run().result()
```

Command line:

```bash
pdb_profiling sifts-mapping \
      --input pdbs.dat \
      --func fetch_from_pdbe_api \
      --kwargs 'dict(api_suffix="api/mappings/interpro/")' \
      --chunksize 50 \
      --skip_pdbs ''
```