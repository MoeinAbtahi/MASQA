# MASQA: Enhancing Software Quality

**MASQA** is a web-based tool designed to help developers improve software quality by resolving code issues, revising them using Large Language Models (LLMs), and comparing code versions. This application integrates with SonarQube to fetch unresolved issues and uses advanced AI models for automated code revision.

## Prerequisites

Before using the application, install the required dependencies by running:

```bash
pip install -r ./requirements.txt
```

## Application Overview

The application is designed to:

1. Fetch unresolved code issues from SonarQube.
2. Provide a platform for uploading and revising issues using AI models.
3. Enable code comparison between original and revised versions with detailed metrics.

## Key Functions

### 1. `get_all_issues(sonar_url, api_token, project_key)`

This function fetches unresolved issues from a SonarQube project using the API.

#### Parameters:
- **sonar_url** (str): The URL of the SonarQube server.
- **api_token** (str): Authentication token for accessing the SonarQube API.
- **project_key** (str): The SonarQube project key to retrieve issues from.

#### Description:
- Retrieves unresolved issues from SonarQube.
- Handles paginated responses to fetch all issues.

### 2. `modify_file_path(original_path, to_remove, to_add)`

This function modifies a file path by removing a prefix and adding a new segment.

#### Parameters:
- **original_path** (str): The initial file path.
- **to_remove** (str): A prefix to be removed.
- **to_add** (str): A new prefix to be added.

#### Description:
- Ensures compatibility across platforms by using forward slashes.
- Adjusts file paths for code revisions.

### 3. `save_csv_file(issues, file_path, to_remove, to_add)`

This function saves a list of code issues to a CSV file after modifying the file paths.

#### Parameters:
- **issues** (list): A list of code issue details.
- **file_path** (str): The destination path for the CSV file.
- **to_remove** (str): A prefix to remove from file paths.
- **to_add** (str): A new prefix to add to the file paths.

#### Description:
- Organizes and saves issue data into a CSV file.
- Allows for file path customization before saving.

### 4. `read_file_contents(file_path)`

Reads the contents of a file and returns them as a string, with each line numbered.

#### Parameters:
- **file_path** (str): The path to the file.

#### Description:
- Reads and formats the file’s contents with line numbers for easier analysis.

### 5. `generate_prompt(file_location, bug_lines, bug_messages, bug_types)`

Generates a prompt for an AI model to fix code issues.

#### Parameters:
- **file_location** (str): The file with issues.
- **bug_lines** (list of int): Line numbers where issues occur.
- **bug_messages** (list of str): Descriptions of the issues.
- **bug_types** (list of str): Types of issues (e.g., Bug, Vulnerability).

#### Description:
- Combines the code with bug descriptions to create a prompt for an AI model.
- Provides a few-shot example to guide the model’s revision.

### 6. `highlight_differences(diff)`

Highlights the differences between two versions of a file in HTML format.

#### Parameters:
- **diff** (list of str): The diff output, showing the differences between the two versions.

#### Description:
- Highlights added and removed lines in the code.
- Displays differences using color-coded HTML for easy comparison.

### 7. `calculate_all_metrics(original_lines, revised_lines)`

Calculates various evaluation metrics comparing original and revised code lines.

#### Parameters:
- **original_lines** (list of str): The original code.
- **revised_lines** (list of str): The revised code.

#### Description:
- Computes metrics like precision, recall, F1 score, BLEU, and ROUGE.
- Provides a detailed assessment of how closely the revised code matches the original.

## Routes

### 1. `/sonarqube`

This route handles fetching issues from SonarQube and saving them to a CSV file.

- **Methods**: GET, POST
- **Steps**: 
  1. Provides a form to enter SonarQube details.
  2. Fetches unresolved issues from SonarQube based on the provided details.
  3. Allows saving the issues in a CSV file.

### 2. `/Code_Issue_Reviser`

This route handles the process of uploading a CSV file, interacting with OpenAI’s API to revise code issues, and updating the UI with results.

- **Methods**: GET, POST
- **Steps**:
  1. Upload and process a CSV file containing code issues.
  2. Generate a prompt for the OpenAI API based on selected issues.
  3. Send the prompt to OpenAI and retrieve the revised code.

### 3. `/Code_Comparer`

This route compares the original and revised versions of a file, calculating and displaying differences and evaluation metrics.

- **Methods**: GET, POST
- **Steps**:
  1. Upload a CSV file with file details.
  2. Select files for comparison.
  3. Highlight code differences and display comparison metrics.

## How to Use

1. **SonarQube Integration**: Start by fetching issues from your SonarQube project via the `/sonarqube` route.
2. **Issue Revision**: Once issues are retrieved, upload the CSV to the `/Code_Issue_Reviser` route to revise the issues using the LLM.
3. **Code Comparison**: After revising the code, use the `/Code_Comparer` route to compare the original and revised code, and evaluate the changes.

![Screenshot_19-11-2024_232935_127 0 0 1](https://github.com/user-attachments/assets/a67b8284-0c7d-48e1-adc0-7dcea8bca80e)
![Screenshot_19-11-2024_232842_127 0 0 1](https://github.com/user-attachments/assets/5d92f319-4d49-4084-98bc-2c1a32658750)
![Screenshot 2024-11-19 232727](https://github.com/user-attachments/assets/bba71550-e70a-40a9-9854-73d333955ef1)
![Screenshot 2024-11-19 232715](https://github.com/user-attachments/assets/c748af90-e055-427f-9418-b6faa192bdcd)





