# Researching Project management in Github (Workflows)

I've been feeling out PM throught GitHub more or less intuitivly, and manageing it, though I was missing some of the automation tools, Namely getting commits to automatically appear on issues when a branch was created to work on that issue. I had been poking around the settings for a while and *saw* the workflows more than once but didn't spend long enough exploring the options, as it was earlier on before wanting to track more than just one project of mine. I asked Co-Pilot how I would be able to accomplish this: 

---

## Co Pilot
To have commits (such as branch activity or PRs) automatically tracked in the action timeline for an issue in a GitHub Project, you should use the built-in automations and workflows in Projects. Here’s how you can set this up:

### 1. Use Built-In Project Automations
GitHub Projects include built-in workflows that can automate status updates based on events, such as when a pull request is opened, merged, or an issue is closed. These automations will update the project status and timeline automatically for any linked issues or pull requests.

- Navigate to your project.
- Click the menu icon (three lines) in the top-right.
- Click **Workflows** in the menu.
- Under "Default workflows," select the workflow you want to edit (for example, tracking PRs or issues).
- Click **Edit** to configure it.
- Save and enable the workflow.

You can set workflows to update the status or archive issues/prs based on events like branch creation, PR open/merge, issue closure, etc. For more, see ["Using the built-in automations"](https://docs.github.com/en/issues/planning-and-tracking-with-projects/automating-your-project/using-the-built-in-automations).

### 2. Automatically Add Items to Projects
You can configure your project to automatically add new pull requests or issues that match specific filters (for example, a branch created from an issue or a PR referencing an issue).

- In your project, go to **Workflows**.
- Click on **Auto-add to project**.
- Select the repository and set a filter (e.g., `is:pr` or `label:bug`).
- Save and turn on the workflow.

This will ensure new matching items are added to your project and tracked in the timeline. See ["Adding items automatically"](https://docs.github.com/en/issues/planning-and-tracking-with-projects/automating-your-project/adding-items-automatically).

### Important Notes:
- Built-in workflows do not retroactively add existing items—only new or updated items that match your filter.
- For tracking branch-specific activity, ensure your PRs or branches mention the relevant issue (e.g., "Fixes #123") so they are cross-linked.
- The project timeline will show actions as items move through statuses automatically, based on your workflow configurations.

For detailed steps and screenshots, refer to:
- [Using the built-in automations](https://docs.github.com/en/issues/planning-and-tracking-with-projects/automating-your-project/using-the-built-in-automations)
- [Adding items automatically](https://docs.github.com/en/issues/planning-and-tracking-with-projects/automating-your-project/adding-items-automatically)

---

## Thoghts (My own Human ones)

Firstly, It seems like the 'every commit' is something that is not exactly doable with the *built in* automation, but this leads me to think maybe I'll create a sub-issue for creating my own automation using a repo key and a precommit setup (another issue, brushup with the precomit configs). 
Secondly, I guess I was a little spoiled with the premium Jira setup I'm coming from. I *do* have a gittea instance up an running that I host. I bet that the PM experience is not as limited (1 automation only for a non premimum Github subscription). While I want to continue to learn and become femilliar with a wider rage of PM and DevOps tools I am always going to be tempted to want to selfhost these things so I can sys-admin them as well.

Well, Let me grab the openapi json for the GitHub API and see if I can't end-run some automation. For the meantime I will save my free automation for another time, but I'm pretty confident that I can automate this with a little AI even.

The PLAN (before I research any further)

1. [ ] Create a token with limited control for testing store as AUTOMATION_TEST_GH_TOKEN in a new PowerShell Profile Global ENV (Yes I like Microsoft for development)
2. [ ] Map the GitHub API OpenAPI Json through my [SchemaVis](https://gist.github.com/Willmo103/c650045b4d5526b716ff8025a07e753e) tool to create Pydantic Models and create a folder to house the models [in this repo](../Code/01-GitHubAPIAutomation/github_models.py)
3. [ ] Explore the models and create some tests for basic commands, basically play around and see what's possible


