# Renovate Reproduction Repo

Renovate might update an (poetry) update PR, instead of a proper
rebase (taking again the newest pyproject.toml / poetry.lock file
version as base), the update is redone on the previous branch version.

However, it is still pushed with the newest branch version as parent.

## Steps to reproduce

1. Let renovate open a normal PR (e.g. boto3 update)
2. Merge an indepenent change (upgrade idna in this case).
3. Wait until a new version is released (no normal "rebase" must be triggered)
4. Renovate updates the first PR, however, it is based on the old branch version
  and therefore reverts the change merged in the mean time.


Concreate example:

1. boto3 1.34.109 -> 1.34.112 PR is opened
2. idna PR is opened
3. idna PR is merged
4. 1.34.113 is released
5. boto3 PR updated boto3 1.34.113 (but "downgrades" idna).
