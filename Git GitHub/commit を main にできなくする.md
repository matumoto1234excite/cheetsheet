# commit を main にできなくする



`.git/hooks/pre-commit`に以下を追記する



```bash
#!bin/sh

branch = "$(git rev-parse --abbrev-ref HEAD)"

if [ "$branch" = "main"]; then
  echo "You can't commit directoly to master branch ~~~~~~!!!!!!"
  # sl にエイリアスがある場合は command sl
  
  exit 1
fi
```

