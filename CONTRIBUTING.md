# Basic collaboration workflow

Before editing:

```bash
git pull --rebase
```

After editing:

```bash
git add .
git commit -m "Describe the update"
git push
```

For code changes, use a separate branch and pull request when practical. Avoid committing credentials, private datasets, generated build directories, or third-party files whose licenses do not permit redistribution.