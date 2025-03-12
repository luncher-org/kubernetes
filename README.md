# Rancher Kubernetes

To create new Rancher Kubernetes release:
```
NEW_TAGS="v1.33.0-alpha.3" GITHUB_OUTPUT=out ./scripts/create-alpha-branch.sh
git branch -m release-v1.33.0-alpha.3
./scripts/build
git push --set-upstream origin release-v1.33.0-alpha.3
```
