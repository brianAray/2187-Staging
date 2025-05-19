# Jenkins Notes

### **Module: Introduction to Jenkins**

### **Introduction to Jenkins**

**Jenkins** is an open-source automation server used to build, test, and deploy software projects. It provides continuous integration (CI) and continuous delivery (CD) capabilities, allowing developers to automate tasks in the software development lifecycle.

---

### **Why Use Jenkins?**

1. **Automation**:
    - Automates repetitive tasks like building, testing, and deploying code.
2. **Continuous Integration/Delivery**:
    - Ensures that code changes are continuously integrated and deployed in a reliable and automated manner.
3. **Extensibility**:
    - Over 1,800 plugins support integration with various tools and technologies (e.g., Git, Docker, Kubernetes).
4. **Open-Source and Community Support**:
    - Widely used, well-documented, and supported by a large community.

---

### **Key Features**

1. **Cross-Platform**:
    - Runs on various operating systems (Windows, Linux, macOS).
2. **Pipeline as Code**:
    - Write and manage build pipelines using code (e.g., Jenkinsfile).
3. **Distributed Builds**:
    - Execute builds across multiple machines for scalability and efficiency.
4. **Integration with Tools**:
    - Supports version control systems (Git, SVN), build tools (Maven, Gradle), and testing frameworks (JUnit, Selenium).
5. **Notifications and Reports**:
    - Send build and deployment results via email, Slack, or other notification channels.
6. **Secure**:
    - Supports role-based access control, SSL, and other security measures.

---

### **Jenkins Workflow**

1. **Developer Pushes Code**:
    - Code changes are pushed to a version control system (e.g., GitHub, GitLab).
2. **Jenkins Triggers a Build**:
    - Jenkins detects the changes and initiates a build.
3. **Build Process**:
    - Executes tasks such as compiling code, running tests, and packaging applications.
4. **Test Execution**:
    - Runs automated tests to verify the code's functionality.
5. **Deployment**:
    - Deploys the application to a staging or production environment if the build passes.

---

### **Jenkins Jobs and Builds**

In Jenkins, the core concept revolves around **jobs** and **builds**. A **job** is a task that Jenkins performs, such as compiling code, running tests, or deploying an application. A **build** refers to a specific instance of that job being executed. Understanding how Jenkins jobs and builds work is fundamental to effectively automating tasks.

---

### **1. Jenkins Jobs**

A **Jenkins job** is a single task or a series of tasks that Jenkins performs, such as compiling code, running tests, or deploying software. Jobs are the building blocks of Jenkins automation.

### **Types of Jenkins Jobs**

There are several types of jobs in Jenkins:

1. **Freestyle Project**:
    - The most basic type of job. It allows you to define tasks such as building, testing, and deploying in a simple graphical interface.
    - Commonly used for simple CI/CD workflows.
2. **Pipeline**:
    - A more advanced and flexible job type used to define continuous integration and delivery pipelines as code. Pipelines are defined using **Jenkinsfiles** (written in Groovy) which provide a domain-specific language (DSL) to define complex workflows.
    - Supports stages, parallel execution, and advanced error handling.
3. **Multi-Branch Pipeline**:
    - Automatically creates pipeline jobs for each branch in a version control repository (e.g., GitHub). Each branch will have its own Jenkins pipeline, and the configuration is typically defined in a `Jenkinsfile` within the branch.
    - Suitable for managing multiple versions of an application.
4. **Matrix Project**:
    - Allows you to define multiple configurations for a job (such as different OS versions or Java versions) and execute them in parallel. Ideal for testing cross-platform or cross-version compatibility.
5. **GitHub Organization**:
    - For projects hosted on GitHub, Jenkins can automatically scan a GitHub organization for repositories and create jobs for each repository.
6. **Maven Project**:
    - Specifically for projects that use **Apache Maven** as a build tool. Jenkins integrates directly with Maven to handle building, testing, and deploying Java applications.

---

### **2. Configuring Jenkins Jobs**

### **Steps to Create a Job**:

1. **Access Jenkins Dashboard**:
    - Go to the Jenkins web interface (usually `http://localhost:8080`).
2. **Create a New Job**:
    - Click on **"New Item"** from the left-hand side.
    - Enter a name for your job, select the job type (e.g., **Freestyle Project**), and click **OK**.
3. **Configure the Job**:
    - **Source Code Management**: Configure version control settings (e.g., GitHub, SVN) and provide repository URL.
    - **Build Triggers**: Set triggers for when the job should run, such as:
        - **Poll SCM**: Check for changes in source code at regular intervals.
        - **Build periodically**: Run the job at a specific schedule (e.g., daily, hourly).
        - **GitHub webhook**: Trigger the job when code is pushed to the repository.
    - **Build**: Define build steps. For example, using shell commands, invoking Maven or Gradle, or running test scripts.
    - **Post-build Actions**: Define actions after the build finishes, such as sending notifications, archiving build artifacts, or deploying the application.
4. **Save the Job**:
    - Click **Save** to create the job.

---

### **3. Jenkins Builds**

A **build** is an execution of a job, and each time a job is triggered, it results in a new build. Builds are identified by a unique build number, and Jenkins keeps a record of all builds for each job.

### **Understanding Builds**:

- **Build Number**: Every time a job is triggered, Jenkins assigns a unique incremental number to that build (e.g., Build #1, Build #2, etc.).
- **Build Status**:
    - **Success**: The build completed successfully.
    - **Failure**: The build failed due to errors (e.g., test failures, compilation errors).
    - **Aborted**: The build was manually stopped.
    - **Unstable**: The build completed, but there were warnings (e.g., test failures that don't prevent the build from succeeding).

### **Viewing Build Information**:

- After triggering a build, you can view the build logs and other information such as:
    - Console Output: Logs of the build process, which include any output from scripts, commands, or tests.
    - Test Results: Results of any automated tests run during the build.
    - Artifacts: Any files or artifacts that were produced during the build (e.g., JAR files, reports).

---

### **4. Managing Jenkins Jobs and Builds**

### **Triggering Builds**:

- **Manual Trigger**: You can manually trigger a build by clicking the **Build Now** button in the job’s dashboard.
- **Automated Trigger**: Build triggers can be set, such as polling source code for changes or using webhooks.

### **Build History**:

- Jenkins keeps track of all builds associated with a job. You can access the build history from the job dashboard.
- From the build history, you can:
    - **Rebuild**: Re-run a previous build.
    - **View Build Logs**: Access detailed logs of each build.
    - **Download Artifacts**: Retrieve the build artifacts (e.g., generated files, logs).

### **Build Parameters**:

- Jobs can be configured to accept **build parameters**. These parameters can be passed during build triggering, allowing customization based on the environment, branch, or specific configuration.

---

### **Module: Jenkins Configuration**

### **Creating a CI/CD Pipeline with Jenkins**

A **CI/CD pipeline** (Continuous Integration/Continuous Delivery) automates the process of integrating code changes, testing, and deploying applications. Jenkins is a popular tool to implement CI/CD pipelines due to its flexibility, extensibility, and broad plugin ecosystem.

In this guide, we'll go over how to create a simple CI/CD pipeline using Jenkins.

---

### **Steps to Create a CI/CD Pipeline in Jenkins**

### **Prerequisites**

1. **Jenkins Installed**: Ensure Jenkins is installed and running.
2. **Source Code Repository**: Code is typically hosted on GitHub, GitLab, or Bitbucket.
3. **Jenkins Plugins**: Ensure Jenkins has the necessary plugins installed (e.g., **Git**, **Pipeline**, **Docker**, **JUnit**).
4. **Build Tools**: Install tools like Maven, Gradle, or npm depending on the project’s build system.

---

### **1. Create a Pipeline Job**

1. **Go to Jenkins Dashboard**:
    - Navigate to the Jenkins homepage (typically `http://localhost:8080`).
2. **Create a New Pipeline**:
    - Click on **New Item** on the left menu.
    - Enter a name for the job (e.g., `MyApp-Pipeline`).
    - Select **Pipeline** and click **OK**.

---

### **2. Define the Pipeline Script**

### **Using the Jenkinsfile**:

A **Jenkinsfile** is a text file that defines the stages and steps in a pipeline using the **Pipeline DSL**. The Jenkinsfile can be stored in your version control system (GitHub, GitLab, etc.).

There are two ways to configure the Jenkins pipeline:

- **Declarative Pipeline** (more structured, recommended).
- **Scripted Pipeline** (more flexible, uses Groovy scripts).

Here’s an example of a simple **Declarative Pipeline**:

```groovy
pipeline {
    agent any

    environment {
        // Define environment variables if needed
        APP_NAME = 'MyApp'
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from the repository
                git 'https://github.com/your-username/your-repo.git'
            }
        }

        stage('Build') {
            steps {
                // Build the application using Maven (or other build tool)
                sh 'mvn clean install'
            }
        }

        stage('Test') {
            steps {
                // Run unit tests
                sh 'mvn test'
            }
        }

        stage('Deploy') {
            steps {
                // Deploy the application (can be to a staging server or Docker container)
                sh 'echo "Deploying to production..."'
                // Example of deploying to Docker:
                // sh 'docker build -t myapp .'
                // sh 'docker run -d -p 8080:8080 myapp'
            }
        }
    }

    post {
        always {
            // Cleanup, notify, or archive test results
            echo 'Cleaning up...'
        }

        success {
            echo 'Build and Deployment Successful!'
        }

        failure {
            echo 'Build or Deployment Failed!'
        }
    }
}

```

This `Jenkinsfile` defines four stages:

- **Checkout**: Clones the source code from the GitHub repository.
- **Build**: Runs the Maven build command to compile the application.
- **Test**: Executes unit tests.
- **Deploy**: Deploys the application (this could be to a server, cloud, or container).

---

### **3. Configure Jenkins Pipeline Job**

1. **Pipeline Configuration**:
    - After creating the pipeline job, in the configuration page, scroll down to the **Pipeline** section.
    - Choose **Pipeline Script from SCM** if you want to pull the `Jenkinsfile` from your source code repository.
        - **SCM**: Choose **Git**.
        - **Repository URL**: Enter your repository URL (e.g., `https://github.com/your-username/your-repo.git`).
        - **Branch**: Specify the branch to build (e.g., `main` or `master`).
2. **Save**: Click **Save** to save the pipeline configuration.

---

### **4. Triggering the Pipeline**

### **Manual Trigger**:

- Go to the pipeline job page and click **Build Now** to trigger the pipeline manually.

### **Automated Trigger** (e.g., on Git commit):

- Jenkins can automatically trigger builds on code changes. This is typically done using **webhooks** in GitHub or GitLab.
- Configure the webhook in the version control system to notify Jenkins on commits to trigger the pipeline.
    - For GitHub: Go to your GitHub repository > Settings > Webhooks > Add webhook and provide the Jenkins server URL (`http://your-jenkins-server/git/notifyCommit`).

---

### **5. Monitoring the Pipeline**

Once the pipeline is triggered, Jenkins will display the progress of each stage on the pipeline page:

- **Console Output**: View logs and output from each stage.
- **Pipeline Visualization**: Jenkins shows the pipeline in a visual format with color indicators (blue for success, red for failure).

---

### **6. Post-Build Actions**

You can define actions that occur after the pipeline execution:

- **Notify**: Send notifications (email, Slack, etc.) on build results.
- **Publish Test Reports**: Use plugins to visualize test results (JUnit, NUnit).
- **Archive Artifacts**: Store build artifacts (e.g., `.jar`, `.war`, `.tar` files) for later use.

Example of archiving artifacts:

```groovy
archiveArtifacts 'target/*.jar'

```

---

### **Jenkins Credential Management**

**Jenkins Credential Management** is a feature in Jenkins that securely stores and manages sensitive information, such as usernames, passwords, API tokens, and SSH keys, which are necessary for performing tasks like accessing version control systems, deploying to servers, or integrating with other services.

Using Jenkins' credential management system helps avoid hardcoding sensitive data into Jenkins pipelines or jobs, thus increasing security and maintainability.

---

### **Types of Credentials in Jenkins**

1. **Username and Password**:
    - Store usernames and passwords for accessing services like GitHub, Docker, and other repositories.
2. **SSH Keys**:
    - Used for authenticating with remote servers or services via SSH.
3. **Secret Text**:
    - Used for storing generic secrets, like API tokens or database passwords.
4. **Secret File**:
    - Allows the storage of files as secrets, such as certificates or keys.
5. **AWS Credentials**:
    - A special type of credentials used to authenticate with AWS services via IAM (Identity and Access Management) keys.
6. **Certificate**:
    - Store certificates required for secure communication, such as SSL certificates.

---

### **Configuring Credentials in Jenkins**

### **1. Adding Credentials to Jenkins**

To add credentials, follow these steps:

1. **Go to Jenkins Dashboard**:
    - Navigate to the Jenkins home page (usually `http://localhost:8080`).
2. **Access Credentials Configuration**:
    - From the left menu, go to **Manage Jenkins** > **Manage Credentials**.
    - Choose the scope (either **Global** or a specific **Folder** or **Domain**).
    - Click **(Global)** or the relevant domain where you want to add credentials.
3. **Add Credentials**:
    - Click **(Global)** > **Add Credentials**.
    - Select the appropriate **Kind** based on the type of credential you want to add.
        - **Username with Password**: For services that require a username and password.
        - **SSH Username with Private Key**: For SSH keys.
        - **Secret Text**: For API tokens or other secrets.
        - **Secret File**: For file-based secrets.
    - Enter the necessary information (e.g., username, password, secret text, or SSH private key).
    - Optionally, provide a **ID** (used to reference the credential in Jenkins jobs) and **Description** (for easy identification).
4. **Save**: After entering the credentials, click **OK** to save them.

---

### **2. Using Credentials in Jenkins Pipeline**

Once you’ve added credentials to Jenkins, you can use them in Jenkins jobs and pipelines. You reference them using the **credentials ID** you assigned earlier.

### **Example with Username/Password**:

If you've added a **Username with Password** credential with ID `my-git-credentials`, you can use it in your Jenkins pipeline like this:

```groovy
pipeline {
    agent any

    environment {
        GIT_CREDENTIALS = credentials('my-git-credentials') // Reference credential by ID
    }

    stages {
        stage('Checkout') {
            steps {
                // Use the credential in the Git command
                git credentialsId: "${GIT_CREDENTIALS}", url: 'https://github.com/your-repo.git'
            }
        }
    }
}

```

### **Example with SSH Keys**:

For **SSH Keys** (for accessing a private repository or server), you can use the `sshagent` block to load SSH credentials:

```groovy
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                script {
                    sshagent(['my-ssh-key']) {
                        sh 'git clone git@github.com:your-username/your-repo.git'
                    }
                }
            }
        }
    }
}

```

In this example, the `my-ssh-key` refers to the SSH credentials added in Jenkins, and `sshagent` makes them available for the build process.

### **Example with Secret Text**:

For secret tokens or API keys (e.g., for AWS, DockerHub, etc.), you can use the **secret text** credential:

```groovy
pipeline {
    agent any

    environment {
        AWS_SECRET_KEY = credentials('aws-secret-key') // Reference secret key
    }

    stages {
        stage('Deploy') {
            steps {
                script {
                    // Use the secret in your script, e.g., AWS CLI
                    sh "aws configure set aws_secret_access_key ${AWS_SECRET_KEY}"
                }
            }
        }
    }
}

```

Here, `AWS_SECRET_KEY` is a secret text credential, and it’s securely injected into the pipeline.

---

### **3. Using Credentials in Freestyle Jobs**

In a **Freestyle Job**, you can also access credentials using the following methods:

1. **Build Environment**:
    - In the job configuration, go to the **Build Environment** section.
    - Check **Use secret text(s) or file(s)**, then click **Add** and choose the appropriate type of credential (e.g., **Secret Text**, **SSH Key**).
    - Select the credential and set an environment variable for it (e.g., `MY_SECRET_API_KEY`).
2. **Git Configuration**:
    - In the **Source Code Management** section, select **Git** and configure the repository URL.
    - Under **Credentials**, select the credential you created for accessing the Git repository.
3. **Build Step**:
    - You can reference the environment variables or credentials directly in build steps. For example, in the shell step, you can access them like this:
        
        ```bash
        echo "Using secret key: $MY_SECRET_API_KEY"
        
        ```
        

---

### **4. Managing Credentials Securely**

While Jenkins credentials management helps you store and use sensitive information securely, you should follow some best practices to enhance security:

- **Limit Access**: Restrict access to credentials to specific Jenkins users or jobs using **Role-based Access Control (RBAC)**.
- **Use Environment Variables**: Use environment variables to pass credentials into jobs securely.
- **Use Vaults**: For enhanced security, consider integrating Jenkins with secret management tools like **HashiCorp Vault** or **AWS Secrets Manager** for more sophisticated credential management.
- **Never Expose Credentials**: Avoid printing sensitive information, such as secrets or tokens, in console logs. Jenkins automatically masks them if they are accessed through the **credentials()** function.

---

### **5. Deleting or Updating Credentials**

- **Delete**: Go to **Manage Jenkins** > **Manage Credentials**, then select the credential and click **Delete**.
- **Update**: To update a credential, select it and click **Edit**. Make your changes and save.

---

### **Jenkins Plugins and Integrations**

Jenkins is highly extensible through **plugins**, which allow you to add new features, integrate with other tools, and extend its capabilities. Jenkins has a vast ecosystem of over 1,800 plugins that support various functionalities such as version control systems, build tools, test frameworks, deployment tools, and more.

In this guide, we will cover key Jenkins plugins and how to integrate them into your Jenkins setup.

---

### **1. Key Jenkins Plugins**

### **a. Git Plugin**

- **Purpose**: Allows Jenkins to integrate with Git repositories (e.g., GitHub, GitLab, Bitbucket).
- **Features**:
**Usage**: To use the Git plugin in Jenkins pipeline:
    - Clone repositories and manage branches.
    - Trigger builds on code changes via GitHub webhooks or polling.
    - Allows Jenkins to checkout code from Git repositories in pipeline jobs.
    
    ```groovy
    pipeline {
        agent any
        stages {
            stage('Checkout') {
                steps {
                    git 'https://github.com/your-username/your-repo.git'
                }
            }
        }
    }
    
    ```
    

### **b. Maven Plugin**

- **Purpose**: Integrates Jenkins with **Apache Maven** for building Java projects.
- **Features**:
**Usage**: Add Maven build steps in a freestyle project or Jenkinsfile:
    - Supports Maven goals and phases.
    - Provides the ability to build Maven projects with Jenkins.
    - Works with **Maven-based Jenkins jobs** and **Pipeline jobs**.
    
    ```groovy
    pipeline {
        agent any
        stages {
            stage('Build') {
                steps {
                    sh 'mvn clean install'
                }
            }
        }
    }
    
    ```
    

### **c. Docker Plugin**

- **Purpose**: Integrates Jenkins with Docker for building, deploying, and managing Docker containers.
- **Features**:
    - Build Docker images.
    - Deploy applications in Docker containers as part of the pipeline.
    - Supports Docker Compose and Kubernetes integration.
    
    **Usage**: Run Docker commands within Jenkins:
    
    ```groovy
    pipeline {
        agent any
        stages {
            stage('Build Docker Image') {
                steps {
                    script {
                        docker.build('myapp')
                    }
                }
            }
        }
    }
    
    ```
    

### **d. Slack Notification Plugin**

- **Purpose**: Send build notifications to a Slack channel.
- **Features**:
**Usage**: Configure Slack in **Manage Jenkins > Configure System**, then use the following in a pipeline:
    - Send build success/failure notifications.
    - Customize message content and formatting.
    
    ```groovy
    post {
        success {
            slackSend(channel: '#build-notifications', message: 'Build Success!')
        }
        failure {
            slackSend(channel: '#build-notifications', message: 'Build Failed!')
        }
    }
    
    ```
    

### **e. Jenkins Pipeline Plugin**

- **Purpose**: Enables the use of **Pipeline-as-Code** in Jenkins, using `Jenkinsfile` for defining the build process.
- **Features**:
**Usage**: Define pipeline stages in the `Jenkinsfile`:
    - Supports Declarative and Scripted Pipelines.
    - Allows for defining build, test, and deploy steps in code.
    
    ```groovy
    pipeline {
        agent any
        stages {
            stage('Build') {
                steps {
                    echo 'Building...'
                }
            }
            stage('Test') {
                steps {
                    echo 'Testing...'
                }
            }
        }
    }
    
    ```
    

### **f. JUnit Plugin**

- **Purpose**: Integrates JUnit test results with Jenkins and provides test reports.
- **Features**:
    - Collect and display results from unit tests.
    - Provides trend analysis of test results.
    - Works with various testing frameworks like JUnit, TestNG, and more.
    
    **Usage**: Publish test results in a pipeline:
    
    ```groovy
    pipeline {
        agent any
        stages {
            stage('Test') {
                steps {
                    sh 'mvn test'
                }
            }
        }
        post {
            always {
                junit '**/target/test-*.xml'
            }
        }
    }
    
    ```
    

---

### **2. Popular Jenkins Integrations**

### **a. Version Control Systems**

1. **GitHub**: Use the GitHub plugin to integrate Jenkins with GitHub for webhooks, pull requests, and commits.
    - Set up webhooks to trigger Jenkins builds automatically when code is pushed.
    - Automatically create jobs for each pull request.
2. **Bitbucket**: Similar to GitHub, you can use the Bitbucket plugin to link Jenkins with your Bitbucket repositories.
    - Use Bitbucket webhooks for build triggers.

### **b. Build Tools**

1. **Gradle**: Integrate Jenkins with Gradle for building Java applications. The **Gradle Plugin** allows you to configure and run Gradle builds from Jenkins.
2. **Ant**: The **Ant Plugin** allows Jenkins to run **Apache Ant** builds for Java projects.

### **c. Cloud Integrations**

1. **Amazon Web Services (AWS)**: Jenkins can integrate with AWS for deployment purposes, such as deploying applications to **Elastic Beanstalk**, **EC2**, **Lambda**, and other AWS services. Use the **AWS CodeDeploy Plugin** and **AWS Credentials Plugin** for secure AWS integrations.
2. **Google Cloud**: Jenkins integrates with Google Cloud through the **Google Cloud Plugin**, allowing you to deploy applications to Google Kubernetes Engine (GKE), App Engine, and other services.

### **d. Continuous Testing Tools**

1. **Selenium**: Jenkins can be integrated with **Selenium** for running automated browser tests.
    - Use the **Selenium Plugin** to set up and trigger Selenium tests in the pipeline.
2. **SonarQube**: Integrate Jenkins with **SonarQube** for static code analysis and quality checks.
    - The **SonarQube Scanner Plugin** allows Jenkins to trigger SonarQube scans and display results.

### **e. Deployment Tools**

1. **Docker**: Integrate Jenkins with Docker to build images, deploy containers, and manage containerized environments.
    - Use the **Docker Pipeline Plugin** for seamless Docker integration in Jenkins pipelines.
2. **Kubernetes**: Use the **Kubernetes Plugin** to deploy Jenkins jobs to a Kubernetes cluster for scalable and efficient build management.

---

### **3. Managing Plugins in Jenkins**

### **Installing Plugins**:

1. Go to **Manage Jenkins** > **Manage Plugins**.
2. Click on the **Available** tab to see a list of plugins you can install.
3. Search for the desired plugin and click **Install**.

### **Managing Installed Plugins**:

1. Go to **Manage Jenkins** > **Manage Plugins** > **Installed**.
2. Here, you can update, disable, or uninstall plugins.
3. Keep plugins up to date to ensure compatibility and security.

### **Checking for Plugin Updates**:

- Regularly check for plugin updates under **Manage Jenkins > Manage Plugins** > **Updates** to ensure your Jenkins instance is using the latest features and fixes.

---

### **WebHook in Jenkins**

A **WebHook** is an HTTP callback mechanism that allows one system to notify another system of an event. In the context of Jenkins, WebHooks are commonly used to trigger Jenkins jobs or pipelines automatically when an event (such as a code push or pull request) occurs in an external system like **GitHub**, **GitLab**, or **Bitbucket**.

WebHooks enable continuous integration (CI) by initiating Jenkins builds in response to specific events, making your CI/CD pipeline more efficient and automated.

---

### **How WebHooks Work**

1. **Event Occurrence**: An event happens in an external system (e.g., a push to a Git repository).
2. **WebHook Trigger**: The external system sends an HTTP POST request to a pre-configured WebHook URL (Jenkins).
3. **Jenkins Receives the Request**: Jenkins listens for the incoming WebHook and processes the request.
4. **Job Triggered**: Jenkins triggers the corresponding job (or pipeline) based on the event received from the external system.

---

### **Setting up WebHook in Jenkins**

Here’s how to set up a WebHook to trigger a Jenkins job when there’s a code push to a GitHub repository:

### **Step 1: Configure Jenkins to Receive WebHooks**

1. **Install Necessary Plugins**:
    - To integrate Jenkins with GitHub, install the **GitHub Plugin** (or **GitLab Plugin** if using GitLab).
    - Navigate to **Manage Jenkins > Manage Plugins** and search for the plugin, then install it.
2. **Create a Jenkins Job**:
    - Create a **Freestyle Project** or a **Pipeline** job that you want to trigger with the WebHook.
    - In the **Source Code Management** section of the job configuration, select **Git** and enter your repository URL.
3. **Enable Build Trigger via WebHook**:
    - In the job configuration, under the **Build Triggers** section, check **GitHub hook trigger for GITScm polling** (for GitHub) or the equivalent option for other platforms (e.g., GitLab).
    - Save the job configuration.

### **Step 2: Set Up WebHook on GitHub (or GitLab, etc.)**

1. **Access the Repository Settings**:
    - Go to the repository in GitHub (or GitLab) that you want to integrate with Jenkins.
    - Navigate to **Settings** > **Webhooks**.
2. **Add a New WebHook**:
    - Click **Add webhook**.
    - In the **Payload URL** field, enter the Jenkins WebHook URL. This is usually in the form:
        
        ```
        http://<JENKINS_URL>/github-webhook/
        
        ```
        
        - Replace `<JENKINS_URL>` with your actual Jenkins server URL.
        - Ensure that Jenkins is publicly accessible, or use a reverse proxy for internal Jenkins servers.
3. **Choose Events**:
    - In GitHub, select the events that will trigger the WebHook. For example, you can select the **Push events** or **Pull request events**.
    - You can also select **Let me select individual events** if you want to customize the types of events that will trigger Jenkins.
4. **Set Content Type**:
    - Choose **application/json** as the content type.
5. **Save the WebHook**:
    - Once you've configured the WebHook, click **Add WebHook** to save it.

### **Step 3: Verify WebHook and Trigger Job**

1. **Test the WebHook**:
    - After setting up the WebHook, try pushing a commit to the repository (or triggering the event you configured in GitHub).
    - Jenkins should automatically trigger the job associated with the WebHook.
2. **Monitor Jenkins Job**:
    - Go to Jenkins and check that the job ran successfully by viewing the build logs.

---