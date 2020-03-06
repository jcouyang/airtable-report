
<p align="center">
  <a href="https://github.com/jcouyang/airtable-report/actions"><img alt="javscript-action status" src="https://github.com/jcouyang/airtable-report/workflows/it/badge.svg"></a>
</p>

# Airtable Report

Report Pull Request Statistic to Airtable

## Usage

### 1. Create Airtable
with the column same as this
https://airtable.com/shrxMRmB9GV6a1TCZ

You can now add action you repository you need to collect data from

`.github/workflows/pull-request-statistic`

```yaml
name: "Upload Pull Request Statistic"
on: 
  pull_request:
    types:
    - closed

jobs:
  upload:
    runs-on: ubuntu-latest
    steps:
    - uses: jcouyang/airtable-report@v1
      with:
        airtable-token: ${{ secrets.AIRTABLE_TOKEN }}
        airtable-base: ${{ secrets.AIRTABLE_BASE}}
        airtable-sheet: events
```

See the [actions tab](https://github.com/jcouyang/airtable-report/actions) for runs of this action! :rocket:

## Config

```yaml
  airtable-picks:
    description: 'Expression to map PR json value into table column'
    required: false
    default: '[["url"], ["title"], ["created_at"], ["merged_at"], ["labels"], ["comments"], ["review_comments"], ["commits"], ["additions"], ["deletions"], ["changed_files"]]'
  airtable-traversal:
    description: 'Traversal Json List item'
    required: false
    default: '{"labels": ["name"]}'
```

## Run package

```bash
npm run package
```

Since the packaged index.js is run from the dist folder.

```bash
git add dist
```

## Create a release branch

Users shouldn't consume the action from master since that would be latest code and actions can break compatibility between major versions.

Checkin to the v1 release branch

```bash
$ git checkout -b v1
$ git commit -a -m "v1 release"
```

```bash
$ git push origin v1
```

Your action is now published! :rocket: 

See the [versioning documentation](https://github.com/actions/toolkit/blob/master/docs/action-versioning.md)
