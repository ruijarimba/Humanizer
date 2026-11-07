# Contributing to Humanizer

Contributions are welcome. Start with an existing
[issue](https://github.com/Humanizr/Humanizer/issues), or open one before a
large behavior change so the direction is clear. Everyone participating in the
project must follow the [code of conduct](CODE_OF_CONDUCT.md).

## Prepare a change

Fork the repository, branch from the latest `main`, and keep the pull request
focused. Use the .NET SDK specified by `global.json` and follow `.editorconfig`.
Build and test commands are listed below.

Before opening a pull request:

- add or update tests for behavior changes;
- update XML documentation and user guidance when behavior or public APIs
  change;
- run the applicable target-framework tests and formatting checks below;
- disclose copied code and its license;
- link the issue with `fixes #123` when the change resolves one.

## Build and test

Run these commands from the repository root:

```shell
dotnet build Humanizer.slnx -c Release
dotnet test --project tests/Humanizer.Tests/Humanizer.Tests.csproj --framework net8.0
dotnet test --project tests/Humanizer.Tests/Humanizer.Tests.csproj --framework net10.0
dotnet test --project tests/Humanizer.Tests/Humanizer.Tests.csproj --framework net11.0
dotnet format Humanizer.slnx --verify-no-changes
```

On Windows, also run the tests with `--framework net48`. Tests use xUnit v3
with Microsoft Testing Platform; use `--filter-class`, `--filter-method`, or
`--filter-namespace` for targeted runs. Culture-specific tests must declare
their culture with `UseCulture`.

For package changes, pack first and then verify the package:

```shell
dotnet pack src/Humanizer/Humanizer.csproj -c Release -o artifacts
pwsh tests/verify-packages.ps1 -PackagePath artifacts
```

## Documentation

The public site source lives under `website/docs`. It includes runnable
examples, generated API reference, immutable release snapshots, and documented
release and rollback commands. Read the
[documentation contribution guide](../website/docs/contributing/documentation.mdx)
before editing it; never hand-edit `website/versioned_docs`.

## Languages

Language work remains especially valuable. Most localization is authored as
YAML under `src/Humanizer/Locales`, with generated registries and targeted
culture tests. Follow the
[locale contribution guide](../website/docs/contributing/adding-or-updating-a-locale.mdx)
and its linked schema and validation references instead of copying an older
formatter implementation.
