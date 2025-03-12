# Rancher Kubernetes

To create new Rancher Kubernetes release:
```
NEW_TAGS="v1.33.0-alpha.3" GITHUB_OUTPUT=out ./scripts/create-alpha-branch.sh
./scripts/build
git push origin refs/heads/v1.33.0-alpha.3:refs/heads/v1.33.0-alpha.3
```