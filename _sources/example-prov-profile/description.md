# Wf4Ever Research Object and Workflow Ontologies

This building block provides access to the Wf4Ever ontologies for describing scientific workflows, their provenance, and research objects.

## Overview

The Wf4Ever (Workflow Forever) project developed a comprehensive set of ontologies for describing computational workflows and research objects. This building block integrates three core ontologies:

### 1. wfdesc - Workflow Description Ontology

The Workflow Description ontology provides a vocabulary for describing:
- Workflow structures and processes
- Workflow inputs and outputs
- Data and parameter flow
- Workflow artifacts and configurations

**Namespace**: `http://purl.org/wf4ever/wfdesc#`

### 2. wfprov - Workflow Provenance Ontology

The Workflow Provenance ontology extends PROV-O to describe:
- Workflow execution traces
- Process runs and their artifacts
- Workflow engines and their activities
- Relationships between workflow descriptions and their executions

**Namespace**: `http://purl.org/wf4ever/wfprov#`

### 3. ro - Research Object Ontology

The Research Object ontology provides concepts for:
- Bundling related resources
- Aggregating research artifacts
- Annotating resources
- Describing folder structures

**Namespace**: `http://purl.org/wf4ever/ro#`

## Purpose

These ontologies enable comprehensive semantic description of computational workflows and their execution provenance, allowing for:
- Better workflow discovery and reuse
- Provenance tracking and reproducibility
- Research object packaging and sharing
- Integration with PROV-O standard

## Key Concepts

### Workflow Description (wfdesc)

**Classes:**
- **Workflow**: A directed graph of computational tasks
- **Process**: A unit of computation
- **Input/Output**: Parameters of a process
- **DataLink**: Connection between outputs and inputs

**Properties:**
- `hasInput`, `hasOutput`: Process parameters
- `hasSubProcess`: Workflow composition
- `hasDataLink`: Data flow
- `hasSource`, `hasSink`: DataLink endpoints

### Workflow Provenance (wfprov)

**Classes:**
- **WorkflowRun**: An execution of a workflow
- **ProcessRun**: An execution of a process
- **WorkflowEngine**: Software executing workflows
- **Artifact**: Data entities used/produced

**Properties:**
- `wasPartOfWorkflowRun`: Links process runs to workflow runs
- `usedInput`: Input artifacts used
- `wasOutputFrom`: Output artifacts generated
- `describedByWorkflow`: Links execution to description
- `describedByProcess`: Links process run to process

### Research Object (ro)

**Classes:**
- **ResearchObject**: A bundled collection of resources
- **Resource**: Any research artifact
- **Folder**: Directory structure
- **FolderEntry**: Entry in a folder
- **AggregatedAnnotation**: Annotation about resources

**Properties:**
- `aggregates`: Resources in the research object
- `rootFolder`: Main folder
- `entryName`: Name of folder entry
- `annotatesAggregatedResource`: Annotation target

## Usage

This building block is designed for use with:
- **CWL (Common Workflow Language)** provenance
- Scientific workflow systems
- Research data packaging
- Reproducibility frameworks

### Example Use Case

The building block can describe a complete workflow execution including:
1. The workflow definition (wfdesc)
2. The execution trace (wfprov)
3. The packaged research object containing inputs, outputs, and provenance (ro)

See the examples section for a complete representation based on a real CWL workflow execution.
