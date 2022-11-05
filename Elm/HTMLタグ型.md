# HTMLタグ型



HTMLタグが型として用意されている



例えば、divタグは

```elm
div [HTMLの属性(attribute)][HTMLの中身]
-- 第一引数がHTMLAttribute型, 第二引数がHTMLMsg型
```

のようになる

```elm
div [][
  div [][text "hoge"]
  div [][text "aiueo"]
]
```

こんな感じになる

```html
<div>
    <div>
        aiueo
    </div>
    <div>
        hoge
    </div>
</div>
```

