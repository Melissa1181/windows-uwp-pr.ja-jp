---
title: "ラスタライザー順序指定ビュー (ROV)"
description: "ラスタライザー順序指定ビューを使うと、深度バッファーの一部の制約に対処できます。特に、透明度が含まれた複数のテクスチャがあって、それらがすべて同じピクセルに適用される場合に有効です。"
ms.assetid: BCB1EE0D-4C1D-4E17-BDB7-173F448E0A7B
keywords:
- "ラスタライザー順序指定ビュー (ROV)"
author: PeterTurcan
ms.author: pettur
ms.date: 02/08/2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
translationtype: Human Translation
ms.sourcegitcommit: c6b64cff1bbebc8ba69bc6e03d34b69f85e798fc
ms.openlocfilehash: ee1ac48111c94f88d87e595eaaf6f5442d137ce4
ms.lasthandoff: 02/07/2017

---

# <a name="rasterizer-ordered-view-rov"></a>ラスタライザー順序指定ビュー (ROV)


ラスタライザー順序指定ビューを使うと、深度バッファーの一部の制約に対処できます。特に、透明度が含まれた複数のテクスチャがあって、それらがすべて同じピクセルに適用される場合に有効です。

ラスタライザー順序指定ビューは、"描画順序に依存しない透明化" (OIT) アルゴリズムをピクセルのレンダリングに適用できるようにします。 深度バッファーではピクセルを描画するか、隠すことしかできず、透明度を利用して中途半端に見えなくするという概念はありません。 OIT アルゴリズムは、透明なテクスチャを正しい順序で適用します。そのため、たとえばですが、透明なガラス オブジェクトをガラス窓の後ろに表示し、そのガラス窓の手前には透明なテクスチャを使用した何らかの植物を表示した場合に、最終的な結果が予想通りに正しく描画されます。 ROV と OIT アルゴリズムがなければ、こうした透明なオブジェクトの描画順序が予想できなくなるため、レンダリングされるシーンが複雑で誤ったものになる可能性があります。

## <a name="span-idrelated-topicsspanrelated-topics"></a><span id="related-topics"></span>関連トピック


[ビュー](views.md)

 

 




