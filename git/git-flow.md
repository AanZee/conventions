# The GIT flow

![GIT flow](attachments/git-flow-aanzee)

## Branches

### Master
Directly committing in the master branch is not allowed. Only a merge from develop or from a hotfix can be merged with master. The lastest version (tag) in the master branch is the version that is currently (or will soon be live). When merging a hotfix or develop with the master branch a version (tag) 

### Develop
Iteration, hotfixe and feature branches are merged in develop. From this branch you can test how, for example, a release and a sprint branch work together. Please note that you may only merge to develop if your work has been tested, reviewed and ready to go live.