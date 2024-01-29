#! /usr/bin/env bash
set -o errexit
set -o pipefail

GITHUB_ACTOR=$1

COMMIT_MSG_BODY="$(npx -y npm-check-updates@latest -p npm -t semver --install never | sed "1,2d; $d" | sed "$ d")"

printf "\n$COMMIT_MSG_BODY\n\n"

if ! [ "$COMMIT_MSG_BODY" = "" ]; then
  npx -y npm-check-updates@latest -p npm -t semver --install never -u
  rm -f package-lock.json
  npm i
  git config user.name "$GITHUB_ACTOR"
  git config user.email "$(gh api /users/$GITHUB_ACTOR | jq .email -r)"
  git add package-lock.json
  git add package.json
  git commit -m "fix(deps): update all non-major dependencies" -m "$COMMIT_MSG_BODY" -m "by GitHub Action"
  git push
fi
