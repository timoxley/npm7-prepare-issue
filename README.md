# npm7-prepare-issue

A test case for npm 7's handling of prepare scripts in workspaces.

See: https://github.com/npm/cli/issues/3034

```
git clone git@github.com:timoxley/npm7-prepare-issue.git
cd npm7-prepare-issue
npm install # this will break
npm install # works on second run
# run this to clean up and try again
npm run clean
```
