---
title: "頂点バッファーとインデックス バッファー"
description: "頂点バッファーは、頂点データを格納するメモリ バッファーです。頂点バッファー内の頂点は、変換、照明の適用、クリッピングを実行するために処理されます。"
ms.assetid: 8A39CD23-85FB-4424-9AC3-37919704CD68
keywords:
- "頂点バッファーとインデックス バッファー"
author: PeterTurcan
ms.author: pettur
ms.date: 02/08/2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
translationtype: Human Translation
ms.sourcegitcommit: c6b64cff1bbebc8ba69bc6e03d34b69f85e798fc
ms.openlocfilehash: cdf65da6504114029c4937ee7db531a1339ed4c2
ms.lasthandoff: 02/07/2017

---

# <a name="vertex-and-index-buffers"></a>頂点バッファーとインデックス バッファー


"頂点バッファー"** は、頂点データを格納するメモリ バッファーです。頂点バッファー内の頂点は、変換、照明の適用、クリッピングを実行するために処理されます。 "インデックス バッファー"** は、インデックス データを格納するメモリ バッファーです。インデックス データは頂点バッファーへの整数オフセットで、プリミティブのレンダリングに使われます。

頂点バッファーには、レンダリング可能な任意の種類の頂点を含めることができます。変換済みでも未変換でも、照明が適用済みでも未適用でもかまいません。 頂点バッファー内の頂点を処理して、変換、照明の適用、クリッピング フラグの生成などの操作を実行できます。 変換は常に実行されます。

頂点バッファーは柔軟なため、変換されたジオメトリを再利用するための最適なステージング ポイントとなります。 1 つの頂点バッファーを作成し、その中の頂点に対して変換、照明、クリッピングを適用したら、そのモデルを必要に応じて何度でも、再変換なしでシーンにレンダリングできます。途中でレンダリング状態が変更されたとしても、再変換を行う必要はありません。 これは、複数のテクスチャを使うモデルをレンダリングする場合に便利です。ジオメトリを 1 回だけ変換すれば、必要なテクスチャの変更を加えながら、変換したジオメトリの一部を必要に応じてレンダリングすることができます。 頂点の処理後に行われたレンダリング状態の変更は、次に頂点が処理されるときに反映されます。

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
<td align="left"><p>[バッファーの概要](introduction-to-buffers.md)</p></td>
<td align="left"><p>バッファー リソースは完全に型指定されたデータのコレクションであり、複数の要素にグループ化されます。 バッファーには、"頂点バッファー"<em></em> 内のテクスチャ座標、"インデックス バッファー"<em></em> 内のインデックス、"定数バッファー"<em></em> 内のシェーダー定数データ、位置ベクトル、法線ベクトル、デバイスの状態などのデータが格納されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>[インデックス バッファー](index-buffers.md)</p></td>
<td align="left"><p><em></em>"インデックス バッファー" は、インデックス データを格納するメモリ バッファーです。インデックス データは頂点バッファーへの整数オフセットで、プリミティブのレンダリングに使われます。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelated-topicsspanrelated-topics"></a><span id="related-topics"></span>関連トピック


[Direct3D Graphics の学習ガイド](index.md)

 

 




