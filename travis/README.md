## Travis CI

### Get encrypted credentials

Follow instruction from [this article](https://gist.github.com/domenic/ec8b0fc8ab45f39403dd#get-encrypted-credentials) and setup encrypted credentials for Travis so it can push to your GitHub repo.

### Example Travis CI file

```
language: java
jdk:
  - oraclejdk8

branches:
  only:
    - /^ready\/.*$/

env:
  global:
  - ENCRYPTION_LABEL: "12c8071d2834"
  - COMMIT_AUTHOR_NAME: "Praqma"
  - COMMIT_AUTHOR_EMAIL: "no-reply@praqma.com"
  - TARGET_BRANCH: "master"
  - TARGET_REPO: "git@github.com:Praqma/jobdsl-helpers.git"

before_script:
  - mkdir ci
  - wget --directory-prefix=ci https://github.com/Praqma/pretested-integration/archive/master.zip
  - unzip ci/*.zip -d /ci

script:
  - bash -ex ci/travis/before.sh
  - echo "test test test!"
  - bash -ex ci/travis/after.sh
```