# Related papers for idea/proposition/graph retrieval architecture

Compiled on 2026-03-18.

## Core papers

### RAPTOR: Recursive Abstractive Processing for Tree-Organized Retrieval
- URL: https://arxiv.org/abs/2401.18059
- Takeaway: Builds a hierarchy by recursively embedding, clustering, and summarizing chunks; retrieves at different abstraction levels.
- Relevance: Very close to the proposed recurse / re-cluster / re-link idea. Strong evidence that hierarchical abstraction can help on long-document, complex QA.
- Risk signal: Gains depend on summary quality; abstraction can wash out detail.

### From Local to Global: A Graph RAG Approach to Query-Focused Summarization
- URL: https://arxiv.org/abs/2404.16130
- Takeaway: Builds an entity graph and community summaries, then answers global corpus-level questions by summarizing over community responses.
- Relevance: Strong precedent for higher-level corpus-specific representations helping global/thematic queries.
- Risk signal: Primarily aimed at query-focused summarization over corpora, not exact evidence retrieval.

### PropRAG: Guiding Retrieval with Beam Search over Proposition Paths
- URL: https://arxiv.org/abs/2504.18070
- Takeaway: Argues triples lose too much context; uses context-rich propositions plus proposition-path search for multi-hop retrieval.
- Relevance: This is the closest direct analogue to “retrieve ideas, then expand through relationships.”
- Risk signal: Suggests richer-than-triples units matter, but still requires careful path control to avoid drift.

### Atomic Fact Decomposition Helps Attributed Question Answering
- URL: https://arxiv.org/abs/2410.16708
- Takeaway: Decomposes generated answers into molecular clauses and atomic facts, retrieves evidence per fact, verifies and edits.
- Relevance: Strong evidence that atomic/molecular decomposition helps attribution and evidence localization.
- Risk signal: Shows decomposition is useful, but mainly in answer verification/editing; does not prove corpus indexing should be built around extracted facts.

### Molecular Facts: Desiderata for Decontextualization in LLM Fact Verification
- URL: https://arxiv.org/abs/2406.20079
- Takeaway: Purely atomic facts often lose critical context; proposes “molecular facts” balancing minimality and decontextuality.
- Relevance: Important warning for any “idea extraction” pipeline: too-atomic representations lose meaning.
- Risk signal: Directly supports the concern that idea extraction can destroy qualifiers and context.

## Landscape / survey / cautionary papers

### Retrieval-Augmented Generation with Graphs (GraphRAG survey)
- URL: https://arxiv.org/abs/2501.00309
- Takeaway: Surveys GraphRAG design space across query processing, retrievers, organizers, generators, and graph data sources.
- Relevance: Useful for positioning the proposed architecture as a GraphRAG-adjacent system rather than a wholly new paradigm.

### GraphRAG under Fire
- URL: https://arxiv.org/abs/2501.14050
- Takeaway: GraphRAG can resist some conventional poisoning attacks better than vanilla RAG, but graph structure creates new attack surfaces.
- Relevance: Useful reminder that higher-order graph structure changes failure modes rather than simply improving retrieval.

## Other relevant threads spotted during search
- Document-level Claim Extraction and Decontextualisation for Fact-Checking — https://arxiv.org/abs/2406.03239
  - Extracting claims and rewriting them to stand alone improved downstream retrieval.
- Tree of Reviews: A Tree-based Dynamic Iterative Retrieval Framework for Multi-hop QA — https://arxiv.org/abs/2404.14464
  - Iterative retrieval structure for multi-hop questions.
- Complex Answer Retrieval (older IR line) — https://arxiv.org/abs/1811.08772
  - Relevant historical precedent: complex questions need multiple nuanced facets, not just one matching chunk.

## Working synthesis
- The proposed architecture is not novel in kind.
- The strongest adjacent evidence comes from:
  1. RAPTOR (hierarchical abstraction)
  2. GraphRAG (graph/community representation)
  3. PropRAG (proposition-level nodes + path search)
  4. atomic/molecular fact work (granularity and decontextualization tradeoffs)
- The key unresolved question is still fidelity: can extracted “ideas” remain grounded enough to support exact evidence retrieval, not just thematic recall?
