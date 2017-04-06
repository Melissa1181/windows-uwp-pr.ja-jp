---
title: "放射光"
description: "放射光は、白熱光などオブジェクトによって放射される光です。"
ms.assetid: 262EB9E2-DF96-401F-93D6-51A7BB60074B
keywords:
- "放射光"
author: PeterTurcan
ms.author: pettur
ms.date: 02/08/2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
translationtype: Human Translation
ms.sourcegitcommit: c6b64cff1bbebc8ba69bc6e03d34b69f85e798fc
ms.openlocfilehash: 50bc904e5810340846b3fd84ffca214d07d38750
ms.lasthandoff: 02/07/2017

---

# <a name="emissive-lighting"></a>放射光


*放射光*は、白熱光などオブジェクトによって放射される光です。 放射を使用すると、レンダリングされたオブジェクトは自己発光しているように見えます。 放射はオブジェクトの色に影響し、暗いマテリアルが明るくなったり、部分的に放射される光の色になったりする場合があります。

放射光は単一の項で表されます。

放射光 = Cₑ

この場合

| パラメーター | 既定値 | 型                                                                 | 説明     |
|-----------|---------------|----------------------------------------------------------------------|-----------------|
| Cₑ        | (0,0,0,0)     | 赤、緑、青、およびアルファ透明度 (すべての浮動小数点値) | 放射色。 |

 

Cₑ の値は、color 1 または color 2 です。 頂点の色が指定されていない場合は、素材の放射色が使用されます。

## <a name="span-idexamplespanspan-idexamplespanspan-idexamplespanexample"></a><span id="Example"></span><span id="example"></span><span id="EXAMPLE"></span>例


この例では、オブジェクトの色は、シーンの環境光と素材のアンビエント色を使用しています。

方程式に従って、生成されるオブジェクトの頂点の色は素材色です。

次の図は、素材色 (緑) を示しています。 放射光は、すべてのオブジェクトの頂点を同じ色で照らします。 頂点の法線やライトの方向には依存しません。 その結果、オブジェクトのサーフェスの周囲にシェーディングの差が生じないため、球体は 2D の円のように見えます。

![緑色の球体の図](images/lighte.jpg)

次の図は、放射光を他の 3 種類のライトとブレンドする方法を示しています。 球体の右側では、緑色の放射光と赤色の環境光がブレンドされています。 球体の左側では、緑色の放射光が赤色の環境光および拡散光とブレンドされ、赤色のグラデーションが生成されています。 鏡面ハイライトの中央は白色ですが、環境光、拡散光、放射光の値のブレンドによって黄色が作成されている状態のまま、反射光の値が急激に低下するため、黄色の輪が作成されています。

![放射光による緑色の球体の図](images/lightadse.jpg)

## <a name="span-idrelated-topicsspanrelated-topics"></a><span id="related-topics"></span>関連トピック


[光源の計算](mathematics-of-lighting.md)

 

 




