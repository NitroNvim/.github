# CONTRIBUTING

## NitroNvim Project installation for contributors

If you wish to contribute to an NitroNvim repository, you should:

1. [Create a fork of the project on GitHub](https://docs.github.com/en/get-started/quickstart/fork-a-repo)
2. Clone your Fork to your machine

- For *SSH*:

  ```shell
  $ git clone git@github.com:<YOUR_GITHUB_USERNAME>/<REPOSITORY_NAME>.git ~/projects/<REPOSITORY_NAME>
  ```

- For *https*:

  ```shell
  $ git clone https://github.com/<YOUR_GITHUB_USERNAME>/<REPOSITORY_NAME>.git ~/projects/<REPOSITORY_NAME>
  ```

3. [Add a new remote repo to track](https://www.atlassian.com/git/tutorials/git-forks-and-upstreams)

   - This means you can push/pull as normal to your own repo, but also easily track & update from the NitroNvim org's remote.
   - For *SSH*:

     ```shell
     $ git remote add upstream git@github.com:NitroNvim/<REPOSITORY_NAME>.git
     ```
  
   - For *HTTPS*:

     ```shell
     $ git remote add upstream https://github.com/NitroNvim/<REPOSITORY_NAME>.git
     ```

4. Any time you create a branch to do some work, use

   ```shell
   $ git fetch upstream && git checkout -b dev-myFEAT upstream/main
   ```

5. Only use the **--rebase** flag to update your dev branch

   - This means that there are no `Merge NitroNvim/main into devBranch` commits, which are to be avoided

   ```shell
   $ git pull upstream --rebase
   ```

6. Tell your Neovim configuration to use the local clone in `~/projects` by setting `dev = true` in the Lazy specification for the plugin. This would look like adding the following somewhere in your `lazy.nvim` plugins:

   ```lua
   { "NitroNvim/<REPOSITORY_NAME>", dev = true }
   ```

## Things to know before contributing

  - When making a PR (pull request), please be very descriptive about what you've done!

  - Commit messages must follow [Conventional Commits Specification](https://www.conventionalcommits.org/en/v1.0.0/).

    - PR titles and commit messages should be formatted with 'fix', 'feat', 'docs', 'refactor', or 'chore'. E.g.: `feat: add new plugin`.

    - If your contribution mostly pertains to a single module in the project, please include that in the title. E.g.: If you have modified something in the `lua/configs/lsp` folder for the lsp configuration use something like `fix(lsp): typo in lsp mappings`.

    - If your contribution contains any sort of breaking change include a `!` at the end of the change type. E.g.: `feat!: move status bar from lualine to feline`.
    
  - PRs should follow the pull request formats where applicable.

  - We are open to all PRs, but if a PR is denied for any reason please don't be discouraged! We'll still be open to discussions. If you have any questions before opening the PR feel free to join the [Discord server](https://discord.nitronvim.com).

  - NitroNvim projects aim to provide the best user experience when it comes to being able to support confident updating for users, for this reason please avoid opening PRs with breaking changes. Avoiding breaking changes is not always going to be possible, so if you think it is completely necessary we are open to discussion.

## How to remove, squash, or edit commits from your PR

> You may have been directed here to remove a commit such as a merge commit: `Merge NitroNvim/main into devBranch` from your PR.

> As these commands edit your git history, you may need to **force push** with `git push origin --force-with-lease`.

1. Run the following:

```
$ git rebase -i HEAD~<NUMBER OF COMMITS TO GO BACK>
```

  <details><summary>Example</summary>
  <p>

  ```shell
  $ git rebase -i HEAD~4
  ```

  ```shell
  pick 28b2dcb feat: statusline add lsp status
  pick dad9a39 fix: typo
  pick 68f72f1 add clickable btn for exiting vim
  pick b281b53 avoid using q! for quitting vim

  # Rebase 52b655b..b281b53 onto 52b655b (4 commands)
  #
  # Commands:
  # p, pick <commit> = use commit
  # r, reword <commit> = use commit, but edit the commit message
  # e, edit <commit> = use commit, but stop for amending
  # s, squash <commit> = use commit, but meld into previous commit
  # f, fixup <commit> = like "squash", but discard this commit's log message
  # x, exec <command> = run command (the rest of the line) using shell
  # b, break = stop here (continue rebase later with 'git rebase --continue')
  # d, drop <commit> = remove commit
  # l, label <label> = label current HEAD with a name
  # t, reset <label> = reset HEAD to a label
  # m, merge [-C <commit> | -c <commit>] <label> [# <oneline>]
  # .        create a merge commit using the original merge commit's
  # .        message (or the oneline, if no original merge commit was
  # .        specified). Use -c <commit> to reword the commit message.
  #
  # These lines can be re-ordered; they are executed from top to bottom.
  #
  # If you remove a line here THAT COMMIT WILL BE LOST.
  #
  # However, if you remove everything, the rebase will be aborted.
  #
  # Note that empty commits are commented out.
  ```

  </p>
  </details>

2. Change the `pick` commands to whatever you wish, you may wish to `s` `squash`, `d` `drop` or `e` `edit` a commit. Then save & quit this git file to run it.

3. If you picked `drop` you are done. If you picked `squash` then you will be brought to a screen to update the commit message for the new aggregated commit, please make sure the new commit message follows the Conventional Commit specification. If you picked `edit` then edit your files, then run:

```shell
$ git add <files>
```

4. Continue rebasing until all edits are finished. Run the following command to continue through the rebase if there are more changes:

```shell
$ git rebase --continue
```

5. Push the changes with `--force-with-lease`:

```shell
$ git push origin --force-with-lease
```

## Help

For help with contributing and anything else NitroNvim related join the [Discord](https://discord.nitronvim.com)