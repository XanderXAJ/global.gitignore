# global.gitignore

GitHub's global .gitignores catted into a single file for use with `git`.

## Why do I want a global .gitignore?

When you work on a project, you might standardise things the programming language, package manager, dependencies, build tooling and the like.
But you might _not_ enforce people use a single IDE, or other tools auxiliary to the project.
**I think this is great**: allowing everyone to use their favoured tooling (where it makes sense) encourages experimentation, allows accessibility and lets the industry move forward.

However!
Everyone needs to be responsible for their tools:
The tools, IDEs and operating systems you use can generate files in order to do their work.
If you're not careful, they can accidentally end up in the projects when they shouldn't.
This can result in innocous extra text files to dramatic slow downs in clones and checkouts due to massive archives being committed!

GitHub maintains a collection of globally useful gitignore files for many common tools that can be leveraged to make it much easier to avoid committing files.
**But git can only reference one file, and Github only provides a collection of them!**

**So this project plugs the gap**: it takes that collection of gitignore files and cats them into a single giant `.global.gitignore` file, ready for use with git.

## Usage

### One-off `curl`

To grab the latest `global.gitignore` `*sh` shells:

```shell
curl -fsSL -o ~/.global.gitignore "https://raw.githubusercontent.com/XanderXAJ/global.gitignore/refs/heads/main/global.gitignore"
```

Then configure git to use it:

```shell
git config set --global core.excludesFile ~/.global.gitignore
```

To update `global.gitignore`, **re-run** the above `curl` command.

### Repo clone

If you prefer to use git, clone the repo via your preferred method (HTTP shown since it doesn't require auth):

```shell
git clone https://github.com/XanderXAJ/global.gitignore.git ~/.global.gitignore
```

Then configure git to use it:

```shell
git config set --global core.excludesFile ~/.global.gitignore/global.gitignore
```

To update `global.gitignore`, run the following:

```shell
git -C ~/.global.gitignore pull
```

## FAQ

### How do I commit a file that is being excluded?

Run the following:

```shell
git add -f <file>
```

### Some IDE/tool files are still commitable. Why is that?

Some files are _intended_ to be committed despite appearing in an IDE/tool folder.

For example, here's part of the [VSCode gitignore](https://github.com/github/gitignore/blob/main/Global/VisualStudioCode.gitignore):

```gitignore
.vscode/*
!.vscode/settings.json
!.vscode/tasks.json
!.vscode/launch.json
!.vscode/extensions.json
```

You can see some specific exclusions (lines beginning `!`) to the ignore rules.

These exclusions are intended by the tool in question to be committed, for example to allow for customisations or recommendations on a per-repo or per-project basis.
To understand more about them, look up the tool's documentation.
