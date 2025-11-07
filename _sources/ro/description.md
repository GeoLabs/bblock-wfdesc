# Research Object Ontology (ro)

## Overview

The Research Object ontology (ro) provides concepts for bundling and aggregating research artifacts. It enables the packaging of workflows, data, and metadata into a single research object.

## Namespace

`http://purl.org/wf4ever/ro#`

## Key Classes

- **ResearchObject** - A bundled collection of resources
- **Resource** - Any research artifact
- **Folder** - Directory structure
- **FolderEntry** - Entry in a folder
- **AggregatedAnnotation** - Annotation about resources
- **Manifest** - Manifest describing the research object

## Key Properties

- `aggregates` - Resources in the research object
- `rootFolder` - Main folder
- `entryName` - Name of a folder entry
- `annotatesAggregatedResource` - Annotation target
- `manifest` - Manifest of the research object

## Usage

This ontology is used to package workflow descriptions, execution provenance, and data into cohesive research objects that can be shared and preserved.
