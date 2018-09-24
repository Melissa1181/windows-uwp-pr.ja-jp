---
author: QuinnRadich
title: Windows ドキュメントの最新情報で新 2018 年 5 月 - UWP アプリの開発
description: 2018 年 5 月の Windows 10 開発者向けドキュメントと Microsoft Build カンファレンスに、新しい機能、ビデオ、および開発者向けガイダンスが追加されました。
keywords: 新着情報, 更新, 機能, 開発者向けガイダンス, Windows 10、月、ビルド
ms.author: quradic
ms.date: 5/7/2018
ms.topic: article
ms.prod: windows
ms.technology: uwp
ms.localizationpriority: medium
ms.openlocfilehash: 322bc056411095019dfc027078cbfef7de0883fb
ms.sourcegitcommit: 194ab5aa395226580753869c6b66fce88be83522
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/24/2018
ms.locfileid: "4151067"
---
# <a name="whats-new-in-the-windows-developer-docs-in-may-2018"></a>Windows 開発者向けドキュメントの最新情報で新 2018 年 5 月

Windows 開発者向けドキュメントは、Windows プラットフォームで開発者に提供される新機能の情報を反映して継続的に更新されています。 次の機能概要、開発者向けガイダンス、ビデオ、およびサンプルには、5 月の[Microsoft Build 2018](https://www.microsoft.com/build)開発者カンファレンスと一致するので利用可能ななりました。

Windows 10 の[ツールと SDK をインストール](http://go.microsoft.com/fwlink/?LinkId=821431)すると、[新しいユニバーサル Windows アプリを作成](../get-started/create-uwp-apps.md)したり、[Windows の既存のアプリ コード](../porting/index.md)がどのように使えるかを試したりすることができます。

## <a name="features"></a>機能

### <a name="motion-in-fluent-design"></a>Fluent Design のモーション

タイミング、イージング、方向、および重力の基礎上に構築され、Fluent Design System のモーションのユーザーが進化しています。 これらの基礎を適用することは、アプリを使用してユーザーをガイドに役立ち、その接続とそのデジタル エクスペリエンスによって、自然界を反映します。 この記事では、複数について説明します。

* これらの基礎を反映するように[、モーションの概要](../design/motion/index.md)が更新されました。
* [モーションの演習で](../design/motion/motion-in-practice.md)は、アプリ内でこれらの基礎を適用する方法の例を示します。
* [方向性と重力](../design/motion/directionality-and-gravity.md)には、アプリのユーザーの概念的モデルが塗りつぶされます。
* [タイミングとイージング](../design/motion/timing-and-easing.md)は、アプリでモーションにリアルさを追加します。

![モーションの動作を確認](../design/motion/images/contextual.gif)

### <a name="fluent-design-updates"></a>Fluent Design の更新プログラム

次の Fluent Design ページ visual の更新プログラムと小規模な変更が追加されました。

* [パディング、余白の配置](../design/layout/alignment-margin-padding.md)
* [色](../design/style/color.md)
* [コマンドの基本](../design/basics/commanding-basics.md)
* [Windows アプリ用の fluent Design](../design/fluent-design-system/index.md)
* [アプリの設計の概要](../design/basics/design-and-ui-intro.md)
* [ナビゲーションの基本](../design/basics/navigation-basics.md)
* [レスポンシブ デザインの手法](../design/layout/responsive-design.md)
* [画面のサイズとブレークポイント](../design/layout/screen-sizes-and-breakpoints-for-responsive-design.md)
* [スタイルの概要](../design/style/index.md)
* [記述スタイル](../design/style/writing-style.md)

さらに、まったく新しい情報がコンテンツ領域が次のページを書き換えるしたします。

* [アイコン](../design/style/icons.md)は、アイコンを使用して、クリック可能なを行うのためのアドバイスを提供します。
* [文字体裁](../design/style/typography.md)では、更新されたガイダンスと図を 1 つの場所に配置するすべてのものと同様の記事からの情報を統合します。

![カラー パレットの画像](../design/style/images/color/accent-color-palette.svg)

### <a name="app-installer-files-in-visual-studio"></a>Visual Studio でアプリ インストーラー ファイル

Visual Studio 2017 Update 15.7 により、アプリ インストーラー ファイルを作成できるようになりましたできます。 アプリを自動更新を[アプリ インストーラー ファイルを作成する Visual Studio を使用する方法について説明](../packaging/create-appinstallerfile-vs.md)し、有効にします。 問題が発生した場合、一般的な問題と解決策を表示する[アプリ インストーラー ファイルを使ったインストールに関する問題のトラブルシューティング](../packaging/troubleshoot-appinstaller-issues.md)を参照してください。

### <a name="edge-webview-control-for-windows-forms-and-wpf-applications"></a>Windows フォーム、WPF アプリケーションの WebView コントロールを境界線します。

デスクトップ アプリケーションにのみ利用可能であった UWP アプリケーションを WebView コントロールを使用して、web コンテンツを表示します。 このコントロールは、レンダリング エンジンを埋め込むことレンダリング書式付き HTML ビューをリモート web サーバー、動的に生成されたコード、またはコンテンツ ファイルからコンテンツを Microsoft Edge を使用します。 最新のリリースの WebView コントロールを見つけ、 [Windows コミュニティ ツールキット](https://docs.microsoft.com/windows/uwpcommunitytoolkit/)。

Windows コミュニティ ツールキットの今後のリリースにおける WebView など、他のコントロールを探します。 詳細については、次を参照してください[WPF および Windows フォーム アプリケーションで UWP のホストを制御します。](https://docs.microsoft.com/windows/uwp/xaml-platform/xaml-host-controls) 。

### <a name="gaze-input-and-interactions"></a>視線入力と操作

[ユーザーの視線、注意、および場所とユーザーの目の動きに基づくプレゼンスを追跡します。](../design/input/gaze-interactions.md) この強力な新しい方法を使用し、UWP アプリとの対話は、支援技術として特に役立ちます。 視線入力は、ゲーム (追跡およびターゲットの入手を含む) と従来の入力デバイス (キーボード、マウス、タッチ) が利用可能ないないその他の対話型シナリオの両方の魅力的な機会も提供されます。

### <a name="msix-packaging-format"></a>MSIX パッケージ形式

Microsoft Build 2018 カンファレンスで発表、MSIX は、Win32、Windows フォーム、WPF、および UWP を含むすべての Windows アプリケーションに適用される新しいコンテナー パッケージ形式です。 この新しい形式は、UWP の優れた機能を継承します。

* 堅牢なインストールおよび更新します。 
* 柔軟な機能のシステムとセキュリティ モデルを管理します。
* Microsoft Store、エンタープライズ管理、多くのカスタム配布モデルをサポートします。

これらのパッケージを作成するためのツールは、Visual Studio と Windows SDK の今後のリリースで利用可能になります。

MSIX パッケージ形式は、オープン ソース フォーマットされるため、パートナーがツールとソリューションを使って MSIX エコシステムをサポートするために簡単です。 MSIX パッケージ形式に関する詳細については、 [MSIX SDK](https://github.com/Microsoft/msix-packaging)を参照してください。 

![MSIX パッケージの画像](images/msix.png)

### <a name="optional-packages-with-executable-code"></a>実行可能コードによるオプション パッケージ

オプション パッケージ、アプリでは、実行可能ファイルの c# コードを含めることができますできるようになりました。 [Visual Studio を使って、メイン アプリ パッケージをサポートするために省略可能なアドオンのパッケージを構成する方法について説明します。](../packaging/optional-packages-with-executable-code.md)

### <a name="page-transitions"></a>ページ切り替え効果

[ページ切り替え](../design/motion/page-transitions.md)は、ユーザーがアプリ内のページ間を移動します。 ユーザーのナビゲーション階層にいるを理解し、ページ間の関係についてのフィードバックに役立ちます。

### <a name="project-rome"></a>Project Rome

Project Rome チームは、iOS と Android Sdk、ユーザー アクティビティなどの新機能を追加して、多くの異なる Sdk 全体で一貫性のあるプログラミング エクスペリエンスを提供するようにコードをリファクタリング見直さがします。 [すべての新しい API のリファレンスと使い方に関するドキュメント](https://docs.microsoft.com/windows/project-rome/)は稼働 Build 2018 開発者会議中にします。

### <a name="sets"></a>セット

Sets 機能は、Windows Insider preview ビルドで利用できます。 Sets 機能を使用する場合は、タイトル バーに専用のタブを持つ各アプリと他のアプリと共有される可能性があるウィンドウにアプリが描画されます。 [Sets の設計](../design/shell/design-for-sets.md)は、設定 UI で最適なエクスペリエンスを提供するアプリを最適化する方法に関するガイダンスがあります。

## <a name="developer-guidance"></a>開発者向けガイダンス

### <a name="get-started"></a>はじめに

当社 Get お revitalized した新しい学習トラックでコンテンツを開始します。 これらの新しいトピックをいくつかの一般的なタスクを実行するための情報が新しい Windows 10 開発者を提供するようにしてください。 チュートリアルが不明できなくてとハンドヘルドのチュートリアルが提供されないも代わりに、既存のドキュメントが存在してその使用方法を指摘します。 チェック アウト改良[コーディングの開始](../get-started/create-uwp-apps.md)ページで、または個々 の学習、各トラックについて説明します。

* [フォームの作成](../get-started/construct-form-learning-track.md)
* [一覧での顧客の表示](../get-started/display-customers-in-list-learning-track.md)
* [設定の保存と読み込み](../get-started/settings-learning-track.md)
* [ファイルの操作](../get-started/fileio-learning-track.md)

![開始イメージを取得します。](../get-started/images/build-your-app.png)

### <a name="advertising-performance-report"></a>広告パフォーマンス レポート

デベロッパー センター ダッシュ ボードで[の広告パフォーマンス レポート](../publish/advertising-performance-report.md)視認性のメトリックが追加されました。 また、広告の視認性の最適化に関する推奨事項を提供する[広告ユニットの視認性の最適化](../monetize/optimize-ad-unit-viewability.md)」の記事を追加しました。

### <a name="targeted-push-notifications"></a>ターゲット プッシュ通知

デベロッパー センター ダッシュ ボードの [[通知](../publish/send-push-notifications-to-your-apps-customers.md)] ページは、今すぐグラフと世界地図ビューで、すべての通知の他の分析データを提供します。

## <a name="videos"></a>ビデオ

### <a name="cwinrt"></a>C++/WinRT

C++/WinRT では、新しい方法の作成と Windows ランタイム Api を使用します。 ヘッダー ファイルに単独の実装は、最新のアプリの機能を最上位アクセス権を提供するために設計されています。 [ビデオ](https://www.youtube.com/watch?v=TLSul1XxppA&feature=youtu.be)をしくみ、し、[開発者ドキュメント](../cpp-and-winrt-apis/index.md)を詳しく説明します。

### <a name="multi-instance-uwp-apps"></a>マルチインスタンスの UWP アプリ

今すぐ Windows ではそれぞれ独自の別のプロセスで、UWP アプリの複数のインスタンスを実行することができます。 [ビデオ](https://www.youtube.com/watch?v=clnnf4cigd0&feature=youtu.be)を方法について、この機能をその[開発者ドキュメント](../launch-resume/multi-instance-uwp.md)をサポートしている新しいアプリを作成する方法と、この機能を使用する理由について説明します。

## <a name="samples"></a>サンプル

### <a name="customer-database-tutorial"></a>顧客データベース チュートリアル

このチュートリアルでは、顧客の一覧を管理するための基本的な UWP アプリを作成し、概念とエンタープライズ開発で便利なプラクティスを紹介します。 紹介の UI 要素を実装して、ローカルの SQLite データベースに対して操作を追加して、さらに移動する場合は、残りの部分のリモート データベースに接続するための緩やかなガイダンスを提供します。 [ここでは、チュートリアルを確認します。](../enterprise/customer-database-tutorial.md)