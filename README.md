# Level Up Lab

A multi-channel content platform for learning and sharing knowledge on my journey as a "maker of things".

## Project Overview

This project develops and manages content across multiple platforms to document, teach, and engage with others on maker topics. The content strategy focuses on broadcasting learning journeys while facilitating community engagement and discussion.

## Target Platforms

### Broadcast Platforms (Primary Content)
- **YouTube**: Video tutorials, project walkthroughs, and educational content
- **Podcast Platform**: Audio discussions, interviews, and deep-dives into maker topics

### Engagement Platforms (Links & Q&A)
- **Facebook**: Community updates and discussion threads
- **Discord**: Real-time community interaction and support
- **Forums**: In-depth technical discussions and troubleshooting
- **Blog Platform**: Written guides, project documentation, and reflections (Hugo-powered static site)

## Hugo Blog

The blog is set up with Hugo static site generator for publishing to GitHub Pages. 

**Quick Start:**
- Read the [HUGO_QUICKSTART.md](HUGO_QUICKSTART.md) for a quick introduction
- See [AUTHORING_GUIDE.md](AUTHORING_GUIDE.md) for complete authoring instructions
- See [PUBLISHING_GUIDE.md](PUBLISHING_GUIDE.md) for deployment instructions

**Key Commands:**
```bash
# Create a new blog post
hugo new content/blog/posts/my-post.md

# Preview locally
hugo server -D

# Publish (automatic via GitHub Actions on push to main)
git push origin main
```

## Content Strategy

### Broadcast Content
YouTube and podcast platforms serve as the primary content hubs where in-depth learning content is created and shared. This includes:
- Tutorial series
- Project documentation
- Learning journey narratives
- Interviews with other makers
- Tool and technique demonstrations

### Engagement Content
Other platforms link back to broadcast content and facilitate:
- Question and answer sessions
- Community discussions
- Troubleshooting help
- Sharing user projects
- Building a maker community

## Repository Structure

- `/content/` - Content planning and scripts
- `/templates/` - Templates for different content types
- `/guidelines/` - Platform-specific guidelines and best practices
- `/calendar/` - Content calendar and scheduling

## Getting Started

See the documentation in each folder for specific guidelines on creating and managing content for different platforms.
