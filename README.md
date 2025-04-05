# MCP Python SDK Documentation

This repository contains the documentation for the Model Context Protocol (MCP) Python SDK. It is built using Sphinx and the Read the Docs theme.

## Overview

The Model Context Protocol (MCP) is an open standard that defines how applications interact with large language models (LLMs). This documentation aims to help developers:

- Understand the core concepts of MCP
- Build MCP servers to expose resources, tools, and prompts
- Create MCP clients to connect to MCP servers
- Explore advanced topics and best practices

## FastMCP

Our documentation includes comprehensive coverage of FastMCP, a high-level, Pythonic interface for building MCP servers. Originally a standalone project, FastMCP has been integrated into the official MCP Python SDK. It provides a developer-friendly way to create MCP servers with minimal boilerplate:

```python
from mcp.server.fastmcp import FastMCP

mcp = FastMCP("Demo 🚀")

@mcp.tool()
def add(a: int, b: int) -> int:
    """Add two numbers"""
    return a + b
```

The SDK provides multiple ways to run your server:
- Development mode with the MCP Inspector
- Claude Desktop integration
- Direct execution for custom deployments

## Building the Documentation

1. **Install Dependencies**

   First, make sure you have Python installed. Then, install the required packages:

   ```bash
   # Using conda (recommended)
   conda activate cuda_test
   pip install -r requirements.txt
   
   # Or using pip in a virtual environment
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   pip install -r requirements.txt
   ```

2. **Build the Documentation**

   To build the documentation:

   ```bash
   make html
   ```

   The built documentation will be in the `_build/html/` directory.

3. **Live Preview**

   For a live preview with auto-reload:

   ```bash
   sphinx-autobuild . _build/html
   ```

   Then open your browser to http://localhost:8000.

## Hosting on GitHub Pages

You can host this documentation on GitHub Pages by following these steps:

1. **Create a `gh-pages` branch**

   ```bash
   git checkout --orphan gh-pages
   git rm -rf .
   touch .nojekyll  # This tells GitHub not to process the site with Jekyll
   git add .nojekyll
   git commit -m "Initial gh-pages commit"
   git push origin gh-pages
   git checkout main  # Go back to your main branch
   ```

2. **Create GitHub Actions Workflow**

   Create a file `.github/workflows/docs.yml` with the following content:

   ```yaml
   name: Build and Deploy Documentation
   
   on:
     push:
       branches: [ main ]
     workflow_dispatch:
   
   jobs:
     build:
       runs-on: ubuntu-latest
       steps:
         - uses: actions/checkout@v3
         - name: Set up Python
           uses: actions/setup-python@v4
           with:
             python-version: '3.10'
         
         - name: Install dependencies
           run: |
             python -m pip install --upgrade pip
             pip install -r requirements.txt
         
         - name: Build documentation
           run: |
             make html
         
         - name: Deploy to GitHub Pages
           uses: peaceiris/actions-gh-pages@v3
           with:
             github_token: ${{ secrets.GITHUB_TOKEN }}
             publish_dir: ./_build/html
             force_orphan: true
             user_name: 'github-actions[bot]'
             user_email: 'github-actions[bot]@users.noreply.github.com'
   ```

3. **Enable GitHub Pages**

   - Go to your GitHub repository
   - Navigate to Settings > Pages
   - Under "Source", select "Deploy from a branch"
   - Select the "gh-pages" branch and "/ (root)" folder
   - Click "Save"

4. **Access Your Documentation**

   Your documentation will be available at:
   `https://[username].github.io/[repository-name]/`

## Documentation Structure

- `index.rst`: Main entry point
- `introduction.rst`: Introduction to MCP
- `getting-started.rst`: Getting started guide
- `server-guide.rst`: Guide for building MCP servers
- `client-guide.rst`: Guide for building MCP clients
- `examples.rst`: Example MCP applications
- `advanced-topics.rst`: Advanced MCP concepts
- `api-reference.rst`: API reference

## Contributing

Contributions to improve the documentation are welcome! Here's how you can contribute:

1. Fork the repository
2. Create a new branch for your changes
3. Make your changes
4. Build the documentation to verify your changes
5. Submit a pull request

## Resources

- [Official MCP Website](https://modelcontextprotocol.io/)
- [MCP Python SDK GitHub](https://github.com/modelcontextprotocol/python-sdk)
- [MCP Specification](https://spec.modelcontextprotocol.io/)
- [Officially Supported Servers](https://github.com/modelcontextprotocol/servers)
- [GitHub Discussions](https://github.com/modelcontextprotocol/python-sdk/discussions)
- [FastMCP GitHub (Legacy)](https://github.com/jlowin/fastmcp)

## License

This documentation is licensed under the MIT License - see the LICENSE file for details. 