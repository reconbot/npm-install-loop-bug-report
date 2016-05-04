# Infinite preinstall loop

We have 2 packages and your app. This is mimicking a [situation](https://github.com/mapbox/node-pre-gyp/issues/162#issuecomment-216877736) from `serialport` and `node-pre-gyp`

# What happens
We get a loop during install that never ends and eventually crashes.

# What should happen
`dep-dep` should get installed before `dep`, then `dep` should be installed and npm should be finished installing.

# Steps to reproduce

 1. Ensure you're using node v0.12.7 and npm v3.8.8
 2. clone this repo
 3. cd into `app`
 4. run `npm install ../dep`
