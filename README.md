# AutoBlog

Automatically generate blog posts from your GitHub repositories and publish them to your Hugo blog site.

## Features

- 🤖 Automatically discovers your new GitHub repositories
- ✍️ Generates blog posts using AI (via OpenRouter) or a fallback method
- 📚 Saves posts to your Obsidian vault
- 🚀 Syncs with your Hugo blog and deploys changes
- 🔄 Keeps track of processed repositories to avoid duplication

## Prerequisites

- Python 3.6+
- GitHub account with repositories
- Obsidian vault setup
- Hugo blog setup
- (Optional) OpenRouter API key for AI-generated content

## Installation

1. Clone this repository:
   ```bash
   git clone https://github.com/yourusername/autoblog.git
   cd autoblog
   ```

2. Install required packages:
   ```bash
   pip install -r requirements.txt
   ```

3. Create a `.env` file based on the provided `.env-example`:
   ```bash
   cp .env-example .env
   ```

4. Fill in your configuration values in the `.env` file

## Configuration

Edit the `.env` file with your specific details:

```
# GitHub settings
GITHUB_TOKEN=your_github_personal_access_token
GITHUB_USERNAME=your_github_username

# Path settings
OBSIDIAN_VAULT_PATH=C:/path/to/your/obsidian/vault
BLOG_REPO_PATH=C:/path/to/your/blog/repository

# OpenRouter settings
OPENROUTER_API_KEY=your_openrouter_api_key  # Optional
```

### GitHub Token Setup

1. Go to GitHub → Settings → Developer settings → Personal access tokens → Tokens (classic)
2. Click "Generate new token" → "Generate new token (classic)"
3. Give your token a name and select these scopes:
   - `repo` (Full control of private repositories)
   - `read:user` (Read user information)
4. Click "Generate token" and copy it immediately
5. Add it to your `.env` file as `GITHUB_TOKEN`

### Path Configuration

- `OBSIDIAN_VAULT_PATH`: Full path to your Obsidian vault's blog posts folder
  - Use forward slashes `/` instead of backslashes `\`
  - If path contains spaces, wrap in quotes: `"C:/Path With Spaces/Blog"`

- `BLOG_REPO_PATH`: Path to your Hugo blog repository
  - Must be a git repository
  - Should contain Hugo's content structure

### OpenRouter Setup (Optional)

1. Register at [openrouter.ai](https://openrouter.ai/)
2. Get your API key from Dashboard → API Keys
3. Add to `.env` as `OPENROUTER_API_KEY`

## Usage

### Basic Usage

Run with the batch file:
```bash
run.bat
```

Or directly with Python:
```bash
python main.py
```

### Command Line Options

- Process repos after a specific date:
  ```bash
  python main.py --date 2023-01-01
  ```

### Workflow

1. **Repository Discovery**
   - Scans your GitHub account for repositories
   - Checks for README.md files
   - Compares against previously processed repos

2. **Content Generation**
   - Attempts AI generation with OpenRouter
   - Falls back to template-based generation if AI fails
   - Extracts:
     - Repository description
     - Code samples (up to 5 files)
     - Language statistics
     - Tags from README content

3. **Content Management**
   - Saves to Obsidian vault with date prefix
   - Syncs to Hugo content directory
   - Updates processed_repos.json

4. **Publishing**
   - Builds Hugo site
   - Commits changes
   - Pushes to blog repository

## Advanced Configuration

### Blog Post Template

Modify `config.py` to customize the blog post template:
```python
blog_post_template = """---
title: "{title}"
date: {date}
draft: false
tags: [{tags}]
---
// ... customize your template
"""
```

### AI Content Generation

Adjust in `blog_generator.py`:
- Change AI model
- Modify prompt
- Adjust temperature (creativity)
- Set token limits

### File Organization

- `processed_repos.json`: Tracks processed repositories
- Generated files: `YYYY-MM-DD-repo-name.md`
- Hugo integration: Posts appear in `content/posts/`

## Troubleshooting

### Common Issues

1. **Path Issues**
   - Use forward slashes `/` in paths
   - Wrap paths with spaces in quotes
   - Verify paths exist before running

2. **GitHub API Issues**
   - Check token permissions
   - Verify token hasn't expired
   - Ensure username is correct

3. **Hugo Integration**
   - Verify Hugo is installed and in PATH
   - Check Hugo content directory structure
   - Ensure git repository is properly initialized

4. **OpenRouter Issues**
   - Verify API key is valid
   - Check API rate limits
   - Monitor usage quotas

### Error Messages

- "No module named 'dotenv'": Run `pip install python-dotenv`
- "Invalid token": Regenerate GitHub token
- "Path does not exist": Check path configurations
- "Hugo build failed": Verify Hugo installation

## Contributing

1. Fork the repository
2. Create a feature branch
3. Commit your changes
4. Push to your branch
5. Create a Pull Request

## License

MIT License - See LICENSE file for details

## Support

- Create an issue for bugs
- Pull requests welcome
- Star the repository if you find it useful

## Acknowledgments

- Built with Python and GitHub API
- Uses OpenRouter for AI content
- Integrates with Hugo and Obsidian

