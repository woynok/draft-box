# bookmarklet 作成

## ChatGPTのページのコードブロックを広げる

`@media (min-width: 1280px)`で定義されている`max-width: 48rem`を広げたい。

### foreachで書き換える場合

```javascript
let elements = document.querySelectorAll(".flex.flex-1.text-base.mx-auto.gap-3");
elements.forEach((element) => {
    element.style.maxWidth = "80rem";
});
```

この場合、bookmarkletを実行したときに存在する要素にしか適用されない。

### @mediaを書き換える場合

1280px よりも一段階大きい 1440px より大きいときに適用されるようにする。

```javascript
let style = document.createElement("style");
style.innerHTML = `
@media (min-width: 1440px) {
    .flex.flex-1.text-base.mx-auto.gap-3 {
        max-width: 90rem;
    }
}
`;
document.head.appendChild(style);
```

上記をone-linerにすると以下のようになる。

```javascript
document.head.appendChild(document.createElement("style")).innerHTML = `@media (min-width: 1440px) { .flex.flex-1.text-base.mx-auto.gap-3 { max-width: 90rem; } } `;
```

さらに、bookmarklet用のコードにすると以下のようになる。

```javascript
javascript:(function(){document.head.appendChild(document.createElement("style")).innerHTML = `@media (min-width: 1440px) { .flex.flex-1.text-base.mx-auto.gap-3 { max-width: 90rem; } } `;})();
```
