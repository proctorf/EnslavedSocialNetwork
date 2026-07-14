# Dataset: Social Networks and Enslaved Community Formation in Mexico City, 1629–1637

This repository contains the data accompanying the article "Social Networks, 'Social Death,' and Enslaved Community Formation, 1629–1637." It includes a participant-level dataset, two nodes files, and two edge files representing different models of social connection among enslaved people in early seventeenth-century Mexico City.

---

## Source

The data in this repository were drawn from marriage applications (*informaciones matrimoniales*) preserved in the **Archivo General de la Nación, México (AGN)**, Ramo Matrimonios. The original documents are in Spanish. All variable names and categorical values in this dataset have been translated into English, with the exception of personal names and archival identifiers (Volumen, Expediente), which retain their original Spanish form.

---

## Files

### `PublicDF.csv`
The primary participant-level dataset. Each row represents one individual's appearance in a marriage application. Each application generated multiple rows — one for the bride, one for the groom, and one for each witness. This file contains 1,489 participant records drawn from 409 marriage applications.

### `nodes_participants.csv`
A deduplicated list of all 1,489 individuals in the dataset, intended for use as a nodes table in network analysis software. Because an individual may appear in more than one application, this file consolidates multiple appearances into a single record. Where name information varied across appearances, non-blank entries were prioritized.

### `nodes_enslavers.csv`
A deduplicated list of the 210 slaveholding households associated with two or more participants in the dataset. Only enslavers with two or more participants are included, as single connections do not contribute to network formation. This file is intended for use as a nodes table alongside `edges_w_households.csv`.

### `edges_undirected.csv`
An undirected edge list representing social connections between participants as documented in the marriage applications. In an undirected graph, edges have no directionality — a connection between Person A and Person B is the same as a connection between Person B and Person A. Each row contains a Source and Target column identifying a pair of individuals connected through their shared participation in a wedding — either as bride and groom, or as witnesses testifying on behalf of one or both parties. This file contains 2,039 edges.

### `edges_w_households.csv`
An undirected edge list that extends `edges_undirected.csv` by adding structural ties created through shared enslavement in the same household. In an undirected graph, edges have no directionality — a connection between Person A and Person B is the same as a connection between Person B and Person A. Individuals who do not appear connected in `edges_undirected.csv` may be connected here if they were enslaved by the same person or household. This file contains 2,574 edges (2,039 participant connections + 535 household connections) and was used to generate the network visualizations discussed in the article.

### `EnslavedNetworks.Rmd`
The R Markdown file used to construct all five CSV files from `PublicDF.csv`. It documents all data preparation and curatorial decisions made in building the dataset.

---

## Variables

### `PublicDF.csv`

| Variable | Description |
|---|---|
| WeddingID | Unique identifier for each marriage application (format: W0001) |
| ID | Unique identifier for each individual participant (format: P0001) |
| Volumen | Volume number in the AGN Matrimonios series (format: 000) |
| Expediente | File number within the volume (format: 000). The suffix "a" (e.g., 015a) indicates a second application within the same expediente, reflecting a case of corrected identity |
| Date | Date of the application (format: yyyy-mm-dd) |
| FirstName | Individual's first name as recorded in the source |
| Surname | Individual's surname as recorded in the source. Blank cells indicate the surname was not recorded |
| Race | Racial or ethnic designation as recorded in the source, translated into English |
| Status | For individuals of African or Asian descent, indicates whether the individual was enslaved, free, or freed at the time of the application. N/A indicates individuals whose racial classification (Indio/a, Spaniard) carried a presumption of free status under colonial law |
| Sex | Sex as deduced from the source |
| Role | Individual's role in the wedding application (Bride, Groom, W1/W2/etc. = Witness) |
| For | For witness entries, indicates whether the witness testified on behalf of the Bride, Groom, or Both. N/A indicates this was not applicable because the participant in question was the Bride or Groom |
| Age | Estimated age as recorded in the source. Available for witnesses only; N/A indicates the age was not recorded |
| EnslaverName | Surname and first name of the enslaver, where recorded (format: Surname, FirstName). N/A indicates the individual was not enslaved  |
| EnslaverID | Unique identifier for the enslaver (format: E0001). N/A indicates the participant was not enslaved |

### `nodes_participants.csv`

| Variable | Description |
|---|---|
| ID | Unique identifier for each individual (format: P0001). Links to Source and Target columns in both edge files |
| Name | Individual's full name, combining FirstName and Surname where available |

### `nodes_enslavers.csv`

| Variable | Description |
|---|---|
| EnslaverID | Unique identifier for the enslaver (format: E0001). Links to Source column in `edges_w_households.csv` |
| EnslaverName | Enslaver's name as recorded in the source (format: Surname, First and Middle Names) |

---

## Notes on the Data

**Accents and special characters**: Diacritical marks and special characters (e.g., n, a, e) have been standardized to their unaccented equivalents throughout this dataset to ensure compatibility across operating systems and software environments.

**Surnames**: Blank surname fields indicate the surname was not recorded in the original source. This is common in the documents.

**Ages**: Ages are recorded for witnesses only. Brides and grooms were not required to provide their age in these proceedings. Ages marked in the original working data as estimates have been included without notation in this public version.

**Race and Status**: Racial and ethnic designations are transcribed and translated from the original documents. They reflect the categories used by colonial notaries. The Status column indicates whether individuals of African or Asian descent were enslaved or free(d). N/A entries indicate individuals whose racial classification carried a presumption of free status under colonial law and for whom the category was not recorded in the source.

**Dates**: All dates are given in yyyy-mm-dd format.

**Enslaver records**: Rows with N/A in the EnslaverName and EnslaverID columns represent individuals who were not enslaved.

**Racial and Ethnic Designation — Curatorial Decisions**: Where the same individual appeared in multiple applications with inconsistent racial or ethnic designations, a single designation was assigned based on the preponderance of evidence across appearances. In cases where one entry recorded a specific African ethnicity and another recorded only a general category (e.g., Angola vs. Negro), the more specific ethnic designation was retained on the grounds that the less specific entry likely reflects incomplete record-keeping rather than a meaningful difference. The following individuals were affected by this decision: P0010, P0194, P0197, P0327, P0582, P0612, P0778, P0830, P0860, P1188, P1223, P1258, P1264, P1332, P1345, P1509, P1517, and P1518. These decisions are explained more fully in the accompanying article.

---

## Using the Files in Network Analysis Software

The two nodes files and two edge files are designed for use in network analysis software such as Gephi or R's igraph package. For the participant-only network, use `nodes_participants.csv` and `edges_undirected.csv`, linking on the ID column. For the full network including household connections, use both nodes files and `edges_w_households.csv`, linking participants on ID and enslavers on EnslaverID.

---

## License

This dataset is released under a [Creative Commons Attribution 4.0 International License (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/). You are free to share and adapt the data for any purpose provided appropriate credit is given.

---

## Citation

Citation information will be added upon publication.

---

## Acknowledgments

This README file was drafted with the assistance of Claude.ai. Claude.ai also served as a coding assistant in crafting the code in `EnslavedNetworks.Rmd`.