# [Insert Project Name]

## Project Description
Provide a high-level summary of the project.

### Purpose and Objectives
Describe the purpose of the project and what it aims to achieve.

### Scope and Key Deliverables
Define what is included and excluded from scope.

List key deliverables, for example:
- Analytical outputs
- Code deliverables
- Documentation

### Expected Timelines
Provide the overall project timeline or key milestones.

## Table of Contents

- [Access & Technology Requirements](#access-technology-requirements)
- [Key Outputs](#key-outputs)
- [Key People](#key-people)
- [How to Run Analysis](#how-to-run-analysis)
- [Caveats](#caveats)
- [Audit / QA](#audit--qa)
- [Want to Make Changes?](#want-to-make-changes)
- [Frequently Asked Questions](#frequently-asked-questions)



## Access & Technology Requirements <a name = 'access-technology-requirements'></a>
List any systems, tools, or permissions required to deliver the project.

| Role / Permission | Description |
|------------------|-------------|
|                  |             |
|                  |             |
|                  |             |


## Information & Data Sources
Details of where relevant files, data, and code are stored.

### Shared File Areas
List and link any shared file areas for the project.

### Data Sources

| Data Source Name | Description |
|------------------|-------------|
|                  |             |
|                  |             |


## Key Outputs <a name = 'key-outputs'></a>
Define the primary deliverables produced by the project.

### Deliverables
- Reports
- Dashboards
- Code repositories
- Documentation


## Key People <a name = 'key-people'></a>
List key contacts and contributors.

**Project Lead:**  
Name / role

**Stakeholders:**  
Name / role

**Analysts and Contributors:**  
Name / role


## How to Run Analysis <a name = 'how-to-run-analysis'></a>
Provide detailed, step-by-step guidance on how to run the analysis.

Include:
- Script locations
- Naming conventions
- Runtime assumptions
- Dependencies between steps


## Caveats <a name = 'caveats'></a>
Provide a brief overview of key assumptions, decisions, or limitations.

More detailed and formal records of assumptions, decisions, and limitations can be found in the **Assumptions, Decisions & Limitations (AD&L) Log**.


## Audit / QA <a name = 'audit--qa'></a>

### Assumptions, Decisions & Limitations Log
- **[AD&L Log Template](AD&L%20Log%20Template.xlsx)**:  Use this log to record all assumptions, decisions, and limitations.

**Guidance:**
- Prior to starting the analysis, record any **starting / baseline assumptions** in the AD&L Log.
- Any new assumptions, decisions, or limitations identified during the analysis must also be recorded in the log.
- Where an assumption, decision, or limitation relates to a code change, the associated **GitLab merge request ID** must be recorded in the log (where prompted).


### Code QA via Merge Requests

Code is QA’d systematically whenever a new merge request is created.

- QA is documented directly in the merge request description using a **standardised template**
- Assumptions, decisions, and limitations relating to a merge request are recorded **only** in the AD&L Log (not in the merge request description)

To review QA on changes made to the codebase:
- Check merge request descriptions, which follow the standard template below:
  - **[QA Merge Request Template](.gitlab/merge_request_templates/QA.md)**

More detail on this process is provided in the next section.


## Want to Make Changes? <a name = 'want-to-make-changes'></a>

### Core Branches

Before making changes, it is important to understand the core branches in the repository and how each should be treated:

- `main` is the original branch and should never be edited directly. Only the `dev` branch should be merged into `main` periodically, to act as a backup of `dev`.
- `dev` is branched off from `main` and acts as the primary working branch that other changes are merged into. It should not be edited directly either.

### Workflow for Making Changes

To contribute to the project, always create a **new branch from `dev`**.

#### 1. Sync your repository

Run the following before starting work (do this regularly):

```
git fetch origin

git status
```

 * `git fetch origin` retrieves the latest updates from the remote repository
 * `git status` confirms:
    * Your current branch
    * Whether you are up to date
    * Any staged/unstaged changes

#### 2. Create a new branch from dev

```
git checkout dev

git pull origin dev

git checkout -b <your-branch-name>

git push -u origin <your-branch-name>
```

This will:

 * Switch to dev
 * Pull the latest version of dev
 * Create a new branch from dev
 * Push the new branch to the remote and enable tracking


#### 3. Make and push your changes

Once you’ve made your updates:
```
git status

git add -A

git commit -m "DESCRIPTION OF CHANGES"

git push origin <your-branch-name>
```

 * git status: Confirm you are on the correct branch
 * git add -A: Stage all changes
 * git commit: Save changes with a clear message
 * git push: Upload changes to the remote repository


#### 4. Merging your changes to dev

Once your branch has been pushed to the remote repository, create a merge request by selecting **“New merge request”** in GitLab.
Ensure:

- The source branch is your test branch
- The target branch is dev (or whichever branch you are merging into)

On the next screen:

- Select “Choose a template”
- Choose [QA Merge Request Template](.gitlab/merge_request_templates/QA.md), the standardised merge request template referenced in the Audit / QA section
- Complete the sections under **“Analyst”**
- Assign a reviewer (the person who will be QA‑ing your work). The reviewer must complete the sections under **“QA reviewer”**.
- Ensure **“Delete source branch”** is selected so that your test branch is removed once merged.

*NOTE: The merge request description can be edited before the merge is completed, but not after the merge has occurred. All QA must therefore be completed prior to merging.*

Any assumptions, decisions, or limitations arising from the change must be recorded in the AD&L Log (linked in the QA template), including the merge request ID.

If you are unsure how to deal with conflicts or other issues within a merge request, contact a team member who will be able to advise.

Once the code has been independently QA‑ed and all issues resolved, select “Merge” to merge your changes into dev.


### Rebasing 

Sometimes you will have instances where new updates or changes have been made to the `dev` branch. To prevent your branch from becoming out of date, you will want to rebase it with the most recent commits from `dev`.

Rebasing can be time-consuming if your code has diverged significantly from `dev`. For this reason, it's recommended to rebase your branch whenever a new merge occurs on `dev`. This will allow you to incorporate new changes from `dev` into your branch while preserving your own modifications.

To start the rebase, run the following lines of code in your R terminal. Please run each line one at a time:

```
git branch

git checkout <your new branch name>

git fetch origin

git rebase origin/dev

```

There will lilely be conflicts when you attempt to rebase. When a conflict occurs, your R terminal will look like this:

```
Auto-merging ..........
Auto-merging ..........
CONFLICT (content): Merge conflict in ..........
CONFLICT (modify/delete): .......... deleted in HEAD and modified in .......... (Rebase 1).  Version .......... (Rebase 1) of .......... left in tree.
error: could not apply ............. Rebase 1
hint: Resolve all conflicts manually, mark them as resolved with
hint: "git add/rm <conflicted_files>", then run "git rebase --continue".
hint: You can instead skip this commit: run "git rebase --skip".
hint: To abort and get back to the state before "git rebase", run "git rebase --abort".
Could not apply ............. Rebase 1

```

To resolve the conflicts, you will need to open the scipts in your coding environment that are listed in the terminal and find the conflict within them. In the above example, I have two conflicts denoted by 'CONFLICT'. If I then open the .......... script, I will find the conflicting code, which will be highlighted in the following style:

```
<<<<<<< HEAD
df2V1 <- function(df1v1)

=======
df2V2 <- function(df1v2)
print(df2V2)

>>>>>>> .......... (Rebase 1)
```

You will need to decide which version to keep. If you are unsure which part to keep, contact another team member. 

To do this, remove the unwanted code plus the additional formatting lines with < or =. Again, using the example above, if I wanted to keep the first version of code (underneath the HEAD), I would need to remove all of the other code around it. See below:


```
df2V1 <- function(df1v1)

```

Once all of the scripts with conflicts have been resolved, use the following command to continue with the rebase: 

```
git add .

git rebase --continue
```

After this, your terminal will enter into an interactive shell. To exit this please just type:

```
:q

# and press enter
```

There may be other commits to rebase with conflicts, so you will need to repeat the above process of rebasing until these are all resolved. 

Once all of the commits have been rebased, the following message will appear in your terminal: 

```
Successfully rebased and updated
```

Run the commands below, and you will have successfully rebased your branch and pushed the changes to the remopte repository.

``` 

git commit -m "Successful rebase of my branch"

git push -u origin <your new branch name>

```

If for whatever reason you need to stop the rebase, you can 
use the command below, and this will abandon the rebase, returning your branch to how it was before. 

``` 
git rebase --abort

```

## Frequently Asked Questions <a name = 'frequently-asked-questions'></a>

<details>
<summary><b>What is Git?</b></summary>

<p>Git is a version control system that tracks changes to files over time.</p>

</details>

<details>
<summary><b>Why is Git useful?</b></summary>

<ul>
<li>Tracks history of changes</li>
<li>Enables collaboration without overwriting work</li>
<li>Allows rollback to previous versions</li>
</ul>

</details>

<details>
<summary><b>What is the difference between local and remote?</b></summary>

<ul>
<li><b>Local</b> → on your machine (where you work)</li>
<li><b>Remote</b> → hosted online (e.g. GitLab)</li>
</ul>

</details>

<details>
<summary><b>How do I get the files from the repository on my local machine?</b></summary>

<p>Get the HTTPS URL from GitLab and run:</p>

<pre><code>git clone &lt;repo_url&gt;</code></pre>

<p>This creates a local copy of the repository.</p>

</details>

<details>
<summary><b>When I clone the repository, where is it saved?</b></summary>

<p>In the current directory where you run <code>git clone</code>.</p>

</details>

<details>
<summary><b>How should I work using Git?</b></summary>

<p>Recommended workflow:</p>

<ol>
<li>Branch off <code>dev</code></li>
<li>Push the new branch (so it is tracked remotely):</li>
</ol>

<pre><code>git push -u origin &lt;branch_name&gt;</code></pre>

<ol start="3">
<li>Make changes</li>
<li><code>git add</code> (stage)</li>
<li><code>git commit</code> (save locally)</li>
<li><code>git push</code> (upload)</li>
</ol>

</details>

<details>
<summary><b>What is a branch?</b></summary>

<p>A branch is a separate line of development used to work on features independently.</p>

</details>

<details>
<summary><b>How do I know I am on the correct branch?</b></summary>

<pre><code>git branch</code></pre>

<p>The current branch is marked with <code>*</code>.</p>

</details>

<details>
<summary><b>How do I know if I have made changes?</b></summary>

<pre><code>git status</code></pre>

<p>This shows modified, staged, and untracked files.</p>

</details>

<details>
<summary><b>What is <code>git add</code>?</b></summary>

<p>Stages changes so they can be included in a commit.</p>

</details>

<details>
<summary><b>What does staged vs unstaged mean?</b></summary>

<ul>
<li><b>Unstaged</b> → changes in your files</li>
<li><b>Staged</b> → changes ready to be committed</li>
</ul>

</details>

<details>
<summary><b>What does a commit do?</b></summary>

<p>Saves a snapshot of your changes in the local repository.</p>

</details>

<details>
<summary><b>What does <code>git push</code> do?</b></summary>

<p>Uploads your commits to the remote repository.</p>

</details>

<details>
<summary><b>How do I get the latest changes from Git?</b></summary>

<pre><code>git pull</code></pre>

<p>Fetches and merges updates from the remote.</p>

</details>

<details>
<summary><b>What is <code>git pull</code> vs <code>git fetch</code>?</b></summary>

<ul>
<li><code>pull</code> = fetch + merge</li>
<li><code>fetch</code> = download changes only</li>
</ul>

</details>

<details>
<summary><b>What does merging a branch mean?</b></summary>

<p>Combining changes from one branch into another.</p>

</details>

<details>
<summary><b>What is a merge conflict?</b></summary>

<p>Occurs when Git cannot automatically combine changes and needs manual resolution.</p>

</details>

<details>
<summary><b>What if I forget to <code>git pull</code> before working?</b></summary>

<p>You may encounter merge conflicts when pushing or merging.</p>

</details>

<details>
<summary><b>What happens if my branch is out of sync?</b></summary>

<ul>
<li>You will need to pull or rebase</li>
<li>You may need to resolve conflicts</li>
</ul>

</details>

<details>
<summary><b>What happens if I make changes I don’t want?</b></summary>

<ul>
<li><b>Before commit:</b><br>
<pre><code>git restore .</code></pre>
</li>
<li><b>After commit:</b> 
<pre><code>git revert</code></pre>
</li>
</ul>

</details>

<details>
<summary><b>What if I push changes but want to undo them?</b></summary>

<ul>
<li>Use <code>git revert</code> </li>
<li>Or create a new commit to fix the issue</li>
</ul>

</details>


<details>
<summary><b>What does <code>git revert</code> do?</b></summary>

<p>Creates a new commit that undoes the changes from a previous commit, without deleting history.</p>

</details>

<details>
<summary><b>How do I use <code>git revert</code>?</b></summary>

<pre><code>git revert &lt;commit_hash&gt;</code></pre>

<p>This will create a new commit that reverses the changes from the specified commit.</p>

</details>

<details>
<summary><b>When should I use <code>git revert</code>?</b></summary>

<ul>
<li>When changes have already been pushed to the remote</li>
<li>When you want to undo changes safely without rewriting history</li>
</ul>

</details>


<details>
<summary><b>How do I keep changes but not commit them?</b></summary>

<ul>
<li>Leave them uncommitted</li>
<li>Use <code>git stash</code> if you need to switch branch</li>
</ul>

</details>

<details>
<summary><b>What happens if I delete the Git folder locally?</b></summary>

<ul>
<li>You can re-clone the repository</li>
<li>Any uncommitted changes will be lost</li>
</ul>

</details>

<details>
<summary><b>Why do I need a personal access token?</b></summary>

<p>Used instead of passwords for secure authentication when pushing/pulling.</p>

</details>

<details>
<summary><b>How should I store a personal access token?</b></summary>

<ul>
<li>Never hard-code it</li>
<li>Use a credential manager or environment variables</li>
</ul>

</details>

<details>
<summary><b>What should I do after making changes?</b></summary>

<pre><code>git add -A
git commit -m "message"
git push</code></pre>

</details>

<details>
<summary><b>Should I commit often?</b></summary>

<p>Yes — small, frequent commits are best practice.</p>

</details>

<details>
<summary><b>What is a good commit message?</b></summary>

<p>A short, clear description of what changed.</p>
