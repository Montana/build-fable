## Build Fable with Travis CI

Hey builders let's get to building Fable with Travis CI! Let's start out with your `.travis.yml` file:

```yaml
language: minimal

services:
  - docker

sudo: required

before_install:
  - docker pull vbfox/fable-build

jobs:
  include:
    - stage: "CI"
      script: docker run -v "${PWD}:/app" -w "/app" vbfox/fable-build bash -c "yarn && yarn postinstall && yarn build"
 ```
 
There's sometimes issues with `Fable` for whatever reason with syntax errors, so you may want to take the time and `lint` your `.travis.yml` file.

### The `package.json`

The `package.json` contains something like the following:

  ```json
    "scripts": {
    "start": "webpack-dev-server",
    "build": "webpack -p",
    "postinstall": "paket restore && paket generate-load-scripts -f netstandard2.0 -t fsx",
    "predeploy": "npm run build",
    "deploy": "gh-pages -d docs"
  },
 ```
As you can see `webpack` is being triggered there as well. That's it - you've now built Fable in Travis CI! Phew, that was easier than we thought.
