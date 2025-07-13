# Using Multiple GitHub Accounts on the Same Computer
`13th july, 2025`

The [official docs](https://docs.github.com/en/account-and-profile/setting-up-and-managing-your-personal-account-on-github/managing-your-personal-account/managing-multiple-accounts) on this are kind of complex. Here is what i do instead -

### 1. Install [GitHub-CLI](https://cli.github.com/)
GitHub-CLI(gh) is the official command-line for GitHub. And we can use it to easily switch git accounts.

### 2. GitHub-CLI as git credential-helper
Run the following command to set `gh` as the git credential-helper,
```bash
gh auth setup-git
```


#### SIDE NOTE:
credential-helpers provide username/password to git whenever we interact with GitHub(push/pull).
- On windows, git-credential-manager is bundled with git and is installed as default credential-helper.
- On linux, we don't get such helpers by default. I generally end up using SSH authentication there instead.


### 3. Add your accounts
Login into your github accounts,
```bash
gh auth login
```

### 4. Switch accounts
To switch to your desired account,
```bash
gh auth switch --user <your-username>
```

### 5. Configure git name and email on per repo basis
After switching accounts with `gh auth switch`, you would be able to access respective repos. 
But git commits will still use the global name and email.

This is a limitation of GitHub-CLI, it does not automatically updates name/email upon switching accounts.
As a workaround, i remove my global git name and email using-
```bash
git config unset --global user.name
git config unset --global user.email
```

And for a repo related to account-1, i will go inside that repo and set the name and email once-
```bash
git config user.name account-1
git config user.email account-1@example.com
```

And repeat for other repos as per their related account.

### That's it, Enjoy!
This was a real problem for me. At some point i even had VMs for separate, headache-free, multi-account access.  

GitHub-CLI is a nice offering. And i hope switching accounts also automatically configures git name and email in future.

Happy Tweaking!
