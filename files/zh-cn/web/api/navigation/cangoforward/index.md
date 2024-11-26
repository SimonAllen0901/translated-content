---
title: Navigation：canGoForward 属性
slug: Web/API/Navigation/canGoForward
l10n:
  sourceCommit: e00c30e3919b1cc08fa1ea3913e75a42a91add02
---

{{APIRef("Navigation API")}}{{SeeCompatTable}}

{{domxref("Navigation")}} 接口的 **`canGoForward`** 只读属性在可以在导航历史记录中向前导航（即 {{domxref("Navigation.currentEntry", "currentEntry")}} 不是历史记录条目列表中的最后一个）时返回 `true`，否则返回 `false`。

## 值

布尔值：如果可以在导航历史记录中向前导航，则为 `true`，否则为 `false`。

## 示例

```js
async function backHandler() {
  if (navigation.canGoBack) {
    await navigation.back().finished;
    // 导航结束后处理任何必要的清理工作
  } else {
    displayBanner("你在第一页");
  }
}

async function forwardHandler() {
  if (navigation.canGoForward) {
    await navigation.forward().finished;
    // 导航结束后处理任何必要的清理工作
  } else {
    displayBanner("你在最后一页");
  }
}
```

## 规范

{{Specifications}}

## 浏览器兼容性

{{Compat}}

## 参见

- [现代客户端路由：导航 API](https://developer.chrome.google.cn/docs/web-platform/navigation-api/)
- [导航 API 说明](https://github.com/WICG/navigation-api/blob/main/README.md)
- Domenic Denicola 的[导航 API 在线演示](https://gigantic-honored-octagon.glitch.me/)