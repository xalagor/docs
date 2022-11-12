---
title: One profile in GitHub and GitLab
slug: one-github-gitlab-profile
type: posts
---

The idea is this: we create a local repository that contains only one `readme.md` file. This repository will be sent to remote repositories at `github.com/username/username` and `gitlab.com/username/username` , so the services will understand that they need to get `readme.md` from them and show them in your profile. There, for convenience, you can take out contacts like Twitter or email from profiles in order to also edit them in one file.

This is how we make several links to repositories for pushing to `origin` . Required with two commands, because `set-url` first overwrites the original URL from `origin` [^1] . Then, if you push to `origin` , the repository will immediately go to both services.

```bash
git remote set-url --add --push origin git@gitlab.com:xalagor/xalagor.git
git remote set-url --add --push origin git@github.com:xalagor/xalagor.git
```

Command `git config -l | grep '^remote\.origin'` shows that the push addresses were written correctly.

```bash
remote.origin.url=git@gitlab.com:xalagor/xalagor.git
remote.origin.fetch=+refs/heads/*:refs/remotes/origin/*
remote.origin.pushurl=git@gitlab.com:xalagor/xalagor.git
remote.origin.pushurl=git@github.com:xalagor/xalagor.git
```


[^1]: https://stackoverflow.com/posts/14290145