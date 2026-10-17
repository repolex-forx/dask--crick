# Repolex Knowledge Graph of dask/crick

RDF knowledge graph data for [dask/crick](https://github.com/dask/crick), parsed by [repolex](https://repolex.ai).

> **Note**: This data is experimental and subject to change without notice.

## How to use this data

The easiest way to get started is to install the [rlex](https://github.com/repolex-ai/rlex) query tool:

```bash
cargo install --git https://github.com/repolex-ai/rlex
```

Verify the install:

```bash
rlex --help
```

**rlex is designed to be used primarily by LLMs in a terminal.** Start up your favorite AI assistant and ask it to use rlex. It handles the SPARQL — you just ask questions in plain English.

To load this repo's data:

```bash
rlex download dask/crick
```

Consult `rlex --help` for other options, including SPARQL queries, HTTP server, and interactive visualization.

## Data structure

All data is stored as gzip-compressed [N-Quads](https://www.w3.org/TR/n-quads/) (`.nq.gz`), a standard RDF format that can be loaded into any triplestore or graph database.

```
.
├── aggregate
│   ├── ast
│   │   └── 720de70c6adf28cb30e8293597ed03b90d09bba8
│   │       └── chunk-001.nq.gz
│   └── repolex
│       └── 720de70c6adf28cb30e8293597ed03b90d09bba8
│           └── chunk-001.nq.gz
├── blob
│   ├── 01aa0bd2c3ed9c1a12483fe9fa2b42dd6dcf332e.nq.gz
│   ├── 1e75e3397b8a2a073625087618be416750ab9e07.nq.gz
│   ├── 252864875d5407844b82089de2eb245362c3d111.nq.gz
│   ├── 2991b67df0698efcfdca9df446b32860828a6015.nq.gz
│   ├── 5728ddf32b3dbcb48edadf874c6104b55b127f7f.nq.gz
│   ├── 57d963a8b919b294a1c895765ffb52fc4c683f25.nq.gz
│   ├── 5a0240549128c4d3d1f429677533fc2bf6355704.nq.gz
│   ├── 5da547c499eea5b8b91ab7f29d6752a376148a8a.nq.gz
│   ├── 624a23461486cf1bf8f4e14a087fb591250d69fe.nq.gz
│   ├── 644a973677dc925f0b96cdb966c29195a6f5accc.nq.gz
│   ├── 653e9a71bf181d169803f8d1bea88b10043cbe60.nq.gz
│   ├── 729b6076eabb2cfabe2be024794df4223bf0a491.nq.gz
│   ├── 7607cf3456a4647a315089ad7a5e90be7a2ed9c9.nq.gz
│   ├── 782cce0fcb3400f19100b8a989f05759662c1fdb.nq.gz
│   ├── 81cf0389818ed9f2e69074734622a2849bf48333.nq.gz
│   ├── 83170de8fbfeddf6a5c590fb89b48bdac7ba8f29.nq.gz
│   ├── 895396b2a4d3f23f1820a108761de6ca3008d099.nq.gz
│   ├── 9cba939f578339a0db0bcc9b9e22faf6fde51fe7.nq.gz
│   ├── ad288dcfc28bc37bfa81ba8ad22dd8160fc0a43d.nq.gz
│   ├── b71992109c63512b7c3719e3eba6c1ab56365e8d.nq.gz
│   ├── b90e5279aadbdab1837e7c34bf41071e937fca47.nq.gz
│   ├── bf03f1038a8353d494b894f29d76af570cfca6b0.nq.gz
│   ├── c8b73bcc917f160168069e58ca7b1cb64bc8994c.nq.gz
│   ├── ca8292f3717f84e403ff7a14cf5be15e0c0d6511.nq.gz
│   ├── cebb99c4698534cd05de71a5ba9ecf75772865c5.nq.gz
│   ├── d0276d32ba08210b13963008a018d77fe2f891b8.nq.gz
│   ├── d18abf4dbe6a1b1e34d8072efb1e494e88dbda7d.nq.gz
│   ├── d4043870458435a2b03ad18ce55575579fbcff3e.nq.gz
│   ├── d55aa6992e1d4e178fb46f56875e111440f2552e.nq.gz
│   ├── da8636babb0afb058f1c1b9798badd1f941c4004.nq.gz
│   ├── dc4d6b30b372d5dec27a634120dd5d983036b520.nq.gz
│   ├── e63d147c3861a77db9450c3c3f355a3f595f9342.nq.gz
│   ├── e65a24c019f0ce0a043b4dfd4d1196241752c8ff.nq.gz
│   ├── e69de29bb2d1d6434b8b29ae775ad8c2e48c5391.nq.gz
│   ├── e6c0c4e5be9fa31892f41dd9bb684b5be856dc42.nq.gz
│   └── fe7ce38c25c552889971cbe71844e218419c21e1.nq.gz
├── branch
│   └── branch.nq.gz
├── commit
│   └── commit.nq.gz
├── filetree
│   └── 720de70c6adf28cb30e8293597ed03b90d09bba8.nq.gz
├── issue
│   └── issue.nq.gz
├── pr
│   └── pr.nq.gz
└── tag
    └── tag.nq.gz

13 directories, 44 files
```

| Directory | What it contains |
|-----------|-----------------|
| `blob/` | Per-file AST graphs, content-addressed by git blob SHA. Each file in the source repo gets its own graph. |
| `aggregate/ast/` | Combined AST graph per parsed commit. Merges all blob graphs for a snapshot of the entire codebase at that point. |
| `aggregate/lsp/` | Language Server Protocol enrichment: resolved symbols, definitions, references, and type information. |
| `aggregate/dataflow/` | Interprocedural data flow edges between functions and modules. |
| `aggregate/repolex/` | Combined graph (AST + LSP + dataflow) per commit. |
| `commit/` | Git commit metadata (author, date, message, parent links). |
| `branch/` | Branch metadata. |
| `tag/` | Tag metadata. |
| `filetree/` | File tree snapshots per commit (which files existed and their blob SHAs). |
| `audit/` | Code architecture and graph audit reports per commit. |

## Source repository

[dask/crick](https://github.com/dask/crick)

---
*Parsed on 2026-10-17 by [repolex](https://repolex.ai)*
