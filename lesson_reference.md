# Introduction to RAG (Retrieval-Augmented Generation)

## 1. What is RAG?

RAG stands for **Retrieval-Augmented Generation**. It is a way to help an AI answer questions using information found in selected documents.

Think of an open-book exam. In a closed-book exam, you answer only from what you remember. In an open-book exam, you first look up the relevant page and then write your answer. RAG works in a similar way:

1. The user asks a question.
2. The system searches useful information from its documents.
3. It gives that information to an AI language model.
4. The model writes an answer using the question and the retrieved information.

**Retrieval** means finding useful information. **Generation** means creating a response. **Augmented** means improved or supported with extra information.

RAG does not automatically make every answer correct. The documents may be incomplete, outdated, or wrong, and the AI may still misunderstand them.

## 2. Why do we need RAG?

An AI language model learns patterns from data during training. It may not know a company's latest leave policy, a new product manual, or a document uploaded yesterday.

RAG helps by finding relevant information at question time. This can:
- Give answers based on a chosen set of documents.
- Make private or recently updated information available to the model without retraining it.
- Help users find information in long files.
- Make answers easier to check when the system shows the source passages.

For example, a college may have hundreds of pages of rules. A student should be able to ask, "What is the attendance requirement?" and receive an answer based on the college handbook.

## 3. How does RAG work?

A common RAG system has two stages.

### Stage A: Prepare the documents

1. **Collect documents:** Add trusted files such as PDFs, guides, or policy pages.
2. **Split into chunks:** Break long documents into smaller sections. A chunk is one small piece of text. Smaller pieces are easier to search.
3. **Create embeddings:** An embedding is a list of numbers that represents the meaning of a piece of text. Text with similar meaning often has embeddings that are close to each other.
4. **Store for search:** Save the chunks and their embeddings in a vector database. This is a database designed to find items with similar meanings.

### Stage B: Answer a question

1. **Receive the question:** The user asks something in normal language.
2. **Find relevant chunks:** The system turns the question into an embedding and searches for document chunks with similar meaning. This step is called retrieval.
3. **Build the context:** The system places the best matching text passages alongside the user's question.
4. **Generate the answer:** The language model reads the question and retrieved passages and writes a helpful response.
5. **Show sources when possible:** The application can show which document passages were used, so the user can verify the answer.

## 4. A simple example

Imagine a student asks a college-help chatbot:

**Question:** "How many days can I take leave?"

The college handbook contains this sentence:

"Students may take up to 10 days of casual leave in one academic year, subject to approval."

Here is what RAG does:

- It searches the handbook and finds the sentence about casual leave.
- It sends that sentence and the student's question to the AI.
- The AI answers: "You may take up to 10 days of casual leave in one academic year, but approval is required."
- The chatbot can show the handbook as the source.

The answer is useful because it is based on the college's document, not just a general guess by the AI.

## 5. Important terms

- **Language model:** An AI program that understands and generates text.
- **Chunk:** A small section of a larger document.
- **Embedding:** A number-based representation of text meaning.
- **Vector database:** A system that stores embeddings and searches for similar ones.
- **Retrieval:** Finding useful information from stored documents.
- **Context:** The information provided to the AI to help it answer.
- **Hallucination:** When an AI gives an answer that sounds confident but is false or unsupported.

## 6. Benefits and limitations

### Benefits
- Uses information from selected documents.
- Can work with new documents without training the language model again.
- Helps answer questions about long collections of text.
- Can provide source passages for checking.

### Limitations
- If the right information is missing, retrieval may find the wrong passage or nothing useful.
- Poorly split documents can hide important meaning.
- Incorrect source documents can lead to incorrect answers.
- RAG reduces some unsupported answers, but it does not guarantee truth.
- The system needs good access controls so users only retrieve documents they are allowed to see.

## 7. When is RAG useful?

RAG is useful when an AI application must answer questions using a changing or specific collection of information. Examples include:
- A company assistant that answers questions from HR policies.
- A customer-support assistant that searches product manuals.
- A college assistant that explains information from student handbooks.
- A research assistant that searches a collection of papers.

## 8. Quick recap

RAG means **Retrieval-Augmented Generation**. It first finds useful information from documents and then gives that information to an AI model to help create an answer.

Remember the simple flow:

**Question → Search documents → Retrieve useful text → Give text to AI → Generate answer**

RAG can make answers more relevant to selected information, but people should still check important answers and their sources.
