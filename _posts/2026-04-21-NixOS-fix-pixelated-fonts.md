---
layout: post
title: "NixOSで日本語をきれいに表示するのに苦労した話"
date: 2026-04-10 10:00:00 +0900
categories: [技術]
tags: [NixOS, flake, i18n]
excerpt: "Nix式による定義とflatpakのキャッシュ削除でどうにかできた"
---

NixOSでは他のディストロと違って、日本語(多分アジア圏の文字全般)を表示するときにアンチエイリアスが効かずにピクセル状になることが多々あります。
[nixpkgs issue #504486](https://github.com/NixOS/nixpkgs/issues/504486)

これについては原因がいくつかあるのですが、

- 日本語系のCJKフォントが入っていない
- ビットマップフォントが使用されている
- アンチエイリアスが既定で無効になっている
- サブピクセルレンダリングが無効になっている

このあたりが原因と思われます。私自身、完全には解決していませんが現状はこのあたりの実装である程度誤魔化しています。
[nixconf modules/fonts.nix](https://github.com/sashisashi569/nixconf/blob/main/modules/fonts.nix)
```
    fonts = {
      fontDir.enable = true;

      packages = with pkgs; [
        dejavu_fonts
        noto-fonts-cjk-sans
        noto-fonts-cjk-serif
      ];

      fontconfig = {
        allowBitmaps = false;
        antialias    = true;

        hinting = {
          enable = true;
          style  = "slight";
        };

        subpixel = {
          rgba      = "rgb";
          lcdfilter = "default";
        };

        defaultFonts = {
          serif     = [ "Noto Serif CJK JP" "Noto Serif" ];
          sansSerif = [ "Noto Sans CJK JP"  "Noto Sans"  ];
          monospace = [ "DejaVu Sans Mono" "Noto Sans Mono CJK JP" ];
```

あと、これをやってもflatpakのfontconfigが自動更新されないので削除したり、パスを通してやる必要があります。ただ、一部アプリケーションではまだ直せていません。
どうにか既定で直してもらいたいものです。
