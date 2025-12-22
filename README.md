# Patent

Patent invention creation project

## Overview

This repository manages patent inventions created using the [Patent Assistant](https://github.com/namtoki/claude-code-marketplace) plugin.

## Tools Used

### Patent Assistant

This project uses the Patent Assistant plugin available from [Claude Code Marketplace](https://github.com/namtoki/claude-code-marketplace).

```bash
# Installation
claude plugins:install patent-assistant --registry namtoki-plugins
```

Patent Assistant provides an automated invention creation process through the following agents:

| Agent | Role |
|-------|------|
| patent_input | Analyze user input and determine project name |
| patent_secretary | Project management and documentation |
| patent_searcher | USPTO prior art search |
| patent_analyzer | Novelty and inventive step analysis |
| patent_adviser | Improvement suggestions |
| patent_document | Invention document creation |
| patent_auditor | Final audit |

## Projects

| Project | Description | Status |
|---------|-------------|--------|
| [patent_auracast_map](./patent_auracast_map/) | Auracast broadcast information map display system | Completed - Filing recommended |

## Usage

```bash
# Start the invention creation process
/patent-assistant:run "Enter your invention idea"
```

## License

The contents of this repository should be treated as confidential information.
