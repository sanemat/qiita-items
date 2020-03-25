terminalから画像をシュッと見たい時、imagemagickに付属のdisplayコマンドが便利。

```bash
display i-want-to-see.png
```
Ubuntu 16.04 で、ウィンドウが開いてくれる。こんなやつ。

![Screenshot from 2019-03-21 00-27-25.png](https://qiita-image-store.s3.amazonaws.com/0/5653/ebd118f1-40e2-be2f-f8ae-978fbc089442.png)

curlでもcatでも行けて便利。

```bash
curl https://www.iana.org/_img/2013.1/iana-logo-header.svg | display
cat i-want-to-see.png | display
```

[command line - What is the fastest way to view images from the terminal? - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/35333/what-is-the-fastest-way-to-view-images-from-the-terminal)
