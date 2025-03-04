# Rancher Kubernetes

To create new Rancher Kubernetes release:
```
NEW_TAGS="v1.33.0-alpha.2 v1.33.0-alpha.3" GITHUB_OUTPUT=out ./scripts/create-alpha-branch.sh
./scripts/build
git push --set-upstream origin v1.33.0-alpha.2
```