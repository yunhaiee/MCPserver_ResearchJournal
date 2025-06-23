# PubMed Scraper MCP Server

A Model Context Protocol (MCP) server that provides tools for searching academic research papers from PubMed and Scopus databases. This server can be connected to Claude and other AI assistants to enable research paper discovery and analysis.

## Features

- **PubMed Search**: Search for articles from NIH's PubMed database
- **Scopus Search**: Search for articles from Elsevier's Scopus database

## Prerequisites

- Python 3.8 or higher
- An Elsevier API key for Scopus searches (optional but recommended)

## Installation

1. **Clone or download this repository**
   ```bash
   git clone <https://github.com/yunhaiee/MCPserver_ResearchJournal>
   cd research-scraper
   ```

2. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

3. **Set up API key (optional)**
   
   For Scopus searches, you'll need an Elsevier API key:
   - Visit [Elsevier Developer Portal](https://dev.elsevier.com/)
   - Create an account and get your API key
   - The current code uses a demo key, but for production use, replace `ELSEVIER_API_KEY` in `research_scraper.py` with your key

## Usage

### Running the MCP Server

   **Connect to Claude Desktop**
   
   In Claude Desktop, go to Settings → Developer → Edit Setting
   1. This will lead you to a file called 'claude_desktop_config.json'
   2. Open this file with an editor.
   3. Copy paste following:
      ```
         {
           "mcpServers": {
             "research-scraper": {
               "command": "uv",
               "args": [
                 "--directory",
                 "C:\\Users\\user\\research-scraper",
                 "run",
                 "research_scraper.py"
               ]
             }
           }
         }
      ```

### Available Tools

#### 1. `search_pubmed`
Search for recent articles from a specific journal containing keywords in their abstract using PubMed API.

**Parameters:**
- `journal`: Name of the journal (e.g., "Accident Analysis and Prevention", "Journal of Safety Research")
- `keyword`: Keyword to filter abstract text (e.g., "elderly", "machine learning", "traffic accidents")

#### 2. `search_scopus`
Search recent articles from Scopus by journal and keyword.

**Parameters:**
- `journal`: Journal name (e.g., "Accident Analysis and Prevention", "Journal of Safety Research")
- `keyword`: Search keyword (e.g., "elderly", "machine learning", "traffic accidents")

## Example Conversations with Claude

### Example 1: Research on Elderly Drivers
```
User: "Find recent research about elderly drivers in traffic safety journals"
```

### Example 2: Machine Learning in Transportation
```
User: "What are the latest machine learning applications in transportation safety?"
```

## Output Format

The tools return formatted results with:
- **Article titles** (bold)
- **Authors**
- **Publication dates** (full date format)
- **DOIs** with clickable links
- **Scopus links** (when available)
- **Abstracts** (truncated for readability)

Example output:
```
1. **Spatiotemporal urban traffic safety analytical framework**
   Authors: Kim Y., Lee D., Derrible S.
   Publication Date: August 2025
   DOI: 10.1016/j.aap.2025.108088
   DOI Link: [10.1016/j.aap.2025.108088](https://doi.org/10.1016/j.aap.2025.108088)
   Scopus Link: [View on Scopus](https://www.scopus.com/...)
   Abstract: Since more than 75% of the population lives in cities...
```

## Integration with Notion

The output is formatted with markdown links that work seamlessly with Notion:
- DOI links are clickable and direct to the research paper
- Scopus links provide access to detailed article information
- All links are properly formatted for copy-paste into Notion
