# SiteCloner

A Python utility for creating local copies of websites from Burp Suite sitemap exports.

## Overview

SiteCloner is a tool that processes Burp Suite sitemap XML exports and creates a complete local copy of a website, preserving its structure and content. This is particularly useful for security researchers, penetration testers, and web developers who need offline access to website content.

## Features

- Creates a complete offline copy of websites from Burp Suite sitemap exports
- Preserves the original website structure
- Handles both text and binary content (images, PDFs, etc.)
- Automatically creates necessary directories
- Sanitizes URL paths to valid filesystem paths
- Provides error handling and reporting

## Requirements

- Python 3.6+
- A Burp Suite sitemap XML export file

## Installation

No special installation is required. Simply clone or download this repository:

```bash
git clone https://github.com/yourusername/SiteCloner.git
cd SiteCloner
````
## Usage

1. Export a sitemap from Burp Suite (see instructions below)
2. Place the exported XML file in the same directory as the script or update the `BURP_XML_FILE` variable
3. Run the script:

```bash
   python3 clone-from-burp.py
```

4. Find your cloned website in the `cloned_site` directory (or the directory specified in `OUTPUT_DIR`)

## Configuration

You can modify these variables at the top of the script:
- `BURP_XML_FILE`: Path to the Burp Suite sitemap XML file (default: 'burp_sitemap.xml')
- `OUTPUT_DIR`: Directory where the cloned site will be saved (default: 'cloned_site')

## What is a Burp Suite Sitemap XML?

Burp Suite is a popular web application security testing tool. Its sitemap feature keeps track of all the URLs that Burp has encountered while browsing or scanning a website.

The sitemap XML export contains detailed information about each request and response, including:
- The URL
- The HTTP method (GET, POST, etc.)
- Request headers and body
- Response headers and body
- MIME types
- Status codes
- And more


This XML file serves as a comprehensive record of a website's structure and content, making it an ideal source for creating offline copies.
How to Export a Sitemap from Burp Suite

1. Open Burp Suite and browse the target website (manually or using the Spider tool)
2. Go to the "Target" tab and select the "Site map" sub-tab
3. Right-click on the host you want to export
4. Select "Save selected items" from the context menu
5. Choose "Base64-encode requests and responses" if you want to preserve binary content
6. Save the file as "burp_sitemap.xml" in your project directory

### How the Script Works
_The clone-from-burp.py script:_


1. Parses the Burp Suite sitemap XML file
2. For each item in the sitemap:
   Extracts the URL and response content
   Determines if the response is base64-encoded
   Decodes the content appropriately
   Creates a suitable file path based on the URL
   Saves the content to the appropriate location

3. Provides a summary of the operation when complete

### Example Output Structure
For a website like example.com with various pages, the output structure might look like:

```
cloned_site/
└── example.com/
    ├── index.html
    ├── about.html
    ├── contact.html
    ├── images/
    │   ├── logo.png
    │   └── banner.jpg
    ├── css/
    │   └── style.css
    └── js/
        └── script.js
```
Limitations

The script can only clone pages that were captured in the Burp Suite sitemap
Dynamic content that requires JavaScript execution won't function in the offline copy
Some relative links might not work correctly in the offline version
The script doesn't modify links to point to local resources
Contributing
Contributions are welcome! Please feel free to submit a Pull Request.
License GPL3


