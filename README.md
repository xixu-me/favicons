# Favicons

A repository of favicons for the top domains on the internet, automatically updated on a weekly basis.

## Overview

This repository hosts a collection of favicon images for the world's most popular domains, sourced from Google's favicon service. The collection is refreshed weekly and available in several formats:

- Individual PNG files in the `assets` branch
- Compressed archives of various sizes in the Releases section
- Custom builds via manual workflow triggers

## Direct Usage

### Access Individual Favicons

Individual favicons are stored in the `assets` branch and are named according to their second-level domain:

- `google.png` for google.com
- `github.png` for github.com

Access patterns:

```
https://raw.githubusercontent.com/xixu-me/favicons/assets/DOMAIN_NAME.png
```

### Download Compressed Archives

Pre-built archives are available in the [Releases](https://github.com/xixu-me/favicons/releases) section:

1. Navigate to the Releases page
2. Find the desired release (named by date and domain count)
3. Download the `archive.tzst` file
4. Extract using the [tzst](https://github.com/xixu-me/tzst):

```bash
# Install tzst if you don't have it
pip install tzst

# Extract the archive
tzst x archive.tzst
```

### Available Archive Sizes

Archives are available with the following domain counts:

- 200 (minimal)
- 500
- 1,000
- 2,000
- 5,000
- 10,000
- 20,000
- 50,000
- 100,000
- 200,000
- 500,000
- 1,000,000 (complete set)

## Self-Build Instructions

### Fork the Repository

1. Click the Fork button at the top right of this repository
2. Clone your forked repository:

   ```bash
   git clone https://github.com/xixu-me/favicons.git
   cd favicons
   ```

### Configure Required Secrets

This workflow requires a Cloudflare API token to access the domain ranking data:

1. Go to your fork's Settings > Secrets and variables > Actions
2. Create a new repository secret:
   - Name: `CLOUDFLARE_API_TOKEN`
   - Value: Your Cloudflare API token with Radar access

### Run the Workflow Manually

1. Go to the Actions tab in your repository
2. Select "The Workflow" from the list of workflows
3. Click "Run workflow"
4. Select the desired domain count from the dropdown
5. Click "Run workflow" to start the build

The workflow will:

1. Validate your input
2. Fetch the top domains from Cloudflare Radar
3. Download favicons for each domain
4. Commit the favicons to the `assets` branch
5. Create a compressed archive
6. Create a release with the archive

### Customize the Workflow

You can modify the run.yml file to change:

- The schedule (currently weekly on Sundays)
- The favicon source URL
- The error handling logic
- The naming conventions

## Technical Details

### File Naming

Favicons are named based on the second-level domain:

- `example.com` → `example.png`
- `subdomain.example.com` → `example.png`

When duplicate second-level domains exist, sequential numbers are added:

- First `github.io` domain → `github.png`
- Second `github.io` domain → `github_1.png`

### Error Handling

The workflow includes:

- Timeout handling (15 seconds per favicon)
- Retry logic (3 attempts)
- Generic/default favicon detection
- Empty file detection
- High failure rate detection (stops if >80% of downloads fail)

## Disclaimers

### Copyright Notice

The favicon images are the property of their respective domain owners. This repository simply provides an aggregation service for easier access and does not claim ownership of any favicon images.

### Rate Limiting

This repository fetches favicons from Google's favicon service, which may impose rate limits. If you're running your own build and encounter high failure rates, try reducing the domain count or adding delays between requests.

### Data Accuracy

The top domains list is provided by Cloudflare Radar and represents their assessment of domain popularity. Domain rankings change over time and may not reflect the most current web traffic patterns.

### API Requirements

Running your own builds requires:

- A Cloudflare account
- API access to Cloudflare Radar
- A valid API token with appropriate permissions

## License

This project's code is licensed under the [MIT License](LICENSE). This license applies only to the code in this repository and not to the favicon images themselves.

## Acknowledgements

- Cloudflare Radar for providing domain ranking data
- Google's favicon service for providing the favicon images
- [tzst](https://github.com/xixu-me/tzst) for efficient compression

---

**Note**: This project is not affiliated with or endorsed by Cloudflare, Google, or any domain owners whose favicons are collected.
