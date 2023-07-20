# Advanced Git

Speaker: Raju Gandhi

- [Advanced Git](#advanced-git)
  - [Git Internals](#git-internals)
    - [Objects](#objects)
      - [Blob](#blob)
      - [Tree](#tree)
      - [Commit](#commit)
      - [Garbage Collection](#garbage-collection)
    - [Refs](#refs)
      - [Branch](#branch)
      - [HEAD](#head)
      - [Tags](#tags)
    - [Reflog](#reflog)
    - [Stash](#stash)
    - [Undo](#undo)
      - [Reset](#reset)
      - [Revert](#revert)
    - [Merge](#merge)
    - [Rebase](#rebase)
  - [Git Myths Dispelled](#git-myths-dispelled)
  - [Other Resources](#other-resources)
    - [References](#references)

## Git Internals

``` bash
HEAD # Symbolic reference
objects/ # Object database
  info/
  pack/
refs/ # References
  heads/
  tags/
```

### Objects

#### Blob

- Immutable
- Stores file content
- One blob per version of a file
- No metadata
- On `git add`, file content stored as a zip under `objects/` with filename equal to the hash of the content
  - Content addressable filesystem
  - 2 or more files with the same content in the repo will result in a single blob

#### Tree

- Immutable
- Stores structure and names of the files
- On `git add`, creates a string in memory of the file structure and metadata, then stores that string as a zip under `objects/` with filename equal to the hash of the content
  - `<permissions> blob <content hash> <filename>`
  - Single tree for each directory in the repo, subdirectories are pointers to other trees
    - `<permissions> tree <tree hash> <dirname>`

#### Commit

- Immutable
- Stores snapshot of repo
- On `git commit`, creates a string in memory of the commit metadata, then stores that string as a zip under `objects/` with filename equal to the hash of the content
  - Index state (root tree)
  - Parent commit (if any)
  - Committer metadata
  - Author metadata
  - Commit message
- Merkle tree
  - A tree structure in which each leaf node is a hash of a block of data, and each non-leaf node is a hash of its children

#### Garbage Collection

- Removes blobs that are not referenced
- Can be run via `git gc`, but also runs on push
- Only removes blobs older than 30 days by default

### Refs

#### Branch

> "A branch is a post-it note written with a pencil"

- Pointer to the commit id of the last commit on the branch
- Commit id stored under `refs/heads` in plaintext
- Deleting a branch just deletes the ref file
- Can't delete a branch that would orphan a commit unless you force it
- A branch implies work-in-progress, should be cleaned up when no longer needed

#### HEAD

> "No commit left behind"

- Pointer to the checked out branch, not directly to a commit, unless you are in a `detached HEAD` state
  - If in a `detached HEAD` state, you lose access to the commit when switching branches
  - Must create a branch to avoid losing the commit
- Indicates the parent of the next commit
- Usually the last commit on the branch

#### Tags

> "A branch is a post-it note written with a sharpie"

- Pointer to a specific commit, never a branch or tag
- Commit id stored under `refs/tags` in plaintext
- Never moves, unless you force it
- Never name a tag the same as a branch, because of ambiguity with `git checkout`
- Never move a public tag, because it will change history out from other contributors

### Reflog

- Updated every time HEAD moves
- Every clone has its own reflog
- Your safety net
- Last in, first out

### Stash

- Pseudo-commits
- Makes a non-standard commit and moves it to the side, not part of the DAG
- Best to avoid stashes, instead create a branch and commit your changes

### Undo

#### Reset

- Moves the HEAD and the branch to the commit specified
- Never reset a public branch, because it will change history out from other contributors

#### Revert

- Creates a new commit reversing the changes of a single commit specified
- Looks at the diff between a commit and its parent
- Fine to revert on a public branch

### Merge

> "If you have divergence, you will always have convergence"

- Creates a new commit with two parents
  - First parent is the commit of the branch you are on
  - Second parent is the commit of the branch you are merging in
- Can merge multiple branches, creating a merge commit with n+1 parents
- Fast-forward merge isn't really a merge, because all commits are safely applied onto the branch
  - No conflicts
  - No history of merge

### Rebase

- Relocates a branch to a new parent
- Apply all commits in order onto the new parent commit
- Changes the ids of commits you are applying, because their parents are changing
- Never rebase a public branch, because it will change history out from other contributors

## Git Myths Dispelled

1. Git stores files -> False
   - Git stores the contents of your files -> True

2. Git stores deltas -> False
   - Commits are self-contained and are a snapshot of the entire repo at the time of commit

## Other Resources

### References

- [How to revert a faulty merge](https://mirrors.edge.kernel.org/pub/software/scm/git/docs/howto/revert-a-faulty-merge.txt)
- [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/)
