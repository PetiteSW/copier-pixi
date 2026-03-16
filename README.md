[![Contributor Covenant](https://img.shields.io/badge/Contributor%20Covenant-2.1-4baaaa.svg)](CODE_OF_CONDUCT.md)

# Copier template for projects that uses Pixi

See [copier](https://copier.readthedocs.io/en/stable/) for details.
Usage example:

```sh
copier copy gh:path/to/the/copier_template myproject  # requires python>=3.9
cd myproject
git init .
git add * .copier-answers.yml .github .gitignore .pre-commit-config.yaml .python-version
git commit -m "Setup from copier_template"
pixi install
pixi run test
pixi run docs
git remote add origin git@github.com:name-of-my-org-or-user-name/myproject.git
```

## Manual Configuration

Once the project is built from the template, there are manual settings to be configured per project/repository.

### Documentation Deployment

1. Select branch of deployed documentation.
   The documentation will be deployed from a branch via GitHub action.
   The branch of the documentation must be selected manually on GitHub.
   Go to `Settings > Pages` and set `source` as  `Deploy from a branch` and `Branch` as `gh-pages`.

2. Enable website link on repository page.
   Once the branch for the documentation is selected after step `1`, it can be shown in the repository page.
   Go to `repository page` > `About section` (in the right sidebar).
   Click the gear and check the "Use your GitHub Pages website" checkbox for "Website".

### Package Deployment
Package deployment can be done using the github CI action.

#### PyPI

1. Create a new project by [adding a trusted publisher](https://docs.pypi.org/trusted-publishers/creating-a-project-through-oidc/).
2. In the GitHub project settings, go to `Environments` and add a new environment `release`.
   Configure appropriate protection rules such as required reviewers and deploying only from protected branches.

#### Conda Forge

Once the pypi wheel is uploaded, we can deploy the package to conda-forge channel.

This should be done manually by either opening a PR or adding this package to an existing recipe.

### Branch Protection Rules
Go to `Settings > Branches` and in the `Branch protection rules` add rule for `main` branch to project it.
Under `Protect matching branches` setting, select
- [ ] `Require a pull request before merging`
- [ ] `Require approvals`
- [ ] `Require branches to be up to date before merging`
- [ ] `Require status checks to pass before merging`

      You can either use all checks, or select `required` checks only.
      The list of jobs you can select as `required` checks will be shown only after they are triggered at least once within a week.
