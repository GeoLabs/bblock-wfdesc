# Workflow Description Ontology (wfdesc)

## Overview

The Workflow Description ontology (wfdesc) is part of the Wf4Ever Research Object Model. It provides a vocabulary for describing the structure of computational workflows.

## Namespace

`http://purl.org/wf4ever/wfdesc#`

## Key Classes

- **Workflow** - A directed graph of computational tasks
- **Process** - A unit of computation
- **Input** - An input parameter to a process
- **Output** - An output parameter from a process
- **Parameter** - A parameter (input or output)
- **DataLink** - Connection between outputs and inputs
- **Configuration** - A configuration parameter

## Key Properties

- `hasInput` - Process has an input parameter
- `hasOutput` - Process has an output parameter
- `hasSubProcess` - Workflow contains a sub-process
- `hasDataLink` - Workflow has data flow connection
- `hasSource` - DataLink source output
- `hasSink` - DataLink sink input

## Usage

This ontology is used to describe the prospective provenance of workflows - the structure and composition of a workflow before execution.
