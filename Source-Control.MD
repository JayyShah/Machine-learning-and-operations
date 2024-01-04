# OverView:

- One important part of machine learning operations or MLOps is model reproducibility. To make a model reproducible, you need to document everything you did to train a model so that anyone can reproduce your steps.

- Next to that, parts of your work may be reusable for other models that need to be trained. It's therefore essential to centrally manage the code you write to train a model. By using source control (or version control) to manage your code, you can easily save, version, share, and reuse any code you create.

# Repositories and Truck-based Development

- Many data scientists prefer working with Python or R to define machine learning workloads. You can have Jupyter notebooks or scripts to prepare data or train a model.

- Working on any code assets becomes easier when you use source control. Source control is the practice of managing code and tracking any changes your team makes to the code.

- If you work with DevOps tools like Azure DevOps or GitHub, the code is stored in a so-called repository or repo.

## Repository

- When setting up the MLOps framework, a machine learning engineer is likely to create the repository. Whether you choose to use Azure Repos in Azure DevOps or GitHub repos, both use Git repositories to store your code.

- There are generally two ways to scope the repo:

    - Monorepo: Keep all machine learning workloads within the same repo.
    - Multiple repos: Create a separate repo for each new machine learning project.

- Which approach your team prefers depends on who should get access to which assets. If you want to ensure quick access to all code assets, monorepos may suit your team's requirements better. If you want to only give people access to a project if they're actively working on it, your team may prefer to work with multiple repos. Keep in mind that managing access control can create more overhead.

## Structure your repo

- Whatever approach you take, it's best practice to agree on the standard top-level folder structure for your projects. For example, you may have the following folders in all your repos:

    - (`.cloud`): contains cloud-specific code like templates to create an Azure Machine Learning workspace.
    - (`.ad/.github`): contains Azure DevOps or GitHub artifacts like YAML pipelines to automate workflows.
    - (`src`): contains any code (Python or R scripts) used for machine learning workloads like preprocessing data or model training.
    - (`docs`): contains any Markdown files or other documentation used to describe the project.
    - (`pipelines`): contains Azure Machine Learning pipelines definitions.
    - (`tests`): contains unit and integration tests used to detect bugs and issues in your code.
    - (`notebooks`): contains Jupyter notebooks, mostly used for experimentation.

*Note*: *Training data should not be included in your repo. The data should be stored in a database or data lake. Azure Machine Learning can have direct access to a database or data lake by storing the connection information as a datastore.*

## Trunk based Developmemt

- Most software development projects use Git as a source control system, which is used by both Azure DevOps and GitHub.

- The main benefit of using Git is the easy collaboration on code while also keeping track of any changes that are made. In addition, you can add approval gates to make sure only changes that have been reviewed and accepted will be made to the production code.

- To accomplish the above, Git makes use of trunk-based development which allows you to create branches.

- The production code is hosted in the main branch. Whenever someone wants to make a change:

    1. You create a full copy of the production code by creating a branch.
    2. In the branch you created, you make any changes and test them.
    3. Once the changes in your branch are ready, you can ask for someone to review the changes.
    4. If the changes are approved, you merge the branch you created with the main repo and the production code will be updated to reflect your changes.

# Work With Azure Repos and Github Repos

- Although you can make changes directly to the main code, it's best practice to use trunk-based development. By working with branches, it's easier to verify whether your changes work as expected before merging them with the main code.

## Agile Planning

- After the initial model development, you'll have a model in production. Just like any application, a model isn't static and may require small or large tweaks over time to ensure it's up-to-date. A reason for updating and retraining the model may be detected data drift causing the model to not perform as expected anymore. Data can change over time, and accordingly, models may need to change over time too.

- To plan and organize the work you need to do as a data scientist, you can use Azure Boards in Azure DevOps or GitHub issues.

## Azure DevOps

- Azure Boards organizes agile planning by work item tracking, visualization, and reporting. You can customize many things to make it fit your project planning.

- Most importantly for a data scientist, you'll get a work item assigned to you to inform you on what you need to do to contribute to the machine learning project. To organize your work, you'll link a work item to a new branch.

- Imagine you're a data scientist working on a machine learning project. The team has a backlog of work items or product backlog items, which are grouped by feature or machine learning lifecycle phase.

- Another way to view the work items for this project is by navigating to Boards. Typically, you'll have columns for new, active, and closed work items. Or tasks that you still need to do, that you're doing, or that are done.

- To pick up a work item and to let your team know you're working on it, you (or someone else) can assign a work item to you. Select the Unassigned box and select your name.

- In the Development control pane, you can select create a branch to create a new branch in the repo, which will automatically be linked to your work item. Once created, you'll be redirected to the new branch where you can view all assets stored in your repository.

- Now that the branch is created, you can work in the branch to make any changes to the code. It's common practice that you clone the branch to an Integrated Development Environment (IDE) like Visual Studio Code to develop and test locally before committing and pushing the changes to the main repo.

## Github

- GitHub is an open-source platform on which all tools are organized per repository. Once you've created a repository, you can use GitHub issues to track your work items, feedback, and bugs.

- When opening a repo in GitHub, you can navigate to the Issues tab to view all open and closed issues. You can select an issue to view its details. The person creating the issue can describe the problem, adding code snippets or screenshots.

- After an issue is created, you'll be able to assign the work to yourself or another GitHub user. If you want to work on the issue, you can create a branch from the Development control.

- A pane will open to help you create a branch that will be linked to the issue. Automatically, the branch will have the name of the issue's title. You can change the branch name if you want.

- If you navigate back to the Code tab to view your repo, you'll be able to switch between branches and see the new branch you've created.

-  Once you've picked up a work item in Azure DevOps or an issue in GitHub, and created a branch to edit the code, you'll want to develop the code locally. You can clone the Git repo from either Azure DevOps or GitHub and work from any IDE you prefer.

# Develop Locally with Visual Studio Code

- To ensure a model stays relevant, you may have to edit any of the assets within a machine learning project.

- For example, you may have to retrain a model with an improved training dataset. Or you may have to improve the model by choosing other hyperparameter values while training.

- As a data scientist, whenever you want to go back to develop and improve the model, you want to ensure the model in production remains untouched. Therefore, when storing all code relevant for the machine learning project in a Git repo, you want to create a branch for development to isolate your work.

- To work on the branch, you can clone the branch to your preferred IDE. You'll learn how you can clone the code and develop locally with Visual Studio Code.

## Development Process

- After opening Visual Studio Code, there are two ways to work with Git:

    - `Use the command palette (CTRL+SHIFT+P)` for a more user-friendly approach.
    - `Use git commands in the integrated terminal (CTRL+SHIFT+`)` for a command-line experience.

### Clone

- To get a local copy, you'll have to clone the repo to your device using the repo's URL.

    - `Git:clone <enter-the-url>` 
    - A local copy of the code will be stored on your device. Choose where you want to store the clone and wait until all files have been copied. When ready, you'll be prompted to navigate to the newly copied repo directly. Alternatively, you can open the local folder in Visual Studio Code to open the local copy.

### Commit

- Once you've cloned the repo to Visual Studio Code, you can edit the code. After modifying a file and saving it, you'll need to commit the change.

- In Visual Studio Code, you can open the Source Control tab to view all changes you've made so far.

- You can commit a change made to a file, like a Python script, by using the Git: Commit option in the command palette or by using the git commit command.

- For each commit, you'll add a message to clarify what you changed. In general, it's best to commit small changes and do it often. By writing clear committing messages, you'll make it easier for your team to understand your work.

### Push

- Once you've made all your changes and committed them. You can push all commits. When you push all your commits, you'll update the repo stored in Azure Repos or GitHub to be identical to your local copy.

- You can push all commits with the Git: Push option in the command palette, or the git push command in the terminal.

- Alternatively, you can also push changes using the Source Control pane. In Source Control, you'll also get an overview of how many commits will be pushed to your repo.

- Ideally, you should verify your code before pushing it to the repo. To verify machine learning workloads, it's a best practice to do linting and unit tests locally.

*Note* : *If someone else has made a change to the repo while you've been working online, you can pull those changes to your local copy without losing your changes and commits. Git will check whether there are any clashes for you.*

# Verify Your Code Locally

- Whenever you change any code in your machine learning project, you want to verify the code and model quality.

- During continuous integration, you create and verify assets for your application. As a data scientist, you'll probably focus on creating scripts used for data preparation and model training. The machine learning engineer uses the scripts later in pipelines to automate these processes.

- To verify your scripts, there are two common tasks:

    - Linting: Check for programmatic or stylistic errors in Python or R scripts.
    - Unit testing: Check the performance of the content of the scripts.

- By verifying your code, you prevent bugs or issues when the model is deployed. You can verify your code locally, by running linters and unit tests locally in an IDE like Visual Studio Code.

- You can also run linters and unit tests in an automated workflow with Azure Pipelines or GitHub Actions.

### Lint Your code

- The quality of your code depends on the standards you and your team agree on. To ensure that the agreed upon quality is met, you can run linters that will check whether the code conforms to the standards of the team.

- Depending on the code language you use, there are several options to lint your code. For example, if you work with Python, you can use either Flake8 or Pylint.

### Use Flake8 to lint your code

- To use Flake8 locally with Visual Studio Code:

    1. Install Flake8 with pip install flake8.
    2. Create a configuration file .flake8 and store the file in your repo.
    3. Configure Visual Studio Code to use Flake8 as the linter by going to your settings (Ctrl+,).
    4. Search for flake8.
    5. Enable Python > Linting > Flake8 Enabled.
    6. Set the Flake8 path to the location in your repo where you stored your .flake8 file.

- To specify what your team's standards are for code quality, you can configure the Flake8 linter. A common method to define the standards is by creating a .flake8 file that is stored with your code.

- The .flake8 file should start with [flake8], followed by any of the configurations you want to use.

- Flake8 has a predefined list of errors it can return. Additionally, you can make use of error codes that are based on the PEP 8 style guide. For example, you can include error codes that refer to proper use of indentation or white spaces.

- You can choose to either select (select) a set of error codes that will be part of the linter or select which error codes to ignore (ignore) from the default list of options.

- When you've configured Visual Studio Code to lint your code, you can open any code file to review the lint results. Any warnings or errors will be underlined. You can select View problem to inspect the issue to understand the error.

### Lint with Azure Pipelines or Github Actions

- You can also run the linter automatically with Azure Pipelines or GitHub Actions. The agent provided by either platform will run the linter when you:

    1. Create a configuration file .flake8 and store the file in your repo.
    2. Define the continuous integration pipeline or workflow in YAML.
    3. As a task or step, install Flake8 with python -m pip install flake8.
    4. As a task or step, run the flake8 command to lint your code.

### Unit Tests

- Where linting verifies how you wrote the code, unit tests check how your code works. Units refer to the code you create. Unit testing is therefore also known as code testing.

- As a best practice, your code should exist mostly out of functions. Whether you've created functions to prepare data, or to train a model. You can apply unit testing to, for example:

    1. Check that column names are right.
    2. Check the prediction level of model on new datasets.
    3. Check the distribution of prediction levels.

- Imagine you created a training script train.py. Assume you stored the training script in the directory src/model/train.py within your repo. To test the train_model function, you must import the function from src.model.train.

- You create the test_train.py file in the tests folder. One way to test Python code is to use numpy. Numpy offers several assert functions to compare arrays, strings, objects, or items.

- For example, to test the train_model function, you can use a small training dataset and use assert to verify whether the predictions are almost equal to your predefined performance metrics.

- To test your code in Visual Studio Code using the UI:

    1. Install all necessary libraries to run the training script.
    2. Ensure pytest is installed and enabled within Visual Studio Code.
    3. Install the Python extension for Visual Studio Code.
    4. Select the train.py script you want to test.
    5. Select the Testing tab from the left menu.
    6. Configure Python testing by selecting pytest and setting the test directory to your tests/ folder.
    7. Run all tests by selecting the play button and review the results.

- To run the test in an Azure DevOps Pipeline or GitHub Action:

    1. Ensure all necessary libraries are installed to run the training script. Ideally, use a requirements.txt listing all libraries with pip install -r requirements.txt
    2. Install pytest with pip install pytest
    3. Run the tests with pytest tests/
    4. The results of the tests will show in the output of the pipeline or workflow you run.

*Note* : *If either during linting or unit testing, an error is returned, the CI pipeline may fail. It's therefore better to verify your code locally first, before triggering the CI pipeline.*

