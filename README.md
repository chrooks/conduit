# Conduit Note Aggregator

Conduit is a cross-platform note aggregation system designed to solve the problem of scattered notes across different formats and platforms. It provides a centralized repository for all notes with powerful organization, search, and integration capabilities.

## Memory Bank

This project uses a Memory Bank approach to maintain documentation and project knowledge. The Memory Bank consists of the following core files:

- `projectbrief.md` - Foundation document defining core requirements and goals
- `productContext.md` - Why this project exists and how it should work
- `systemPatterns.md` - System architecture and design patterns
- `techContext.md` - Technologies used and development setup
- `activeContext.md` - Current work focus and next steps
- `progress.md` - What works, what's left to build, and current status

## Sprint Planning and GitHub Issues

This project uses GitHub Issues to track tasks from sprint plans. A GitHub Actions workflow has been set up to automatically create issues from the sprint plans defined in `memory-bank/progress.md`.

### How to Use the GitHub Actions Workflow

The workflow can be triggered in two ways:

1. **Automatically**: When changes are pushed to `memory-bank/progress.md` on the main branch
2. **Manually**: Through the GitHub Actions UI

#### Manual Trigger

To manually trigger the workflow:

1. Go to the "Actions" tab in your GitHub repository
2. Select the "Create Sprint Issues" workflow
3. Click "Run workflow"
4. Configure the following options:
   - **Sprint number**: Select which sprint to process (1-5), or leave empty to process all sprints
   - **Create/update GitHub Project**: Whether to create or update a GitHub Project
   - **GitHub Project name**: The name of the GitHub Project to use

#### Required Permissions

The workflow requires the following permissions:

1. `issues: write` - To create and update issues
2. `project: write` - To create and update projects (if using the project feature)

You may need to update the repository settings to grant these permissions to GitHub Actions.

### How It Works

The workflow:

1. Reads the `memory-bank/progress.md` file
2. Extracts tasks from the specified sprint section(s)
3. Creates GitHub issues for each task that doesn't already exist
4. Optionally adds the issues to a GitHub Project
5. Labels issues with `sprint-X` and `automated` labels

### Customizing the Workflow

You can customize the workflow by editing the `.github/workflows/create-sprint-issues.yml` file:

- Change the trigger conditions
- Modify the issue format
- Adjust the project integration
- Add additional labels or metadata

## Development Setup

See `memory-bank/techContext.md` for detailed information on the development setup and technical stack.

## Project Status

See `memory-bank/progress.md` for the current project status and upcoming work.
