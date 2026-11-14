# Rag-Projects-V1
This repo contains all RAG based project that is used for practicing.

The rag chuncking stratigies:
1. Fixed-Size Chunking
2. Fixed-Size with Overlap
3. Sentence-Based Chunking
4. Paragraph-Based Chunking
5. Semantic Chunking - (Chucking based on meaning needs embedding model) 
6. Recursive Chunking - (Chuncking priority wise eg- "\n\n" "\n" "." "," " "  The chunking gives pripority from left to right)
7. Document Structure-Based Chunking(The doc is chuncked into header topic sub-topic)
8. Parent-Child Chunking (Here The chucks is furthur divided into childs so that the context is taken from parents while the actual chucnck that is retrieved is the child.)

Common measures for embedding:
1.Cosine similarity
2.Euclidian Distance
3.Dot Product


Search Stratigies:
1.Similarity Search

    Most basic.

    Query -> Embedding -> Nearest Chunks 

2.Keyword Search

    BM25

    Looks for exact terms.

    Example:

    Error 0x80070005

    Often better than semantic search.

3.Hybrid Search

    Combines:

    Vector Search + Keyword Search

    Most production systems use this.

Re-ranking chuncks:
    Top retrieved chuncks are not alwasys the best so we need to re-rank these chuncks. And also we select the top few chucnks from the re-ranked chuncks.

    eg-
        Retrieve 20 chunks -> Re-ranker model ->  Choose best 5

Metadata Filtering:
    We can also keep meta data of document for fast search.

    eg- if a query is asking for HR policy then document having meta data HR is fetched.

Sample prompt for rag:

    You are a helpful assistant.

    Use only the provided context.

    If the answer is not found,
    say "I don't know."

    Context:
    {context}

    Question:
    {question}
       
       
Possible reasons for hallucination in rag systems:
    -Bad Retrieval
    -Missing Data
    -Bad Prompt
    -Chunking Errors

Advanced RAG patterns:

    1.Parent-Child Retrieval 

        Parent Chunk
            ↓
        Small Child Chunks

        -Retrieve child.
        -Send parent.

        Best of both worlds.

    2.Multi-Query RAG

        Create multiple versions of query.

        Example:

        Q-> How do I install Python?

        Generated:

            Python installation
            Setup Python
            Install CPython

        Search all.

        Merge results.

    3.HyDE (Hypothetical Document Embeddings)

        Question
        ↓
        LLM creates fake answer
        ↓
        Embed fake answer
        ↓
        Search with that

        
        Often improves retrieval.


    4.Agentic RAG

        Agent decides:

            Search?
            Search again?
            Use database?
            Use web?
            Summarize?

        Flow:

            Question
            ↓
            Agent
            ↓
            Multiple Retrieval Steps
            ↓
            Answer

Evaluation of RAG:

    There are 7 metrics
    
    Retrieval Metrics
        -Recall
        -Precision
        -MRR
        -Hit Rate
    Generation Metrics
        -Faithfulness
        -Relevance
        -Answer Correctness

    Frameworks:

        -RAGAS
        -DeepEval
        -TruLens
        -LangSmith


Sample Enterprise Level RAG Architecture:

    PDFs
    Websites
    Database
    SharePoint
    Confluence
        ↓
    Document Pipeline
        ↓
    Chunking
        ↓
    Embeddings
        ↓
    Qdrant
        ↓
    Retriever
        ↓
    Re-ranking
        ↓
    Prompt Builder
        ↓
    GPT-4
        ↓
    Answer + Citations