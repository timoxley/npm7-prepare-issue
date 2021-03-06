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

Key Things:

1. apple depends on banana
2. banana's `prepare` script sleeps for 2s, touches `INSTALLED` file, then runs `banana/index.js`
3. `banana/index.js` checks for `INSTALLED`, then prints 'banana'
4. apple's prepare script runs `apple/index.js`
5. `apple/index.js` requires `banana/index.js`, checks for `INSTALLED`, then prints 'apple'

The problem is that when:

* apple's `prepare` script runs
* banana's `prepare` script is still sleeping so 
* apple's `prepare` script errors because banana's `INSTALLED` file hasn't been created yet.

Note: Using `prepublish` instead of `prepare` seems to work fine.
