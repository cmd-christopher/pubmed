---
name: pubmed
description: Search and retrieve biomedical literature from PubMed using NCBI E-utilities.
metadata: { "openclaw": { "emoji": "🧬", "requires": { "bins": ["curl"] } } }
---

# PubMed (NCBI E-utilities)

Interface for searching and fetching data from PubMed and other NCBI databases.

## Configuration

Store your API key in `secrets/pubmed_api_key.txt`.
Load it into an environment variable before use:
```bash
PUBMED_API_KEY=$(cat secrets/pubmed_api_key.txt 2>/dev/null || echo "")
```

## Tools & Usage

All requests use the base URL: `https://eutils.ncbi.nlm.nih.gov/entrez/eutils/`

### 1. Search (ESearch)
Find IDs (PMIDs) matching a query.
```bash
# Search for 'CRISPR' in PubMed (default db), limit to 5 results
curl -s "https://eutils.ncbi.nlm.nih.gov/entrez/eutils/esearch.fcgi?db=pubmed&term=CRISPR&retmax=5&retmode=json&api_key=$PUBMED_API_KEY"
```

### 2. Fetch (EFetch)
Download records (abstracts/full text if available) by ID.
```bash
# Get abstract for PMID 30000000 in text format
curl -s "https://eutils.ncbi.nlm.nih.gov/entrez/eutils/efetch.fcgi?db=pubmed&id=30000000&rettype=abstract&retmode=text&api_key=$PUBMED_API_KEY"

# Get XML record for PMID 30000000
curl -s "https://eutils.ncbi.nlm.nih.gov/entrez/eutils/efetch.fcgi?db=pubmed&id=30000000&retmode=xml&api_key=$PUBMED_API_KEY"
```

### 3. Summary (ESummary)
Get document summaries (DocSums).
```bash
curl -s "https://eutils.ncbi.nlm.nih.gov/entrez/eutils/esummary.fcgi?db=pubmed&id=30000000&retmode=json&api_key=$PUBMED_API_KEY"
```

## Guidelines
- **Rate Limits**: 3 requests/sec without key; 10 requests/sec with key.
- **Large Batches**: Use Entrez History (`&usehistory=y`) for large sets.
- **Spaces**: Replace spaces with `+` in terms.
- **Tool/Email**: For intensive use, provide `&tool=OpenClaw&email=drwilms@gmail.com`.

## Common Fields
- `[au]`: Author
- `[ti]`: Title
- `[tiab]`: Title/Abstract
- `[dp]`: Publication Date (YYYY/MM/DD)
- `[journal]`: Journal name
