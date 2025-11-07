# Workflow Provenance Ontology (wfprov)

## Overview

The Workflow Provenance ontology (wfprov) extends PROV-O to describe workflow execution traces. It links workflow runs to their descriptions and tracks the provenance of workflow executions.

## Namespace

`http://purl.org/wf4ever/wfprov#`

## Key Classes

- **WorkflowRun** - An execution of a workflow
- **ProcessRun** - An execution of a process
- **WorkflowEngine** - Software that executes workflows
- **Artifact** - Data entity used or generated

## Key Properties

- `wasPartOfWorkflowRun` - Links process run to workflow run
- `usedInput` - Input artifacts used
- `wasOutputFrom` - Output artifacts generated
- `describedByWorkflow` - Links run to workflow description
- `describedByProcess` - Links process run to process description
- `wasEnactedBy` - Links run to workflow engine

## Usage

This ontology is used to describe the retrospective provenance of workflows - what actually happened during execution, linking it to the workflow description (wfdesc).
