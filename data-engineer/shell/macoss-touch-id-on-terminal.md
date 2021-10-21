# MacOS's Touch ID on Terminal

```bash
sudo /etc/pam.d/sudo
```



Add the following line **on top**\


```
auth sufficient pam_tid.so
```

![](<../../.gitbook/assets/Screen Shot 2021-10-21 at 21.15.54.png>)

Ref: [https://dev.to/equiman/how-to-use-macos-s-touch-id-on-terminal-5fhg](https://dev.to/equiman/how-to-use-macos-s-touch-id-on-terminal-5fhg)
