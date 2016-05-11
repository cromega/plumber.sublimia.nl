+++
date = "2016-05-11T23:51:05+01:00"
draft = true
title = "introducing keyguard"
tags = ["software"]
languages = ["english"]

+++

At Pivotal we often change workstations. We do pair-programming every day, we tend to rotate pairs every (other (or so)) day so enginners usually don't have their own desks and machines to work on. One of the truly dreadful problems this setup creates is managing SSH keys for GitHub authentication.

<!--more-->

Engineers tend to have their SSH keys on an encrypted pendrive which they plug in, run a script from it that adds the key to the ssh-agent with a day expiry and they start hacking happily.

For various reasons I couldn't have that. The reasons included things like lazyness and a difficult to explain reluctance to have more than one pendrive on my keychain. And I really didn't want to encrypt mine.

After some time of giving the puppy eyes to whichever teammate was sitting next to me to load their SSH keys every day I decided it was time to engineer the everloving bejesus out of this situation.

The result of this effort is [KeyGuard](https://github.com/cromega/keyguard)!

The unsophisticated name hides a similarly unsophisticated app that can serve an SSH key over HTTP as a response to a request that has to pass some sort of authentication.

Since I'm a happy [YubiKey](https://www.yubico.com/faq/yubikey/) user I can get my SSH key by curling an endpoint and touching my one-time password generator button.

It works like this:

```
curl -s https://this.is.where.my.ssh.key.is | bash
OTP: cckgleoslgkjrbieccviiuerrlhecsfsdfsawgfdhre
Identity added: /tmp/tmp.PDuXEGY80t (/tmp/tmp.PDuXEGY80t)
Lifetime set to 32400 seconds
```

Much secure, very convenience, amaze!

In fact, KeyGuard only supports Yubi authentication at the moment but as soon as I get a bit less lazy I will add some other schemes to it.



