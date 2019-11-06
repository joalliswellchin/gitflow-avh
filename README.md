# git-flow (AVH Edition)

A collection of Git extensions to provide high-level repository operations
for Vincent Driessen's [branching model](http://nvie.com/git-model "original
blog post"). This fork adds functionality not added to the original branch.


## Getting started

For the best introduction to get started with `git flow`, please read Jeff
Kreeftmeijer's blog post:

[http://jeffkreeftmeijer.com/2010/why-arent-you-using-git-flow/](http://jeffkreeftmeijer.com/2010/why-arent-you-using-git-flow/)

Or have a look at one of these screen casts:

* [How to use a scalable Git branching model called git-flow](http://buildamodule.com/video/change-management-and-version-control-deploying-releases-features-and-fixes-with-git-how-to-use-a-scalable-git-branching-model-called-gitflow) (by Build a Module)
* [A short introduction to git-flow](http://vimeo.com/16018419) (by Mark Derricutt)
* [On the path with git-flow](https://vimeo.com/codesherpas/on-the-path-gitflow) (by Dave Bock)

A quick cheatsheet was made by Daniel Kummer:

[http://danielkummer.github.io/git-flow-cheatsheet/](http://danielkummer.github.io/git-flow-cheatsheet/)

## Installing git-flow

```console
wget --no-check-certificate -q -O - https://github.com/seigneur/gitflow-avh/raw/develop/contrib/gitflow-installer.sh install develop| sudo bash
```

or clone repo and run 
```
sudo make install
```

## Post installation setup
Install GNU getopt via Homebrew:    

    brew install gnu-getopt

Add to your profile the content `export FLAGS_GETOPT_CMD="$(brew --prefix gnu-getopt)/bin/getopt"`.

## git flow usage

### Initialization

To initialize a new repo with the basic branch structure, use:

    git flow init [-d]

This will then interactively prompt you with some questions on which branches
you would like to use as development and production branches, and how you
would like your prefixes be named. You may simply press Return on any of
those questions to accept the (sane) default suggestions.

The ``-d`` flag will accept all defaults.

![Screencast git flow init](http://i.imgur.com/lFQbY5V.gif)
    
Once completed please run the following command to set up the main flow:

    git flow config switch --main

Also configure the hooks:

    git config gitflow.path.hooks /usr/local/share/doc/gitflow/hooks/

#### Further settings in github
1. Set develop as your default branch in github
2. Follow steps here - https://help.github.com/en/github/administering-a-repository/managing-the-automatic-deletion-of-branches

### Switching to a decentralized flow

    git flow config switch <[ClientName]-epicName>

    And use --main flag to revert for eg.

    git flow config switch --main

### Creating feature/release/hotfix/support branches

* To list/start/finish/delete feature branches, use:

```shell
git flow feature
git flow feature start <name> [<base>]
git flow feature finish <name>
git flow feature delete <name>
```

  For feature branches, the `<base>` arg must be a branch, when omitted it defaults to the develop branch.

* To push/pull a feature branch to the remote repository, use:

```shell
git flow feature publish <name>
git flow feature track <name>
```

* To list/start/finish/delete release branches, use:

```shell
git flow release
git flow release start <release> [<base>]
git flow release finish <release>
git flow release delete <release>
```

  For release branches, the `<base>` arg must be a branch, when omitted it defaults to the develop branch.

* To list/start/finish/delete hotfix branches, use:

```shell
git flow hotfix
git flow hotfix start <release> [<base>]
git flow hotfix finish <release>
git flow hotfix delete <release>
```

  For hotfix branches, the `<base>` arg must be a branch, when omitted it defaults to the production branch.

* To list/start support branches, use:

```shell
git flow support
git flow support start <release> <base>
```

  For support branches, the `<base>` arg must be a branch, when omitted it defaults to the production branch.

### Share features with others

You can easily publish a feature you are working on. The reason can be to allow other programmers to work on it or to access it from another machine. The publish/track feature of gitflow simplify the creation of a remote branch and its tracking.

When you want to publish a feature just use:
```shell
git flow feature publish <name>
```

or, if you already are into the `feature/<name>` branch, just issue:
```shell
git flow feature publish
```

Now if you execute `git branch -avv` you will see that your branch `feature/<name>` tracks `[origin/feature/<name>]`. To track the same remote branch in another clone of the same repository use:
```shell
git flow feature track <name>
```

This will create a local feature `feature/<name>` that tracks the same remote branch as the original one, that is `origin/feature/<name>`.

When one developer (depending on your work flow) finishes working on the feature he or she can issue `git flow feature finish <name>` and this will automatically delete the remote branch. All other developers shall then run:
```shell
    git flow feature delete <name>
```

to get rid of the local feature that tracks a remote branch that no more exist.

### Share hotfixes with others

You can publish an hotfix you are working on. The reason can be to allow other programmers to work on it or validate it or to access it from another machine.

When you want to publish an hotfix just use (as you did for features):
```shell
git flow hotfix publish <name>
```

or, if you already are into the `hotfix/<name>` branch, just issue:
```shell
git flow hotfix publish
```

Other developers can now update their repositories and checkout the hotfix:
```shell
git pull
git checkout hotfix/<name>
```
and eventually finish it:
```shell
git flow hotfix finish
```


### Using Hooks and Filters

For a wide variety of commands hooks or filters can be called before and after
the command.  
The files should be placed in .git/hooks  
In the directory hooks you can find examples of all the hooks available.

## License terms

git-flow is published under the FreeBSD License, see the
[LICENSE](LICENSE) file. Although the FreeBSD License does not require you to
share any modifications you make to the source code, you are very much
encouraged and invited to contribute back your modifications to the community,
preferably in a Github fork, of course.

## Showing your appreciation

Of course, the best way to show your appreciation for the git-flow tool itself
remains contributing to the community.  If you'd like to show your appreciation
in another way, however, consider donating through PayPal:

[![PayPal][2]][1]

[1]: https://www.paypal.com/cgi-bin/webscr?cmd=_donations&business=S85FXJ9EBHAF2&lc=US&item_name=gitflow&item_number=gitflow&no_note=0&cn=Add%20special%20instructions%20to%20the%20seller&no_shipping=1&rm=1&return=https%3a%2f%2fgithub%2ecom%2fpetervanderdoes%2fgitflow&cancel_return=https%3a%2f%2fgithub%2ecom%2fpetervanderdoes%2fgitflow&currency_code=USD&bn=PP%2dDonationsBF%3abtn_donate_SM%2egif%3aNonHosted

[2]: https://www.paypalobjects.com/en_US/i/btn/btn_donate_SM.gif
