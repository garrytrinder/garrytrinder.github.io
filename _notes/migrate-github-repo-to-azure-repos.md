# Migrate GitHub repo to Azure Repos

- Clone GitHub repo
- Create Azure DevOps Repo
- Add DevOps as a remote
 - `git remote add devops <devopsurl>`
- Push all branches to DevOps and set as tracking
  - `git push devops -u --all`
- Remove GitHub remote
  - `git remote remove origin`
- Rename Azure Devops remote
  - `git remote rename devops origin`