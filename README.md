# Student Management

A simple home page for a student management application. It displays a welcome
message and does not include other functionality.

## Run locally

1. Clone the repository:
   ```sh
   git clone https://github.com/Suryaaa27/DevOpsLab.git
   cd DevOpsLab
   ```
2. Open `index.html` in a web browser.

## Jenkins: build on GitHub pushes

The `Jenkinsfile` checks out the source, verifies that the home page contains
the welcome message, and archives `index.html` as the build artifact. Its
validation uses Jenkins pipeline steps, so it works on Windows and Unix agents
without requiring a shell.

1. Install Jenkins and the **GitHub** plugin. Ensure the Jenkins controller can
   reach GitHub and that Git is installed on the agent.
2. In Jenkins, create a **Pipeline** job. Under **Pipeline**, select
   **Pipeline script from SCM**, choose **Git**, enter
   `https://github.com/Suryaaa27/DevOpsLab.git`, and set the script path to
   `Jenkinsfile`. Save the job and run it once to verify the setup.
3. Configure a GitHub webhook for the repository. In GitHub, open
   **Settings → Webhooks → Add webhook**, set the payload URL to
   `https://<your-jenkins-host>/github-webhook/`, choose **application/json**,
   select **Just the push event**, and add the webhook. Jenkins must be
   publicly reachable by GitHub; configure a webhook secret if required by
   your environment.
4. Push a change to the repository. GitHub sends the push event to Jenkins,
   which checks out the updated source and runs the pipeline. Check the job's
   build history and **Console Output** for results. The archived
   `index.html` is available on each successful build.

The GitHub webhook is configured in the GitHub repository settings; it cannot
be created by the Jenkinsfile itself.
