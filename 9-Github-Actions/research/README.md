# Creating Github Actions

In the past few months I've had copilot or whichever Chat AI Interface create a github actions workflow for me, or configured it from a template without *realy* understanding what was going on or why the suggested workflows didn't exactly work for my use cases.

The Goal with this personal development task is to fully grasp how to preform github testing anc CICD automation from both the server-side: Github Actions, and from the developer side a la precommit and build scripts. This interlaces with the other current learning goals which is to track my personal projects using github Projects as well as the rabbithole things I fall into (This Repo)

## Starting with Gemini

I Had a chat running where I was geting some tips on debuggig a portion of my testing module for Wembed, I wanted to see if it would give me a simple refrence document (in my personal flavor) but since it already had canvas open it just wrote me files to run my project, no dice.

In a new chat window; "I need to understand the in's and outs of how to configure a github actions workflow" Intentially leaving it vague and letting my stored instructions guide the general response (Using flash for this).

THe Response:

A GitHub Actions workflow is an automated process defined in a **YAML** file within the `.github/workflows` directory of your repository. It's triggered by specific events, such as a push to a branch or a pull request, and runs a series of jobs. Each job consists of one or more steps that execute commands or actions.

-----

### Anatomy of a Workflow File

A workflow file is structured hierarchically. Here's a breakdown of the key components:

  * **`name`**: A user-friendly name for your workflow. It appears on the Actions tab of your repository.

  * **`on`**: Defines the events that trigger the workflow. This can be a single event like `push`, an array of events like `[push, pull_request]`, or a more complex configuration specifying branches or paths.

      * **Example**:

    <!-- end list -->

    ```yaml
    on:
      push:
        branches:
          - main
      pull_request:
        types:
          - opened
          - synchronize
    ```

  * **`jobs`**: A map of jobs that run in the workflow. By default, jobs run in parallel, but you can configure them to run sequentially using the `needs` keyword. Each job has an `id` and its own configuration.

      * **`runs-on`**: Specifies the type of runner (virtual machine) the job will run on. Common options include `ubuntu-latest`, `windows-latest`, and `macos-latest`.
      * **`steps`**: An ordered list of steps that a job will execute. A step can be a shell command or a pre-built action from the GitHub Marketplace.
          * **`name`**: A name for the step.
          * **`uses`**: Specifies a GitHub Action to use. Actions are reusable code that simplifies tasks. For example, `actions/checkout@v4` checks out your repository's code.
          * **`run`**: Executes a command in the shell of the runner.

-----

### Key Concepts

  * **Actions**: Actions are the building blocks of a workflow. They can be developed by the community, by GitHub, or by you. The `uses` keyword references an action, typically in the format `owner/repo@version`.
  * **Runners**: These are the servers where your workflows run. GitHub provides hosted runners (`ubuntu-latest`, `windows-latest`, `macos-latest`) which are free for public repositories. You can also use self-hosted runners for more specific environments.
  * **Contexts**: Workflows have access to various contexts that provide information about the run, the repository, and the environment. Some common contexts include:
      * **`github`**: Information about the event that triggered the workflow. For example, `github.event.pull_request.head.ref` gets the head branch of a pull request.
      * **`env`**: Environment variables. You can set them at the workflow, job, or step level.
      * **`secrets`**: Sensitive information stored securely in the repository or organization settings. Access them with `secrets.MY_SECRET`.
  * **Artifacts**: Files generated during a workflow run that you can save and share between jobs or download. The `actions/upload-artifact` and `actions/download-artifact` actions are used for this purpose.

-----

### Example Workflow: Basic Build and Test

Here's a simple workflow to illustrate these concepts. This workflow runs on every push to the `main` branch, checks out the code, sets up Python, installs dependencies, and runs tests.

```yaml
name: Python CI

on:
  push:
    branches:
      - main
  pull_request:
    branches:
      - main

jobs:
  build_and_test:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout repository
        uses: actions/checkout@v4
        
      - name: Setup Python
        uses: actions/setup-python@v5
        with:
          python-version: '3.10'
          
      - name: Install dependencies
        run: |
          python -m pip install --upgrade pip
          pip install -r requirements.txt
          
      - name: Run tests
        run: pytest
```
