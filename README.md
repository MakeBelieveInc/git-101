# Git 101
Presentation materials for Git learning session

### Part 1: Conceptual Overview
1. Distributed Version Control model
  1. No central authority; the "main repository" exists, but there's nothing special about it
  2. Each user has a copy of the entire change history
  3. Delta-based rather than file-based
    - Can start from initial state and construct current state from the change history
    - Concurrent development is much simpler
      - Analogy: team arithmetic
2. Simplified workflow 
  - diagrams/vocabulary only, no demo yet
    1. Clone
    2. Branch
      - much simpler and more important to the workflow than with TFS
      - more on this in the next part
    3. Commit
    4. Pull
    5. Merge
    6. Push

### Part 2. Branching and forking
1. Git branching strategy with GitHub-style origin
  1. OPTIONAL: Cover forking now? Later during demo?
  2. Create a branch for each feature/task - all work is done in a branch
  3. Make changes
  4. Multiple local commits in the same branch; they're not getting pushed anywhere yet
  5. Team pushes commits to master while we're working
  6. Rebase branch, merge in new changes from master
    - keeps all this feature's commits consecutive once they're back in master
    - optional: squash commits with `rebase -i`
  7. Merge branch back into master
2. Ease of moving back and forth through time leads to microversioning, which leads to being able to choose any point in history and promote it to UAT/Production, which leads to continuous deployment

### Part 3: Real-world demo  
1. Workflow - Detailed (happy path)
  1. Fork: upstream/master => origin/master (origin takes the place of a Develop branch)
  2. Clone: origin/master => local/master
    - or init, remote add, pull
  3. Remote
      1. `git remote -v`
      2. `git remote --add upstream [url]`
      3. `git remote -v` 
      4. Show that we now have origin and upstream remotes, explain difference
  4. Branch: local/master => local/task123
    - `git checkout -b task123`
  5. Make changes: local/task123
    1. Edit an existing file
    2. Add a new file and explain `git add`
  7. Commit: local/task123
    - `git commit -am "[task123] I did some stuff"`
  8. Checkout: local/master
    1. `git checkout master`
    2. Show that files have changed
  9. Pull: upstream => local
    - upstream/master => local/master
  10. Checkout: local/task123
    - show that it hasn't changed while we were on local/master
  11. Rebase: local/task123 => updated local/master
    - move local/task123 commits up to new position on local/master
    - merge in all team commits between old position and new one
  12. Push: local => origin
    - upstream/master => origin/master
    - local/task123 => origin/task123
    - ALTERNATIVE: Merge local branch into local master and push that to origin
  13. Pull request: origin/task123 => upstream/master
  14. Merge: origin/task123 => upstream/master
  15. Delete branches: local/task123, origin/task123
    1. `git branch -d task123`
    2. `git branch -d origin/task123`
