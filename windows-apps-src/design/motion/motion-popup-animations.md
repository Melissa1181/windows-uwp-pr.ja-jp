---
author: mijacobs
Description: Use pop-up animations to show and hide pop-up UI for flyouts or custom pop-up UI elements. Pop-up elements are containers that appear over the app's content and are dismissed if the user taps or clicks outside of the pop-up element.
title: UWP アプリでのポップアップ UI のアニメーション
ms.assetid: 4E9025CE-FC90-4d4c-9DE6-EC6B6F2AD9DF
label: Motion--Pop-up animations
template: detail.hbs
ms.author: mijacobs
ms.date: 05/19/2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: Windows 10, UWP
ms.localizationpriority: medium
ms.openlocfilehash: bcec5b62f400f2eb1410a61615d550f26520357f
ms.sourcegitcommit: 0ab8f6fac53a6811f977ddc24de039c46c9db0ad
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/15/2018
ms.locfileid: "1651941"
---
# <a name="pop-up-ui-animations"></a>ポップアップ UI のアニメーション



ポップアップ アニメーションを使って、ポップアップ UI やカスタム ポップアップ UI 要素の表示と非表示を切り替えます。 ポップアップ要素とは、アプリのコンテンツの上に表示されるコンテナーのことで、ユーザーがポップアップ要素の外部をタップまたはクリックすると消えます。

> **重要な API**: [**PopInThemeAnimation クラス**](https://msdn.microsoft.com/library/windows/apps/br210383)、[**PopupThemeTransition クラス**](https://msdn.microsoft.com/library/windows/apps/hh969172)


## <a name="dos-and-donts"></a>推奨と非推奨


-   ポップアップ アニメーションは、アプリ ページ自体には含まれないカスタム ポップアップ UI 要素を表示したり非表示にしたりするために使います。 Windows で用意されているコモン コントロールには、既にこのアニメーションが組み込まれています。
-   ヒントやダイアログにポップアップ アニメーションを使わないでください。
-   アプリのメイン コンテンツ内の UI の表示と非表示を切り替えるためにポップアップ アニメーションを使わないでください。ポップアップ アニメーションは、メイン アプリ コンテンツの上に表示されるポップアップ コンテナーの表示と非表示を切り替えるときにのみ使います。

## <a name="related-articles"></a>関連記事

* [アニメーションの概要](https://msdn.microsoft.com/library/windows/apps/mt187350)
* [ポップアップ UI のアニメーション化](https://msdn.microsoft.com/library/windows/apps/xaml/jj649433)
* [クイック スタート: ライブラリのアニメーションを使った UI のアニメーション化](https://msdn.microsoft.com/library/windows/apps/xaml/hh452703)
* [**PopInThemeAnimation クラス**](https://msdn.microsoft.com/library/windows/apps/br210383)
* [**PopOutThemeAnimation クラス**](https://msdn.microsoft.com/library/windows/apps/br210391)
* [**PopupThemeTransition クラス**](https://msdn.microsoft.com/library/windows/apps/hh969172)

 

 



