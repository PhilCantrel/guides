# Helpful Info

### MISC Useful commands

`Cmd+Shift+P > Dev Tool Menu in Chrome`

`Cmd+k > Search menu on GitHub`

## Scout :Engage/Recruit

### :Engage Staging

1. checkout to staging branch.

2. merge your working branch to staging branch

3. push

4. `cap staging deploy`

5. Add needed tags & milestones on GitHub

6. test on staging server

## Scout :Onboard

bundle exec

bin/webpack-dev-server

rails server -p 3001

lvh.me:3001

Sidekiq

make sure the postgresql@12 service is running

#### :Onboard Staging

merge working branch to staging, 

### CLI Shortcuts

```
CTRL+U then CTRL+R (search previous commands)
CTRL+R cycle search
```

### ZSH Shortcuts

```bash
10to12 -> change from PG10 to 12
12to10 -> change from PG12 to 10
guide -> opens this .md
mkcdir -> make directory and cd into it
scout -> scout repo
onboard -> onboard repo
cbw -> client branding repo
pmapi -> padmore api repo
padmore -> padmore front end repo
```

### Git Shortcuts in .gitconfig

    st = status
    co = checkout
    br = branch
    cm = commit -m
    po = push -u origin

### PGVM

**Commands**

`pgvm install (version number)`

`pgvm use (version number)`

### Postgresql

User: phil

Pass: psql123

### Communicating with servers

`scp directory-from(server or local) directory-to(server or local)`

[New User Session - Employment Office](https://scouterecruitstaging.com/admin)

### Fabiano's guide repo

[Useful information to setup a fresh macos · GitHub](https://gist.github.com/ffscalco/74f110e969274fea887a24a65d1e2570)

# Useful Git Commands

### Create a Git branch and checkout in one command:

`$ git checkout -b **<branch_name>**`

### Reverse Commits

### Option 1: `git reset --hard`

Say you have this, where C is your HEAD and (F) is the state of your files.

```
   (F)
A-B-C
    ↑
  master
```

You want to **nuke commit C and never see it again and lose all the changes in locally modified files**. You do this:

```
git reset --hard HEAD~1
```

The result is:

```
 (F)
A-B
  ↑
master
```

Now B is the HEAD. Because you used `--hard`, your files are reset to their state at commit B.

### Option 2: `git reset`

Ah, but suppose commit C wasn't a disaster, but just a bit off. You want to **undo the commit but keep your changes** for a bit of editing before you do a better commit. Starting again from here, with C as your HEAD:

```
   (F)
A-B-C
    ↑
  master
```

You can do this, leaving off the `--hard`:

```
git reset HEAD~1
```

In this case the result is:

```
   (F)
A-B-C
  ↑
master
```

In both cases, HEAD is just a pointer to the latest commit. When you do a `git reset HEAD~1`, you tell Git to move the HEAD pointer back one commit. But (unless you use `--hard`) you leave your files as they were. So now `git status` shows the changes you had checked into C. You haven't lost a thing!

### Option 3: `git reset --soft`

For the lightest touch, you can even **undo your commit but leave your files and your [index](https://git.wiki.kernel.org/index.php/WhatIsTheIndex)**:

```
git reset --soft HEAD~1
```

This not only leaves your files alone, it even leaves your *index* alone. When you do `git status`, you'll see that the same files are in the index as before. In fact, right after this command, you could do `git commit` and you'd be redoing the same commit you just had.

### Option 4: you did `git reset --hard` and need to get that code back

One more thing: **Suppose you destroy a commit** as in the first example, **but then discover you needed it after all**? Tough luck, right?

Nope, there's *still* a way to get it back. Type `git reflog` and you'll see a list of (partial) commit [shas](https://en.wikipedia.org/wiki/SHA-1#Data_integrity) (that is, hashes) that you've moved around in. Find the commit you destroyed, and do this:

```
git checkout -b someNewBranchName shaYouDestroyed
```

You've now resurrected that commit. Commits don't actually get destroyed in Git for some 90 days, so you can usually go back and rescue one you didn't mean to get rid of.
