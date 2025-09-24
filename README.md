## Class: Reproducibility: A Crash Course in Git & GitHub

**Objective:** By the end of this session, students will be able to create a local Git repository, track changes, push their project to a remote GitHub repository, and understand the basic branching workflow for collaboration.

#### Prerequisites:
1.  **Install Git:** Please install Git on your laptop from [git-scm.com](https://git-scm.com).
2.  **Create a GitHub Account:** Sign up for a free account at [github.com](https://github.com).
3.  **Configure Git:** Open your terminal (or Git Bash on Windows) and run these two commands with your own information:
    ```sh
    git config --global user.name "Your Name"
    git config --global user.email "youremail@vt.edu"
    ```
---

#### Why Git, why Github

* **The Problem:** How many of you have a directory with files that look like this? 
    `thesis_v1.docx`
    `thesis_v2_final.docx`
    `thesis_v2_final2.docx`
    `thesis_v2_final2_FOR_REAL_this_time.docx`

* **The Solution: Version Control.** Version control is a system that records changes to files over time, allowing you to recall specific versions later. It's like an unlimited "undo" button for an entire project.

* **Git vs. GitHub** 
    * **Git:** The software that runs on your computer to track changes locally.
    * **GitHub:** A website that hosts your Git projects (serves as a remote repository) in the cloud, enabling backup, sharing, and collaboration.
    * **Analogy:** Git is [very much un-] like Microsoft Word (the program on your computer), and GitHub is like Google Docs (the cloud platform where you store files and collaborate).

---
#### The Core Workflow - Solo Researcher 

1.  **Create a Project & Initialize Git**
    * Open your terminal, create a new project directory, and move into it.
        ```sh
        mkdir myFirstGitProject
        cd myFirstGitProject
        ```
    * Initialize a new Git repository. This command creates a hidden `.git` subdirectory.
        ```sh
        git init
        ```
2.  **Check the Status**
    * The most important command: `git status`. It tells you the current state of your repository.
        ```sh
        git status
        ```
3.  **The `add` & `commit` Cycle (The Heart of Git)**
    * Create a simple `README.md` file.
        ```sh
        echo "# This is a README for my first git project" > README.md
        ```
    * Tell Git to track (stage) the new file. The **staging area** is like a draft of your next snapshot.
        ```sh
        git add README.md
        ```
    * **Commit** the staged file to take a permanent snapshot. The `-m` flag is for the required commit message.
        ```sh
        git commit -m "Initial commit: Add project README"
        ```
4.  **Make Another Change**
    * Modify the README and add a mock script.
        ```sh
        echo "This project does some really cool stuff." >> README.md
        echo "echo "hello World!"" > helloWorld.sh
        ```
    * Add and commit all changes. The `.` refers to the current directory.
        ```sh
        git add .
        git commit -m "Add helloWorld script and update README"
        ```
5.  **View Your History**
    * Use `git log` to see the history of your commits.
        ```sh
        git log --oneline
        ```
6. **DOs and DONTs**
    * DONT use git to track raw data or other large files that will only be read! Never edit your data files (use scripts to read them when you need them)! Add your data files to a `.gitignore` file in the main git directory
    * DO use multiple git projects! DONT do everything under one git repo, you will become over burdened trying to keep up...
    * DO commit often! Its a lot harder to keep up if you only commit changes every few weeks. 
    * DONT commit all files all at once when a lot of change are made unless they are all related to the same issue


---
#### Going Remote with GitHub 

0. **create an SSH Key For Your Remote**
    * Check to see if you have already made an ssh key
        ```sh
        cd # navigate to your home directory
        ls .ssh/ # list files in your ssh directory
        ```
    * You should see a pair of private/public keys called something like `id_rsa`  and `id_rsa.pub`.
    * If you **DO NOT** already have an ssh key, make one using the following:
        ```sh
        ssh-keygen -t rsa -b 4096
        ```
    * Then navigate back to your new project directory.
    * log into github.com
    * Navigate to Settings, SSH and GPG keys. Then add a new SSH key.

1.  **Create a Remote Repository**
    * In your web browser, go to github.com, login and click "New repository."
    * Name it `myFirstGitProject`.
    * **Important:** Leave it public and **DO NOT** initialize it with a README, .gitignore, or license.

2.  **Connect Local to Remote**
    * GitHub will now show you commands under "...or push an existing repository from the command line." Copy and paste them into your terminal:
        ```sh
        git remote add origin [https://github.com/YOUR_USERNAME/myFirstGitProject.git](https://github.com/YOUR_USERNAME/myFirstGitProject.git)
        git branch -M main
        ```
3.  **Push Your Code!** 🚀
    * This command sends your commit history from your local machine up to GitHub.
        ```sh
        git push -u origin main
        ```
    * Refresh your GitHub page. Your files are now online!

---

#### Collaboration with Branches 

* **The Concept:** Never* work directly on your `main` branch. For any new feature, create a separate **branch** to work in safely. The `main` branch should always be your stable, working version.

1.  **Create and Switch to a New Branch**
    * This command creates a new branch called `newAnalysis` and immediately switches you to it.
        ```sh
        git checkout -b newAnalysis
        ```
2.  **Do Some Work on the Branch**
    * Create a new file, then add and commit it.
        ```sh
        echo "Preliminary results look promising." > results.txt
        git add results.txt
        git commit -m "Add preliminary results file"
        ```
3.  **Push the New Branch to GitHub**
    ```sh
    git push origin newAnalysis
    ```
4.  **The Pull Request (PR)**
    * Go to your GitHub repository in the browser. Click the **"Compare & pull request"** button.
    * A **Pull Request** is a formal request to merge your changes from one branch into another. This is the heart of collaboration where others can review your work.
    * Give it a title, click "Create pull request," and then "Merge pull request."

5.  **Update Your Local Machine**
    * To get the newly merged changes back to your local machine:
        ```sh
        git checkout main
        git pull origin main
        ```
---
#### Wrap-up & Resources 

**Recap the Full Workflow:**
    
1.  `git pull`
2.  `git checkout -b <new-branch-name>`
3.  *Do your work...*
4.  `git add .`
5.  `git commit -m "Descriptive message"`
6.  `git push origin <new-branch-name>`
7.  Open a **Pull Request** on GitHub.

**Key Command:** When in doubt, run `git status`.

**Resources:**
  * AI! is really good at this stuff. Ask it!
  * You can find this tutorial at `github.com/nsantantonio/exampleGit`
  * Here is a work in progress to show how an entire research can be completed start to finish, including data cleaning, analysis, figure generation and manuscript preparation `github.com/nsantantonio/reproducibleScience`
