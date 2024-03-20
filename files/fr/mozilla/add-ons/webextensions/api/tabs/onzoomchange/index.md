---
title: tabs.onZoomChange
slug: Mozilla/Add-ons/WebExtensions/API/tabs/onZoomChange
---

{{AddonSidebar}}

Envoyé lorsqu'un onglet est agrandi.

## Syntaxe

```js
browser.tabs.onZoomChange.addListener(listener);
browser.tabs.onZoomChange.removeListener(listener);
browser.tabs.onZoomChange.hasListener(listener);
```

Les événements ont trois fonctions :

- `addListener(callback)`
  - : Ajoute un écouteur à cet événement.
- `removeListener(listener)`
  - : Arrêtez d'écouter cet événement. L'argument `listener` de l'écouteur est l'écouteur à supprimer.
- `hasListener(listener)`
  - : Vérifiez si `listener` est enregistré pour cet événement. Renvoie `true` s'il écoute, sinon `false`.

## Syntaxe addListener

### Paramètres

- `callback`

  - : Fonction qui sera appelée lorsque cet événement se produit. La fonction recevra les arguments suivants :

    - `ZoomChangeInfo`
      - : [`object`](#ZoomChangeInfo). Informations sur l'événement de zoom.

## Objets supplémentaires

### ZoomChangeInfo

- `tabId`
  - : `integer`. ID de l'onglet qui a été zoomé.
- `oldZoomFactor`
  - : `number`. Le facteur de zoom précédent.
- `newZoomFactor`
  - : `number`. Le nouveau facteur de zoom.
- `zoomSettings`
  - : {{WebExtAPIRef('tabs.ZoomSettings')}}. Paramètres de zoom pour l'onglet.

## Exemples

Ecoutez les événements de zoom et consignez les informations :

```js
function handleZoomed(zoomChangeInfo) {
  console.log("Tab: " + zoomChangeInfo.tabId + " zoomed");
  console.log("Old zoom: " + zoomChangeInfo.oldZoomFactor);
  console.log("New zoom: " + zoomChangeInfo.newZoomFactor);
}

browser.tabs.onZoomChange.addListener(handleZoomed);
```

{{WebExtExamples}}

## Compatibilité des navigateurs

{{Compat}}

> **Note :**
>
> Cette API est basée sur l'API Chromium [`chrome.tabs`](https://developer.chrome.com/extensions/tabs#method-executeScript). Cette documentation est dérivée de [`tabs.json`](https://chromium.googlesource.com/chromium/src/+/master/chrome/common/extensions/api/tabs.json) dans le code de Chromium code.
>
> Les données de compatibilité relatives à Microsoft Edge sont fournies par Microsoft Corporation et incluses ici sous la licence Creative Commons Attribution 3.0 pour les États-Unis.

<!--
// Copyright 2015 The Chromium Authors. All rights reserved.
//
// Redistribution and use in source and binary forms, with or without
// modification, are permitted provided that the following conditions are
// met:
//
//    * Redistributions of source code must retain the above copyright
// notice, this list of conditions and the following disclaimer.
//    * Redistributions in binary form must reproduce the above
// copyright notice, this list of conditions and the following disclaimer
// in the documentation and/or other materials provided with the
// distribution.
//    * Neither the name of Google Inc. nor the names of its
// contributors may be used to endorse or promote products derived from
// this software without specific prior written permission.
//
// THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS
// "AS IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT
// LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR
// A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT
// OWNER OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL,
// SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT
// LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE,
// DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY
// THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT
// (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE
// OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
-->