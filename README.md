# Github-Actions

### Step 1: Create a Workflow File

1. In your GitHub repository, navigate to the **Actions** tab.
2. Click **New workflow**.
3. Choose **"set up a workflow yourself"** or start from a template if a suitable one is available.
4. This will create a new `.yml` or `.yaml` file under the `.github/workflows` directory in your repository. You can name it `gradle-build.yml` or any other descriptive name.

### Step 2: Define the Workflow

Paste the following YAML content into your new workflow file. This is a basic configuration that can be customized as needed:

```yaml
name: Java CI with Gradle

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  build:

    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v2
    - name: Set up JDK 11
      uses: actions/setup-java@v2
      with:
        java-version: '11'
        distribution: 'adopt'
        
    - name: Grant execute permission for gradlew
      run: chmod +x ./gradlew

    - name: Build with Gradle
      run: ./gradlew build
```

### Explanation of the Workflow File

- **`name`**: Names the workflow (e.g., "Java CI with Gradle").
- **`on`**: Defines when the workflow will run. In this example, it runs on push and pull request events to the `main` branch.
- **`jobs`**: Defines the jobs to be run. This example has a single job called `build`.
- **`runs-on`**: Specifies the type of machine to run the job on. Here, it's set to `ubuntu-latest`.
- **`steps`**: A sequence of steps to be run within the `build` job.
  - **`actions/checkout@v2`**: Checks out your repository under `$GITHUB_WORKSPACE`, so your workflow can access it.
  - **`actions/setup-java@v2`**: Sets up a specific version of Java. This example uses JDK 11.
  - **Grant execute permission for gradlew**: Ensures the Gradle wrapper script can be executed.
  - **Build with Gradle**: Executes the Gradle build command. This runs the build task, which compiles your Java source code, runs tests, and generates outputs.

### Step 3: Customize and Extend

- **Customize Java Version**: Adjust the `java-version` to match the JDK version your project requires.
- **Customize Gradle Commands**: Replace `./gradlew build` with any Gradle tasks your project needs. For example, you might use `./gradlew clean test` to clean the project and run tests without assembling the outputs.

### Step 4: Commit and Push

Commit the workflow file to your repository and push it to GitHub. The workflow will trigger based on the events you've specified.

### Monitoring Workflow Runs

After pushing the workflow file, you can monitor the workflow execution in the **Actions** tab of your GitHub repository. Here, you can see each run, inspect the logs, and troubleshoot if necessary.

This tutorial gives you a basic setup. GitHub Actions is highly customizable, allowing you to add more jobs, run jobs in parallel, deploy your application, and much more depending on your project's needs.
