---
title: Prowlarr Contributing
description: 
published: true
date: 2021-08-15T01:10:57.101Z
tags: prowlarr, development, contributing
editor: markdown
dateCreated: 2021-05-24T03:34:59.943Z
---

## How to Contribute

We're always looking for people to help make Prowlarr even better, there are a number of ways to contribute.

## Documentation

Setup guides, FAQ, the more information we have on the [wiki](https://wiki.servarr.com/prowlarr) the better.

## Development

Prowlarr is written in C# (backend) and JS (frontend). The backend is built on the .Net5 framework, while the frontend utilizes Reactjs.

### Tools required

- Visual Studio 2019 or higher is recommended (<https://www.visualstudio.com/vs/>).  The community version is free and works (<https://www.visualstudio.com/downloads/>).

> VS 2019 V16.9 or higher is recommended as it includes the .net5 SDK
{.is-info}

- HTML/Javascript editor of choice (VS Code/Sublime Text/Webstorm/Atom/etc)
- [Git](https://git-scm.com/downloads)
- The [Node.js](https://nodejs.org/) runtime is required. The following versions are supported:
  - **12.0** or later
  - **14.0** or later
{.grid-list}

> Prowlarr will **NOT** run on older versions such as `8.x`, `6.x` or any version below `12.0`
{.is-warning}

- [Yarn](https://yarnpkg.com/) is required to build the frontend

### Getting started

1. Fork Prowlarr
1. Clone the repository into your development machine. [*info*](https://docs.github.com/en/github/creating-cloning-and-archiving-repositories/cloning-a-repository-from-github)

#### Building the frontend

- Navigate to the cloned directory
- Install the required Node Packages

     ```bash
     yarn install
     ```

- Start webpack to monitor your development environment for any changes that need post processing using:

     ```bash
     yarn start
     ```

#### Building the Backend

The backend solution is most easily built and ran in Visual Studio or Rider, however if the only priority is working on the frontend UI it can be built easily from command line as well when the correct SDK is installed.

##### Visual Studio

> Ensure startup project is set to `Prowlarr.Console` and    framework to `net5.0`
{.is-info}

1. First `Build` the solution in Visual Studio, this will ensure all projects are correctly built and dependencies restored
1. Next `Debug/Run` the project in Visual Studio to start Prowlarr
1. Open <http://localhost:9696>

##### Command line

1. Clean solution

  ```shell
  dotnet clean $slnFile -c Debug
  ```

1. Restore and Build debug configuration for the correct platform (Posix or Windows)

```shell
dotnet msbuild -restore src/Prowlarr.sln -p:Configuration=Debug -p:Platform=Posix -t:PublishAllRids
```

1. Run the produced executable from `/_output`

### Contributing Code

- If you're adding a new, already requested feature, please comment on [GitHub Issues](https://github.com/Prowlarr/Prowlarr/issues "GitHub Issues") so work is not duplicated (If you want to add something not already on there, please talk to us first)
- Rebase from Prowlarr's develop branch, do not merge
- Make meaningful commits, or squash them
- Feel free to make a pull request before work is complete, this will let us see where its at and make comments/suggest improvements
- Reach out to us on the discord if you have any questions
- Add tests (unit/integration)
- Commit with \*nix line endings for consistency (We checkout Windows and commit \*nix)
- One feature/bug fix per pull request to keep things clean and easy to understand
- Use 4 spaces instead of tabs, this is the default for VS 2019 and WebStorm

#### Contributing Indexers

- If you're contributing a C# indexer please phrase your commit as something like: `New: (Indexer) {Indexer Name}`, `New: (Indexer) {Usenet|Torrent} {Indexer Name}`, `New: (Indexer) {Torznab|Newznab} {Indexer Name}`
- If you're updating a C# indexer please phrase your commit as something like: `Fixed: (Indexer) {Indexer Name} {changes}` e.g. `Fixed: (Indexer) Changed BHD to use API`
- For Cardigann/YML Indexers please see [the definition and description of the yml format](/prowlarr/cardigann-yml-definition)

##### Indexer YML Definition

### Pull Requesting

- Only make pull requests to `develop`, never `master`, if you make a PR to `master` we will comment on it and close it
- You're probably going to get some comments or questions from us, they will be to ensure consistency and maintainability
- We'll try to respond to pull requests as soon as possible, if its been a day or two, please reach out to us, we may have missed it
- Each PR should come from its own [feature branch](http://martinfowler.com/bliki/FeatureBranch.html) not develop in your fork, it should have a meaningful branch name (what is being added/fixed)
  - `new-feature` (Good)
  - `fix-bug` (Good)
  - `patch` (Bad)
  - `develop` (Bad)
- Commits should be wrote as `New:` or `Fixed:` for changes that would not be considered a `maintenance release`

### Unit Testing

Prowlarr utilizes nunit for its unit, integration, and automation test suite.

#### Running Tests

Tests can be run easily from within VS using the included nunit3testadapter nuget package or from the command line using the included bash script `test.sh`.

From VS simply navigate to Test Explorer and run or debug the tests you'd like to examine.

Tests can be run all at once or one at a time in VS.

From command line the `test.sh` script accepts 3 parameters

```bash
test.sh <PLATFORM> <TYPE> <COVERAGE>
```

#### Writing Tests

While not always fun, we encourage writing unit tests for any backend code changes. This will ensure the change is functioning as you intended and that future changes dont break the expected behavior.

> We currently require 80% coverage on new code when submitting a PR
{.is-info}

If you have any questions about any of this, please let us know.

## Translation

Prowlarr uses a self hosted open access [Weblate](https://translate.servarr.com) instance to manage its json translation files. These files are stored in the repo at `src/NzbDrone.Core/Localization`

### Contributing to an Existing Translation

Weblate handles synchronization and translation of strings for all languages other than English. Editing of translated strings and translating existing strings for supported languages should be performed there for the Prowlarr project.

The English translation, `en.json`, serves as the source for all other translations and is managed on GitHub repo.

### Adding a Language

Adding translations to Prowlarr requires two steps

- Adding the Language to weblate
- Adding the Language to Prowlarr codebase

### Adding Translation Strings in Code

The English translation, `src/NzbDrone.Core/Localization/en.json`, serves as the source for all other translations and is managed on GitHub repo. When adding a new string to either the UI or backend a key must also be added to `en.json` along with the default value in English. This key may then be consumed as follows:

> PRs for translation of log messages will not be accepted
{.is-warning}

#### Backend Strings

Backend strings may be added utilizing the Localization Service `GetLocalizedString` method

```dotnet
private readonly ILocalizationService _localizationService;

public IndexerCheck(ILocalizationService localizationService)
{
  _localizationService = localizationService;
}
        
var translated = _localizationService.GetLocalizedString("IndexerHealthCheckNoIndexers")
```

#### Frontend Strings

New strings can be added to the frontend by importing the translate function and using a key specified from `en.json`

```js
import translate from 'Utilities/String/translate';

<div>
  {translate('UnableToAddANewIndexerPleaseTryAgain')}
</div>
```
