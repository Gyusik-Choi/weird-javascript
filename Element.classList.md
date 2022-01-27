# Element.classList

Element

https://developer.mozilla.org/ko/docs/Web/API/Element

<br>

Element.classList는 DOMTokenList를 반환한다

예를 들어,

```html
<div class="item">...</div>
<script>
    const item = document.querySelector(".item")
    console.log(item)
    // <div class="item">...</div>
    console.log(item.classList)
    // DOMTokenList ["item", value: "item"]
    console.log(item.className)
    // item
</script>
```



