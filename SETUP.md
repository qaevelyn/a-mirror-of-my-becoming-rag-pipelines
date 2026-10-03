# Setup

Every pipeline in this fleet reads documents from disk, chunks them,
embeds them locally, and writes them to a local Chroma vector store.
Nothing leaves your machine.

This document covers what a reader needs before running any of the
five ships. Read it once. Then pick the ship you want and follow its
own README for the specifics.

---

## Sovereign, by design

Every pipeline in this fleet is sovereign. That is not a marketing
word. It is an architectural claim, and it has three parts:

1. **No cloud dependency.** The pipeline does not call a cloud API.
   Nothing that requires an account, a key, a credit card, or a rate
   limit.

2. **No data leaves your machine.** Your documents are read from
   disk, chunked in memory, embedded locally, and stored locally.
   Nothing is uploaded. Nothing is telemetered. Nothing is logged
   anywhere but your own disk.

3. **No vendor permission required.** You install the tools. You
   run them. You own the output. If a vendor changes their terms
   tomorrow, nothing in this pipeline breaks, because no vendor is
   in the loop.

Sovereign means you can run this on a laptop with no internet
connection and it works. Airplane mode. Off the grid. Nothing
phones home.

---

## The environment

Each ship names its own environment. The README and the notebook
say what to install and what to pull. Read the ship first. Install
exactly what it names.

Once the environment is installed, the pipeline runs offline. On
your hardware. Under your control.

---

## What the pipelines need

Three things to point the pipeline at:

1. **A source of documents.** A folder of markdown, text, or JSON
   files. Or a specific list of files.

2. **A place to put the vector store.** A folder on your disk. The
   pipeline creates it on first run.

3. **An embedding model available in your local Ollama.** The
   ship's README names the model it uses. If the model is missing,
   the pipeline fails loudly.

---

## Three ways to point the pipeline at your data

Pick one. All three work. Each has different trade-offs.

### Option A — Edit the paths in the notebook

Best for trying it once, understanding what the pipeline does.

Open the notebook. Find the first code cell (marked `# ===== SETUP =====`).
Replace the placeholder paths with your own:

```python
# ===== SETUP =====
SOURCE_FILES = [
    "~/path/to/your/corpus/your-document-1.md",
    "~/path/to/your/corpus/your-document-2.md",
]
VECTOR_STORE_PATH = "~/path/to/your/vector-store"
EMBEDDING_MODEL = "your-ollama-embedding-model"
# ===== END SETUP =====
Run the notebook.

Trade-off: the notebook is now customized to your paths. If you want
to run it again with a different corpus, you edit it again.

Option B — Use a config.json file
Best for keeping the notebook unchanged and swapping corpora between
runs.

Create a file called config.json in the same folder as the notebook:

json
{
  "source_files": [
    "~/Documents/my-corpus/notes.md",
    "~/Documents/my-corpus/journal.md"
  ],
  "vector_store_path": "~/Documents/my-vector-store",
  "embedding_model": "your-ollama-embedding-model"
}
The notebook reads it automatically:

python
import json, os

CONFIG_PATH = "config.json"
with open(CONFIG_PATH) as f:
    config = json.load(f)

SOURCE_FILES = [os.path.expanduser(p) for p in config["source_files"]]
VECTOR_STORE_PATH = os.path.expanduser(config["vector_store_path"])
EMBEDDING_MODEL = config["embedding_model"]
Trade-off: two files instead of one. The notebook stays untouched.

Option C — Use environment variables
Best for automation, scheduled runs, or pointing the pipeline at
different corpora without editing any file.

Set the variables in your shell:

bash
export MIRROR_CORPUS_DIR="$HOME/Documents/my-corpus"
export MIRROR_VECTOR_STORE="$HOME/Documents/my-vector-store"
export MIRROR_EMBED_MODEL="your-ollama-embedding-model"
The notebook reads them:

python
import os, glob

CORPUS_DIR = os.path.expanduser(os.environ.get("MIRROR_CORPUS_DIR", "~/Documents/default-corpus"))
VECTOR_STORE_PATH = os.path.expanduser(os.environ.get("MIRROR_VECTOR_STORE", "~/Documents/default-vector-store"))
EMBEDDING_MODEL = os.environ.get("MIRROR_EMBED_MODEL", "your-ollama-embedding-model")

SOURCE_FILES = glob.glob(os.path.join(CORPUS_DIR, "*.md"))
Trade-off: the pipeline has no idea what it will read until the shell
tells it. That is the point. Change the shell, change the run.

What the pipeline does with your documents
For each source file, the pipeline:

Reads the file

Chunks it into segments

Embeds each chunk via Ollama

Writes each chunk to the Chroma store with its embedding, its
text, and metadata (source path, chunk index, filename)

The pipeline is idempotent. Running it twice does not duplicate
anything. Each chunk gets a deterministic ID built from its source
path and its chunk index. The store uses upserts, not inserts.

The pipeline is resumable. If it crashes mid-run, relaunch it. The
sidecar file records which files have already been processed.

What the pipeline does NOT do
It does not upload anything. All processing is local.

It does not call a cloud API. Your documents stay on your machine.

It does not phone home. No telemetry. No analytics. No version
check.

It does not require an account. No sign-up. No API key. No credit
card.

This is the state of the code as published. You get it as-is. If you
improve it, the AGPL-3.0 requires that you publish your improvements
under the same license.

Licensing
Every ship in this fleet is dual-licensed:

AGPL-3.0 — the code is free to use, modify, and redistribute
under the terms of the license. The full text is in each ship's
LICENSE file. Under AGPL-3.0, if you run a modified version as a
network service, you must offer the source of your modifications
to your users.

Commercial license — available for organizations that need to
use the code without the AGPL-3.0 obligations. Contact the author
for pricing.

Free does not mean free to exploit. If you build a product on this
work, the author expects to be paid.

What you get
This fleet is published as-is. It runs. It is documented. It is the
work of one person building on consumer hardware with no team, no
budget, and no cloud account.

You are welcome to read the code, run it, and improve it. The AGPL
requires that improvements you distribute are published under the
same license. That is the trade: free to use, free to modify, free
to share — as long as the sharing continues.

Author
Evelyn Caro — Sovereign AI Builder.

qaevelyn.github.io

© 2026 Evelyn Caro. All rights reserved.
