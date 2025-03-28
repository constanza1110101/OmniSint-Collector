OmniSINT Collector
License
Rust Version
OSINT
Build Status
Version

A comprehensive OSINT (Open Source Intelligence) framework written in Rust, designed to gather, correlate, and analyze information from diverse public sources. OmniSINT Collector creates actionable intelligence with minimal noise, helping security professionals build comprehensive target profiles while respecting privacy and legal boundaries.

<p align="center">
  <img src="docs/images/omnisint_logo.png" alt="OmniSINT Collector Logo" width="300"/>
</p>
Table of Contents
Features
Use Cases
Installation
Prerequisites
From Source
Using Docker
Configuration
Usage
Basic Commands
Examples
Module Details
Username Discovery
Dark Web Monitoring
Search Engine Intelligence
Social Media Analysis
Document Metadata Extraction
Domain Intelligence
Geospatial Analysis
Output Formats
API Integration
Security and Privacy
Performance Considerations
Contributing
Roadmap
Legal Disclaimer
License
Features
Username Discovery: Automatically check usernames across 300+ platforms with identity correlation
Dark Web Monitoring: Search for leaked credentials and sensitive information across multiple sources
Advanced Search Engine Dorking: Customizable patterns for targeted information gathering across major search engines
Social Media Intelligence: Profile discovery, content analysis, and relationship mapping
Document Metadata Analysis: Extract and analyze metadata from public documents
Domain Intelligence: Gather DNS, WHOIS, SSL certificates, and subdomain information
Geospatial Analysis: Correlate location data from multiple sources with visualization
Relationship Mapping: Automatically identify connections between different data points
Confidence Scoring: Evaluate the reliability of findings with detailed confidence metrics
Customizable Reports: Generate comprehensive reports in multiple formats (HTML, JSON, TXT)
Rate Limiting: Built-in protections to respect service limitations and avoid blocking
Proxy Support: Configurable proxy settings for anonymity and geolocation flexibility
Use Cases
Building Threat Actor Profiles: Gather comprehensive information about potential threat actors
Security Assessments: Evaluate an organization's OSINT exposure and security posture
Pre-Engagement Reconnaissance: Gather intelligence before security engagements
Digital Footprint Analysis: Help individuals understand and manage their online exposure
Phishing Infrastructure Detection: Identify domains and infrastructure used in phishing campaigns
Brand Protection: Monitor for impersonation and brand abuse
Corporate Intelligence: Gather public information about competitors or potential partners
Installation
Prerequisites
Rust 1.60 or higher
OpenSSL development libraries
pkg-config (for Unix-like systems)
Optional: Docker for containerized deployment
From Source
Clone the repository:

bash

Hide
git clone https://github.com/username/omnisint-collector.git
cd omnisint-collector
Build the project:

bash

Hide
cargo build --release
Install the binary:

bash

Hide
cargo install --path .
Using Docker
Build the Docker image:

bash

Hide
docker build -t omnisint-collector .
Run the container:

bash

Hide
docker run -v $(pwd)/config:/app/config -v $(pwd)/output:/app/output omnisint-collector
Configuration
OmniSINT Collector uses a JSON configuration file to control its behavior. Create a config.json file in the project directory or specify a custom path with the --config flag.

Example configuration:

json

Hide
{
  "api_keys": {
    "shodan": "YOUR_SHODAN_API_KEY",
    "virustotal": "YOUR_VIRUSTOTAL_API_KEY",
    "hunter": "YOUR_HUNTER_API_KEY"
  },
  "proxy_settings": {
    "enabled": false,
    "url": "socks5://127.0.0.1:9050",
    "username": null,
    "password": null
  },
  "rate_limits": {
    "username_discovery": {
      "requests_per_minute": 30,
      "burst": 5
    },
    "search_engine": {
      "requests_per_minute": 10,
      "burst": 2
    }
  },
  "modules": {
    "username_discovery": {
      "enabled": true,
      "platforms": ["twitter", "github", "instagram", "linkedin", "reddit"],
      "correlation_threshold": 0.7
    },
    "dark_web": {
      "enabled": true,
      "sources": ["breached_databases", "paste_sites", "forums"],
      "search_terms": []
    },
    "search_engine": {
      "enabled": true,
      "engines": ["google", "bing", "duckduckgo"],
      "dorks": [
        "site:{target}",
        "intitle:{target}",
        "intext:{target} password",
        "filetype:pdf intext:{target}"
      ],
      "max_results_per_dork": 20
    },
    "social_media": {
      "enabled": true,
      "platforms": ["twitter", "instagram", "facebook", "linkedin", "reddit"],
      "relationship_mapping": true,
      "max_depth": 2
    },
    "document_metadata": {
      "enabled": true,
      "file_types": ["pdf", "doc", "docx", "xls", "xlsx", "ppt", "pptx"],
      "extract_authors": true,
      "extract_creation_dates": true,
      "extract_software_info": true
    },
    "domain_intelligence": {
      "enabled": true,
      "gather_dns": true,
      "gather_whois": true,
      "gather_ssl_certs": true,
      "subdomain_enumeration": true,
      "max_subdomains": 100
    },
    "geospatial": {
      "enabled": true,
      "sources": ["social_media", "image_metadata", "ip_geolocation"],
      "visualization_enabled": true
    }
  },
  "output": {
    "format": "html",
    "directory": "output",
    "report_template": "templates/default.html",
    "include_confidence_scores": true
  },
  "user_agents": [
    "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4472.124 Safari/537.36",
    "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/14.1.1 Safari/605.1.15"
  ]
}
Usage
Basic Commands
bash

Hide
# Show help
omnisint-collector --help

# Collect intelligence on a username
omnisint-collector collect johndoe username

# Collect intelligence on an email address
omnisint-collector collect john.doe@example.com email

# Collect intelligence on a domain
omnisint-collector collect example.com domain

# Specify output format
omnisint-collector collect example.com domain --output json

# Use a custom configuration file
omnisint-collector collect example.com domain --config my-config.json
Examples
Investigate a username across multiple platforms:

bash

Hide
omnisint-collector collect techguru username
Check if an email has been exposed in data breaches:

bash

Hide
omnisint-collector collect security@company.com email
Analyze a domain's public footprint:

bash

Hide
omnisint-collector collect example.org domain
Module Details
Username Discovery
This module searches for username presence across various platforms and services:

Social networks (Twitter, Instagram, Facebook, etc.)
Professional networks (LinkedIn, GitHub, etc.)
Forums and discussion boards (Reddit, HackerNews, etc.)
Gaming platforms (Steam, Xbox, PSN, etc.)
Content creation platforms (YouTube, TikTok, etc.)
For each discovered account, the tool collects:

Profile URL
Account creation date (when available)
Last activity time (when available)
Associated data (bio, location, etc.)
Dark Web Monitoring
This module searches for target information across:

Known data breach databases
Paste sites (Pastebin, etc.)
Dark web forums and marketplaces
Credential dumps
The module extracts:

Leaked credentials
Personal information exposure
Mentions in hacking forums
Data breach involvement
Search Engine Intelligence
Leverages search engines with advanced dorks to find:

Documents containing target information
Mentions in websites and news
Exposed sensitive information
Digital footprints
Supports custom dork patterns with target variable substitution.

Social Media Analysis
Performs in-depth analysis of social profiles:

Profile information extraction
Post content analysis
Connection/relationship mapping
Sentiment analysis
Location data extraction
Temporal activity patterns
Document Metadata Extraction
Identifies and analyzes publicly accessible documents:

Author information
Creation and modification dates
Software used
Organization information
Hidden metadata
Extracted text content
Domain Intelligence
Gathers comprehensive information about domains:

WHOIS data (registrar, dates, contacts)
DNS records (A, AAAA, MX, TXT, etc.)
SSL certificate information
Subdomain enumeration
Related IP addresses
Technology stack identification
Geospatial Analysis
Correlates location data from multiple sources:

Social media check-ins and posts
Image EXIF data
IP geolocation
Mentioned locations in content
Visualization on interactive maps
Output Formats
OmniSINT Collector supports multiple output formats:

HTML: Interactive reports with visualizations
JSON: Structured data for programmatic processing
TXT: Plain text reports for quick review
Reports include:

Executive summary
Key findings
Risk assessment
Detailed findings by module
Confidence scores
Recommendations
API Integration
OmniSINT Collector can be integrated with other tools through its API:

rust

Hide
// Example Rust code for API integration
let collector = OmniSINTCollector::new("config.json").await?;
let report = collector.collect_intelligence("target", "username").await?;
let json_report = collector.generate_report(&report, "json").await?;
Security and Privacy
OmniSINT Collector is designed with security and privacy in mind:

Only collects publicly available information
Respects robots.txt and rate limits
Uses proxies to prevent IP blocking
Securely stores API keys and credentials
Includes options to redact sensitive information in reports
Performance Considerations
Rate Limiting: Built-in rate limiting prevents overloading services
Parallel Processing: Uses Rust's async capabilities for efficient concurrent operations
Resource Usage: Configurable to limit CPU and memory consumption
Large Targets: Special handling for targets with extensive digital footprints
Contributing
Contributions are welcome! Please see CONTRIBUTING.md for details on:

Code of conduct
Development setup
Submission guidelines
Adding new platforms
Improving detection algorithms
Roadmap
Future development plans include:

Q3 2025: Add blockchain address analysis
Q4 2025: Implement machine learning for entity correlation
Q1 2026: Add automated report generation with GPT integration
Q2 2026: Develop real-time monitoring capabilities
Q3 2026: Implement browser extension for on-demand intelligence gathering
Legal Disclaimer
OmniSINT Collector is designed for legitimate security research, penetration testing, and personal digital footprint assessment. Users are responsible for ensuring they comply with applicable laws and regulations.

This tool should only be used:

With proper authorization
For legitimate security purposes
In accordance with relevant privacy laws
Within the terms of service of queried platforms
License
This project is licensed under the MIT License - see the LICENSE file for details.

plaintext

Hide
MIT License

Copyright (c) 2025 OmniSINT Project

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
