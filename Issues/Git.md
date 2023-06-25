# 目录
[toc]

## fatal: Could not read from remote repository.

```git
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@    WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!     @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
IT IS POSSIBLE THAT SOMEONE IS DOING SOMETHING NASTY!
Someone could be eavesdropping on you right now (man-in-the-middle attack)!
It is also possible that a host key has just been changed.
The fingerprint for the RSA key sent by the remote host is
SHA256:uNiVztksCsDhcc0u9e8BujQXVUpKZIDTMczCvj3tD2s.
Please contact your system administrator.
Add correct host key in /c/Users/h433899/.ssh/known_hosts to get rid of this message.
Offending RSA key in /c/Users/h433899/.ssh/known_hosts:14
Host key for github.com has changed and you have requested strict checking.
Host key verification failed.
fatal: Could not read from remote repository.
Please make sure you have the correct access rights
and the repository exists.
```


这个错误通常是由于 GitHub 更改了其主机密钥而导致的。这可能是正常的，但也可能是恶意攻击的迹象。为了解决这个问题，您需要更新您的 known_hosts 文件，以包含 GitHub 的新主机密钥。

您可以使用以下命令将新的主机密钥添加到您的 known_hosts 文件中：
```shell

ssh-keygen -R github.com
ssh-keyscan github.com >> ~/.ssh/known_hosts

```

