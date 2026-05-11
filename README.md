# pgvector-semantic-search-postgresql
Beginner-friendly PostgreSQL pgvector VECTOR(1536) setup guide for fixing SQL State 42704 and building semantic search/RAG systems.
# PostgreSQL pgvector VECTOR(1536) Setup Guide

A beginner-friendly production guide for fixing:

ERROR: type "vector" does not exist  
(SQL State 42704)

while building semantic search and RAG systems using PostgreSQL + pgvector.

---

## Why This Error Happens

PostgreSQL does not natively understand vector data types.

When developers attempt to create:

```sql
embedding VECTOR(1536)
```

without enabling pgvector inside the target database, PostgreSQL throws:

```text
ERROR: type "vector" does not exist
SQL State: 42704
```

---

## Step 1 — Enable pgvector

```sql
CREATE EXTENSION IF NOT EXISTS vector;
```

---

## Step 2 — Create VECTOR(1536) Table

```sql
CREATE TABLE documents (
    id SERIAL PRIMARY KEY,
    content TEXT,
    embedding VECTOR(1536)
);
```

---

## Step 3 — Create HNSW Index

```sql
CREATE INDEX ON documents
USING hnsw (embedding vector_cosine_ops);
```

---

## Technologies

- PostgreSQL
- pgvector
- OpenAI Embeddings
- Semantic Search
- RAG Architecture

---

## Full Tutorial

https://aicodewithharitha.com/create-vector-search-table-fix-vector-does-not-exist/
