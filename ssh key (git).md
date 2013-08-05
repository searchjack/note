- from: http://blog.csdn.net/redhat7890/article/details/5131803

#生成 key

>    ssh-keygen -t rsa


    $ ssh-keygen -t rsa
    Generating public/private rsa key pair.
    Enter file in which to save the key (/c/Users/searchjack/.ssh/id_rsa):
    Enter passphrase (empty for no passphrase):
    Enter same passphrase again:
    Your identification has been saved in /c/Users/searchjack/.ssh/id_rsa.
    Your public key has been saved in /c/Users/searchjack/.ssh/id_rsa.pub.
    The key fingerprint is:
    63:21:e1:3d:a7:7f:23:55:d2:33:6b:cc:2b:f3:11:4a searchjack@SEARCHJACK-PC

===


# 最后得到了两个文件：id_rsa和id_rsa.pub

- 将 ```id_rsa.pub``` 里面的内容添加到 :

>    https://github.com/settings/ssh
