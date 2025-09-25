**HealthCare GraphRAG with Neo4j**

This project implements Graph Retrieval-Augmented Generation (GraphRAG) using LLMs and Neo4j on biomedical data. The system builds a heterogeneous biomedical knowledge graph (Drugs, Diseases, Proteins), embeds nodes into vectors, and enables natural language querying via Cypher query generation.

**Dataset**

The project uses four input files:

drugs.json → Metadata for drug nodes (DRUG)

diseases.json → Metadata for disease nodes (DISEASE)

proteins.json → Metadata for protein nodes (PROTEIN)

associations.csv → Relationships (edges) between nodes

 Non-DRUG/PROTEIN/DISEASE entities in the associations file are pruned.

**Implementation Steps**
**1. Graph Construction (Neo4j)**

Create directed heterogeneous graph in Neo4j.

Insert nodes from JSON files and edges from associations.

Prune invalid nodes/edges with missing metadata.

Report total node/edge count using Cypher queries.

2. Node Embeddings & Vector Database

Embed node metadata using Sentence Transformers or equivalent embedding models.

Store embeddings + documents in a vector DB .

Validate by querying with semantic similarity search.

**3. GraphRAG Pipeline**

Implements an agentic RAG system:

Entity Extraction → Extract relevant entities from user query.

Entity Matching → Retrieve candidates from vector DB and use LLM as judge.

Cypher Query Generation → Form graph queries based on matched entities.

Context Retrieval → Execute Cypher queries on Neo4j graph.

Answer Generation → LLM synthesizes final answer grounded on graph context.

**4. Edge Cases**

Non-KG related queries → handled gracefully without graph lookup.

Missing entities or failed lookups → provide fallback responses.

**Example Queries**

One-hop traversal: "Which diseases are treated by Drug X?"

Multi-hop traversal: "Find proteins targeted by drugs that treat Disease Y."

Metadata lookup: "Give me details about Protein Z."
