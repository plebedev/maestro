# Maestro - A Framework for Claude Opus, GPT and local LLMs to Orchestrate Subagents


This Python script demonstrates an AI-assisted task breakdown and execution workflow using the Anthropic API. It utilizes two AI models, Opus and Haiku, to break down an objective into sub-tasks, execute each sub-task, and refine the results into a cohesive final output.

## New
Mestro now runs locally thanks to the Ollama platform. Experience the power of Llama 3 locally! 

Before running the script

Install Ollama client from here
https://ollama.com/download

then

```bash
pip install ollama
```
And 

```bash
ollama.pull('llama3:70b')
```
This will depend on the model you want to use it, you only need to do it once or if you want to update the model when a new version it's out.
In the script I am using both versions but you can customize the model you want to use

ollama.pull('llama3:70b')
ollama.pull('llama3:8b')

Then

```bash
python maestro-ollama.py
```

## Higly requested features
- SEARCH 🔍

Now, when it's creating a task for its subagent, Claude Opus will perform a search and get the best answer to help the subagent solve that task even better.

Make sure you replace your Tavil API for search to work

Get one here https://tavily.com/
  
- GPT4 SUPPORT

Add support for GPT-4 as an orchestrator in maestro-gpt.py
Simply
```bash
python maestro-gpt.py
```

After you complete your installs.


## Features

- Breaks down an objective into manageable sub-tasks using the Opus model
- Executes each sub-task using the Haiku model
- Provides the Haiku model with memory of previous sub-tasks for context
- Refines the sub-task results into a final output using the Opus model
- Generates a detailed exchange log capturing the entire task breakdown and execution process
- Saves the exchange log to a Markdown file for easy reference
- Utilizes an improved prompt for the Opus model to better assess task completion
- Creates code files and folders when working on code projects.

## Prerequisites

To run this script, you need to have the following:

- Anthropic API key

## Installation

Option 1: Using requirements.txt
1. Clone the repository or download the script file.
2. Install the required Python packages by running the following command:
```shell
pip install -r requirements.txt
```

Option 2: Using Poetry
1. Clone the repository
2. Install [Python](https://www.python.org/), For example, on macOS, you can install Python 3.12 using Homebrew:
```shell
$ brew install python@3.12
```
3. Install [Poetry](https://python-poetry.org/) For example, on macOS, you can install Poetry using Homebrew:

```shell
$ brew install poetry
```
4. Configure virtual environments to be project-local.
```shell
$ poetry config virtualenvs.in-project true
$ poetry config --list
cache-dir = "/Users/<username>/Library/Caches/pypoetry"
experimental.new-installer = true
installer.parallel = true
virtualenvs.create = true
virtualenvs.in-project = true
virtualenvs.path = "{cache-dir}/virtualenvs"  # /Users/<username>/Library/Caches/pypoetry/virtualenvs
```
5. Initialize the virtual environment.

```shell
$ poetry env use python3.12
...
$ poetry install
Creating virtualenv src in <ROOT>/.venv
Updating dependencies
...
```

Replace the placeholder API key in the script with your actual Anthropic API key:

```python
client = Anthropic(api_key="YOUR_API_KEY_HERE")
```

If using search, replace your Tavil API
```python
tavily = TavilyClient(api_key="YOUR API KEY HERE")
```

## Usage

1. Open a terminal or command prompt and navigate to the directory containing the script.
2. Run the script using the following command:

```bash
python maestro.py
```

3. Enter your objective when prompted:

```bash
Please enter your objective: Your objective here
```

The script will start the task breakdown and execution process. It will display the progress and results in the console using formatted panels.

Once the process is complete, the script will display the refined final output and save the full exchange log to a Markdown file with a filename based on the objective.

## Code Structure

The script consists of the following main functions:

- `opus_orchestrator(objective, previous_results=None)`: Calls the Opus model to break down the objective into sub-tasks or provide the final output. It uses an improved prompt to assess task completion and includes the phrase "The task is complete:" when the objective is fully achieved.
- `haiku_sub_agent(prompt, previous_haiku_tasks=None)`: Calls the Haiku model to execute a sub-task prompt, providing it with the memory of previous sub-tasks.
- `opus_refine(objective, sub_task_results)`: Calls the Opus model to review and refine the sub-task results into a cohesive final output.

The script follows an iterative process, repeatedly calling the opus_orchestrator function to break down the objective into sub-tasks until the final output is provided. Each sub-task is then executed by the haiku_sub_agent function, and the results are stored in the task_exchanges and haiku_tasks lists.

The loop terminates when the Opus model includes the phrase "The task is complete:" in its response, indicating that the objective has been fully achieved.

Finally, the opus_refine function is called to review and refine the sub-task results into a final output. The entire exchange log, including the objective, task breakdown, and refined final output, is saved to a Markdown file.

## Customization

You can customize the script according to your needs:

- Adjust the max_tokens parameter in the client.messages.create() function calls to control the maximum number of tokens generated by the AI models.
- Change the models to what you prefer, like replacing Haiku with Sonnet or Opus.
- Modify the console output formatting by updating the rich library's Panel and Console configurations.
- Customize the exchange log formatting and file extension by modifying the relevant code sections.

## Running in IntelliJ

Prior to setting-up IntelliJ, make sure the virtual environment has been initialized.

* Open the project
* Navigate to **File > Project Structure...**
    * Navigate to **Platform Settings > SDKs**
        * Click the "+" symbol to **Add Python SDK...**
        * Select **Virtualenv Environment** on the left
        * Select **Existing environment**
            * For **Interpreter**, use the Python executable in the installed virtual environment (e.g. `<ROOT>/.venv/bin/python`)
            * Submit the new SDK
    * Navigate to **Project Settings > Modules**
        * Click the "+" symbol to **Add New Module...**
        * Select a type of **Python** on the left
        * For **Module SDK**, select the newly created SDK
        * For **Content root**, select `<ROOT>`


## License

This script is released under the MIT License.

## Acknowledgements

- Anthropic for providing the AI models and API.
- Rich for the beautiful console formatting.
