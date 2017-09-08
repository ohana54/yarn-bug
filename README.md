# yarn-bug

## The setup is 3 packages:
1. package-a depends on webpack@3
2. package-b depends on webpack@1
3. package-c depends on webpack@1
4. Yarn Workspaces enabled

## Steps:
`yarn install` inside package-b

webpack@1 is hoisted to `[root-folder]/node_modules`, while webpack@3 is installed in `package-a/node_modules`.

This is good, but the problem is with the linked binary:

### Expected:
`package-b/node_modules/.bin/webpack` is linked to `[root-folder]/node_modules/webpack/bin/webpack.js`

### Actual:
`package-b/node_modules/.bin/webpack` is linked to `package-a/node_modules/webpack/bin/webpack.js`
