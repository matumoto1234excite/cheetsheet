# マルチディスプレイ

`xrandr` を使う

- https://wiki.archlinux.jp/index.php/%E3%83%9E%E3%83%AB%E3%83%81%E3%83%87%E3%82%A3%E3%82%B9%E3%83%97%E3%83%AC%E3%82%A4
- https://wiki.archlinux.jp/index.php/Xrandr

自分の使ってるポート端子とかが見れる

```bash
xrandr
```

右側にディスプレイ画面

```bash
xrandr --output eDP1 --auto --output HDMI2 --auto --right-of eDP1
```

