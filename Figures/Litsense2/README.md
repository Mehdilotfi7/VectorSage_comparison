# LitSense 2.0: Failure Cases for Natural-Language Queries

This note documents two practical limitations observed in LitSense 2.0 during our comparison experiments: failure to return results for some natural-language-style queries and inconsistency in returned results for the same query across attempts. LitSense 2.0 uses a two-phase retrieval design in which lexical matching is performed first and semantic reranking is applied only to the candidates retrieved in that first stage. If lexical candidate generation fails, the system returns no results.

## Why this happens

According to the LitSense 2.0 system description, sentence and passage retrieval begin with a lexical candidate-generation step, followed by semantic reranking using MedCPT. For sentence search, the system first requires 60% query-term overlap, then relaxes to 30%; for passage search, it begins at 30% and relaxes to 10%. If no items satisfy these thresholds, the system does not produce any results. 

This design improves ranking quality when suitable lexical candidates exist, but it also means that semantic matching cannot rescue a query if the initial lexical stage fails. As a result, natural-language queries that are descriptive, indirect, or phrased differently from the terminology used in titles, abstracts, or indexed passages may return no results despite being conceptually meaningful.

## Screenshot evidence

### Example 1: No results for an NLP-style query

**Query:**  
see the json file in data for quries.

**Observed behavior:**  
LitSense 2.0 returned no results.

**Screenshot:**  
![LitSense 2.0 no results for natural-language query](./Screenshot%20_1_LitSense_NCBI_NLM_NIH.png)
**Screenshot:**  
![LitSense 2.0 first run](./Screenshot%202%20LitSense%20-%20NCBI%20-%20NLM%20-%20NIH.png)

**Run B:**  
`[briefly describe changed results]`

**Screenshot:**  
![LitSense 2.0 second run](./Screenshot%203%20LitSense%20-%20NCBI%20-%20NLM%20-%20NIH.png)

**Interpretation:**  
This failure is consistent with the system architecture reported by the authors: semantic reranking is applied only after lexical candidate generation, so a query with weak lexical overlap to the indexed biomedical text can terminate before semantic evidence is used. 



## Inconsistency across repeated use

### Example 2: Same query, different outcomes

**Query:**  
`[PASTE THE EXACT QUERY USED]`

**Run A:**  
`[briefly describe results, e.g. no results / a small set of results / different top-ranked items]`

**Screenshot:**  
![LitSense 2.0 first run](./Screenshot%202%20LitSense%20-%20NCBI%20-%20NLM%20-%20NIH.png)

**Run B:**  
`[briefly describe changed results]`

**Screenshot:**  
![LitSense 2.0 second run](./Screenshot%203%20LitSense%20-%20NCBI%20-%20NLM%20-%20NIH.png)

**Interpretation:**  
When the same query yields different outcomes across attempts, this suggests instability in practical retrieval behavior. In our evaluation context, such inconsistency is problematic because a retrieval system should respond reliably to identical information needs. While the LitSense 2.0 paper reports strong benchmark performance overall, its architecture still depends on a lexical-first candidate generation stage, which can make borderline natural-language queries sensitive to phrasing, indexing differences, or retrieval thresholds. [page:1][page:2]

## Relevance to our comparison

These observations are important because our benchmark includes queries written in realistic, question-like natural language rather than optimized keyword strings. In that setting, a system that depends heavily on lexical overlap may fail even when the query clearly expresses a valid biomedical information need. Since LitSense 2.0 applies semantic reranking only after lexical filtering, its performance can remain constrained on queries whose meaning is clear semantically but whose wording does not sufficiently match the indexed text. [page:1][page:2]

## Takeaway

LitSense 2.0 is a strong biomedical retrieval system, but these screenshots illustrate an important limitation for our use case: semantic understanding is not fully independent of lexical candidate generation. Consequently, some natural-language queries may return no results, and repeated use may expose inconsistencies for the same query, especially when the query lies near the boundary of the system’s lexical matching thresholds. [page:1][page:2]
