---
layout: post
title: Viewing Gitlab Issues from Magit
category: emacs
tags: [emacs, git]
---

The setup was not really clear (I think). References: 
- [How to run forge](https://magit.vc/manual/forge/Getting-Started.html#Getting-Started)
- [Set the authentication file](https://practical.li/spacemacs/source-control/forge-configuration.html) and also [here](https://gist.github.com/Azeirah/542f1db12e3ef904abfc7e9c2e83310e)

1. `M-x package-list-package` and install `forge`
2. Go to [Gitlab](https://gitlab.com/-/profile/personal_access_tokens) and create a personal token with all access, Copy the token key
3. Open `~/.authinfo`
    ```
    machine gitlab.com/api/v4 login <your_gitlab_username>^forge password <your_gitlab_access_token>
    ```
4. `M-x epa-encrypt-file`, select `OK`
5. Setup a new password
6. Add in `.emacs`
    ```
    ; Auto run forge
    (with-eval-after-load 'magit
      (require 'forge))
    ; For forge authentication
    (setq auth-sources '("~/.authinfo.gpg"))
    ```
7. Do `C-x e` at the end of each lines above
8. Open the magit, then type `f a`
9. Add the repo and it will ask if you want to download stuff.
