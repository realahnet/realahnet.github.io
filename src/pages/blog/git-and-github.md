---
layout: ../../layouts/BasePostsLayout.astro

name: "An Introduction to Git and GitHub"
desc: "In this blog, we'll look at Git and GitHub with their real-world applications."
top_desc: "Git and GitHub"
date: "12 November 2025"
time: "8 min"
---

# An Introduction to Git and GitHub

<img src="https://media.licdn.com/dms/image/v2/D4D12AQFS_42v39bhsA/article-cover_image-shrink_720_1280/article-cover_image-shrink_720_1280/0/1675016970735?e=2147483647&v=beta&t=9c2zQlKEcKJmEUgiVj-WH6SyNGMttabxrIlZ99HbttI" alt="Git Cover Photo">

## Introduction

Git is one of the most important and popular tools used by developers today. It helps teams manage changes without losing track of progress or creating conflicts. In this post we'll explore the fundamentals of Git and GitHub and look at their real-world applications.

## What is Git?

Git is a version control system that lets you save snapshots of your code, known as commits, so you can track changes in your project over time.

Git also makes it easy to create separate versions of your work using branches, try out your code at various points, and revert to earlier states if needed. By connecting your repository to a remote service like GitHub, Git also enables smooth collaboration without conflicting changes.

## History of Git

Git was created by Linus Torvalds in 2005 after the Linux kernel team lost access to the version control system they used (BitKeeper). It was designed to handle large, distributed projects efficiently and allow developers to work together without conflicts.

Over the years, Git has grown into one of the most widely used tools in software development, being used in projects of all kinds across many different fields.

---

## How Git Works

### Repositories

Let's understand what a repository is. It is like a space where all the files and their history are stored. On your computer, you work in the working directory, where you edit files, and when you’re ready to save changes, you move them to the staging area. From there, you create a commit, which is like taking a snapshot of your project at that moment, with a descriptive message explaining the changes. A new repository is initialized by the command <code>git init</code>.

### Staging Changes

Let's think of it like a waiting area for your changes until you have added them into Git. Git doesn't automatically stage your changes. It is done via the <code>git add</code> command. This lets you carefully choose which changes to commit, and you can make multiple commits from different staged sets of changes. Think of it as preparing a snapshot before saving it permanently to your project’s history.

### Commits

Commits are snapshots of your code that record the changes that have happened at a particular point. Before a commit is created, your changes are staged as shown in the previous section, which prepares them to be saved. Then a commit is created by the command, <code>git commit</code> and it includes a descriptive commit message explaining the changes.

### Branches

A branch is a separate version of your code that diverges from a common point, which may be a shared commit across all branches. It allows each version to work independently of each other. Furthermore, branches allow various developers to collaborate and maintain their own versions of code, and when the testing is done, the changes can be merged into the production branch.

---

## What is GitHub?

Unlike Git, which is a tool, GitHub is an online platform where repositories are pushed to. It is one of the most popular Git hosting services, where many of the famous open-source projects reside.

GitHub makes collaboration and project management easier: you can create remote repositories to store your code online, submit pull requests for code review, track progress and bugs through issues, and use built-in tools to work with teams with the best efficiency. GitHub also supports automated testing and deployment of your code whenever changes are pushed via GitHub Actions.

## Should You Learn Git?

Absolutely. Learning Git is essential for any developer. The benefits of Git have already been outlined in this blog, but looking at it practically, using Git grants the developers the magic power to achieve maximum efficiency by collaborating together. It is a unique way that never ends up causing conflicts between different developers on the same project.

Git and GitHub are widely used in the industry and in open-source projects. Knowing Git makes it easier to contribute to real-world projects and grants you the ability to participate in many real-world jobs that utilize version control systems.

## Practical Example

Let's say I made a portfolio website, and I want to host it somewhere. Since a portfolio site is always mostly static, I can use GitHub Pages. GitHub allows you to host a static website as long as no backend stuff is being done completely for free! This is amazing for students that are looking forward to creating their own websites or getting started with web development.

<ol>

<li>First, create a new GitHub repository.</li>
<li>
    Configure your username and email ID:
    <pre class="text-center max-w-full overflow-x-auto"><code class="block">git config --global user.name "user-name-here"</code></pre>
    <pre class="text-center max-w-full overflow-x-auto"><code class="block">git config --global user.email "user-email-here"</code></pre>
</li>

<li>
    Initialize your local repository with:
    <code class="block text-center w-full">git init</code>
</li>

<li>
    Link your local repository with GitHub by running the following command:
    <code class="block text-center w-full">git remote add origin repo-url</code>
</li>

<li>
    Stage your commits by running the following command:
    <code class="block text-center w-full">git add .</code>
    <p class="italic">Note: using '.' here adds all of the files inside the folder.</p>
</li>

<li>
    Create a commit message by running the following command:
    <code class="block text-center w-full">git commit -m "message-here"</code>
</li>

<li>
    Push your changes to GitHub by running the following command:
    <code class="block text-center w-full">git push -u origin branch-name</code>
</li>
</ol>

Your code should now be on GitHub!

---

# Summary

From this blog, we have seen that Git and GitHub are powerful tools that make managing code and collaborating with others much easier. Git helps you track changes and maintain a complete history of your project, while GitHub allows you to share your work, contribute to open-source projects, and collaborate efficiently.

By mastering Git, you open yourself to a world full of opportunities. It gives you confidence in managing your code and opens your door to contributing to real-world projects. The best way to get started with Git is to start using it in your own projects. The more you practice, the more natural version control will become in your development workflow.
