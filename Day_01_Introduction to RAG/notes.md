**RAG: Retrieval-Augmented Generation for Knowledge-Intensive NLP**
-------------------------------------------------------------------

This 2020 paper by Lewis et al. from Facebook AI Research introduces **RAG (Retrieval-Augmented Generation)**, a hybrid approach that combines pre-trained language models with external knowledge retrieval to improve performance on knowledge-intensive NLP tasks.

### **Core Innovation**

RAG merges two types of memory:

*   **Parametric memory**: A pre-trained seq2seq model (BART-large, 400M parameters) that stores knowledge in its weights
    
*   **Non-parametric memory**: A dense vector index of Wikipedia (21M document chunks) accessed via a neural retriever (DPR)
    

### **How It Works**

1.  Given an input query, RAG uses a bi-encoder retriever to find the top-K most relevant Wikipedia passages
    
2.  The generator (BART) conditions on both the input and retrieved documents to produce outputs
    
3.  Two variants are proposed:
    
    *   **RAG-Sequence**: Uses the same retrieved documents for the entire output sequence
        
    *   **RAG-Token**: Can use different documents for each output token
        

The system is trained end-to-end without requiring supervision on which documents to retrieve.

### **Key Results**
**Open-Domain QA**: RAG achieved state-of-the-art results on Natural Questions, TriviaQA, WebQuestions, and CuratedTrec, outperforming both pure parametric models (T5) and extractive approaches.

**Generation Quality**: Compared to BART baseline, RAG produces responses that are:

*   More factual (42.7% vs 7.1% in human evaluations)
    
*   More specific (37.4% vs 16.8%)
    
*   More diverse (higher n-gram diversity without special decoding)
    

**Additional Tasks**: Strong performance on MS-MARCO abstractive QA, Jeopardy question generation, and FEVER fact verification (within 4.3% of state-of-the-art despite not using retrieval supervision).

### **Advantages**

*   **Updateable knowledge**: Can swap the Wikipedia index to update the model's knowledge without retraining
    
*   **Interpretability**: Retrieved documents provide provenance for model decisions
    
*   **Efficiency**: Fewer parameters needed compared to purely parametric models for similar performance
    
*   **Reduced hallucination**: Grounding in retrieved documents leads to more factual outputs
    

This paper laid foundational work for modern retrieval-augmented systems and demonstrated that combining parametric and non-parametric memory is highly effective for knowledge-intensive tasks.