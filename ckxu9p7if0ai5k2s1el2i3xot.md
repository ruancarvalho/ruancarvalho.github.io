## Configuring Git to use HTTPS Protocol

In this tutorial you will see how configure Git to use HTTPS protocol instead the GIT transport, so package managers can fetch dependencies.

----

A few years ago, I was trying to clone the [angular-seed](https://github.com/angular/angular-seed) repository. At the time, I was using bower (yeah, long time ago) to install dependencies.

But, I was getting the following error, in gitbash:

```bash
Additional error details:
fatal: unable to connect to github.com:
github.com[0: 192.30.252.129]: errno=No such file or directory
```

After some research, and reading the logs, I’ve found that bower couldn't execute some commands because Git was using URLs with git:// to fetch some repositories, and I was behind the firewall of the company I was working, at the time.

To solve this, we need to configure Git to use HTTPS protocol instead the GIT transport, so bower could fetch dependencies:

```bash
$ git config --global url."https://".insteadOf git://
```

After this, all URLs will use https:// to find the address. This can be useful when you're under a proxy in your company, or a firewall, for example.