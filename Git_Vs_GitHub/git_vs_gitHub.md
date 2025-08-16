# Git vs GitHub

## 1. What is Git?
- **Type:** Distributed Version Control System (DVCS)  
- **Created by:** Linus Torvalds in 2005  
- **Purpose:** Tracks changes in source code during software development  

### Key Features
- Works locally without internet  
- Branching & merging support  
- Stores history of changes  
- Lightweight and fast  

**Usage:** Developers use Git commands (`git init`, `git add`, `git commit`, etc.) to manage repositories on their system.  

---

## 2. What is GitHub?
- **Type:** Cloud-based hosting platform for Git repositories  
- **Owned by:** Microsoft  
- **Purpose:** Provides a central place to store, collaborate, and share Git repositories  

### Key Features
- Remote repository hosting  
- Collaboration tools (Pull Requests, Issues, Wiki)  
- CI/CD integration (GitHub Actions)  
- Access control & permissions  
- Social coding (followers, stars, forks)  

---

## 3. Main Difference

| Feature           | Git (Tool)                           | GitHub (Platform)                          |
|-------------------|--------------------------------------|--------------------------------------------|
| **Definition**    | Local version control system         | Cloud-based hosting service for Git repos  |
| **Scope**         | Works on local machine               | Requires Git to work                       |
| **Internet**      | Not needed                           | Needed (for remote operations)             |
| **Collaboration** | Limited to local sharing             | Easy collaboration, PRs, discussions       |
| **Ownership**     | Open-source                          | Microsoft                                  |


# Git vs GitHub – Interview Points

## 🔹 Basic Questions

**Q1. What is Git?**  
A distributed version control system to track code changes.

**Q2. What is GitHub?**  
A cloud-based platform to host Git repositories and collaborate.

**Q3. Difference between Git and GitHub?**  
- Git is the **tool** (VCS).  
- GitHub is the **service/platform** to host and collaborate.  

**Q4. Do you need GitHub to use Git?**  
No. Git can be used standalone. GitHub just provides hosting & collaboration.  

---

## 🔹 Intermediate Questions

**Q5. How do Git and GitHub work together?**  
- Git manages code locally.  
- GitHub allows remote storage, collaboration, and integration.  

**Q6. What are GitHub alternatives?**  
- GitLab  
- Bitbucket  
- SourceForge  

**Q7. How do you push code from Git to GitHub?**  
1. Initialize local repo (`git init`)  
2. Add remote (`git remote add origin <url>`)  
3. Push (`git push origin main`)  

**Q8. What is a Pull Request (PR)?**  
A feature of GitHub (not Git) for merging code collaboratively.  

---

## 🔹 Advanced / Scenario Questions

**Q9. How do you manage conflicts when collaborating on GitHub?**  
- Use `git fetch`, `git merge`  
- Resolve conflicts manually  
- Commit and push updated code  

**Q10. Difference between Fork and Clone in GitHub?**  
- **Clone:** Copy repository to your **local machine**  
- **Fork:** Copy repository under your **GitHub account** to propose changes  

**Q11. Can Git be used without GitHub in a corporate environment?**  
Yes. Companies often host private Git servers (GitLab, Bitbucket, or self-hosted Git).  
