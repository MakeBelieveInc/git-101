# Git 101
Presentation materials for Git learning session

## Conceptual Overview
1. Distributed Version Control model
  1. No central authority; the "main repository" exists, but there's nothing special about it
  2. Each user has a copy of the entire change history
2. Workflow - Diagram only
  1. Fork
  2. Branch
  3. Commit
  4. Pull - Upstream master to local master
  5. Merge - Master to branch
  6. (optional, not preferred) Merge to local master
  7. Push to origin
  8. Merge to main
 
## Real-world operation  
1. Workflow - Detailed (happy path)
  1. Fork
  2. Clone
    - or init/remote pull
  3. Remote add upstream
  4. Branch
  5. Make changes
  6. Add
  7. Commit
  8. Pull upstream master
  9. Rebase
  10. Merge - master to branch
  11. Push - branch to origin
  12. Pull request
  13. Merge to main
