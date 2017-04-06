---
title: "ストリーミング リソースの領域をタイル表示する方法"
description: "ストリーミング リソースを作成するときは、次元、フォーマット要素のサイズ、およびミップマップや配列スライスの数 (該当する場合) によって、サーフェス領域全体をサポートするために必要なタイルの数が決まります。"
ms.assetid: 3485FD8D-2A06-4B0A-8810-ECF37736F94B
keywords:
- "ストリーミング リソースの領域をタイル表示する方法"
- "リソースの領域, タイル表示"
- "サイズの一覧表, リソース, タイル表示"
author: PeterTurcan
ms.author: pettur
ms.date: 02/08/2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
translationtype: Human Translation
ms.sourcegitcommit: c6b64cff1bbebc8ba69bc6e03d34b69f85e798fc
ms.openlocfilehash: 699c9e3ce1477589f9331038ae3c7433b5dc1bde
ms.lasthandoff: 02/07/2017

---

# <a name="how-a-streaming-resources-area-is-tiled"></a>ストリーミング リソースの領域をタイル表示する方法


ストリーミング リソースを作成するときは、次元、フォーマット要素のサイズ、およびミップマップや配列スライスの数 (該当する場合) によって、サーフェス領域全体をサポートするために必要なタイルの数が決まります。 タイル内のピクセル/バイト レイアウトは、実装によって決定されます。 1 つのタイルに収まるピクセル数は、形式の要素のサイズに応じて固定され、標準スウィズルを使用するかどうかに関係なく同じです。

指定されたサーフェスのサイズと形式要素の幅によって使用されるタイルの数は、次のセクションの表に基づいて定義されており、予測可能です。 ミップマップを含むリソースや、サーフェスのサイズがタイルに満たない場合は、いくつかの制約が存在します。「[ミップマップのパッキング](mipmap-packing.md)」を参照してください。

アプリケーションが、ある形式でのメモリへの書き込みと別の形式での読み取りの結果に依存しない限り、複数のストリーミング リソースがさまざまな形式で同一のメモリを指定できます。 ただし、形式が同じ形式ファミリーである場合 (つまり、型指定なしの親の形式が同じである場合)、アプリケーションは、ある形式でのメモリへの書き込みと別の形式での読み取りの結果に依存する可能性があります。 たとえば、DXGI\_FORMAT\_R8G8B8A8\_UNORM と DXGI\_FORMAT\_R8G8B8A8\_UINT は互換性がありますが、DXGI\_FORMAT\_R16G16\_UNORM とは互換性がありません。

ある形式のデータが別の形式のエイリアスとして定義されている場合は例外です。タイルのすべてのビットに 0 が含まれている場合、そのタイルは、(メモリ レイアウトに関係なく) メモリの内容が 0 であることを解釈する任意の形式で使用できます。 そのため、DXGI\_FORMAT\_R8\_UNORM 形式でタイルを 0x00 にクリアし、DXGI\_FORMAT\_R32G32\_FLOAT などの形式で使用でき、その内容は引き続き (0.0f,0.0f) と表示されます。

タイル内でのデータのレイアウトは、タイルがリソース全体に割り当てられているかどうかに依存しません。 そのため、たとえば、サーフェスの複数の場所で同時にタイルを再利用し、すべての場所で一貫性のある動作を実現できます。

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
<td align="left"><p>[Texture2D と Texture2DArray のサブリソースのタイル表示](texture2d-and-texture2darray-subresource-tiling.md)</p></td>
<td align="left"><p>これらの表では、[<strong>Texture2D</strong>](https://msdn.microsoft.com/library/windows/desktop/ff471525) および [<strong>Texture2DArray</strong>](https://msdn.microsoft.com/library/windows/desktop/ff471526) サブリソースをタイル表示する方法を示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>[Texture3D サブリソースのタイル表示](texture3d-subresource-tiling.md)</p></td>
<td align="left"><p>この表では、[<strong>Texture3D</strong>](https://msdn.microsoft.com/library/windows/desktop/ff471562) サブリソースをタイル表示する方法を示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>[バッファーのタイル表示](buffer-tiling.md)</p></td>
<td align="left"><p>[バッファー ](introduction-to-buffers.md) リソースは 64 KB のタイルに分割されます。サイズが 64 KB の倍数でない場合は、最後のタイルに空きが生じます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>[ミップマップのパッキング](mipmap-packing.md)</p></td>
<td align="left"><p>ストリーミング リソースのサイズ、形式、ミップマップの数、配列スライスに応じて、いくつかの mips (配列スライスごと) をいくつかのタイルにパッキングすることができます。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelated-topicsspanrelated-topics"></a><span id="related-topics"></span>関連トピック


[ストリーミング リソースの作成](creating-streaming-resources.md)

 

 




