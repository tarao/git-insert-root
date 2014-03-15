git insert-root
===============

Inserts a new root commit with optional initial files by
reconstructing entire commit log of the current branch.

## Installation

Place ``git-insert-root`` somewhere in your ``PATH``.

## Usage

### Insert an empty root commit

```sh
git checkout -b current
git insert-root -e
```

- You will be in ``current`` branch with an empty root commit after ``git insert-root`` command
- The commit message will be ``(empty)``

### Insert an empty root commit with a message

```sh
git insert-root -m "some message"
```

- You will be asked to fill a message if you omit ``-m`` option

### Insert a root commit with initial files

```sh
echo foo > foo.txt
echo bar > bar.txt
git insert-root -m "Initial commit" foo.txt bar.txt
```

- Note that you have to prepare the files before running the command
- Files can be untracked one or some existing file in your branch

### Leaving the root commit branch

```sh
git checkout -b current
git insert-root -e -b empty
git checkout empty
```

- ``empty`` becomes a branch with a single root commit

## Tips

You may have a problem with merging from some other branch after
inserting a root commit.

```sh
git checkout branch-A
git checkout -b branch-B
git insert-root -e

git checkout branch-A
vi make-some-change
git add make-some-change
git commit -m "make some change"

git checkout branch-B
git merge branch-A  # CONFLICT!
```

To avoid this, make a merge commit just after inserting the root commit.

```sh
git checkout branch-A
git checkout -b branch-B
git insert-root -e

git merge branch-A  # do this and this should not make conflict

git checkout branch-A
vi make-some-change
git add make-some-change
git commit -m "make some change"

git checkout branch-B
git merge branch-A  # this also works
```

## Acknowledgment

The idea of implementation is taken from the following insights:

- http://stackoverflow.com/a/15706715
- http://stackoverflow.com/a/3898842
