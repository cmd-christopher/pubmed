# PubMed Skill for Gemini CLI

🧬 Search and retrieve biomedical literature from PubMed using NCBI E-utilities.

## Description

This skill allows the Gemini CLI to interact with the PubMed database via NCBI's E-utilities. It supports searching for publications, fetching abstracts or full records, and retrieving document summaries.

## Installation

To use this skill, ensure you have `curl` installed and place `SKILL.md` in your skills directory.

## Configuration

Store your NCBI API key in `secrets/pubmed_api_key.txt` to benefit from higher rate limits (10 requests/second vs 3 requests/second).

```bash
PUBMED_API_KEY=$(cat secrets/pubmed_api_key.txt 2>/dev/null || echo "")
```

## Features

- **Search (ESearch)**: Find PMIDs matching specific search terms.
- **Fetch (EFetch)**: Retrieve full records or abstracts in various formats (text, XML).
- **Summary (ESummary)**: Get JSON/XML document summaries.

## Usage Examples

### Search for articles
```bash
curl -s "https://eutils.ncbi.nlm.nih.gov/entrez/eutils/esearch.fcgi?db=pubmed&term=CRISPR&retmax=5&retmode=json"
```

### Fetch an abstract
```bash
curl -s "https://eutils.ncbi.nlm.nih.gov/entrez/eutils/efetch.fcgi?db=pubmed&id=30000000&rettype=abstract&retmode=text"
```

## License

This project is open-source. Please refer to NCBI's terms of service for data usage.
