# Infinite preinstall loop

We have 2 packages and your app. This is mimicking a [situation](https://github.com/mapbox/node-pre-gyp/issues/162#issuecomment-216877736) from `serialport` and `node-pre-gyp`

# What happens
We get a loop during install that installs `dep-dep` over and over again. It never ends and eventually crashes.

```
kidrobot:app$ npm i ../dep

> dep@1.0.0 preinstall /Users/wizard/src/tmp/app/node_modules/.staging/dep-4a52e41f
> npm install ../dep-dep


> dep@1.0.0 preinstall /Users/wizard/src/tmp/app/node_modules/.staging/dep-4a52e41f/node_modules/.staging/dep-789925ce
> npm install ../dep-dep


> dep@1.0.0 preinstall /Users/wizard/src/tmp/app/node_modules/.staging/dep-4a52e41f/node_modules/.staging/dep-789925ce/node_modules/.staging/dep-1f67fb3b
> npm install ../dep-dep


> dep@1.0.0 preinstall /Users/wizard/src/tmp/app/node_modules/.staging/dep-4a52e41f/node_modules/.staging/dep-789925ce/node_modules/.staging/dep-1f67fb3b/node_modules/.staging/dep-7d290440
> npm install ../dep-dep


> dep@1.0.0 preinstall /Users/wizard/src/tmp/app/node_modules/.staging/dep-4a52e41f/node_modules/.staging/dep-789925ce/node_modules/.staging/dep-1f67fb3b/node_modules/.staging/dep-7d290440/node_modules/.staging/dep-577d9c9f
> npm install ../dep-dep


> dep@1.0.0 preinstall /Users/wizard/src/tmp/app/node_modules/.staging/dep-4a52e41f/node_modules/.staging/dep-789925ce/node_modules/.staging/dep-1f67fb3b/node_modules/.staging/dep-7d290440/node_modules/.staging/dep-577d9c9f/node_modules/.staging/dep-6a5d4026
> npm install ../dep-dep

^C

```

# What should happen
`dep-dep` should get installed before `dep`, then `dep` should be installed and npm should be finished installing.

# Steps to reproduce

 1. Ensure you're using node v0.12.7 and npm v3.8.8
 2. clone this repo
 3. cd into `app`
 4. run `npm install ../dep`
