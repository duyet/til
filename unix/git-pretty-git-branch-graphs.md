# Git - Pretty git branch graphs

```bash
git log --all --decorate --oneline --graph
```

Result:

```bash
....
| * 5fe09a2 Update README.md
| * 67feb9d Create ci.yml
| * 17ccd2e remove circleci
| * aab9865 circleci - remove docker_layer_caching
| * 48f3f19 Bump to Airflow 1.10.6
| | *   5404764 (origin/1.10.6) Merge pull request #4 from duyetdev/master
| | |\
| |/ /
|/| |
| | * 177af87 Update README.md
| |/
|/|
* |   c0b1a5b (tag: 1.10.6, 1.10.6) Merge pull request #2 from duyetdev/airflow-1.10.6
|\ \
| * | 63c9e0a (origin/airflow-1.10.6, airflow-1.10.6) Update README
|/ /
* |   fbd78e2 Merge pull request #3 from duyetdev/master
|\ \
| * | 74f2d63 Update config.yml
| * | 6a38d88 Update README.md
* | | 393f242 Update README.md
.....
```

Tips:

> "**A Dog**" = git log --**a**ll --**d**ecorate --**o**neline --**g**raph

