This is hello world using bazel, llvm and jj.

It is not meant as a full tutorial. I am going to skip over bazel, bazelisk and jj and such.

## Build and Run

```
bazelisk build :helloworld
bazelisk run :helloworld
```

## Crafting the initial commit

Here are the steps to set up the repo and initial commit. 
It is trivial, but this should help anyone (especially future me) 
to create a similar repo and initial commit from scratch.

```
DIRNAME="llvm-bazel-helloworld"
mkdir ${DIRNAME}
cd llvm-bazel-helloworld
git init
jj init --git-repo=.

touch WORKSPACE

# (... edit MODULE.bazel)
# (... add BUILD.bazel and helloworld.cc)

# (... edit .gitignore)
# Run "jj untrack" stuff that is in .gitignore
jj untrack bazel-bin
jj untrack bazel-out
jj untrack bazel-testlogs
jj untrack bazel-${DIRNAME}

# Start by describing the initial commit.
jj describe

# Check that our initial commit is how it should be.
jj diff --git

# Move on.
jj new
```

Oh, I should have started with a github repo.
A few more commands... omitting the `jj squash` to amend the commit
with edits to this file.

```
# (... create github repo)
git remote add origin git@github.com:burakemir/llvm-bazel-helloworld.git
jj git fetch
jj log
jj rebase -d skmqnlxu

jj branch create main -r @- 
jj branch track main@origin
jj git push
```

