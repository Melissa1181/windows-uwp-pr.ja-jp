---
title: ゲーム DVR URI
assetID: 472f705e-bf28-7894-b1ba-80933d8746a6
permalink: en-us/docs/xboxlive/rest/atoc-reference-dvr.html
author: KevinAsgari
description: " ゲーム DVR URI"
ms.author: kevinasg
ms.date: 20-12-2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: Xbox Live, Xbox, ゲーム, UWP, Windows 10, Xbox One
ms.localizationpriority: medium
ms.openlocfilehash: 7c9be3254d9264c1d06dd0a327c36b473a457a35
ms.sourcegitcommit: a160b91a554f8352de963d9fa37f7df89f8a0e23
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/22/2018
ms.locfileid: "4122770"
---
# <a name="game-dvr-uris"></a>ゲーム DVR URI
 
このセクションでは、*ゲーム DVR*の Xbox Live サービスからユニバーサル Resource Identifier (URI) アドレスと関連付けられているハイパー テキスト トランスポート プロトコル (HTTP) 方法に関する詳細を提供します。
 
本体のみが、ゲーム クリップを記録できますにアクセスできる任意のデバイスにクリップを表示できます。
 
問題の URI の関数によってこれらの Uri のドメインは。
 
   *  gameclipsmetadata.xboxlive.com 
   *  gameclipstransfer.xboxlive.com 
  
<a id="ID4EZB"></a>

 
## <a name="in-this-section"></a>このセクションの内容

[/public/scids/{scid}/clips](uri-publicscidclips.md)

&nbsp;&nbsp;クリップをパブリックにアクセスします。 この URI に実際にで指定できる 2 つのフォーム`/public/scids/{scid}/clips`と`/public/titles/{titleId}/clips`します。 詳しくは、後のセクションをご覧ください。

[/{uri}](uri-uri.md)

&nbsp;&nbsp;ゲーム クリップ データにアクセスします。

[/users/me/scids/{scid}/clips](uri-usersmescidclips.md)

&nbsp;&nbsp;最初のアクセスは、要求をアップロードします。

[/users/me/scids/{scid}/clips/{gameClipId}](uri-usersmescidclipsgameclipid.md)

&nbsp;&nbsp;ゲーム クリップ データへのアクセスとメタデータ。

[/users/{ownerId}/clips](uri-usersowneridclips.md)

&nbsp;&nbsp;ユーザーのクリップのアクセスの一覧です。

[/users/{ownerId}/scids/{scid}/clips/{gameClipId}](uri-usersowneridscidclipsgameclipid.md)

&nbsp;&nbsp;すべての Id を見つけることがわかっている場合はシステムから 1 つのゲーム クリップにアクセスします。
 
<a id="ID4EOC"></a>

 
## <a name="see-also"></a>関連項目
 
<a id="ID4EQC"></a>

 
##### <a name="parent"></a>Parent 

[ユニバーサル リソース識別子 (URI) リファレンス](../atoc-xboxlivews-reference-uris.md)

   