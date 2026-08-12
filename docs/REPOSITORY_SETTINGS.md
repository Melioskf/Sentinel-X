# GitHub Repository Settings Checklist

Some repository-level controls are not represented by files and must be enabled in GitHub Settings.

## Required / strongly recommended

- [ ] Enable Dependabot alerts.
- [ ] Enable Dependabot security updates.
- [ ] Enable secret scanning and push protection where available.
- [ ] Enable code scanning / CodeQL results.
- [ ] Protect `main` with a ruleset or branch protection rule.
- [ ] Require pull requests before merging.
- [ ] Require CI checks before merging.
- [ ] Require CODEOWNERS review for protected areas.
- [ ] Prevent force pushes to `main`.
- [ ] Prevent branch deletion for `main`.
- [ ] Consider requiring signed commits if the maintainer workflow supports them.
- [ ] Consider enabling automatic deletion of merged branches.

## Recommended `main` protection

At minimum, configure:

- pull request required;
- at least one approval for collaborative work;
- required status checks from `.github/workflows/ci.yml`;
- required CodeQL checks where practical;
- CODEOWNERS review for `.github/`, `backend/`, `frontend/`, `contracts/`, `sdk/`, and `docs/`;
- no force pushes;
- no branch deletion.

## Security settings

GitHub's repository security features should be enabled independently of the files in this repository. A `SECURITY.md` file explains disclosure; it does not itself enable secret scanning, push protection, Dependabot alerts, or code scanning.

## License decision

The historical README states MIT licensing, but the repository currently has no committed `LICENSE` file. Before treating the project as formally licensed for redistribution, the maintainer should confirm the intended license and add the corresponding license file. This is intentionally left as an explicit legal decision rather than guessed by automation.

## Discussions / wiki

Discussions and the wiki are currently disabled. Enable them only if the project needs those channels; the source-of-truth engineering documentation should remain in `docs/`.
