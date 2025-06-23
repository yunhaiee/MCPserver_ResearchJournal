# PubMed Scraper MCP Server

A Model Context Protocol (MCP) server that provides tools for searching academic research papers from PubMed and Scopus databases. This server can be connected to Claude and other AI assistants to enable research paper discovery and analysis.

## Features

- **PubMed Search**: Search for articles by journal name and keywords in abstracts
- **Scopus Search**: Search for articles from Elsevier's Scopus database
- **Rich Metadata**: Extract titles, authors, publication dates, DOIs, and abstracts
- **Direct Links**: Generate clickable links to research papers and DOI references
- **MCP Integration**: Seamlessly integrate with Claude and other AI assistants

## Prerequisites

- Python 3.8 or higher
- An Elsevier API key for Scopus searches (optional but recommended)

## Installation

1. **Clone or download this repository**
   ```bash
   git clone <repository-url>
   cd pubmed-scraper
   ```

2. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

3. **Set up API key (optional)**
   
   For Scopus searches, you'll need an Elsevier API key:
   - Visit [Elsevier Developer Portal](https://dev.elsevier.com/)
   - Create an account and get your API key
   - The current code uses a demo key, but for production use, replace `ELSEVIER_API_KEY` in `pubmed_scraper.py` with your own key

## Usage

### Running the MCP Server

1. **Start the server**
   ```bash
   python pubmed_scraper.py
   ```

2. **Connect to Claude Desktop**
   
   In Claude Desktop, go to Settings → Model Context Protocol and add a new server:
   - **Name**: PubMed Scraper
   - **Transport**: stdio
   - **Command**: `python`
   - **Arguments**: `path/to/pubmed_scraper.py`

### Available Tools

#### 1. `search_pubmed_articles`
Search for recent articles from a specific journal containing keywords in their abstract.

**Parameters:**
- `journal`: Name of the journal (e.g., "Accident Analysis and Prevention", "Journal of Safety Research")
- `keyword`: Keyword to filter abstract text (e.g., "elderly", "machine learning", "traffic accidents")

**Example:**
```
Search for articles about elderly drivers in Accident Analysis and Prevention journal
```

#### 2. `search_scopus`
Search recent articles from Scopus by journal and keyword.

**Parameters:**
- `journal`: Journal name (e.g., "Accident Analysis and Prevention", "Journal of Safety Research")
- `keyword`: Search keyword (e.g., "elderly", "machine learning", "traffic accidents")
- `max_results`: Maximum number of results (default: 10)

**Example:**
```
Search for machine learning articles in Journal of Transportation Safety and Security
```

#### 3. `test_pubmed_connection`
Test the connection to PubMed with a simple search.

## Example Conversations with Claude

### Example 1: Research on Elderly Drivers
```
User: "Find recent research about elderly drivers in traffic safety journals"

Claude can use:
- search_pubmed_articles("Accident Analysis and Prevention", "elderly")
- search_scopus("Journal of Safety Research", "elderly", 5)
```

### Example 2: Machine Learning in Transportation
```
User: "What are the latest machine learning applications in transportation safety?"

Claude can use:
- search_scopus("Journal of Transportation Safety and Security", "machine learning", 10)
- search_pubmed_articles("Accident Analysis and Prevention", "machine learning")
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

## Troubleshooting

### Common Issues

1. **Import errors**: Make sure all dependencies are installed with `pip install -r requirements.txt`

2. **API rate limiting**: The tools include retry logic, but if you encounter rate limits, wait a few minutes before trying again

3. **No results found**: Try different keyword variations or check journal name spelling

4. **Connection issues**: Ensure you have internet access and the APIs are accessible

### Debug Mode

To see detailed request information, the code includes print statements that show:
- Request attempts and responses
- Content length and status codes
- Parsing results

## API Limits and Best Practices

- **PubMed**: No API key required, but respect rate limits
- **Scopus**: Requires API key, has usage limits based on your plan
- **Recommendations**:
  - Use specific keywords for better results
  - Limit `max_results` to reasonable numbers (5-20)
  - Cache results when possible for repeated searches

## Contributing

Feel free to submit issues, feature requests, or pull requests to improve this tool.

## License

This project is open source. Please check the license file for details.

## Support

For issues or questions:
1. Check the troubleshooting section above
2. Review the code comments for implementation details
3. Test with the `test_pubmed_connection` tool first
