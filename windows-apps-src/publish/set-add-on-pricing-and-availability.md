---
author: jnHs
Description: When submitting an add-on, the options on the Pricing and availability page determine what to charge for your add-on and how it should be offered to customers.
title: アドオンの価格と使用可能状況の設定
ms.assetid: B3D4B753-716B-460B-A3B1-ED5712ECD694
ms.author: wdg-dev-content
ms.date: 05/08/2018
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: windows 10, uwp, アドオン, iap, 価格
ms.localizationpriority: medium
ms.openlocfilehash: b5b7a6424fea3d62849e992f56b0b40ab72a55f5
ms.sourcegitcommit: 194ab5aa395226580753869c6b66fce88be83522
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/24/2018
ms.locfileid: "4156555"
---
# <a name="set-add-on-pricing-and-availability"></a>アドオンの価格と使用可能状況の設定


アドオンを申請するときに、**[価格と使用可能状況]** ページのオプションで、アドオンの料金やユーザーに提供する方法を指定します。

## <a name="markets"></a>市場

既定では、アドオンは販売できるすべての市場 (今後追加される可能性のある市場も含む) にその基本価格で公開されます。

ただし、アプリと同様に、アドオンを提供する市場を選ぶためのオプションもあります。 ほとんどの場合、アプリと同じ一連の市場の選びますが、必要に応じて柔軟に変更できます。 

詳しい情報と利用可能な市場の一覧については、「[市場の選択の定義](define-pricing-and-market-selection.md)」をご覧ください。

## <a name="visibility"></a>表示

アドオンをユーザーが購入できるようにするかどうかを指定できます。 

既定のオプションは **[親製品のストア登録情報に表示することができます]** です。 アドオンをすべてのユーザーに提供する場合は、このオプションをオンのままにしておきます。 

広範囲に公開したくないアドオンについては、**[ストアに表示しない]** と、次のいずれかのオプションを選びます。

-   **[親製品内のみから購入することができます]**: このオプションを選ぶと、ユーザーはアプリ内からアドオンを購入できますが、アドオンはアプリのストア登録情報ページには表示されません。 初期の内部テスト期間中など、一般に広く公開されていない場合にのみ、このオプションを使います。
-   **[購入の停止: 直接リンクを知っているユーザーは製品のストア登録情報を表示できます。ただし、製品をダウンロードできるのは、以前にその製品を所有していたか、またはプロモーション コードを持っている場合で、かつ Windows 10 デバイスを使用している場合のみです。このアドオンは、親製品のストア登録情報には表示されません]**: このオプションを選ぶと、アドオンはアプリの登録情報ページに表示されず、新しいユーザーはアドオンを購入することができません。 ただし、**このオプションは、Windows 8.1 またはそれ以前のバージョンのユーザーについてはサポートされていません**。 アプリが Windows 8.1 またはそれ以前のバージョンで利用できる場合、それらのユーザーは引き続きアドオンを購入できます。 Windows 8.1 またはそれ以前バージョンのユーザーに対して、このアドオンの提供を停止するには、アプリを更新してアドオンを提供するコードを削除し、新しいアプリの提出パッケージを公開する必要があります。 アプリが Windows 8.1 またはそれ以前のバージョンを対象としていない場合でも、この方法をお勧めします。利用できないようにすることを選択したアドオンをユーザーに提供しないことは、ユーザーのエクスペリエンス向上につながります。
    
 > [!NOTE] 
 > **[購入の停止]** オプションを選んだ場合や、アプリのコードからアドオンを削除するアプリの更新プログラムを提出した場合でも、オペレーティング システムに関係なく、アドオンを購入済みのユーザーには影響しません。


## <a name="schedule"></a>スケジュール

既定では (**[表示]** セクションで **[ストアに表示しない]** のオプションのいずれかを選択した場合を除き)、アドオンが認定に合格して公開プロセスが完了すると、そのアプリはすぐにユーザーが利用できるようになります。 他の日付を選択するには、**[オプションの表示]** を選択してこのセクションを展開します。 

詳しくは、「[正確なリリース スケジュールの構成](configure-precise-release-scheduling.md)」をご覧ください。


## <a name="pricing"></a>価格設定

(**購入の停止]** オプションを選択した場合は、**可視性**」セクションで) を除き、アドオンの基本価格を選択する必要があります。 既定の選択は、**無料**、有料のアドオンの場合は、必ず (米ドル.99 以降) 利用可能な価格帯のいずれかを選択します。

価格変更をスケジュールして、アドオンの価格を変更する日時を指定することもできます。 さらに、これらの変更を特定の市場向けにカスタマイズすることもできます。 

> [!TIP]
> サブスクリプション アドオンの場合、それ以降の申請でより高い基本価格を選択することによって、または価格の増加価格変更をスケジュールすることによって、アドオンの公開後の価格を上げることはできません。 これらのメソッドのいずれかを使用して、割引価格を選択することができますが、価格を下げるとその新しい価格より高いさせるできなくなります。 このため、サブスクリプション アドオンの適切な価格帯を選択するかを確認することが特に重要です。 

詳しくは、「[アプリの価格の設定とスケジュール](set-and-schedule-app-pricing.md)」をご覧ください。


## <a name="sale-pricing"></a>セール価格

期間限定でアドオンを割引価格で提供する場合は、特売を作成し、そのスケジュールを設定できます。 詳しくは、「[アプリとアドオンの販売](put-apps-and-add-ons-on-sale.md)」をご覧ください。


