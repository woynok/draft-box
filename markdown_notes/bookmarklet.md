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

## udemy の 動画を縦に広げる

下記の elementの `max-height` を 95vh に変更する。

```css
div.ud-main-content-wrapper > div.ud-main-content > div > div > main > div > div.app--row--1ydzX.app--body-container--10gJo > div > div > div
div.ud-main-content-wrapper > div.ud-main-content > div > div > main > div > div.app--row--1ydzX.app--body-container--10gJo > div.curriculum-item-view--scaled-height-limiter--1j3Pp
div.ud-main-content-wrapper > div.ud-main-content > div > div > main > div > div.app--row--1ydzX.app--body-container--10gJo > div > div > div > div > div > div > div
```

ただし、query selector で取得するときには、none が返ってくることがあるので、それを考慮して以下のようにする。

```javascript
let element = document.querySelector("div.ud-main-content-wrapper > div.ud-main-content > div > div > main > div > div.app--row--1ydzX.app--body-container--10gJo > div > div > div");
if (element) {
    element.style.maxHeight = "95vh";
}
element = document.querySelector("div.ud-main-content-wrapper > div.ud-main-content > div > div > main > div > div.app--row--1ydzX.app--body-container--10gJo > div.curriculum-item-view--scaled-height-limiter--1j3Pp");
if (element) {
    element.style.maxHeight = "95vh";
}
element = document.querySelector("div.ud-main-content-wrapper > div.ud-main-content > div > div > main > div > div.app--row--1ydzX.app--body-container--10gJo > div > div > div > div > div > div > div");
if (element) {
    element.style.maxHeight = "95vh";
}
```


また、章立ての領域を狭くして、横の幅に余裕を持たせるために下記の2つのelement の width を変える
```css
/* 75 % から 90% に変更 */
div.ud-main-content-wrapper > div.ud-main-content > div > div > main > div
/* 25 % から 10% に変更 */
div.ud-main-content-wrapper > div.ud-main-content > div > div > main > div > div.app--sidebar-column--2t0E8
```

```javascript
document.querySelector("div.ud-main-content-wrapper > div.ud-main-content > div > div > main > div").style.width = "90%";
document.querySelector("div.ud-main-content-wrapper > div.ud-main-content > div > div > main > div > div.app--sidebar-column--2t0E8").style.width = "10%";
```

bookmarklet用のコードにすると以下のようになる。

```javascript
javascript:(function(){let element = document.querySelector("div.ud-main-content-wrapper > div.ud-main-content > div > div > main > div > div.app--row--1ydzX.app--body-container--10gJo > div > div > div");if (element) {element.style.maxHeight = "95vh";}element = document.querySelector("div.ud-main-content-wrapper > div.ud-main-content > div > div > main > div > div.app--row--1ydzX.app--body-container--10gJo > div.curriculum-item-view--scaled-height-limiter--1j3Pp");if (element) {element.style.maxHeight = "95vh";}element = document.querySelector("div.ud-main-content-wrapper > div.ud-main-content > div > div > main > div > div.app--row--1ydzX.app--body-container--10gJo > div > div > div > div > div > div > div");if (element) {element.style.maxHeight = "95vh";}document.querySelector("div.ud-main-content-wrapper > div.ud-main-content > div > div > main > div").style.width = "90%";document.querySelector("div.ud-main-content-wrapper > div.ud-main-content > div > div > main > div > div.app--sidebar-column--2t0E8").style.width = "10%";})();
```
