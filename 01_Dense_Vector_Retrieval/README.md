<p align = "center" draggable="false" ><img src="https://github.com/AI-Maker-Space/LLM-Dev-101/assets/37101144/d1343317-fa2f-41e1-8af1-1dbb18399719"
     width="200px"
     height="auto"/>
</p>

<h1 align="center" id="heading">Session 1: Dense Vector Retrieval</h1>

### [Quicklinks]()

| 📰 Module Sheet                                                                 | ⏺️ Recording | 🖼️ Slides | 👨‍💻 Repo       | 📝 Homework | 📁 Feedback |
| :------------------------------------------------------------------------------- | :----------- | :-------- | :------------ | :---------- | :---------- |
| [Dense Vector Retrieval](../00_Docs/Modules/01_Dense_Vector_Retrieval/README.md) |[Recording!](https://us02web.zoom.us/rec/share/sHWvo0Nd1aI0SEhKecOLEX9kFGVJJAdYfsKiuTmm8t85W48Z2lnjpnzTy8jAd8R5.PwuqibGwAZhvDd8c) <br> passcode: `C62n^@Q!`| [Session 1 Slides](https://canva.link/htfqf8i39yejyhn) | You are here! | [Session 1 Assignment](https://forms.gle/Z9qskfVaAvPjn6gz8) | [Feedback 6/2](https://forms.gle/21a2uoL9DVZPwgJP6) |


## 🏗️ How AIM Does Assignments

> 📅 **Assignments will always be released to students as live class begins.** We will never release assignments early.

Each assignment will have a few of the following categories of exercises:

- ❓ **Questions** - these will be questions that you will be expected to gather the answer to. These can appear as general questions, or questions meant to spark a discussion in your breakout rooms.

- 🏗️ **Activities** - these will be work or coding activities meant to reinforce specific concepts or theory components.

- 🚧 **Advanced Builds (optional)** - Take on a challenge. These builds require you to create something with minimal guidance outside of the documentation.

## Main Assignment

In this assignment, you will build a vector RAG application using LangChain v1, OpenAI embeddings, and Qdrant.

The main notebook is:

```text
01_Cat_Health_Vector_RAG_LangChain_Qdrant.ipynb
```

The notebook uses the bundled cat health guideline PDF in `data/cat_health_guidelines.pdf`.

### Setup

From this folder, install the environment with uv:

```bash
uv sync
```

Then open the notebook in Cursor or VS Code and select the Python/Jupyter environment created by uv.

You will also need an OpenAI API key available when running the notebook.

---

## 🏗️ Activity #1: Embedding Similarity

Run the embedding similarity primer in the notebook.

You will compare embeddings for terms like:

- `king`
- `queen`
- `banana`
- `cat`
- `veterinarian`
- `cat health guidelines`

#### ❓Question #1

Why is cosine similarity useful for dense vector retrieval?

##### ✅ Answer:

Consine similarity is useful because it can take the numerical values from the embedding model and compare them to find out if the vecors are similar. This allows for comparing two ore more phrases or sets of text that could have no common words but are related in meaning. The result of the consine always provides a confidence level since it is rated on a scale of 0 to 1.
---

## 🏗️ Activity #2: Build the Vector RAG Pipeline

Run the notebook sections that:

1. Load the PDF into LangChain `Document` objects
2. Split the document into chunks
3. Embed the chunks
4. Store the chunk embeddings in in-memory Qdrant
5. Retrieve relevant chunks with similarity scores
6. Generate an answer grounded in retrieved context

#### ❓Question #2

Why is metadata important for a RAG application?

##### ✅ Answer:

The metadata gets embedded into the chunks that can be used to provide transparency of sourcing to the enduser when attached to their query. Depending on what you add as your metadata it can also provide additional context for the searches such as how updated the information might be or who the author was.

#### ❓Question #3

What tradeoff do we make when choosing chunk size and chunk overlap?

##### ✅ Answer:

This is ultimately choosing how much context is within each chunk which impacts the completeness or percision of the returned data. Smaller chunks can be more precise answers but requires retrieving more chunks to build a complete answer. While chunk overlap can help retain context within a chunk but it causes increased storage in duplicate text across chunks

#### ❓Question #4

What does a similarity score help you understand, and what does it not prove by itself?

##### ✅ Answer:

Similarity score helps understand the positive relationship between the query and the returned vector chunks. High scores are going to indicate a higher relavance to the query. It is giving a confidence rating but it is not giving validity to the returned data. The data from the vector could be semantically similar but completely incorrect information.

---

## 🏗️ Activity #3: Vibe Check Retrieval Quality

Run the notebook's vibe check queries and inspect both:

- The retrieved context
- The generated answer

#### ❓Question #5

For the vibe check queries, did the retrieved context seem relevant before generation? Why or why not?

##### ✅ Answer:

**Vibe Check Query 1:** The first context is very relevant but lacks completeness. It speaks about different preventative care actions but cuts off during the final sentance in reference to recommendations "Thus, recommen- dations for prevention and control should re ﬂect knowledge of the'". The second context is not very relevant is it just talking about cats in the medical system and not specifically about preventative actions. The third chunk provides some preventative care and it is relevant. The final chunk is slightly relevant. It doesn't provide any direct answers but it does provide some external references that could result in more answers if presented to the user that asked the question.

**Vibe Check Query 2:** The first context is very relevant. It calls out specific symptoms or behaviors that should trigger conversations with the vet as well as what questions to ask.The second context has some relevance as it mentions a reason to have a vet visit related to DJD symptoms but mostly the chunk has extra data that isn't relevant. While the third chunk doesn't call out vet calls or visits it does list some symptoms that can be linked to serious conditions which would imply the followup with the Vet. The last chunk is less relevant because it is more about questions and activities during the vet visit and not specifically about reasons to call the vet

**Vibe Check Query 3:** The first chunk as good relevance as it discusses Daily energy requirements (DER) for the cat and how it relates to the food intake. The second context is less direct but does reference food labeled with "Association of American Feed Control" so this would be useful information to provide back to the user. The third chunk includes sections about engery levels, caloric intake and the prevelence of diabities in cat but I don't see it giving any actionable advice and so I would rate it less relevant but adjacent to the question. I would say the last context is also relevant because it discusses the changing in diet as the kitten grows.

**Vibe Check Query 4:** None of these context are relevant because the question is absurd and wouldn't have any relevant data in this PDF.

---

## 🏗️ Activity #4: Tune Retrieval

Improve retrieval quality by changing one or more of:

- Chunk size
- Chunk overlap
- Retrieval `k`
- Query wording

Document what changed and whether retrieval improved.

##### Settings Changed:

- Chunk Size from 1000 to 500
- Chunk Overlap from 200 to 50
- Retrieval `k` from 4 to 8

##### Results: (More details stored in the 01_Cat_Health_Vector_RAG_LangChain_Qdrant.ipynb notebook)

1. Chunk setting resulted in 232 chunks instead of 135
2. The first test resulted in a less relevant answer that included an message about not having enough data to provide a definitive answer. It seemed that the source contexts had data but since they were missing the larger size there wasn't enough context
3. Increasing the number of vectors passed to LLM allowed for more context even with the lower chunks getting a more complete answer. 

## Loom Link
https://www.loom.com/share/e5af536532484703bea37e98ca181541
---

## Optional Deep Dive: RAG From Scratch

If you want to look underneath the library abstractions, run the optional reference notebook:

```text
02_Cat_Health_Vector_RAG_From_Scratch.ipynb
```

It builds the same retrieval pipeline again with only:

- `pypdf` for extracting text from the PDF
- Python standard-library HTTP requests for calling OpenAI
- Handcrafted document, chunking, embedding, similarity-search, vector-store, and generation primitives

This notebook is a reference walkthrough, not an additional assignment. Its purpose is to make the responsibilities hidden by LangChain, Qdrant, and provider SDKs visible.

---

## Submitting Your Homework

### Main Assignment

Follow these steps to prepare and submit your homework:

1. Pull the latest updates from upstream into the main branch of your AIE9 repo:

```bash
git checkout main
git pull upstream main
git push origin main
```

2. Start Cursor from the `01_Dense_Vector_Retrieval` folder.
3. Complete the notebook.
4. Answer the questions in this `README.md`.
5. Add, commit, and push your modified work to your origin repository.

When submitting your homework, provide the GitHub URL to your AIE9 repo.
