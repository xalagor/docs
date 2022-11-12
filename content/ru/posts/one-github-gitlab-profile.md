---
title: Один профиль в GitHub и GitLab
slug: one-github-gitlab-profile
type: posts
---

Идея заключается вот в чём: создаём локальный репозиторий, который содержит только один файл `readme.md`. Этот репозиторий будет отправляться в удалённые репозитории по адресам `github.com/username/username` и `gitlab.com/username/username` — так сервисы поймут, что нужно достать из них `readme.md` и показать в вашем профиле. Туда для удобства можно вынести из профилей контакты вроде Twitter или электронной почты, чтобы также редактировать их в одном файле.

Вот так делаем несколько ссылок на репозитории для пуша в `origin`. Обязательно двумя коммандами, потому что `set-url` сначала перезаписывает изначальный URL от `origin` [^1]. Потом, если делать пуш на `origin`, репозиторий сразу отправится на оба сервиса.

```bash
git remote set-url --add --push origin git@gitlab.com:xalagor/xalagor.git
git remote set-url --add --push origin git@github.com:xalagor/xalagor.git
```

Команда `git config -l | grep '^remote\.origin'` показывает, что адреса для пуша записались правильно.

```bash
remote.origin.url=git@gitlab.com:xalagor/xalagor.git
remote.origin.fetch=+refs/heads/*:refs/remotes/origin/*
remote.origin.pushurl=git@gitlab.com:xalagor/xalagor.git
remote.origin.pushurl=git@github.com:xalagor/xalagor.git
```

[^1]: https://stackoverflow.com/posts/14290145
