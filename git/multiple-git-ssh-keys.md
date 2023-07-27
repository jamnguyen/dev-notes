## Setup Multiple SSH keys by folder structure

Sometimes you need to use many SSH keys to separate usages, e.g. business and personal repos. Here's how you can do it by using `.gitconfig` files.

### Generate keys

Check out [Github's manual](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account) to genrate and link your keys to Github. Other code hosts like Gitlab or Bitbucket have similar processes.

Assuming that you had generated `~/.ssh/key_work` & `~/.ssh/key_personal` and linked them to your git accounts.

### Create SSH Config file

Create `~/.ssh/config`, something like this:

```
# Business account
Host *
	AddKeysToAgent yes
	IdentityFile ~/.ssh/key_work

# Personal account
Host *
	AddKeysToAgent yes
	IdentityFile ~/.ssh/key_personal
```

We are setting Host to \* for every key because we will use Git configs to select the appropriate SSH key based on profiles.

### Setup your workplace

Let's separate your repos into business' and personal's so that git can choose which key to use:

```
~/path/to/workplace
|__ .gitconfig
|__ work/
    |_ .gitconfig.business
|__ personal/
    |_ .gitconfig.personal
```

In `.gitconfig`:

```
[includeIf "gitdir:~/path/to/workplace/work/"]
path = ~/path/to/workplace/work/.gitconfig.business

[includeIf "gitdir:~/path/to/workplace/personal/"]
path = ~/path/to/workplace/personal/.gitconfig.personal

[core]
excludesfile = ~/.gitignore
```

In `.gitconfig.business`:

```
[user]
email = your-email@example.com
name = Your Name

[github]
user = "username"

[core]
sshCommand = "ssh i ~/.ssh/key_business.pub"
```

In `.gitconfig.personal`:

```
[user]
email = your-email@example.com
name = Your Name

[github]
user = "username"

[core]
sshCommand = "ssh i ~/.ssh/key_personal.pub"
```

### Test

Now try some git commands like `clone`, `fetch` in `/business` and `/personal`, you should have permission now.

Happy coding!

### References

- [8 Easy Steps to Set Up Multiple GitHub Accounts](https://blog.gitguardian.com/8-easy-steps-to-set-up-multiple-git-accounts/)
