# Overview:

- When you want to implement artificial intelligence (AI) at scale, automation plays a key part. The goal is to move from experimentation to production with machine learning operations (MLOps).

- There are several workloads that can be automated. To automate workloads, you'll create pipelines that group together tasks in a specific order. To automate the pipeline, you can run them at a schedule or trigger them based on an event.

# Azure Machine Learning Pipelines

- As a data scientist, you'll work primarily with Azure Machine Learning to train and manage models. After experimentation, you should convert your work into production Python code to allow for automation with Azure (DevOps) Pipelines or GitHub Actions.

## Experiment In Azure Machine Learning

- Azure Machine Learning provides a set of features that help you organize your work. For example, with Azure Machine Learning you can:

    1. Register datasets to easily reuse data stored in a data lake.
    2. Train a model on remote compute instances or clusters depending on your requirements.
    3. Track all your executed scripts with experiments to easily compare your work.
    4. Register trained models and deploy a model for batch or real-time consumption.

- Most of your work as a data scientist will consist of experimentation: testing different configurations to train a model and reviewing performance metrics to decide which model to deploy to production.

- Assuming you experiment in a Jupyter notebook (.ipynb files), you'll want to convert the experiment to production Python code by:

    - Removing all nonessential code.
    - Refactoring code into functions.
    - Combining related functions in Python scripts (.py files).
    - Creating unit tests for each Python script.
    - Create a pipeline to group scripts into a workflow that can be automated.

- Once your code is ready for production, you can automate the execution of scripts with Azure Machine Learning pipelines.

### Create Azure Machine Learning Pipelines

- The concept of a pipeline is found throughout various tools, often providing a way to group tasks in a certain order. The main advantage of a pipeline is that you can schedule it or trigger it to run.

- An Azure Machine Learning pipeline is created within the Azure Machine Learning workspace. To create a pipeline, you can define the steps with Python scripts.

- Optionally, you can create a pipeline with Azure Machine Learning components. When you create a component, the script will be stored with metadata like the necessary environment in the Azure Machine Learning workspace. Components can be shared and used by anyone within the same workspace, making it easier for others to quickly create new pipelines, building on your work.

- To create a pipeline that can be used for automation, it's recommended to define a pipeline job in YAML that can be triggered using a CLI (v2) command.

- The YAML file that defines the pipeline needs to specify the following information:

    - What to run: The steps defined as Python scripts or components.
    - How to run it: Any inputs or outputs the steps may expect.
    - Where to run it: The compute needed to execute the code (commonly an Azure Machine Learning compute cluster).

- Once the pipeline has finished executing, you can review the pipeline and its executed steps in the Azure Machine Learning workspace.

- When you convert your machine learning workloads to Python scripts and group tasks within a pipeline, your model will be ready for production. Defining the pipeline in a YAML file allows you to automate training and retraining by triggering the pipeline run with CLI (v2). You can run a CLI command, referring to the pipeline YAML file, from Azure (DevOps) Pipelines or GitHub Actions.

# Azure Pipelines

- One option to automate workflows is to use Azure Pipelines, which is part of the Azure DevOps Services. With Azure Pipelines, you can automatically build, test, and deploy your code.

- Within a machine learning project, you can use Azure Pipelines to create any Azure Machine learning workspace assets like the workspace itself, data assets, compute clusters, or jobs to run Azure Machine Learning pipelines.

### Create Azure Pipelines

- Azure Pipelines helps you to automate your work by executing steps whenever a trigger occurs. To use Azure Pipelines to automate machine learning workloads, you'll trigger an Azure Machine Learning pipeline with Azure Pipelines.

    1. Trigger an Azure Pipeline. Commonly with a change to the repo (commit or pull request).
    2. Run the Azure Pipeline, a group of jobs which consist of steps.
    3. A step initiates an Azure Machine Learning pipeline.
    4. An Azure Machine Learning pipeline runs scripts or Azure Machine Learning components.
    5. A script or component represents a machine learning task.

- To create the Azure Pipeline, you define the steps you want to include in a YAML file. In the YAML file of the Azure Pipeline, you'll include:

    - Trigger: What event initiates the pipeline.
    - Stage: A group of jobs commonly aligned with different development environments (dev/test/prod).
    - Job: A set of steps, which run on an agent. For machine learning workloads, you'll likely use a Microsoft-hosted Ubuntu agent.
    - Step: A script or task you want to execute. For example, a CLI command, which initiates an Azure Machine Learning pipeline (az ml job create).

### Run a Pipeline with Azure DevOps

- After you've created the YAML files and stored it in your Azure Repo, you can configure Azure DevOps to run the pipeline.

    1. Within Azure DevOps, navigate to the Pipelines tab and select Pipelines.
    2. Create a New pipeline.
    3. Select Azure Repos Git as the location of your code.
    4. Choose the repo that contains your code.
    5. Choose Existing Azure Pipelines YAML file.
    6. Choose the path that points to the YAML file you created for the Azure Pipeline.
    7. After you review the pipeline, you can Save and run.

- The pipeline is triggered by a commit to the main branch. When you configure the pipeline, Azure Pipelines will commit a change to the main branch, which will trigger the pipeline to run for the first time. Anytime after set-up, you can trigger the pipeline by pushing commits to the repo from Visual Studio Code or Azure Repos.

- When you select on a job, you can view its process. Each step in a job is reflected in the navigation pane on the left. The overview will show which steps ran successfully and which failed. Any potential error messages will show in the command line interface when you select that step. By reviewing the output, you'll be able to troubleshoot the error.

- When a task triggers an Azure Machine Learning pipeline to run, you'll also be able to review the pipeline run in the Azure Machine Learning workspace to view any metrics or errors that may be of interest to you.

# Github Actions

- When you want to automate workflows with GitHub, you use GitHub Actions.

- GitHub is primarily used to host code projects. When you host your machine learning code in a GitHub repository (repo), you can create GitHub Actions to automatically build, test, and deploy your code.

### Create a Github Action

-  Use GitHub Actions to run an Azure Machine Learning pipeline.

    1. Define an event that will trigger the workflow.
    2. Run the workflow, which consists of jobs.
    3. A job contains one or more steps.
    4. As a step, run an Azure Machine Learning pipeline.
    5. The Azure Machine Learning pipeline is made up of scripts or Azure Machine Learning components.

- To create the workflow for GitHub Actions, you define the steps you want to run in a YAML file. In the YAML file, you'll include:

    - Event: How you want to trigger the workflow.
    - Job: A group of steps you want to execute on a runner. For machine learning workloads, you'll likely use an Ubuntu Linux virtual machine.
    - Step: A script or action you want to run. For example, a CLI command to initiate the Azure Machine Learning pipeline (az ml job create).

- The example workflow will:

    - Check out the repo to make it available on the runner.
    - Install the Azure Machine Learning extension for the CLI.
    - Sign in to Azure using the predefined AZURE_CREDENTIALS.
    - Navigate to the src folder, which contains all your production code.
    - Run the Azure Machine Learning pipeline.

### Run a WorkFlow with Github Actions

- Suppose you created the YAML file to define the workflow. You store the YAML file in the .github/workflows/ directory in your repository.

- To view the workflow, navigate to the GitHub Actions tab of your repo.GitHub will automatically pick up any workflows that are stored in the .github/workflows/ directory.

- You can trigger the workflow with the events specified in your workflow YAML file. In the example, a push to the repo will trigger the workflow to run. Anytime you make a change and push your commits to the repo (locally in Visual Studio Code or directly in GitHub), the workflow will run.

- Select the latest run to further inspect whether all steps have successfully executed or what error messages you received.

- When a workflow triggers an Azure Machine Learning pipeline, you should also review the pipeline run in the Azure Machine Learning workspace as errors may still occur within the Azure Machine Learning pipeline. Any error messages will be viewable in the outputs folder of the Azure Machine Learning pipeline experiment run.