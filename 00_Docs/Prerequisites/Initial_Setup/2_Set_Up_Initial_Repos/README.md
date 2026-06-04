# 🧑‍💻 Your Version Control Workflow

We can break down your specific workflow into two distinct Gitflows for the course:

1. Initial Setup: Setting Up Your Local and Remote Git Repos
2. Weekly Workflow: Working on Assignments

In this walkthrough, we’ll cover the Initial Setup.

## **Part I: Setting Up Your Local and Remote Git Repos**

You might be wondering: "*How do I make changes to this very repo that I’m reading right now?*" 

Short answer: **You don’t**!

Let’s set up the repo that you *will make changes to every week when doing your assignments.*

### 0️⃣ Pre-Requisites

First, do these things:

- [Set up your SSH key on GitHub.com](https://github.com/AI-Maker-Space/Interactive-Dev-Environment-for-AI-Engineers?tab=readme-ov-file#-setting-up-keys-and-tokens).
- If you're on Windows, [set up Windows Subsystem for Linux (WSL2)](https://github.com/AI-Maker-Space/Interactive-Dev-Environment-for-AI-Engineers?tab=readme-ov-file#rocket-lets-get-started).

### 1️⃣ Create a Brand New GitHub Repo

You can follow [this guide](https://docs.github.com/en/repositories/creating-and-managing-repositories/quickstart-for-repositories) if you need to, but creating a blank repo is pretty straightforward. A few notes on the seeing you should use, as shown below.

1. Please use the **repository name** that corresponds to your cohort! e.g., AIEC1. Don't get fancy with the name - your life will be easier if you keep the name simple.
2. The process will be easiest if you make sure **Add a README file is deselected**.

![image](https://i.imgur.com/WQtlxc5.png)

🎉 Congrats! *You’ve just created an empty remote repository on GitHub.*

### 2️⃣ Get [Secure Shell Protocol (SSH)](https://en.wikipedia.org/wiki/Secure_Shell) Address

Once you've created your new repository, copy the repo’s SSH address. You'll want to copy this address as shown below. Click the 'copy' icon at the end of the address bar 

![image](https://i.imgur.com/62QNyfz.png)

### 3️⃣ Clone Your GitHub Repo Locally

Execute the command:

```
git clone git@github.com:yourusername/yourrepo.git
```

Then we need to Change Directory, or `cd` into our newly cloned repository!

```
cd yourrepo
```

> *If you see a warning message like: `warning: You appear to have cloned an empty repository`that means you've done everything right!
> 

🎉 Congrats! *You’ve just cloned your empty remote repo locally to your machine using an SSH key.*

### 4️⃣ Add Class Repo as an Upstream Remote

First, run this command:

```markdown
git remote add upstream git@github.com:AI-Maker-Space/The-AI-Engineering-Certification-v1.0.git
```

Verify both remotes are connected. *You should see both "origin" (your repo) and "upstream" (class repo)*.

```
git remote -v
```

You should see an output very similar to this (your origin will be a different address)

```
origin  git@github.com:yourusername/yourrepo.git (fetch)
origin  git@github.com:yourusername/yourrepo.git (push)
upstream        git@github.com:AI-Maker-Space/The-AI-Engineering-Certification-v1.0.git (fetch)
upstream        git@github.com:AI-Maker-Space/The-AI-Engineering-Certification-v1.0.git (push)

```

🎉 Congrats! *You’ve just connected AI Makerspace’s remote class repo (which we manage) to your remote class repo (which you manage)!*

### 5️⃣ Your First [Pull](https://git-scm.com/docs/git-pull)

It’s time to pull down the course materials from AI Makerspace’s remote repository, which is upstream of both your local and remote repos.

> *You will do this each week as new assignments are released!
> 

```markdown
git pull upstream main --allow-unrelated-histories
```

🎉 Congrats! *You’ve just pulled down course materials from AI Makerspace’s remote repo, **down to your local repository**.*

### 6️⃣ Your First [Push](https://git-scm.com/docs/git-push)

Now we need to push everything up from our local repo to our remote repository on GitHub.com

```markdown
git push origin main
```

🎉 Congrats! *You just pushed the course materials in your local repo up to your remote repo (origin) on GitHub.com. 

> During steps 5️⃣ and 6️⃣, notice the use of `main`.`main` is simply the name given to the [default branch](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/about-branches#about-the-default-branch) in a repo.
> 
