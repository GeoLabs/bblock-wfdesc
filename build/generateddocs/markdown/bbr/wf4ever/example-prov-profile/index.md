
# Wf4Ever Research Object and Workflow Ontologies (Schema)

`ogc.bbr.wf4ever.example-prov-profile` *v1.0*

This building block provides access to the Wf4Ever ontologies for describing scientific workflows, their provenance, and research objects. It includes wfdesc (Workflow Description), wfprov (Workflow Provenance), and ro (Research Object) ontologies.

[*Status*](http://www.opengis.net/def/status): Under development

## Description

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

## Examples

### Workflow Run with Provenance (based on CWL execution)
#### json
```json
{
  "@id": "urn:uuid:f02b8997-a6b1-4909-9946-9129c2b3f10c",
  "@type": "WorkflowRun",
  "name": "Run of mangrove analysis workflow",
  "describedByWorkflow": {
    "@id": "arcp://uuid,f02b8997-a6b1-4909-9946-9129c2b3f10c/workflow/packed.cwl#main",
    "@type": ["Workflow", "Process"],
    "name": "Prospective provenance"
  },
  "wasAssociatedWith": [
    {
      "@id": "urn:uuid:5b925446-32a4-4104-9724-fa7360e1ef60",
      "@type": "WorkflowEngine",
      "name": "cwltool 3.1.20251031082601"
    }
  ],
  "usedInput": [
    {
      "@type": "Artifact",
      "@id": "urn:uuid:192e18cb-9182-4147-ad13-03076e7a3b3d",
      "name": "cloud_cover_max",
      "value": 20.0
    },
    {
      "@type": "Artifact",
      "@id": "urn:uuid:91b4ec49-d11a-4407-9685-032bf7e95258",
      "name": "days_back",
      "value": 90
    },
    {
      "@type": "Artifact",
      "@id": "urn:hash::sha1:e71003c6b7dd4093ce139ac0c51a6ba38d54a439",
      "name": "output_dir",
      "value": "outputs"
    }
  ],
  "wasOutputFrom": [
    {
      "@id": "urn:uuid:83c8708e-ccbd-494e-b939-1298b65b1539",
      "@type": ["Folder", "Artifact"],
      "name": "outputs",
      "aggregates": [
        {
          "@type": "FolderEntry",
          "entryName": "catalog.json",
          "@id": "urn:uuid:4d15cb37-a4a3-4170-a7aa-529399cb4753"
        },
        {
          "@type": "FolderEntry",
          "entryName": "mangrove-analysis-20251103-151416",
          "@id": "urn:uuid:f1477d81-2d56-4874-9d5b-eb5de2a571af",
          "aggregates": [
            {
              "@type": "FolderEntry",
              "entryName": "mangrove_mask.tif"
            },
            {
              "@type": "FolderEntry",
              "entryName": "biomass_summary.csv"
            },
            {
              "@type": "FolderEntry",
              "entryName": "carbon_summary.csv"
            },
            {
              "@type": "FolderEntry",
              "entryName": "mangrove-analysis-20251103-151416.json"
            }
          ]
        }
      ]
    }
  ]
}

```

#### jsonld
```jsonld
{
  "@context": "https://raw.githubusercontent.com/GeoLabs/bblock-wfdesc/undefined/build/annotated/bbr/wf4ever/example-prov-profile/context.jsonld",
  "@id": "urn:uuid:f02b8997-a6b1-4909-9946-9129c2b3f10c",
  "@type": "WorkflowRun",
  "name": "Run of mangrove analysis workflow",
  "describedByWorkflow": {
    "@id": "arcp://uuid,f02b8997-a6b1-4909-9946-9129c2b3f10c/workflow/packed.cwl#main",
    "@type": [
      "Workflow",
      "Process"
    ],
    "name": "Prospective provenance"
  },
  "wasAssociatedWith": [
    {
      "@id": "urn:uuid:5b925446-32a4-4104-9724-fa7360e1ef60",
      "@type": "WorkflowEngine",
      "name": "cwltool 3.1.20251031082601"
    }
  ],
  "usedInput": [
    {
      "@type": "Artifact",
      "@id": "urn:uuid:192e18cb-9182-4147-ad13-03076e7a3b3d",
      "name": "cloud_cover_max",
      "value": 20.0
    },
    {
      "@type": "Artifact",
      "@id": "urn:uuid:91b4ec49-d11a-4407-9685-032bf7e95258",
      "name": "days_back",
      "value": 90
    },
    {
      "@type": "Artifact",
      "@id": "urn:hash::sha1:e71003c6b7dd4093ce139ac0c51a6ba38d54a439",
      "name": "output_dir",
      "value": "outputs"
    }
  ],
  "wasOutputFrom": [
    {
      "@id": "urn:uuid:83c8708e-ccbd-494e-b939-1298b65b1539",
      "@type": [
        "Folder",
        "Artifact"
      ],
      "name": "outputs",
      "aggregates": [
        {
          "@type": "FolderEntry",
          "entryName": "catalog.json",
          "@id": "urn:uuid:4d15cb37-a4a3-4170-a7aa-529399cb4753"
        },
        {
          "@type": "FolderEntry",
          "entryName": "mangrove-analysis-20251103-151416",
          "@id": "urn:uuid:f1477d81-2d56-4874-9d5b-eb5de2a571af",
          "aggregates": [
            {
              "@type": "FolderEntry",
              "entryName": "mangrove_mask.tif"
            },
            {
              "@type": "FolderEntry",
              "entryName": "biomass_summary.csv"
            },
            {
              "@type": "FolderEntry",
              "entryName": "carbon_summary.csv"
            },
            {
              "@type": "FolderEntry",
              "entryName": "mangrove-analysis-20251103-151416.json"
            }
          ]
        }
      ]
    }
  ]
}
```

#### ttl
```ttl
@prefix ore: <http://www.openarchives.org/ore/terms/> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
@prefix ro: <http://purl.org/wf4ever/ro#> .
@prefix wfdesc: <http://purl.org/wf4ever/wfdesc#> .
@prefix wfprov: <http://purl.org/wf4ever/wfprov#> .

<urn:uuid:f02b8997-a6b1-4909-9946-9129c2b3f10c> a wfprov:WorkflowRun ;
    rdfs:label "Run of mangrove analysis workflow" ;
    wfprov:describedByWorkflow <arcp://uuid,f02b8997-a6b1-4909-9946-9129c2b3f10c/workflow/packed.cwl#main> ;
    wfprov:usedInput <urn:hash::sha1:e71003c6b7dd4093ce139ac0c51a6ba38d54a439>,
        <urn:uuid:192e18cb-9182-4147-ad13-03076e7a3b3d>,
        <urn:uuid:91b4ec49-d11a-4407-9685-032bf7e95258> ;
    wfprov:wasOutputFrom <urn:uuid:83c8708e-ccbd-494e-b939-1298b65b1539> .

<arcp://uuid,f02b8997-a6b1-4909-9946-9129c2b3f10c/workflow/packed.cwl#main> a wfdesc:Process,
        wfdesc:Workflow ;
    rdfs:label "Prospective provenance" .

<urn:hash::sha1:e71003c6b7dd4093ce139ac0c51a6ba38d54a439> a wfprov:Artifact ;
    rdfs:label "output_dir" .

<urn:uuid:192e18cb-9182-4147-ad13-03076e7a3b3d> a wfprov:Artifact ;
    rdfs:label "cloud_cover_max" .

<urn:uuid:4d15cb37-a4a3-4170-a7aa-529399cb4753> a ro:FolderEntry ;
    ro:entryName "catalog.json" .

<urn:uuid:83c8708e-ccbd-494e-b939-1298b65b1539> a ro:Folder,
        wfprov:Artifact ;
    rdfs:label "outputs" ;
    ore:aggregates <urn:uuid:4d15cb37-a4a3-4170-a7aa-529399cb4753>,
        <urn:uuid:f1477d81-2d56-4874-9d5b-eb5de2a571af> .

<urn:uuid:91b4ec49-d11a-4407-9685-032bf7e95258> a wfprov:Artifact ;
    rdfs:label "days_back" .

<urn:uuid:f1477d81-2d56-4874-9d5b-eb5de2a571af> a ro:FolderEntry ;
    ro:entryName "mangrove-analysis-20251103-151416" ;
    ore:aggregates [ a ro:FolderEntry ;
            ro:entryName "mangrove_mask.tif" ],
        [ a ro:FolderEntry ;
            ro:entryName "carbon_summary.csv" ],
        [ a ro:FolderEntry ;
            ro:entryName "biomass_summary.csv" ],
        [ a ro:FolderEntry ;
            ro:entryName "mangrove-analysis-20251103-151416.json" ] .


```


### Simple Workflow Description
#### json
```json
{
  "@type": "Workflow",
  "@id": "http://example.org/workflow/my-analysis",
  "name": "Data Analysis Workflow",
  "description": "A simple workflow for data analysis",
  "hasInput": [
    {
      "@type": "Input",
      "@id": "http://example.org/workflow/my-analysis/input/data",
      "name": "input-data"
    }
  ],
  "hasOutput": [
    {
      "@type": "Output",
      "@id": "http://example.org/workflow/my-analysis/output/result",
      "name": "analysis-result"
    }
  ],
  "hasSubProcess": [
    {
      "@type": "Process",
      "@id": "http://example.org/workflow/my-analysis/process/transform",
      "name": "Data Transformation",
      "hasInput": [
        {
          "@type": "Input",
          "@id": "http://example.org/workflow/my-analysis/process/transform/input",
          "name": "raw-data"
        }
      ],
      "hasOutput": [
        {
          "@type": "Output",
          "@id": "http://example.org/workflow/my-analysis/process/transform/output",
          "name": "transformed-data"
        }
      ]
    }
  ],
  "hasDataLink": [
    {
      "@type": "DataLink",
      "hasSource": {
        "@id": "http://example.org/workflow/my-analysis/input/data"
      },
      "hasSink": {
        "@id": "http://example.org/workflow/my-analysis/process/transform/input"
      }
    }
  ]
}

```

#### jsonld
```jsonld
{
  "@context": "https://raw.githubusercontent.com/GeoLabs/bblock-wfdesc/undefined/build/annotated/bbr/wf4ever/example-prov-profile/context.jsonld",
  "@type": "Workflow",
  "@id": "http://example.org/workflow/my-analysis",
  "name": "Data Analysis Workflow",
  "description": "A simple workflow for data analysis",
  "hasInput": [
    {
      "@type": "Input",
      "@id": "http://example.org/workflow/my-analysis/input/data",
      "name": "input-data"
    }
  ],
  "hasOutput": [
    {
      "@type": "Output",
      "@id": "http://example.org/workflow/my-analysis/output/result",
      "name": "analysis-result"
    }
  ],
  "hasSubProcess": [
    {
      "@type": "Process",
      "@id": "http://example.org/workflow/my-analysis/process/transform",
      "name": "Data Transformation",
      "hasInput": [
        {
          "@type": "Input",
          "@id": "http://example.org/workflow/my-analysis/process/transform/input",
          "name": "raw-data"
        }
      ],
      "hasOutput": [
        {
          "@type": "Output",
          "@id": "http://example.org/workflow/my-analysis/process/transform/output",
          "name": "transformed-data"
        }
      ]
    }
  ],
  "hasDataLink": [
    {
      "@type": "DataLink",
      "hasSource": {
        "@id": "http://example.org/workflow/my-analysis/input/data"
      },
      "hasSink": {
        "@id": "http://example.org/workflow/my-analysis/process/transform/input"
      }
    }
  ]
}
```

#### ttl
```ttl
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
@prefix wfdesc: <http://purl.org/wf4ever/wfdesc#> .

<http://example.org/workflow/my-analysis> a wfdesc:Workflow ;
    rdfs:label "Data Analysis Workflow" ;
    wfdesc:hasDataLink [ a wfdesc:DataLink ;
            wfdesc:hasSink <http://example.org/workflow/my-analysis/process/transform/input> ;
            wfdesc:hasSource <http://example.org/workflow/my-analysis/input/data> ] ;
    wfdesc:hasInput <http://example.org/workflow/my-analysis/input/data> ;
    wfdesc:hasOutput <http://example.org/workflow/my-analysis/output/result> ;
    wfdesc:hasSubProcess <http://example.org/workflow/my-analysis/process/transform> ;
    rdfs:comment "A simple workflow for data analysis" .

<http://example.org/workflow/my-analysis/output/result> a wfdesc:Output ;
    rdfs:label "analysis-result" .

<http://example.org/workflow/my-analysis/process/transform> a wfdesc:Process ;
    rdfs:label "Data Transformation" ;
    wfdesc:hasInput <http://example.org/workflow/my-analysis/process/transform/input> ;
    wfdesc:hasOutput <http://example.org/workflow/my-analysis/process/transform/output> .

<http://example.org/workflow/my-analysis/process/transform/output> a wfdesc:Output ;
    rdfs:label "transformed-data" .

<http://example.org/workflow/my-analysis/input/data> a wfdesc:Input ;
    rdfs:label "input-data" .

<http://example.org/workflow/my-analysis/process/transform/input> a wfdesc:Input ;
    rdfs:label "raw-data" .


```

## Schema

```yaml
$schema: https://json-schema.org/draft/2020-12/schema
description: Workflow Description, Provenance and Research Object schema based on
  wfdesc, wfprov and ro ontologies
type: object
properties:
  '@type':
    oneOf:
    - type: string
      enum:
      - Workflow
      - Process
      - Input
      - Output
      - Parameter
      - DataLink
      - Configuration
      - WorkflowRun
      - ProcessRun
      - WorkflowEngine
      - Artifact
      - ResearchObject
      - Resource
      - Folder
      - FolderEntry
      - AggregatedAnnotation
      - Manifest
    - type: array
      items:
        type: string
  name:
    type: string
    description: Name of the workflow, process, or resource
    x-jsonld-id: http://www.w3.org/2000/01/rdf-schema#label
  description:
    type: string
    description: Description of the workflow, process, or resource
    x-jsonld-id: http://www.w3.org/2000/01/rdf-schema#comment
  value:
    description: Value of an artifact or parameter
  hasInput:
    type: array
    items:
      type: object
    x-jsonld-id: http://purl.org/wf4ever/wfdesc#hasInput
    x-jsonld-type: '@id'
  hasOutput:
    type: array
    items:
      type: object
    x-jsonld-id: http://purl.org/wf4ever/wfdesc#hasOutput
    x-jsonld-type: '@id'
  hasSubProcess:
    type: array
    items:
      type: object
      description: Sub-processes within the workflow
    x-jsonld-id: http://purl.org/wf4ever/wfdesc#hasSubProcess
    x-jsonld-type: '@id'
  hasDataLink:
    type: array
    items:
      type: object
    x-jsonld-id: http://purl.org/wf4ever/wfdesc#hasDataLink
    x-jsonld-type: '@id'
  hasSource:
    type: object
    description: Source output of a data link
    x-jsonld-id: http://purl.org/wf4ever/wfdesc#hasSource
    x-jsonld-type: '@id'
  hasSink:
    type: object
    description: Sink input of a data link
    x-jsonld-id: http://purl.org/wf4ever/wfdesc#hasSink
    x-jsonld-type: '@id'
  describedByWorkflow:
    type: object
    description: Links a workflow run to its description
    x-jsonld-id: http://purl.org/wf4ever/wfprov#describedByWorkflow
    x-jsonld-type: '@id'
  describedByProcess:
    type: object
    description: Links a process run to its description
    x-jsonld-id: http://purl.org/wf4ever/wfprov#describedByProcess
    x-jsonld-type: '@id'
  wasPartOfWorkflowRun:
    type: object
    description: Links a process run to the workflow run
    x-jsonld-id: http://purl.org/wf4ever/wfprov#wasPartOfWorkflowRun
    x-jsonld-type: '@id'
  usedInput:
    type: array
    items:
      type: object
    description: Input artifacts used by a process run
    x-jsonld-id: http://purl.org/wf4ever/wfprov#usedInput
    x-jsonld-type: '@id'
  wasOutputFrom:
    type: array
    items:
      type: object
    description: Output artifacts generated
    x-jsonld-id: http://purl.org/wf4ever/wfprov#wasOutputFrom
    x-jsonld-type: '@id'
  wasAssociatedWith:
    type: array
    items:
      type: object
    description: Agents associated with the execution
  wasEnactedBy:
    type: object
    description: Workflow engine that executed the run
  aggregates:
    type: array
    items:
      type: object
    description: Resources aggregated in a research object or folder
    x-jsonld-id: http://www.openarchives.org/ore/terms/aggregates
    x-jsonld-type: '@id'
  rootFolder:
    type: object
    description: Root folder of a research object
    x-jsonld-id: http://purl.org/wf4ever/ro#rootFolder
    x-jsonld-type: '@id'
  entryName:
    type: string
    description: Name of a folder entry
    x-jsonld-id: http://purl.org/wf4ever/ro#entryName
  annotatesAggregatedResource:
    type: object
    description: Resource being annotated
    x-jsonld-id: http://purl.org/wf4ever/ro#annotatesAggregatedResource
    x-jsonld-type: '@id'
  manifest:
    type: object
    description: Manifest of a research object
  isDescribedBy:
    type: object
    description: Description of a resource
    x-jsonld-id: http://www.openarchives.org/ore/terms/isDescribedBy
    x-jsonld-type: '@id'
x-jsonld-extra-terms:
  Workflow: http://purl.org/wf4ever/wfdesc#Workflow
  Process: http://purl.org/wf4ever/wfdesc#Process
  WorkflowInstance: http://purl.org/wf4ever/wfdesc#WorkflowInstance
  Input: http://purl.org/wf4ever/wfdesc#Input
  Output: http://purl.org/wf4ever/wfdesc#Output
  Parameter: http://purl.org/wf4ever/wfdesc#Parameter
  DataLink: http://purl.org/wf4ever/wfdesc#DataLink
  Artifact: http://purl.org/wf4ever/wfprov#Artifact
  Configuration: http://purl.org/wf4ever/wfdesc#Configuration
  WorkflowEngine: http://purl.org/wf4ever/wfprov#WorkflowEngine
  WorkflowRun: http://purl.org/wf4ever/wfprov#WorkflowRun
  ProcessRun: http://purl.org/wf4ever/wfprov#ProcessRun
  ResearchObject: http://purl.org/wf4ever/ro#ResearchObject
  Resource: http://purl.org/wf4ever/ro#Resource
  AggregatedAnnotation: http://purl.org/wf4ever/ro#AggregatedAnnotation
  Folder: http://purl.org/wf4ever/ro#Folder
  FolderEntry: http://purl.org/wf4ever/ro#FolderEntry
x-jsonld-prefixes:
  wfdesc: http://purl.org/wf4ever/wfdesc#
  wfprov: http://purl.org/wf4ever/wfprov#
  ro: http://purl.org/wf4ever/ro#
  rdfs: http://www.w3.org/2000/01/rdf-schema#
  ore: http://www.openarchives.org/ore/terms/
  prov: http://www.w3.org/ns/prov#
  cwlprov: https://w3id.org/cwl/prov#

```

Links to the schema:

* YAML version: [schema.yaml](https://raw.githubusercontent.com/GeoLabs/bblock-wfdesc/undefined/build/annotated/bbr/wf4ever/example-prov-profile/schema.json)
* JSON version: [schema.json](https://raw.githubusercontent.com/GeoLabs/bblock-wfdesc/undefined/build/annotated/bbr/wf4ever/example-prov-profile/schema.yaml)


# JSON-LD Context

```jsonld
{
  "@context": {
    "Workflow": "wfdesc:Workflow",
    "Process": "wfdesc:Process",
    "WorkflowInstance": "wfdesc:WorkflowInstance",
    "Input": "wfdesc:Input",
    "Output": "wfdesc:Output",
    "Parameter": "wfdesc:Parameter",
    "DataLink": "wfdesc:DataLink",
    "Artifact": "wfprov:Artifact",
    "Configuration": "wfdesc:Configuration",
    "WorkflowEngine": "wfprov:WorkflowEngine",
    "WorkflowRun": "wfprov:WorkflowRun",
    "ProcessRun": "wfprov:ProcessRun",
    "ResearchObject": "ro:ResearchObject",
    "Resource": "ro:Resource",
    "AggregatedAnnotation": "ro:AggregatedAnnotation",
    "Folder": "ro:Folder",
    "FolderEntry": "ro:FolderEntry",
    "name": "rdfs:label",
    "description": "rdfs:comment",
    "hasInput": {
      "@id": "wfdesc:hasInput",
      "@type": "@id"
    },
    "hasOutput": {
      "@id": "wfdesc:hasOutput",
      "@type": "@id"
    },
    "hasSubProcess": {
      "@id": "wfdesc:hasSubProcess",
      "@type": "@id"
    },
    "hasDataLink": {
      "@id": "wfdesc:hasDataLink",
      "@type": "@id"
    },
    "hasSource": {
      "@id": "wfdesc:hasSource",
      "@type": "@id"
    },
    "hasSink": {
      "@id": "wfdesc:hasSink",
      "@type": "@id"
    },
    "describedByWorkflow": {
      "@id": "wfprov:describedByWorkflow",
      "@type": "@id"
    },
    "describedByProcess": {
      "@id": "wfprov:describedByProcess",
      "@type": "@id"
    },
    "wasPartOfWorkflowRun": {
      "@id": "wfprov:wasPartOfWorkflowRun",
      "@type": "@id"
    },
    "usedInput": {
      "@id": "wfprov:usedInput",
      "@type": "@id"
    },
    "wasOutputFrom": {
      "@id": "wfprov:wasOutputFrom",
      "@type": "@id"
    },
    "aggregates": {
      "@id": "ore:aggregates",
      "@type": "@id"
    },
    "rootFolder": {
      "@id": "ro:rootFolder",
      "@type": "@id"
    },
    "entryName": "ro:entryName",
    "annotatesAggregatedResource": {
      "@id": "ro:annotatesAggregatedResource",
      "@type": "@id"
    },
    "isDescribedBy": {
      "@id": "ore:isDescribedBy",
      "@type": "@id"
    },
    "wfdesc": "http://purl.org/wf4ever/wfdesc#",
    "wfprov": "http://purl.org/wf4ever/wfprov#",
    "ro": "http://purl.org/wf4ever/ro#",
    "rdfs": "http://www.w3.org/2000/01/rdf-schema#",
    "ore": "http://www.openarchives.org/ore/terms/",
    "prov": "http://www.w3.org/ns/prov#",
    "cwlprov": "https://w3id.org/cwl/prov#",
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://raw.githubusercontent.com/GeoLabs/bblock-wfdesc/undefined/build/annotated/bbr/wf4ever/example-prov-profile/context.jsonld)

## Sources

* [Wf4Ever Workflow Description Ontology](http://purl.org/wf4ever/wfdesc)
* [Wf4Ever Workflow Provenance Ontology](http://purl.org/wf4ever/wfprov)
* [Wf4Ever Research Object Ontology](http://purl.org/wf4ever/ro)
* [Wf4Ever Research Object Model](https://w3id.org/ro/)

# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/GeoLabs/bblock-wfdesc](https://github.com/GeoLabs/bblock-wfdesc)
* Path: `_sources/example-prov-profile`

