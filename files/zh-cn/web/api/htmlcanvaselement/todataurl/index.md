---
title: HTMLCanvasElement.toDataURL()
slug: Web/API/HTMLCanvasElement/toDataURL
---

{{APIRef("Canvas API")}}

**`HTMLCanvasElement.toDataURL()`** 方法返回一个包含图片表示的 [data URI](/zh-CN/docs/Web/URI/Reference/Schemes/data)，此图片的格式由 `type` 参数指定。

可以指定所需的文件格式和图片质量。如果未指定文件格式，或指定的文件格式不受支持，则数据将以 `image/png` 导出。换句话说，如果传入的类型非 `image/png`，但是返回的值以 `data:image/png` 开头，那么这个类型是不受支持的。

浏览器被要求支持 `image/png`，许多浏览器也会支持 `image/jpeg` 和 `image/webp` 在内的其他格式。

对于支持编码分辨率元数据的文件格式，创建的图像数据将具有 96dpi 的分辨率。

> [!WARNING]
> `toDataURL()` 将整个图像编码为内存中的字符串。对于较大的图像，这可能会有性能影响，甚至在赋值给 {{domxref("HTMLImageElement.src")}} 时可能超出浏览器的 URL 长度限制。你通常应该优先选择 [`toBlob()`](/zh-CN/docs/Web/API/HTMLCanvasElement/toBlob)，结合 {{domxref("URL/createObjectURL_static", "URL.createObjectURL()")}} 来使用。

## 语法

```js-nolint
toDataURL()
toDataURL(type)
toDataURL(type, encoderOptions)
```

### 参数

- `type` {{optional_inline}}
  - : 图片格式，默认为 `image/png`
- `encoderOptions` {{optional_inline}}
  - : 在指定图片格式为 `image/jpeg` 或 `image/webp` 的情况下，可以从 0 到 1 的区间内选择图片的质量。如果超出取值范围，将会使用默认值 `0.92`。其他参数会被忽略。

### 返回值

包含 [data URI](/zh-CN/docs/Web/URI/Reference/Schemes/data) 的字符串。

## 示例

有如下{{HTMLElement("canvas")}}元素

```html
<canvas id="canvas" width="5" height="5"></canvas>
```

可以用这样的方式获取一个 data-URL

```js
var canvas = document.getElementById("canvas");
var dataURL = canvas.toDataURL();
console.log(dataURL);
// "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAUAAAAFCAYAAACNby
// blAAAADElEQVQImWNgoBMAAABpAAFEI8ARAAAAAElFTkSuQmCC"
```

### 设置 jpegs 图片的质量

```js
var fullQuality = canvas.toDataURL("image/jpeg", 1.0);
// data:image/jpeg;base64,/9j/4AAQSkZJRgABAQ...9oADAMBAAIRAxEAPwD/AD/6AP/Z"
var mediumQuality = canvas.toDataURL("image/jpeg", 0.5);
var lowQuality = canvas.toDataURL("image/jpeg", 0.1);
```

### 示例：动态更改图片

可以使用鼠标事件来动态改变图片（这个例子中改变图片灰度）。

#### HTML

```html
<img class="grayscale" src="myPicture.png" alt="Description of my picture" />
```

#### JavaScript

```js
window.addEventListener("load", removeColors);

function showColorImg() {
  this.style.display = "none";
  this.nextSibling.style.display = "inline";
}

function showGrayImg() {
  this.previousSibling.style.display = "inline";
  this.style.display = "none";
}

function removeColors() {
  var aImages = document.getElementsByClassName("grayscale"),
    nImgsLen = aImages.length,
    oCanvas = document.createElement("canvas"),
    oCtx = oCanvas.getContext("2d");
  for (
    var nWidth, nHeight, oImgData, oGrayImg, nPixel, aPix, nPixLen, nImgId = 0;
    nImgId < nImgsLen;
    nImgId++
  ) {
    oColorImg = aImages[nImgId];
    nWidth = oColorImg.offsetWidth;
    nHeight = oColorImg.offsetHeight;
    oCanvas.width = nWidth;
    oCanvas.height = nHeight;
    oCtx.drawImage(oColorImg, 0, 0);
    oImgData = oCtx.getImageData(0, 0, nWidth, nHeight);
    aPix = oImgData.data;
    nPixLen = aPix.length;
    for (nPixel = 0; nPixel < nPixLen; nPixel += 4) {
      aPix[nPixel + 2] =
        aPix[nPixel + 1] =
        aPix[nPixel] =
          (aPix[nPixel] + aPix[nPixel + 1] + aPix[nPixel + 2]) / 3;
    }
    oCtx.putImageData(oImgData, 0, 0);
    oGrayImg = new Image();
    oGrayImg.src = oCanvas.toDataURL();
    oGrayImg.onmouseover = showColorImg;
    oColorImg.onmouseout = showGrayImg;
    oCtx.clearRect(0, 0, nWidth, nHeight);
    oColorImg.style.display = "none";
    oColorImg.parentNode.insertBefore(oGrayImg, oColorImg);
  }
}
```

## 规范

{{Specifications}}

## 浏览器兼容性

{{Compat}}

## 参考

- 定义接口，{{domxref("HTMLCanvasElement")}}
- [HTTP](/zh-CN/docs/Web/HTTP) 参考中的 [Data URI](/zh-CN/docs/Web/URI/Reference/Schemes/data)
