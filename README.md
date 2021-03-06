# GitHub Cheat Sheet

All the hidden and not hidden features of Git and GitHub. This cheat sheet was inspired by Zach Holman's [Git and GitHub Secrets](http://www.confreaks.com/videos/1229-aloharuby2012-git-and-github-secrets) talk at Aloha Ruby Conference 2012. Also see Zach's [slides](https://speakerdeck.com/holman/git-and-github-secrets).

## Ignore Whitespace

Adding `?w=1` to any diff URL will remove any changes only in whitespace, enabling you to see only that code that has changed.

## Cloning a Repo

When cloning a repo the `.git` can be left off the edge.

```bash
$ git clone https://github.com/tiimgreen/github-cheat-sheet
```

## Hub - Git wrapper

[Hub](https://github.com/github/hub) is a command line tool that wraps git in order to extend it with extra features and commands that make working with GitHub easier.

This allows you to do things like:

```bash
$ hub clone tiimgreen/toc
```

Which translates to:

```bash
$ git clone git://github.com/tiimgreen/toc.git
```

## Previous Branch

To move to the previous directory in the command line:

```bash
$ cd -
```

Similarly, to move to the last branch in git:

```bash
$ git checkout -
# Switched to branch 'master'

$ git checkout -
# Switched to branch 'next'
```

## git.io

[git.io](http://git.io) is a simple URL shortener for GitHub.

[http://git.io/wO0xUg](http://git.io/wO0xUg)

## Gists

[Gists](https://gist.github.com/) are an easy way to work with small bits of code without creating a fully fledged repo.

Although, Gists can be treated as a full repo so they can be cloned like any other:
```bash
$ git clone https://gist.github.com/tiimgreen/10545817
```

![Gists](http://i.imgur.com/dULZXXo.png)

## Keyboard Shortcuts

When on a repo page keyboard shortcuts allow you to navigate easily.

Pressing `t` will bring up a file explorer.

Pressing `w` will bring up the branch selector.

Pressing `s` will select the search bar.

To see all of the shortcuts for given page type `shift+?`

## Closing issues with commits

If a particular commit fixes an issue, any of the keywords `fix/fixes/fixed` or `close/closes/closed`, followed by the issue number, will close the issue.

```bash
$ git commit -m "Fix cock up, fixes #12"
```

This closes the issue and references the closing commit.

![Closing Repo](http://i.imgur.com/URXFprQ.png)

## Cross-link issues

If you want to link to another issue in the same repo, simple type hash `#` then the issue number, it will be auto-linked.

To link to an issue in another repo, `user_name/repo_name#ISSUE_NUMBER` e.g. `tiimgreen/toc#12`.

## Syntax Highlighting in Markdown Files

For example, to syntax highlight Ruby code in your Markdown files write:

    ```ruby
    require 'tabbit'
    table = Tabbit.new('Name', 'Email')
    table.add_row('Tim Green', 'tiimgreen@gmail.com')
    puts table.to_s
    ```

This will produce:

```ruby
require 'tabbit'
table = Tabbit.new('Name', 'Email')
table.add_row('Tim Green', 'tiimgreen@gmail.com')
puts table.to_s
```

GitHub uses [Linguist](https://github.com/github/linguist) to perform language detection and syntax highlighting. You can find out which keywords are valid by perusing the [languages YAML file](https://github.com/github/linguist/blob/master/lib/linguist/languages.yml).

## Commit History by Author

To view all commits on a repo by author add `?author=username` to the URL.

```
https://github.com/rails/rails/commits/master?author=dhh
```

## Empty Commits

Commits can be pushed with no code changes by adding `--allow-empty`

```bash
$ git commit -m "Big-ass commit" --allow-empty
```

![Trololol](http://img1.wikia.nocookie.net/__cb20130905205853/flylikeabird3/images/0/0c/Mexican_troll_face_by_mariodude12312-d5mtl9z.png)

## Comparing Branches

To use GitHub to compare branches, change the URL to look like this:

```
https://github.com/user/repo/compare/{range}
```

Where `{range} = master...4-1-stable`

e.g.:
```
https://github.com/rails/rails/compare/master...4-1-stable
```

`{range}` can be changed to things like:
```
https://github.com/rails/rails/compare/master@{1.day.ago}...master
https://github.com/rails/rails/compare/master@{2014-10-04}...master
```
which allows you to see the difference on the master branch up a set time ago or a specified date.

## Line Highlighting in Repos

Adding `#L52` to the end of a code file URL will highlight that line number.

It also works with ranges, e.g. `#L53-L60`:

```
https://github.com/rails/rails/blob/master/activemodel/lib/active_model.rb#L53-L60
```

![Line Highlighting](http://i.imgur.com/8AhjrCz.png)

## Emojis

Emojis can be generated on Pull Requests, Issues, READMEs, etc. using `:name_of_emoji:`

```
:smile:
:poop:
:shipit:
:+1:
```

:smile:
:poop:
:shipit:
:+1:

The full list of supported Emojis on GitHub can be found [here](http://www.emoji-cheat-sheet.com/).

## Images/GIFs

Images and GIFs can be added to comments, READMEs etc.:

```
![Alt Text](http://image_url.com/image.jpg)
```

![Jim Carrey](http://wac.450f.edgecastcdn.net/80450F/thefw.com/files/2013/05/Irene.gif)

All images are cached on GitHub, so if your host goes down, the image will remain available.

## Styled Git Status

```bash
$ git status
```

![git status](http://i.imgur.com/o3PEHAA.png)

Can be changed to:

```bash
$ git status -sb
```

![git status -sb](http://i.imgur.com/xNI1bT0.png)

## Git Query

A git query allows you to search all your previous commit messages and finds the most recent one matching the query.

```bash
$ git show :/query
```

Where `query` is the term you want to search, this then finds the last one and gives details on the lines that were changed.

![git show :/query](http://i.imgur.com/SA0oZbE.png)

NOTE: Press `q` to quit.

## Merged Branches

```bash
$ git branch --merged
```

Will give you a list of all branches that have been merged into your current branch.

Conversely:

```bash
$ git branch --no-merged
```

Will give you a list of branches that have not been merged into your current branch.

## .gitconfig Recommendations

Your `.gitconfig` is the file that contains all your preferences.

### Aliases

Aliases are helpers that let you define your own git calls. For example you could set `git a` to run `git add --all`.

To add an alias, either navigate to `~/.gitconfig` and fill it out in the following format:

```
[alias]
	co = checkout
	cm = commit
	p = push
```

or type in the command line:

```bash
$ git config alias.new_alias git_function
```
e.g.
```bash
$ git config alias.cm commit
```

NOTE: for an alias with multiple functions use quotes:
```bash
$ git config alias.ac 'add -A . && commit'
```

Some recommendations include:

```bash
$ git cm
```
is Alias of:
```bash
$ git commit
```
<br>
```bash
$ git ac
```
is Alias of:
```bash
$ git add .
$ git commit
```
<br>
```bash
$ git st
```
is Alias of:
```bash
$ git status -sb
```

### Auto-correct

Currently if you type `git comit` you will get this result:
```bash
$ git comit -m "Message"
# git: 'comit' is not a git command. See 'git --help'.

# Did you mean this?
# 	commit
```

To call `commit` when `comit` is typed, just enable autocorrect:

```bash
$ git config --global help.autocorrect 1
```

So now you will get this result:

```bash
$ git comit -m "Message"
# WARNING: You called a Git command named 'comit', which does not exist.
# Continuing under the assumption that you meant 'commit'
# in 0.1 seconds automatically...
```

### Color

To add more colour to your git command line:

```bash
$ git config --global color.ui 1
```
