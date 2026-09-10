# 🌊 Knowledge Graphs for Water Management

## EULiST Summer School 2026

Welcome to the participant repository for the **Knowledge Graphs for Water Management – EULiST Summer School 2026**, hosted in **Hannover, Germany, from 13–19 September 2026**.

🔗 **Summer School Website:** https://kgwm.l3s.uni-hannover.de/

This repository serves as the collaborative workspace for participants during the hands-on Knowledge Graph activities and group project sprints.

---

## 🎯 About the Summer School

The **Knowledge Graphs for Water Management Summer School** brings together researchers working across:

* 💧 Water and wastewater management
* 🌱 Environmental science and sustainability
* 🧠 Artificial Intelligence
* 🔗 Knowledge Graphs and Semantic Web technologies
* 📊 Data management and interoperability
* 🏙️ Sustainable and intelligent water systems

The Summer School combines environmental engineering, sustainable water governance, and semantic technologies.

A central objective is to explore how heterogeneous water-related data from different disciplines and repositories can be transformed into **interoperable Knowledge Graphs** that support data integration, exploration, querying, and decision-making.

Participants work collaboratively on real-world water-management scenarios and develop semantic models as part of interdisciplinary group projects.

---

# 🧩 Purpose of this Repository

This repository is primarily intended for **Summer School participants**.

Each participant group will use the repository to share and develop:

* Data sources relevant to their selected water-management use case
* RML mappings for transforming heterogeneous data into RDF
* Ontologies, vocabularies, and semantic models
* Generated RDF Knowledge Graphs
* SPARQL queries
* Example competency questions
* Jupyter notebooks for Knowledge Graph construction and exploration
* Intermediate and final group-project results

The repository provides a shared environment where the different groups can document their work and learn from the approaches developed by the other teams.

---

# 🗂️ Repository Structure

A suggested repository organization is:

```text
knowledge-graphs-water-management/
│
├── README.md
│
├── notebooks/
│   ├── 01_generate_knowledge_graph.ipynb
│   └── 02_run_sparql_queries.ipynb
│
├── group-01/
├── group-02/
│   └── ...
└── requirements.txt
```

Each group should maintain its own directory containing the datasets, mappings, queries, and documentation required to reproduce its Knowledge Graph.

---

# 👥 Group Workflow

During the group project, participants will progressively move from heterogeneous data sources to an integrated Knowledge Graph.

```text
Data Sources
     │
     ▼
Understand & Inspect Data
     │
     ▼
Define Semantic Model
     │
     ▼
Create RML Mappings
     │
     ▼
Generate RDF Triples
     │
     ▼
Build Knowledge Graph
     │
     ▼
Validate & Explore KG
     │
     ▼
Run SPARQL Queries
     │
     ▼
Answer Water-Management Questions
```

### 1. Select and understand the data

Identify the data sources needed for your group's water-management problem.

Possible formats may include:

```text
CSV
JSON
XML
RDF
APIs
Open Data Portals
Scientific datasets
Environmental monitoring data
```

Document the source, structure, meaning, and provenance of the data.

---

## 🗃️ 2. Share Data Sources

Each group should place or document its data sources under:

```text
group-XX/XX.csv
```

For larger datasets that should not be stored directly in GitHub, include a file containing:

* Dataset name
* Dataset description
* Source URL
* Access date
* License, where available
* Relevant variables or attributes

Example:

```text
Dataset: Wastewater Monitoring Dataset
Source: <dataset URL>
Format: CSV
Description: Measurements collected from wastewater monitoring stations.
Relevant attributes:
    - station
    - sampling date
    - pollutant
    - concentration
```

---

# 🔗 3. Create the Semantic Model

Before writing the mapping, identify the main entities and relationships represented in your data.

For example:

```text
WaterBody
   │
   ├── hasMonitoringStation → MonitoringStation
   │
   ├── hasMeasurement → Measurement
   │
   └── locatedIn → Location

Measurement
   │
   ├── measuresParameter → WaterQualityParameter
   ├── hasValue → Value
   └── observedAt → Date
```

Whenever possible, reuse existing vocabularies and ontologies instead of creating new concepts.

---

# 🧭 4. RML Mappings

The **RDF Mapping Language (RML)** is used to describe how heterogeneous source data can be transformed into RDF.

Each group should store its mappings under:

```text
groups/group-XX/mappings/
```

For example:

```text
groups/group-01/mappings/water-quality-mapping.rml.ttl
```

A simplified mapping may look like:

```turtle
@prefix rr: <http://www.w3.org/ns/r2rml#> .
@prefix rml: <http://semweb.mmlab.be/ns/rml#> .
@prefix ql: <http://semweb.mmlab.be/ns/ql#> .
@prefix ex: <http://example.org/water/> .

<#MeasurementMapping>
    rml:logicalSource [
        rml:source "data/measurements.csv" ;
        rml:referenceFormulation ql:CSV
    ] ;

    rr:subjectMap [
        rr:template "http://example.org/water/measurement/{id}" ;
        rr:class ex:Measurement
    ] ;

    rr:predicateObjectMap [
        rr:predicate ex:hasValue ;
        rr:objectMap [
            rml:reference "value"
        ]
    ] .
```

The exact mappings will depend on the structure and semantics of each group's data.

---

# 🧠 5. Generate the Knowledge Graph

A Jupyter notebook will be provided to demonstrate how to execute the mappings and generate an RDF Knowledge Graph.

The notebook will be available under:

```text
notebooks/01_generate_knowledge_graph.ipynb
```

The general workflow will be:

```text
Input Data
     +
RML Mapping
     │
     ▼
SDM-RDFizer
     │
     ▼
RDF Triples
     │
     ▼
Water Management Knowledge Graph
```

An example RDF result could look like:

```turtle
ex:measurement_001
    a ex:Measurement ;
    ex:measuresParameter ex:Nitrate ;
    ex:hasValue "4.7" ;
    ex:observedAt "2026-09-15" .
```

Generated Knowledge Graphs should be placed under:

```text
groups/group-XX/knowledge-graph/
```

---

# 🔎 6. Query the Knowledge Graph with SPARQL

After generating the Knowledge Graph, participants can use **SPARQL** to explore the integrated information.

A second Jupyter notebook will demonstrate how to load the RDF graph and execute SPARQL queries:

```text
notebooks/02_run_sparql_queries.ipynb
```

Example query:

```sparql
PREFIX ex: <http://example.org/water/>

SELECT ?measurement ?parameter ?value
WHERE {
    ?measurement a ex:Measurement ;
                 ex:measuresParameter ?parameter ;
                 ex:hasValue ?value .
}
LIMIT 20
```

---

# ❓ Competency Questions

Before writing SPARQL queries, groups are encouraged to formulate **natural-language competency questions** describing what their Knowledge Graph should be able to answer.

For example:

> Which water-quality parameters have been measured at each monitoring station?

> Which monitoring stations report pollutant concentrations above a given threshold?

> Which wastewater treatment plants are associated with particular treatment processes?

> How have measurements for a specific water-quality indicator changed over time?

These questions can subsequently be translated into SPARQL.

Each group should store its queries under:

```text
groups/group-XX/queries/
```

For example:

```text
CQ1_water_quality_parameters.sparql
CQ2_monitoring_stations.sparql
CQ3_pollution_threshold.sparql
```

---

# 📓 Jupyter Notebooks

The repository will contain introductory notebooks demonstrating the main technical workflow.

### `01_generate_knowledge_graph.ipynb`

This notebook will demonstrate how to:

* Load example source data
* Inspect the RML mapping
* Execute the mapping
* Generate RDF triples
* Save the resulting Knowledge Graph
* Inspect example triples

### `02_run_sparql_queries.ipynb`

This notebook will demonstrate how to:

* Load an RDF Knowledge Graph
* Inspect the graph
* Run SPARQL queries
* Display query results
* Experiment with new competency questions

The notebooks are intended as starting points that groups can adapt to their own datasets and mappings.

---

# 📦 Group Deliverables

By the end of the project sprint, each group should aim to provide:

```text
group-XX/
├── README.md
├── data/
├── mappings/
├── ontology/
├── knowledge-graph/
└── queries/
```

The group's `README.md` should briefly explain:

1. **Water-management challenge**
2. **Research or competency questions**
3. **Data sources**
4. **Main entities and relationships**
5. **RML mapping strategy**
6. **Generated Knowledge Graph**
7. **Example SPARQL queries**
8. **Interesting results or observations**
9. **Possible future extensions**

---

# 🎓 Learning Objectives

Through these exercises, participants will gain hands-on experience with:

* Knowledge Graph construction
* Semantic data integration
* RDF and linked data
* Ontology and vocabulary reuse
* RML mappings
* Heterogeneous environmental datasets
* SPARQL querying
* Knowledge Graph validation and exploration
* Interdisciplinary semantic modeling
* Collaborative Knowledge Graph development

The broader goal is to understand how semantic technologies can improve **interoperability and integration of complex water-related data** and support intelligent and sustainable water-management applications.

---

# 🌍 Knowledge Graphs for Water Management

Water-management information is inherently heterogeneous. Relevant information may originate from:

* Monitoring stations
* Wastewater treatment plants
* Environmental agencies
* Research datasets
* Scientific publications
* Public-health systems
* Geographic information systems
* Municipal infrastructure
* Regulatory sources
* Open-data portals

Knowledge Graphs provide a semantic layer through which these distributed resources can be represented and connected.

```text
                    Water Management
                           │
          ┌────────────────┼────────────────┐
          │                │                │
     Water Quality     Wastewater       Infrastructure
          │                │                │
          └─────────── Knowledge ───────────┘
                         Graph
                           │
              ┌────────────┼────────────┐
              │            │            │
             RDF          RML         SPARQL
```

Rather than treating individual datasets as isolated resources, the Summer School explores how they can become part of an interconnected and queryable semantic information space.

---

# 🤝 Collaboration Guidelines

This is a shared participant repository, so please:

* Work primarily inside your assigned group's directory.
* Do not modify another group's files without coordination.
* Use meaningful filenames.
* Document the source of datasets.
* Document important ontology or vocabulary choices.
* Keep RML mappings readable and commented.
* Add example SPARQL queries whenever possible.

A useful commit message could be:

```bash
git commit -m "Add RML mapping for wastewater monitoring data"
```

rather than:

```bash
git commit -m "update"
```

---

# 🚀 Getting Started

Clone the repository:

```bash
git clone <repository-url>
cd <repository-name>
```

Create a Python environment:

```bash
python -m venv .venv
```

Activate it on Linux/macOS:

```bash
source .venv/bin/activate
```

On Windows:

```bash
.venv\Scripts\activate
```

Install the required packages:

```bash
pip install -r requirements.txt
```

Start Jupyter:

```bash
jupyter notebook
```

Then open:

```text
notebooks/01_generate_knowledge_graph.ipynb
```

and follow the exercises.

---

## 🔖 Useful Resources

* **Summer School:** https://kgwm.l3s.uni-hannover.de/
* **RDF:** https://www.w3.org/RDF/
* **SPARQL:** https://www.w3.org/TR/sparql11-query/
* **RML:** https://rml.io/
* **Leibniz Data Manager:** https://service.tib.eu/ldmservice/
* **Open Research Knowledge Graph:** https://orkg.org/

---

## 📜 Acknowledgement

This repository supports the hands-on and collaborative activities of the **Knowledge Graphs for Water Management – EULiST Summer School 2026**.

The Summer School brings together researchers from environmental science, water and wastewater infrastructure management, data science, Semantic Web, and Knowledge Graph communities to explore how integrated semantic technologies can contribute to sustainable and intelligent water-management systems.
