<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=gradient&customColorList=0,2,12,24&height=220&section=header&text=Corpus%20Research%20Assistant&fontSize=46&fontColor=ffffff&animation=fadeIn&fontAlignY=36&desc=A%20Persistent%2C%20Multi-Source%20AI%20Knowledge%20Assistant&descSize=18&descAlignY=58" alt="Corpus Research Assistant banner" width="100%"/>

<a href="https://git.io/typing-svg"><img src="https://readme-typing-svg.demolab.com?font=Fira+Code&weight=500&size=22&duration=3200&pause=900&color=2D8CFF&center=true&vCenter=true&width=760&lines=Drop+URLs.+Ask+questions.;Query+every+source+as+if+it+were+ONE+document.;Grounded+answers+with+source+citations.;Persistent+memory.+Incremental+ingestion." alt="Typing animation"/></a>

<br/>

![Python](https://img.shields.io/badge/Python-3.10+-3776AB?style=for-the-badge&logo=python&logoColor=white)
![n8n](https://img.shields.io/badge/n8n-Workflow_Automation-EA4B71?style=for-the-badge&logo=n8n&logoColor=white)
![Gemini](https://img.shields.io/badge/Gemini-1.5_Flash-4285F4?style=for-the-badge&logo=googlegemini&logoColor=white)
![ChromaDB](https://img.shields.io/badge/ChromaDB-Vector_Store-FF6446?style=for-the-badge)
![Streamlit](https://img.shields.io/badge/Streamlit-UI-FF4B4B?style=for-the-badge&logo=streamlit&logoColor=white)
![RAG](https://img.shields.io/badge/Architecture-RAG-2D8CFF?style=for-the-badge)
![dotenv](https://img.shields.io/badge/python--dotenv-Config-ECD53F?style=for-the-badge&logo=dotenv&logoColor=black)

### 🧠 Research Assistant With Memory

**Drop URLs. Ask questions across all of them as if they were one document.**

</div>

---

## 📖 About

**Research Assistant With Memory** is an AI-powered knowledge retrieval system designed to transform web pages into a **persistent, searchable knowledge base**. Users can submit URLs, ingest their content, and ask natural-language questions across multiple sources through a Streamlit interface.

The system combines **workflow automation** with **semantic search** and **large language models (Google Gemini)** to generate context-aware answers grounded in retrieved source content. Each answer is designed to include **source URL citations**, with an explicit fallback when the available sources do not contain sufficient information.

Unlike a single-session chatbot, the system **retains previously ingested knowledge**, so users can add new sources over time without losing their existing collection.

> **Core technologies:** `n8n` · `Gemini API (gemini-1.5-flash)` · `ChromaDB` · `Streamlit` · `Python` · `python-dotenv`

```
User → Streamlit UI → n8n Webhook → Chunk + Embed → ChromaDB ⇄ Retriever → Gemini → Cited Answer → UI
```

---

## 🧭 Table of Contents

| # | Section | # | Section |
| :-: | :-- | :-: | :-- |
| 1 | [Original Problem Statement](#-1-original-problem-statement) | 6 | [Project Structure](#-6-project-structure) |
| 2 | [Project Overview](#-2-project-overview) | 7 | [Prerequisites & Environment](#-7-prerequisites--environment-configuration) |
| 3 | [Core Features](#-3-core-features) | 8 | [Installation and Setup](#-8-installation-and-setup) |
| 4 | [System Architecture](#-4-system-architecture) | 9 | [Reliability & Grounding](#-9-reliability-grounding-and-error-handling) |
| 5 | [Technology Stack](#-5-technology-stack) | 10 | [Conclusion](#-10-conclusion) |

---

## 📌 1. Original Problem Statement

> ### *“Drop URLs, ask questions across all of them like they are one document.”*

Build a system where an **n8n webhook** receives URLs, scrapes the HTML content, and chunks and embeds it into **ChromaDB**. A **Streamlit** app lets the user ask natural-language questions across all ingested sources. **Gemini** retrieves relevant chunks and answers with **citations** showing which URL each fact came from. New URLs can be added at any time **without losing prior ones**.

### ✅ Required capabilities

| | Capability | Description |
| :-: | :-- | :-- |
| 📥 | **Automated ingestion** | Accept URLs through an n8n webhook and extract their raw HTML text. |
| 🧬 | **Semantic indexing** | Split extracted text into manageable chunks, generate embeddings, and store them in ChromaDB. |
| 🔎 | **Multi-source question answering** | Answer questions using relevant information retrieved from all previously ingested sources. |
| 🔗 | **Source-grounded responses** | Generate answers using Gemini and include citations that identify the originating URLs. |
| 🛑 | **Explicit fallback** | Return a clear *“Not found in sources”* response when the indexed knowledge does not support an answer. |
| 💾 | **Persistent memory** | Retain previously indexed content across application sessions and support incremental ingestion. |

---

## 🎯 2. Project Overview

Traditional research often involves opening multiple articles, switching between browser tabs, manually comparing information, and repeatedly searching for the same facts. This project introduces a **unified research workflow** in which users can build a personal knowledge base from web sources and query it through a conversational interface.

The application follows a **Retrieval-Augmented Generation (RAG)** approach. Instead of relying solely on a language model's pretrained knowledge, it **retrieves relevant passages** from the indexed documents and uses those passages as the **evidence** for answering questions.

### 🔄 From problem to solution

```mermaid
flowchart LR
    subgraph P["😩 Traditional research"]
        P1["Many browser tabs"]
        P2["Manual copy and compare"]
        P3["Repeated searching"]
    end
    subgraph S["🚀 Corpus Research Assistant"]
        S1["Unified knowledge base"]
        S2["Semantic retrieval"]
        S3["Cited, grounded answers"]
    end
    P1 --> S1
    P2 --> S2
    P3 --> S3
    classDef bad fill:#3b1d1d,stroke:#ff4d6d,color:#ffd6dc
    classDef good fill:#0b2a52,stroke:#2d8cff,color:#e6f0ff
    class P1,P2,P3 bad
    class S1,S2,S3 good
```

| Challenge | Proposed Solution |
| :--- | :--- |
| Information scattered across multiple URLs | Unified persistent knowledge base |
| Manual content collection | n8n-based ingestion workflow (`Webhook -> HTTP -> HTML Extract`) |
| Difficulty locating relevant passages | Embedding-based semantic retrieval via ChromaDB |
| Unsupported AI-generated answers | Source-grounded generation and explicit fallback |
| Repeated ingestion of existing material | Persistent vector storage and incremental indexing |

---

## ✨ 3. Core Features

```mermaid
mindmap
  root((Corpus Research Assistant))
    Ingestion
      n8n Webhook
      HTTP Request
      HTML Extract
    Indexing
      Text chunking
      Embeddings
      ChromaDB storage
    Answering
      Semantic retrieval
      Gemini 1.5 Flash
      Source citations
      Not found in sources
    Memory
      Persistent chroma_db
      Incremental ingestion
    Interface
      Streamlit chat
```

<table>
<tr>
<td width="50%" valign="top">

### 3.1 📥 Automated URL ingestion
The ingestion workflow begins when a user submits one or more URLs to an **n8n webhook**. The workflow is responsible for receiving the URLs, retrieving accessible web content, extracting meaningful text using **HTML extraction nodes**, and preparing it for indexing.

</td>
<td width="50%" valign="top">

### 3.2 🧬 Text chunking and embedding generation
Long web pages are divided into **smaller text chunks**. Each chunk can be retrieved independently, allowing the system to identify specific passages rather than supplying an entire article to the language model. **Embeddings** convert these chunks into numerical vector representations that capture semantic relationships.

</td>
</tr>
<tr>
<td width="50%" valign="top">

### 3.3 💾 Persistent vector database
**ChromaDB** stores the document embeddings together with the associated text and source metadata. The metadata preserves the **originating URL for every chunk** so that retrieved evidence can be traced back to its source.

</td>
<td width="50%" valign="top">

### 3.4 💬 Natural-language question answering
A **Streamlit** interface provides the user-facing research experience. Users can ask questions in ordinary language. The retrieval layer identifies relevant chunks from ChromaDB, and **Google Gemini** uses the retrieved evidence to formulate a readable response.

</td>
</tr>
</table>

### 3.5 🔗 Source citations and grounded answers

Responses identify the URL associated with each relevant piece of evidence. Citations are **derived from retrieved source metadata** rather than generated as unsupported links. When the retrieved context is insufficient, the system explicitly responds: ***"Not found in sources."***

### 🧪 Example queries to try

| Query | Expected behavior |
| :-- | :-- |
| *"What does source A say about topic X?"* | Retrieves matching chunks and answers with the originating URL cited |
| *"Compare what my sources say about X"* | Pulls evidence from several URLs and cites each one |
| *"Ask about something not in any ingested page"* | Replies **Not found in sources.** instead of guessing |
| *Ingest a new URL, then ask again* | New knowledge is added without losing earlier sources |

---

## 🏗️ 4. System Architecture

The architecture consists of **two connected workflows: document ingestion and question answering.**

### 🗺️ End-to-end flow

```mermaid
flowchart TD
    subgraph ING["📥 Workflow 1 - Document Ingestion"]
        A["User submits URLs"] --> B["n8n Webhook"]
        B --> C["HTTP Request: Fetch web pages"]
        C --> D["HTML Node: Extract text"]
        D --> E["Python Backend: Split into chunks"]
        E --> F["Generate Embeddings"]
        F --> G[("ChromaDB")]
        G --> H[("Persistent Knowledge Base")]
    end

    subgraph QA["💬 Workflow 2 - Question Answering"]
        I["User asks a question"] --> J["Streamlit Interface"]
        J --> K["Generate query embedding"]
        K --> L["Semantic retrieval from ChromaDB"]
        L --> M{"Relevant evidence found?"}
        M -->|Yes| N["Gemini API - 1.5 Flash"]
        M -->|No| O["Not found in sources"]
        N --> P["Answer with source citations"]
        O --> Q["Display fallback"]
    end

    H -.->|"stored vectors"| L

    classDef store fill:#0b2a52,stroke:#2d8cff,color:#e6f0ff
    classDef ok fill:#0f3d2e,stroke:#22c55e,color:#eafff3
    classDef warn fill:#3b2a0b,stroke:#f59e0b,color:#fff4de
    class G,H store
    class N,P ok
    class O,Q warn
```

### 📨 Sequence: ingesting a URL

```mermaid
sequenceDiagram
    autonumber
    actor U as User
    participant UI as Streamlit UI
    participant W as n8n Webhook
    participant H as HTTP Request
    participant X as HTML Extract
    participant B as Python Backend
    participant C as ChromaDB

    U->>UI: Submit URL
    UI->>W: POST url
    W->>H: Fetch web page
    H-->>W: Raw HTML
    W->>X: Extract meaningful text
    X-->>W: Clean text
    W-->>B: Text and source URL
    B->>B: Split into chunks
    B->>B: Generate embeddings
    B->>C: Store vectors, text and URL metadata
    C-->>UI: Knowledge base updated
    UI-->>U: Source ingested
```

### 💬 Sequence: asking a question

```mermaid
sequenceDiagram
    autonumber
    actor U as User
    participant UI as Streamlit UI
    participant R as Retriever
    participant C as ChromaDB
    participant G as Gemini 1.5 Flash

    U->>UI: Ask a natural-language question
    UI->>R: Question
    R->>R: Generate query embedding
    R->>C: Semantic similarity search
    C-->>R: Top chunks and source URLs
    alt Relevant evidence found
        R->>G: Question and retrieved passages
        G-->>UI: Answer grounded in evidence
        UI-->>U: Answer with source citations
    else No relevant evidence
        R-->>UI: Insufficient context
        UI-->>U: Not found in sources
    end
```

### 🔁 Lifecycle of the knowledge base

```mermaid
stateDiagram-v2
    [*] --> Empty
    Empty --> Ingesting: Submit first URL
    Ingesting --> Indexed: Chunks and embeddings stored
    Indexed --> Ingesting: Add another URL
    Indexed --> Querying: Ask a question
    Querying --> Grounded: Evidence found
    Querying --> NotFound: Evidence missing
    Grounded --> Indexed: Answer with citations
    NotFound --> Indexed: Fallback shown
    Indexed --> Indexed: Restart app, data persists
```

### 🗃️ Conceptual data model

```mermaid
erDiagram
    SOURCE_URL ||--o{ CHUNK : yields
    COLLECTION ||--o{ CHUNK : stores
    CHUNK {
        string text
        vector embedding
        string source_url
    }
    SOURCE_URL {
        string url
    }
    COLLECTION {
        string name
    }
```

> Every chunk keeps its **original URL as metadata**, which is what makes accurate citations possible.

---

## 🧰 5. Technology Stack

| Layer | Technology | Role |
| :-: | :-- | :-- |
| 🐍 | **Python** | Application logic, backend processing, and RAG pipeline |
| 🔀 | **n8n** | Visual workflow automation, webhook orchestration, and HTML scraping |
| 🧠 | **Gemini API** (`gemini-1.5-flash`) | Context-aware answer generation and fast inference |
| 🗄️ | **ChromaDB** | Local vector storage and similarity search |
| 🎨 | **Streamlit** | Interactive user interface (`app.py`) |
| 🔐 | **python-dotenv** | Environment-based configuration management |

```mermaid
flowchart LR
    ENV["python-dotenv<br/>.env config"] --> PY
    N8N["n8n<br/>webhook and scraping"] --> PY["Python<br/>RAG pipeline"]
    PY <--> DB[("ChromaDB<br/>vectors")]
    PY <--> LLM["Gemini 1.5 Flash<br/>generation"]
    PY <--> UI["Streamlit<br/>interface"]
    classDef n fill:#0b2a52,stroke:#2d8cff,color:#e6f0ff
    class ENV,N8N,PY,DB,LLM,UI n
```

---

## 📂 6. Project Structure

Based on the implemented architecture, the repository is structured as follows:

```plaintext
research-assistant/
│
├── backend/
│   ├── config.py             # Environment & model configuration
│   ├── database.py           # Database connection logic
│   ├── llm_engine.py         # Gemini API integration
│   ├── prompts.py            # System prompts & citation formatting
│   └── retriever.py          # ChromaDB semantic search logic
│
├── frontend/
│   └── app.py                # Streamlit user interface
│
├── chroma_db/                # Persistent local vector database directory
├── n8n/
│   └── workflow.json         # Exported n8n ingestion workflow
│
├── .env                      # API keys (Git ignored)
├── .env.example              # Environment variables template
├── .gitignore                # Security exclusions
├── requirements.txt          # Python dependencies
└── README.md                 # Project documentation
```

### 🧩 How the modules connect

```mermaid
flowchart LR
    APP["frontend/app.py<br/>Streamlit UI"] --> RET["backend/retriever.py<br/>semantic search"]
    APP --> DBM["backend/database.py<br/>DB connection"]
    RET --> DBM
    DBM --> CH[("chroma_db/<br/>persistent store")]
    APP --> LLM["backend/llm_engine.py<br/>Gemini integration"]
    PR["backend/prompts.py<br/>prompts and citations"] --> LLM
    CFG["backend/config.py<br/>env and model config"] -.-> RET
    CFG -.-> DBM
    CFG -.-> LLM
    N8["n8n/workflow.json<br/>ingestion workflow"] --> APP
    classDef f fill:#0b2a52,stroke:#2d8cff,color:#e6f0ff
    classDef s fill:#0f3d2e,stroke:#22c55e,color:#eafff3
    class APP,RET,DBM,LLM,PR,CFG,N8 f
    class CH s
```

---

## ⚙️ 7. Prerequisites & Environment Configuration

### ✅ Prerequisites

| Requirement | Details |
| :-- | :-- |
| 🐍 **Python** | 3.10+ installed locally |
| 🔀 **n8n** | An active n8n instance (Cloud or Local) |
| 🔑 **Gemini API key** | A Google Gemini API Key |

### 🔐 Environment variables

Create a `.env` file in the root directory based on your `config.py` setup:

```bash
# Gemini AI Configuration
GEMINI_API_KEY=your_gemini_api_key_here

# Database Configuration
CHROMA_DB_PATH=./chroma_db
COLLECTION_NAME=research_assistant
```

| Variable | Description |
| :-- | :-- |
| `GEMINI_API_KEY` | Google Gemini API key used for answer generation |
| `CHROMA_DB_PATH` | Directory of the persistent local ChromaDB store |
| `COLLECTION_NAME` | Name of the ChromaDB collection holding your chunks |

> [!WARNING]
> **Security Note:** Never commit your `.env` file. It is explicitly ignored in the `.gitignore`.

---

## 🚀 8. Installation and Setup

```mermaid
flowchart LR
    A["1. Clone"] --> B["2. Virtual env"] --> C["3. Install deps"] --> D["4. Configure n8n"] --> E["5. Launch app"]
    classDef n fill:#0b2a52,stroke:#2d8cff,color:#e6f0ff
    class A,B,C,D,E n
```

<details open>
<summary><b>1️⃣ Clone the repository</b></summary>

```bash
git clone <your-repository-url>
cd research-assistant
```

</details>

<details open>
<summary><b>2️⃣ Set up the virtual environment</b></summary>

```bash
python -m venv venv
.\venv\Scripts\activate  # Windows
```

On macOS / Linux use `source venv/bin/activate` instead.

</details>

<details open>
<summary><b>3️⃣ Install dependencies</b></summary>

```bash
pip install -r requirements.txt
```

</details>

<details open>
<summary><b>4️⃣ Configure n8n</b></summary>

Import the `workflow.json` into n8n. Ensure the **Webhook URL is active** and the **HTML extraction node is properly linked to your backend ingestion endpoint**.

</details>

<details open>
<summary><b>5️⃣ Launch the application</b></summary>

```bash
streamlit run frontend/app.py
```

</details>

---

## 🛡️ 9. Reliability, Grounding, and Error Handling

```mermaid
flowchart TD
    Q["Question"] --> RT["Retrieve passages from ChromaDB"]
    RT --> CK{"Supporting passages?"}
    CK -->|Yes| PR["prompts.py: use ONLY supplied passages"]
    PR --> GM["Gemini answers"]
    GM --> CT["Cite URLs from chunk metadata"]
    CK -->|No| NF["Not found in sources"]
    classDef ok fill:#0f3d2e,stroke:#22c55e,color:#eafff3
    classDef warn fill:#3b2a0b,stroke:#f59e0b,color:#fff4de
    class GM,CT ok
    class NF warn
```

| Safeguard | How it works |
| :-- | :-- |
| 🧾 **Retrieval-grounded generation** | The `prompts.py` file strictly instructs Gemini to use **only supplied passages** as evidence and explicitly acknowledge missing information. |
| 🏷️ **Source metadata integrity** | Every indexed chunk in ChromaDB retains its **original URL as metadata**, ensuring accurate tracing back to the source. |
| 💾 **Persistent storage** | `chroma_db` is stored locally within the project directory, ensuring that data **persists across application and server restarts**. |

---

## 🎓 10. Conclusion

The **Research Assistant With Memory** creates a robust workflow where users can continuously expand their knowledge base and ask questions across previously indexed sources. By utilizing **Gemini's rapid inference**, **n8n's seamless webhooks**, and **ChromaDB's persistent semantic retrieval**, the system prioritizes **grounded, verifiable answers** over AI hallucinations.

---

<div align="center">

**⭐ If you find this project useful, consider giving it a star!**

<img src="https://capsule-render.vercel.app/api?type=waving&color=gradient&customColorList=0,2,12,24&height=120&section=footer" alt="footer" width="100%"/>

</div>
