---
doc-status: Draft
sequence: 6
type:
  - Preventative
mitigates:
  - tr-1
  - tr-2
title: Data quality & classification/sensitivity


- 

This document outlines a structured approach to implementing data quality and data sensitivity controls within a RAG based LLM implementation. The below controls ensure that organizations can maintain high standards of data accuracy, completeness, and freshness, while safeguarding sensitive information through robust classification.

1.Data Quality Controls
  Data Accuracy: Ensure that the data feeding into the LLM is accurate, validated, and updated regularly. This can be enforced by setting up:
   Automatic validation rules for structured data.
   Auditing mechanisms for manual data entry or unstructured data sources.
   Version control to track data changes over time.
   Within standard Langchain based Implementation above can be achieved by Retriever Filtering: 
   In LangChain, when setting up the retriever, ensure that only validated and vetted documents are pulled in. This can be done by:
   Creating a custom retriever that filters data sources based on accuracy scores or approval tags.
   Use a retrieval system like Elasticsearch or Pinecone with metadata filtering to pull documents that meet specific accuracy thresholds.
   Automated Data Validation: Implement pre-processing steps in LangChain pipelines where incoming documents are checked against validation rules (e.g., text consistency, known data patterns) before passing them 
   to the LLM.

Data Completeness: Control the completeness of datasets by monitoring for missing data, inconsistencies, and outliers. Implement alerts for incomplete or unstructured data before they are used in the LLM.
  Implement pre-processing steps in LangChain pipelines where incoming documents are checked against validation rules (e.g., text consistency, known data patterns) before passing them to the LLM.

Data Source Reliability: Define approved data sources that meet your quality standards. Ensure the retriever pulls data only from these vetted sources, with controls in place to flag data from questionable origins.  

Metadata Management: Enforce the consistent use of metadata to maintain context, timestamps, and lineage for all data used by the LLM. This ensures transparency in how the LLM processes and uses the data.
  Write a wrapper to check for predefined metadata and reject any documents without sufficient metadata.

Data Freshness: Establish automated refresh cycles and policies for each data type based on its nature and required accuracy. E.g., live financial data needs to be real-time, while other data might have a longer refresh cycle. 
 Set TTL for documents in your document store to ensure data isn’t stale. In LangChain, you can add custom logic to check if documents retrieved are up-to-date based on timestamps. 

2.Data Sensitivity & Classification Controls 
  Data Classification: Implement a strict classification system for data sensitivity, e.g., public, internal, confidential, or restricted. The LLM’s access to these data classes should be based on:
   Organizational policies.
   Business use cases.
   User access levels.
  Access Controls: Restrict access to sensitive data based on role-based access control (RBAC). Ensure the LLM cannot retrieve or generate responses from datasets classified beyond the access level of the 
  requestor.

  Encryption and Masking: For sensitive data, enforce encryption both at rest and in transit. Additionally, use data masking techniques before sensitive data can be accessed by the LLM to prevent any 
  unintentional exposure.
   When indexing documents in vector stores like Pinecone or FAISS, include sensitivity levels as metadata (e.g., public, confidential, internal). You can enforce this using LangChain’s document loaders, ensuring 
   that every document is classified and tagged.

    
  

