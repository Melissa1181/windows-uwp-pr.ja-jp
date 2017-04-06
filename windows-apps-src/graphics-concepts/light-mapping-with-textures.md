---
title: "テクスチャでのライト マッピング"
description: "ライト マップは、3D シーン内の照明に関する情報を含むテクスチャまたはテクスチャのグループです。"
ms.assetid: 5C7518D2-AC92-4A97-B7AF-4469D213D7BD
keywords:
- "テクスチャでのライト マッピング"
author: PeterTurcan
ms.author: pettur
ms.date: 02/08/2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
translationtype: Human Translation
ms.sourcegitcommit: c6b64cff1bbebc8ba69bc6e03d34b69f85e798fc
ms.openlocfilehash: 1154be19719cc3101c114c0bd700fb735824bcda
ms.lasthandoff: 02/07/2017

---

# <a name="light-mapping-with-textures"></a>テクスチャでのライト マッピング


ライト マップは、3D シーン内の照明に関する情報を含むテクスチャまたはテクスチャのグループです。 ライト マップは、光と影の領域をプリミティブにマップします。 マルチパスおよび複数テクスチャ ブレンドにより、アプリケーションがシェーディング手法より現実的な外観によってシーンをレンダリングできるようになります。

アプリケーションが 3D シーンを現実的にレンダリングするには、光源がシーンの外観に与える効果を考慮に入れる必要があります。 フラットおよびグロー シェーディングなどの手法は、この点においては貴重なツールですが、ニーズを満たすのには不十分な可能性があります。 Direct3D は、マルチパスおよび複数テクスチャ ブレンドをサポートします。 これらの機能により、アプリケーションがシェーディング手法だけを使ってレンダリングされたシーンより現実的な外観によってシーンをレンダリングできるようになります。 1 つ以上のライト マップを適用することにより、アプリケーションは光と影の領域をそのプリミティブにマップできます。

ライト マップは、3D シーン内の照明に関する情報を含むテクスチャまたはテクスチャのグループです。 照明情報は、ライト マップのアルファ値、色値、またはその両方に格納できます。

マルチパス テクスチャ ブレンドを使ってライト マップを実装した場合、アプリケーションはライト マップを最初のパスのプリミティブにマップします。 また、基本テクスチャのレンダリングには 2 つ目のパスを使います。 例外は反射光マップです。 その場合、まず基本テクスチャをレンダリングしてから、ライト マップを追加してください。

複数テクスチャ ブレンドにより、アプリケーションがライト マップと基本テクスチャを 1 つのパスでレンダリングできるようになります。 複数テクスチャ ブレンド用のユーザーのハードウェアがある場合、アプリケーションはライト マップを実行する際にそれを利用します。 これにより、アプリケーションのパフォーマンスが大幅に向上します。

ライト マップを使って、Direct3D アプリケーションはプリミティブのレンダリング時にさまざまな照明効果を実現します。 シーン内のモノクロとカラーの照明をマップできるだけでなく、鏡面ハイライトや拡散光などのディテールも追加できます。

Direct3D のテクスチャ ブレンドを使ってライト マップを実行する方法については、以下のトピックをご覧ください。

## <a name="span-idin-this-sectionspanin-this-section"></a><span id="in-this-section"></span>このセクションの内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">トピック</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>[モノクロ ライト マップ](monochrome-light-maps.md)</p></td>
<td align="left"><p>モノクロ ライト マップを使うと、古い 3D アクセラレータ ボードが宛先ピクセルのアルファ値を使ったテクスチャ ブレンドをサポートしていない場合に、古いアダプターでもマルチパス テクスチャ ブレンドを実行できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>[カラー ライト マップ](color-light-maps.md)</p></td>
<td align="left"><p>カラー ライト マップは、ライト マップ内で照明情報に RGB データを使います。 アプリケーションは通常、カラー ライト マップを使う場合の方が現実的に 3D シーンをレンダリングします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>[反射ライト マップ](specular-light-maps.md)</p></td>
<td align="left"><p>光源から照射されると、反射率の高いマテリアルを使用している光沢のあるオブジェクトには反射光が適用されます。 照明モジュールによって生成された鏡面ハイライトを使用するのではなく、反射ライト マップをプリミティブに適用した方が、より正確なハイライトが得られる場合があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p>[拡散ライト マップ](diffuse-light-maps.md)</p></td>
<td align="left"><p>つや消しサーフェスでは、拡散光が反射します。 拡散光の明るさは、光源からの距離と、サーフェスの法線および光源方向ベクトルの角度によって決まります。 テクスチャ ライト マップは、複雑な拡散光をシミュレートできます。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelated-topicsspanrelated-topics"></a><span id="related-topics"></span>関連トピック


[テクスチャ](textures.md)

 

 




