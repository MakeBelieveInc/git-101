# Git 101
Presentation materials for Git learning session

## Part 1: Conceptual Overview

### What Does Distributed Version Control Mean?
  1. No central authority; the "main repository" exists, but there's nothing special about it
  2. Each user has a copy of the entire change history
  3. Delta-based rather than file-based
    - Can start from initial state and construct current state from the change history
    - Concurrent development is much simpler
      - Analogy: team arithmetic

### Basic Git Vocabulary
  1. Pull
  2. Push
  3. Merge
  4. Commit
  5. Add
  6. Branch
    - much simpler and more important to the workflow than with TFS
    - more on this in the next part
  8. Remote

##Part 2: Branching and the Version Tree

### GitFlow-Like Branching Strategy (whiteboard diagram)
  1. (optional) Create fork with GitHub-style origin? Save for demo?
  2. Create branch
    - new branch for each feature/task 
    - all work is done in a branch
  3. Make changes
  4. Multiple local commits in the same branch; they're not getting pushed anywhere yet
  5. Team pushes commits to master while we're working
  6. Rebase branch, merge in new changes from master
    - keeps all this feature's commits consecutive once they're back in master
    - optional: squash commits with `rebase -i`
  7. Merge branch back into master

**Talking point: Ease of moving back and forth through time leads to microversioning, which leads to being able to choose any point in history and promote it to UAT/Production, which leads to continuous deployment**

## Part 3: Git in Action

##Demo: Detailed Happy-Path (c9.io + GitHub)
  1. Show original repo on GitHub
  2. Fork: upstream/master => origin/master (origin takes the place of a Develop branch)
  3. Clone: origin/master => local/master

        mv .c9 ..
        git clone [url] .
        mv ../.c9 .
        
    - or init, remote add, pull
    
  4. Remote

        git remote -v
        git remote --add upstream [url]
        git remote -v

    - Show that we now have origin and upstream remotes, explain difference
  5. Branch: local/master => local/task123

        git checkout -b task123
        
  6. Make changes: local/task123
    - Edit an existing file
    - Add a new file and explain `git add`
  7. Commit: local/task123 

        git commit -am "[task123] I did some stuff"
        
  8. Checkout: local/master

        git checkout master
        
    - Show that files have changed
  9. Pull: upstream/master => local/master

    `git pull upstream` or `git pull upstream/master`
    
  10. Checkout: local/task123

        git checkout task123
        
    - show that it hasn't changed while we were on local/master
  11. Rebase: local/task123 => updated local/master

    `git rebase master` or `git rebase -i master`
        
    - move local/task123 commits up to new position on local/master
    - merge in all team commits between old position and new one
  12. Push: local => origin
    1. Option 1: push local branch to origin branch

        git push task123 origin/task123
        
    2. Option 2: merge local branch down to master, push to origin/master
  13. Pull request: origin/task123 => upstream/master
  14. Merge on GitHub: origin/task123 => upstream/master
  15. Delete branches: local/task123, origin/task123

        git branch -d task123
        git branch -d origin/task123
