# Entur - CircleCI Docs Orb [![CircleCI](https://circleci.com/gh/entur/docs-orb/tree/master.svg?style=svg)](https://circleci.com/gh/entur/docs-orb/tree/master)
This orb simplify pushing files to Google Cloud Storage. 

https://circleci.com/orbs/registry/orb/entur/docs

## Usage

Import the orb and give it a name. Add this to the `orbs`-key in your CircleCI-configuration:
```yaml
orbs:
 docs: entur/docs@volatile 
 # volatile selects the newest version. More examples of versioning here: https://circleci.com/docs/2.0/creating-orbs/#semantic-versioning-in-orbs
```

Use the orb in your workflow like this:
```yaml
workflows:
  version: 2.1

  my-workflow: 
    jobs:
    - entur-docs/publish-docs:
        context: global
        project-name: customers
        docs-path: docs
```
         
Available commands and jobs can be found in `src`. Usage examples in `examples`             

Add $DOCKERHUB_LOGIN and $DOCKERHUB_PASSWORD credentials in your context to log in to Docker hub
## Pack and publish orb

Make sure you have the CircleCI CLI:
```bash
curl -fLSs https://circle.ci/cli | bash 
```      

Pack the contents of src/ to a single orb file:
```bash
circleci config pack ./src > orb.yml
```

Validate that the orb is valid:
```bash
circleci orb validate orb.yml
```

After commit & push to the repository, the orb will be automatically published as part of the workflow in CircleCI. 

A dev-orb will be published as: `entur/docs@dev:YOUR-BRANCH-NAME`. Release orbs are created on push to the master branch. 

You can read more here: https://circleci.com/docs/2.0/creating-orbs/
