---
author: QuinnRadich
title: Windows 10 の開発者向け新着情報、ツール、機能
description: Windows 10 ビルド 17763 と新しい開発者ツールは、ツール、機能、およびユニバーサル Windows プラットフォームによって強化されたエクスペリエンスを提供します。
keywords: 新機能、新機能, 更新, 更新プログラム, 機能, 新規, Windows 10, 最新, 開発者, 17763
ms.author: quradic
ms.date: 10/02/2018
ms.topic: article
ms.prod: windows
ms.technology: uwp
ms.localizationpriority: medium
ms.openlocfilehash: c354d9ed4bae4cd8b484fcc3281dc5ac753dab1e
ms.sourcegitcommit: e6daa7ff878f2f0c7015aca9787e7f2730abcfbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/03/2018
ms.locfileid: "4312888"
---
# <a name="whats-new-in-windows-10-for-developers-build-17763"></a>ビルド 17763 の開発者向け新機能では、Windows 10 の新規作成

Windows 10 ビルド 17763 (年 2018年 10 月とも呼ばれます Update またはバージョン 1809)、Visual Studio 2017 および更新された SDK と組み合わせて、ツール、機能、およびさせる、優れたユニバーサル Windows プラットフォーム アプリのエクスペリエンスを提供します。 Windows 10 の[ツールと SDK をインストール](http://go.microsoft.com/fwlink/?LinkId=821431)すると、[新しいユニバーサル Windows アプリを作成](../get-started/create-uwp-apps.md)したり、[Windows の既存のアプリ コード](../porting/index.md)がどのように使えるかを試したりすることができます。

ここには、Windows 開発者にとって重要なこのリリースの新機能、強化された機能、ガイダンスを集めました。 Windows SDK に追加された新しい名前空間の完全な一覧は、 [Windows 10 ビルド 17763 API の変更](windows-10-build-17763-api-diff.md)を参照してください。 Windows 10 での注目すべき機能について詳しくは、「[Windows 10 の優れた機能](http://go.microsoft.com/fwlink/?LinkId=823181)」をご覧ください。 また、Windows プラットフォームに過去に追加された機能と今後追加される機能の概要については、[Windows 開発者向けプラットフォーム機能に関するページ](https://developer.microsoft.com/windows/platform/features)をご覧ください。

## <a name="design--ui"></a>設計および UI

機能 | 説明
 :------ | :------
アプリのアイコンとロゴ | [アプリのアイコンとロゴのページ](../design/style/app-icons-and-logos.md)書き換えられたとできるようになりました最新の Visual Studio のアイコンのツールを表示、Microsoft Store でアプリの登録情報へのイメージの追加の情報を提供します。
設計のランディング ページ | [設計のランディング ページを更新](https://developer.microsoft.com/windows/apps/design)するには、デザイン領域を UWP と Fluent Design を最新の追加機能に関する情報の概要の概要を説明があります。
Fluent Design を制御します。 | Fluent Design System と、アプリの apparence を強化するために、次の新しい UI コントロールが追加されました。 </br> * [CommandBarFlyout](../design/controls-and-patterns/command-bar-flyout.md)では、UI のキャンバス上の項目のコンテキストでユーザーの一般的なタスクを表示できます。 </br> * [DropDownButton](../design/controls-and-patterns/buttons.md#create-a-drop-down-button)、 [SplitButton](../design/controls-and-patterns/buttons.md#create-a-split-button)、および[ToggleSplitButton](../design/controls-and-patterns/buttons.md#create-a-toggle-split-button)は、アプリのユーザー インターフェイスを強化するために特殊な機能を備えたボタン コントロールを提供します。 </br> * [メニュー バー](../design/controls-and-patterns/menus.md)では、水平方向の行で複数の最上位のメニューのセットを示しています。 </br> * [NavigationView](../design/controls-and-patterns/navigationview.md)の場合、アプリがナビゲーション オプションの数を減らしてとコンテンツの多くのスペースを必要と上部のナビゲーションをサポートします。 </br> * [ツリー ビュー](../design/controls-and-patterns/tree-view.md)は、データ バインディングをサポート、項目テンプレート、ドラッグ アンド ドロップに拡張されています。
Fluent Design の更新 | 次の Fluent Design ページ visual の更新プログラムと小規模な変更が追加されました。 </br> * [パディング、余白の配置](../design/layout/alignment-margin-padding.md) </br> * [色](../design/style/color.md) </br> * [Windows アプリ用の fluent Design](../design/fluent-design-system/index.md) </br> * [アプリの設計の概要](../design/basics/design-and-ui-intro.md) </br> * [ナビゲーションの基本](../design/basics/navigation-basics.md) </br> * [レスポンシブ デザイン テクニック](../design/layout/responsive-design.md) </br> * [画面サイズとブレークポイント](../design/layout/screen-sizes-and-breakpoints-for-responsive-design.md) </br> * [スタイルの概要](../design/style/index.md) </br> * [記述スタイル](../design/style/writing-style.md) </br> さらに、まったく新しい情報がコンテンツ領域が次のページを書き換えるしたします。 </br> * [アイコン](../design/style/icons.md)は、アイコンを使用して、クリック可能なを行うのためのアドバイスを提供します。 </br> * [文字体裁](../design/style/typography.md)では、更新されたガイダンスと図を 1 つの場所に配置するすべてのものと同様の記事からの情報を統合します。
視線入力と操作 | [視線の操作](../design/input/gaze-interactions.md)をユーザーの視線、注意、および場所と、目の動きに基づくプレゼンスを追跡するアプリを許可します。 この機能は、支援技術として使用できる、ゲームや従来型入力デバイスが利用可能ないないその他の対話型シナリオの機会を提供します。
手書きの表示 | [HandwritingView](../design/controls-and-patterns/text-handwriting-view.md)では、新しいインク入力サーフェスの TextBox および RichEditBox です。 ユーザーは、書き込みサーフェスにコントロールを展開するペンでテキスト コントロールをタップします。 このガイドでは、管理し、アプリケーションで HandwritingView をカスタマイズする方法について説明します。
Fluent Design のモーション | タイミング、イージング、方向、および重力の基礎上に構築され、Fluent Design System のモーションの使用が進化しています。 これらの基礎を適用することは、アプリを使用してユーザーをガイドに役立ち、その接続とそのデジタル エクスペリエンスによって、自然界を反映します。 さらに、次の記事をご覧ください。 </br> * これらの基礎を反映するように[、モーションの概要](../design/motion/index.md)が更新されました。 </br> * [モーションの演習で](../design/motion/motion-in-practice.md)は、アプリ内でこれらの基礎を適用する方法の例を示します。 暗黙的なアニメーションは、XAML 要素のプロパティが変更された場合は、新旧の値の間で補間を簡単に許可するに関する情報も含まれています。 </br> * [方向性と重力](../design/motion/directionality-and-gravity.md)には、アプリのユーザーの概念的モデルが塗りつぶされます。 </br> * [タイミングとイージング](../design/motion/timing-and-easing.md)は、アプリでモーションにリアルさを追加します。 </br> * [XAML プロパティのアニメーション](../design/motion/xaml-property-animations.md)を使用すると、基になるコンポジションのビジュアルを操作することがなく直接 XAML 要素のプロパティをアニメーション化できます。
ページ切り替え効果 | [ページ切り替え](../design/motion/page-transitions.md)は、ユーザーがアプリ内のページ間を移動します。 ユーザーのナビゲーション階層にいるを理解し、ページ間の関係についてのフィードバックに役立ちます。
テキストのスケーリング | 新しい[テキスト スケーリング ガイダンス](../design/input/text-scaling.md)は、新しいテキスト スケーリング動作、ユーザーが OS と個々 のアプリケーションの両方の間での相対的なフォント サイズを変更する機能を提供する対応するために、アプリケーションを更新する方法について説明します。 拡大鏡アプリ (これ通常だけ、画面の領域内のすべてを拡大し、独自の操作性の問題が導入されています) を使って、ディスプレイの解像度を変更または DPI スケーリングのサイズを変更の表示と一般的な表示に基づくすべての証明書利用者のではなく距離)、ユーザーは、テキストだけで、100% (既定のサイズ) からの範囲のサイズを変更する設定にすばやくアクセスできる 225% です。
ツールキット | 新しい機能を備えた[Adobe XD、Adobe Illustrator ツールキット](../design/downloads/index.md)が更新されています。 これらの設計ツールキットは、UWP アプリを設計するためのコントロールとレイアウト テンプレートを提供します。
UI コマンド実行 | [UWP コマンド実行のインフラストラクチャ](../design/basics/commanding-basics.md)の更新プログラムは、コマンドのオブジェクト (動作、ラベル、アイコン、キーボード アクセラレータ、アクセス キー、および説明) の優れたカプセル化し、標準の切り取り、コピーなどの一般的なコマンドのセットを貼り付ける、終了など、。これにより、これらのプロパティを手動で設定する必要があります。 </br> 新しい[XamlUICommand](https://docs.microsoft.com/en-us/uwp/api/windows.ui.xaml.input.xamluicommand)クラスは、呼び出されたときにアクションを実行する対話型の UI 要素のコマンドの動作を deveining の基底クラスを提供します。 これは、 [StandardUICommand](https://docs.microsoft.com/en-us/uwp/api/windows.ui.xaml.input.standarduicommand)一連の定義済みプロパティを持つ標準的なプラットフォームのコマンドを公開するための親クラスです。 
Windows UI ライブラリ | [Windows UI のライブラリ](https://aka.ms/winui-docs)とは、UWP アプリのコントロールとその他のユーザー インターフェイス要素を提供する NuGet パッケージのセットです。 これらのパッケージは、ユーザーが最新の OS バージョンに存在しない場合でも、アプリが動作するように以前のバージョンの Windows 10 と互換性があります。 </br> Windows UI ライブラリの新機能について詳しくは、次を参照してください[この NuGet パッケージに含まれている API 名前空間の一覧。](https://docs.microsoft.com/uwp/api/overview/winui/) 。

## <a name="develop-windows-apps"></a>Windows アプリの開発

機能 | 説明
 :------ | :------
バーコード スキャナー | [バーコード スキャナー](https://docs.microsoft.com/windows/uwp/devices-sensors/pos-barcodescanner)のマニュアルは再編成、され、複数の詳細とコード スニペットを向上しています。 新しいトピックもが追加されました[取得バーコード データの理解と](https://docs.microsoft.com/windows/uwp/devices-sensors/pos-barcodescanner-scan-data)を取得し、バーコード スキャナーのデータを処理する方法について説明します。
C++/WinRT | [、C++/WinRT](https://aka.ms/cppwinrt)このリリースの新機能が含まれています。 たとえば、新しい関数とが独自の[コレクションのプロパティとコレクション型](/windows/uwp/cpp-and-winrt-apis/collections)の実装をサポートする基底クラス。 </br> C++ で[{Binding}](/windows/uwp/xaml-platform/binding-markup-extension)マークアップ拡張機能を使用できるようになりました/WinRT ランタイム クラスです。 詳しくとコード例では、[データ バインディングの概要](/windows/uwp/data-binding/data-binding-quickstart)をご覧ください。 </br> 他の新しい C + + WinRT コンテンツが含まれています。 [XAML カスタム (テンプレート化) コントロール](/windows/uwp/cpp-and-winrt-apis/xaml-cust-ctrl)です。[Author COM コンポーネント](/windows/uwp/cpp-and-winrt-apis/author-coclasses)です。ファイルと[値のカテゴリを参照](/windows/uwp/cpp-and-winrt-apis/cpp-value-categories)します。
C++/WinRT のコード例 | 250 C + が追加されました/付随既存 C + 当社のドキュメントのトピックを WinRT コードの一覧/CX コード例を紹介します。
ガイダンスの貢献に関するページ | [貢献ガイダンス](https://github.com/MicrosoftDocs/windows-uwp/blob/docs/CONTRIBUTING.md)UWP のドキュメントの更新されました。 この新しいガイダンス明確にワークフローと、ドキュメントを外部の貢献度を期待します。
DirectX グラフィックスのインフラストラクチャー (DXGI) | 不足している DXGI Api、用の新しいドキュメントが追加されているし、Windows 10 を提示するときのベスト プラクティスに関する記事を提供してきました。 </br> * [最適なパフォーマンスを得るため、DXGI フリップ モデルを使用して](https://docs.microsoft.com/windows/desktop/direct3ddxgi/for-best-performance--use-dxgi-flip-model): パフォーマンスと最新バージョンの Windows でのプレゼンテーション スタック内の効率を最大化する方法について説明します。 </br> * [IDXGIOutput6::CheckHardwareCompositionSupport メソッド](https://docs.microsoft.com/windows/desktop/api/dxgi1_6/nf-dxgi1_6-idxgioutput6-checkhardwarecompositionsupport): ハードウェア ストレッチがサポートされていることをアプリケーションに通知します。 </br> * [DXGI_HARDWARE_COMPOSITION_SUPPORT_FLAGS 列挙](https://docs.microsoft.com/windows/desktop/api/dxgi1_6/ne-dxgi1_6-dxgi_hardware_composition_support_flags): サポートされているレベルのハードウェア構成について説明します。
はじめに | [概要](../get-started/index.md)コンテンツは、開発者は新しい Windows 10 が、次の一般的なタスクに実現方法で情報とガイダンスを提供する新しいトピックと revitalized されました。 </br> * [フォームを作成します。](../get-started/construct-form-learning-track.md) </br> * [リスト内の顧客の表示](../get-started/display-customers-in-list-learning-track.md) </br> * [保存し、読み込みの設定](../get-started/settings-learning-track.md) </br> * [ファイルを操作します。](../get-started/fileio-learning-track.md)
マップ スタイル シート エディター | 対話的にアプリケーションを追加する地図の外観をカスタマイズするのにには、新しい[マップ スタイル シート エディター](https://www.microsoft.com/p/map-style-sheet-editor/9nbhtcjt72ft?rtc=1#activetab=pivot:overviewtab)アプリケーションを使用します。
Microsoft について説明します | 新しい[Microsoft Learn サイト](https://www.microsoft.com/learning/default.aspx)は、Microsoft の開発者に新しい実践的な学習とトレーニングの機会を提供します。 現時点では、Microsoft Learn トレーニングと Microsoft 365、Microsoft Azure、Office 365、および Windows Server の認定を提供します。
メモ帳 | [メモ帳が更新されて](http://aka.ms/ant-man)、ズームの追加、検索/置換、折り返しおよび Unix/Linux (LF) と Mac (変更リクエスト) 行の末尾のサポート
Project Rome | ようになりました["rome"プロジェクト](https://docs.microsoft.com/windows/project-rome/)はサポートされているプラットフォームと Sdk の間で一貫性のあるプログラミング エクスペリエンスを提供します。 </br>  新しい[Microsoft Graph の通知](https://developer.microsoft.com/graph/docs/concepts/notifications-concept-overview)では、"rome"プロジェクトを使用して、アプリのユーザーを中心とした、クロス プラットフォームの通知プラットフォームを提供します。
画面 snipping | 新しい[URI スキーム](../launch-resume/launch-screen-snipping.md)では、アプリをプログラムで新しいの切り取り領域を開くか、注釈の特定のイメージの切り取り領域とスケッチ アプリを起動します。
デスクトップ アプリケーションで UWP コントロール | ここで、Windows 10 では、WPF、Windows フォーム、および C++ Win32 デスクトップ アプリケーションで UWP コントロールを使用できます。 つまり、外観や操作感を既存のデスクトップ アプリケーション、最新の Windows 10 の UI 機能のみで利用可能な Windows Ink と Fluent Design System をサポートするコントロールなどの UWP コントロールの機能を強化することができます。 この機能は、 *XAML 諸島*と呼ばれます。 </br> 使用しているアプリケーション プラットフォームに応じて、アプリケーションで XAML 諸島を使用する方法をいくつか用意されています。 WPF および Windows フォーム アプリケーションでは、一連のデザイナー指向の開発エクスペリエンスを提供する[Windows コミュニティ ツールキット](https://docs.microsoft.com/windows/uwpcommunitytoolkit/)でコントロールを使用できます。 C++ Win32 アプリケーションでは、 [Windows.UI.Xaml.Hosting](https://docs.microsoft.com/uwp/api/windows.ui.xaml.hosting)名前空間の*API をホストしている UWP XAML*を使う必要があります。 詳細については、[デスクトップ アプリケーションで UWP コントロール](../xaml-platform/xaml-host-controls.md)を参照してください。 </br> **注:** Api と XAML 諸島を有効にするコントロールは開発者プレビューとして現在利用可能です。 それらプロトタイプ コードで今すぐ試すをお勧めしますがないことで使う運用コードこの時点でお勧めしますしないでください。
Windows Machine Learning | [Windows Machine Learning](https://docs.microsoft.com/windows/ai/)ができるようになりました正式に起動、最先端の機械学習モデルの評価を高速化のサポートなどの機能を提供することです。 アプリケーションに統合する必要がある開発者をサポートするためにいくつかの新規および更新されたリソースを新しいドキュメント サイトを作成します。 </br> * [チュートリアル: Windows Machine Learning のデスクトップ アプリケーション (C++) 作成](https://docs.microsoft.com/windows/ai/get-started-desktop): このチュートリアルでは、デスクトップ用のシンプルな Windows ML アプリケーションを構築する方法を示しています。 </br> * [チュートリアル: Windows Machine Learning UWP アプリケーション (c#) 作成](https://docs.microsoft.com/windows/ai/get-started-uwp): このステップ バイ ステップ チュートリアルでは、Windows ML を使って、初めての UWP アプリケーションを作成します。 </br> * [Windows.AI.MachineLearning Namespace](https://docs.microsoft.com/uwp/api/windows.ai.machinelearning): Windows 10 SDK の最新リリースのための API リファレンスは更新されており、開発者は Win32 および UWP アプリケーションのこの API を使用できるようになりました。
Windows Mixed Reality | 開発者は、ハードウェアで保護された要求バックバッファー テクスチャ ディスプレイのハードウェアでサポートされている場合は、ここで PlayReady などのソースからのハードウェアで保護されたコンテンツを使用するアプリケーションを許可することができます。 ハードウェア保護のサポートと設定は、 [Windows.Graphics.Holographic.HolographicCamera](https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographiccamera)の新しいプロパティを使用してプライマリ レイヤーおよびクワッド レイヤー[経由で利用できます。Windows.Graphics.Holographic.HolographicQuadLayerUpdateParameters](https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicquadlayerupdateparameters)します。

## <a name="iot-core"></a>IoT Core

機能 |説明:--|:---[AssignedAccessSettings |[[AssignedAccessSettings クラス](https://docs.microsoft.com/uwp/api/windows.system.userprofile.assignedaccesssettings)により、さまざまなメソッドの呼び出しと、ユーザーにアクセスするプロパティには、特定のデバイスのアクセスの設定が割り当てられています。
既定のアプリの概要 |[Windows 10 IoT Core 既定のアプリ](https://docs.microsoft.com/windows/iot-core/develop-your-app/iotcoredefaultapp)は、新機能や天気予報、手描き入力などの機能と更新されたとオーディオされました。
ダッシュ ボード |[Windows 10 Iot Core のダッシュ ボード](https://docs.microsoft.com/windows/iot-core/tutorials/quickstarter/devicesetup)には、自社のデバイスにカスタム FFUs をフラッシュする Dragonboard 410 C または NXP を使用する開発者で使用できます。
スクリーン キーボード |デスクトップ エディションの Windows として同じタッチ キーボードのコンポーネントを使用できるようになりました[IoT デバイスのスクリーン キーボード](https://docs.microsoft.com/windows/iot-core/develop-your-app/onscreenkeyboard)します。 これにより、ディクテーション モード、IME サポート、および入力スコープの完全なセットなどの機能です。
タイトル バーにサインイン ダイアログの |Windows 10 IoT Core[システム ダイアログ ボックスのタイトル バー](https://docs.microsoft.com/windows/iot-core/develop-your-app/signindialogtitlebars)を構成するオプションが追加されました。
タッチでスリープ解除 |[タッチでスリープ解除](https://docs.microsoft.com/windows/iot-core/learn-about-hardware/wakeontouch)により、デバイスの画面を簡単に有効にするユーザーの画面に触れたとき中の使用中でないときにオフにできます。 Windows.System.Update |新しい[Windows.System.Update 名前空間](https://docs.microsoft.com/uwp/api/windows.system.update)は、システムの更新プログラムの対話型のコントロールを使用できます。 この名前空間は、Windows 10 IoT Core のみです。

## <a name="web-development"></a>Web 開発

機能 |説明:--|:---EdgeHTML 18 |Windows 10 年 2018年 10 月は、 [EdgeHTML 18](https://docs.microsoft.com/microsoft-edge/dev-guide)、Microsoft Edge ブラウザーと UWP アプリ用の JavaScript エンジンに最新の更新プログラムでの船舶を更新します。 EdgeHTML 18 では、Web 認証 API、WebView コントロールの新機能、最先端と展開のサポートが表示されます。 ツールの側では、EdgeHTML 18 は、Edge DevTools と Edge DevTools プロトコルに WebDriver の新機能と自動更新、および拡張機能をもたらします。 すべての詳細について[EdgeHTML 18 の新機能では](https://docs.microsoft.com/microsoft-edge/dev-guide)[最新の Windows 10 で DevTools (EdgeHTML 18) の更新](https://docs.microsoft.com/microsoft-edge/devtools-guide/whats-new)を確認します。
プログレッシブ Web アプリ |Pwa は、Windows 用に開発かどうか。 次のガイドを確認します。 </br> * [単純な web アプリを PWA としてビルドします。](https://docs.microsoft.com/microsoft-edge/progressive-web-apps/get-started) </br> * [Windows ランタイムを使った、PWA を強化します。](https://docs.microsoft.com/en-us/microsoft-edge/progressive-web-apps/windows-features) </br> * [Microsoft ストアに、PWA の公開](https://docs.microsoft.com/microsoft-edge/progressive-web-apps/microsoft-store)API の拡張機能を web |Mozilla Developer Network ドキュメントにブラウザー間の web 開発は、[従来の Microsoft API 拡張機能](https://developer.mozilla.org/docs/Web/API/Microsoft_API_extensions)の一覧が追加されました。 これらの API の拡張機能は、Internet Explorer または Microsoft Edge に固有のもの MDN web ドキュメントの互換性とブラウザーのサポートに関する既存の情報を補足します。従来の Microsoft [CSS 拡張機能](https://developer.mozilla.org/docs/Web/CSS/Microsoft_Extensions)と[JavaScript の拡張機能](https://developer.mozilla.org/docs/Web/JavaScript/Microsoft_JavaScript_extensions)は、利用可能なもとリッチ web MDN から API の情報を直接表面化を見つけることができます[Visual Studio Code](https://code.visualstudio.com/updates/v1_25#_new-css-pseudo-selectors-and-pseudo-elements-from-mdn) 。
WebVR |主要な更新プログラムには、 [WebVR 開発者向けガイド](https://docs.microsoft.com/microsoft-edge/webvr/)、完全に再設計ホーム ページと内容のテーブルの再編成を含むなりました。 など、いくつかの新しいトピックも書き込んだ。 </br> * [WebVR は何ですか。](https://docs.microsoft.com/microsoft-edge/webvr/what-is-webvr) WebVR、それを使用する理由と、用の開発を開始する方法について説明します。 </br> * [プログレッシブ Web アプリで WebVR](https://docs.microsoft.com/microsoft-edge/webvr/webvr-in-pwas): WebVR をプログレッシブ Web アプリ (PWA) を追加する方法について説明します。 </br> * [WebView で WebVR](https://docs.microsoft.com/microsoft-edge/webvr/webvr-in-webview): Windows 10 アプリケーションの WebView コントロールに WebVR を追加する方法について説明します。 </br> * [WebVR デモ](https://docs.microsoft.com/microsoft-edge/webvr/demos): Microsoft Edge と Windows Mixed Reality イマーシブ ヘッドセットを使用していくつかの WebVR デモを確認します。

## <a name="publish--monetize-windows-apps"></a>Windows アプリを公開および収益化する

機能 | 説明
 :------ | :------
MSIX | [MSIX](https://docs.microsoft.com/windows/msix/overview)は、すべての Windows アプリを最新のパッケージ化エクスペリエンスを提供する新しい Windows アプリ パッケージ形式です。 オープン ソースの MSIX 形式には、最新の展開機能を有効にするときに、既存のパッケージの機能が保持されます。
MSIX パッケージ作成ツール | 新しい[MSIX パッケージ作成ツール](https://docs.microsoft.com/windows/msix/mpt-overview)) で、ソース コードにアクセスできない場合でも、MSIX 形式で、既存のデスクトップ アプリケーションを再パッケージ化することができます。 これは、コマンドライン、またはその対話型の UI を使って実行できます。
MSIX のデスクトップ アプリのコンバーターのサポート | 使用して、MSIX パッケージを出力する[Desktop App Converter](https://docs.microsoft.com/windows/uwp/porting/desktop-to-uwp-root)を使用する、`-MakeMSIX`パラメーター。
MSIX の MakeAppx.exe ツールのサポート | MakeAppx.exe ツールを使用して、UWP アプリまたは従来のデスクトップ アプリケーションの MSIX パッケージを作成することができます。 このツールは、Windows 10 SDK に含まれており、コマンド プロンプトまたはスクリプト ファイルから使用できます。 </br> UWP アプリでは、 [MakeAppx.exe ツールを使ったアプリ パッケージの作成](https://docs.microsoft.com/windows/uwp/packaging/create-app-package-with-makeappx-tool)を参照してください。 </br> デスクトップ アプリケーションは、[デスクトップ アプリケーションを手動でパッケージ](https://docs.microsoft.com/windows/uwp/porting/desktop-to-uwp-manual-conversion)を参照してください。
パッケージのサポート フレームワーク | [パッケージのサポートのフレームワーク](https://docs.microsoft.com/windows/msix/package-support-framework-overview)では、修正プログラムの適用、既存のデスクトップ アプリケーションをソース コードにアクセスしていないとき MSIX コンテナーで実行できるようにするために役立つオープン ソースのキットです。
Store 分析 API | [Microsoft Store 分析 API](../monetize/access-analytics-data-using-windows-store-services.md)には、次の新しいメソッドができるようになりましたが含まれます。 </br> * [UWP アプリのインサイト データを取得します。](../monetize/get-insights-data-for-your-app.md) </br> * [デスクトップ アプリケーションのインサイト データを取得します。](../monetize/get-insights-data-for-your-desktop-app.md) </br>* [デスクトップ アプリケーションのアップグレード ブロックを取得します。](../monetize/get-desktop-block-data.md) </br> * [デスクトップ アプリケーションのアップグレード ブロックに関する詳細を取得します。](../monetize/get-desktop-block-data-details.md)

## <a name="videos"></a>ビデオ

Fall Creators Update 以降、以下のビデオが公開されました。Windows 10 の開発者向け新機能および強化された機能が紹介されています。

### <a name="cwinrt"></a>C++/WinRT

C++/WinRT では、新しい方法の作成と Windows ランタイム Api を使用します。 ヘッダー ファイルに単独の実装は、最新のアプリの機能を最上位アクセス権を提供するために設計されています。 [ビデオ](https://www.youtube.com/watch?v=TLSul1XxppA&feature=youtu.be)をしくみ、し、[開発者ドキュメント](../cpp-and-winrt-apis/index.md)を詳しく説明します。

### <a name="get-started-for-devs-create-and-customize-a-form-on-windows-10"></a>開発者向けの概要: を作成し、Windows 10 でのフォームをカスタマイズします。

Windows 開発者向け[ドキュメントの概要](../get-started/index.md)、基本的なアプリの開発タスクの実践的なエクスペリエンスを提供します。 このビデオでは、これらのトピックでは、いずれかを紹介してで、アプリでのフォームの UI の作成の基本について説明します。 [ビデオをご覧ください](https://www.youtube.com/watch?v=AgngKzq4hKI&feature=youtu.be)アクションを次のコードを確認する[」のトピックを確認します](http://aka.ms/CreateForms)。

### <a name="enhance-your-bot-with-project-personality-chat"></a>プロジェクトの個性チャットと、ボットを強化します。

プロジェクトの特徴チャットでは、チャット ボットにカスタマイズ可能なペルソナを追加できます。 Microsoft ボット Framework SDK との統合、顧客との対話をより親近感を与えるための方法の小さな話しかける機能を追加できます。 [ビデオ](https://www.youtube.com/watch?v=5C_uD8g2QKg&feature=youtu.be)をし、それには、実践的なエクスペリエンスの[対話型デモを試す](http://aka.ms/PersonalityChat)を実装する方法について説明します。

### <a name="multi-instance-uwp-apps"></a>マルチインスタンスの UWP アプリ

今すぐ Windows ではそれぞれ独自の別のプロセスで、UWP アプリの複数のインスタンスを実行することができます。 [ビデオ](https://www.youtube.com/watch?v=clnnf4cigd0&feature=youtu.be)を方法について、この機能をその[開発者ドキュメント](../launch-resume/multi-instance-uwp.md)をサポートしている新しいアプリを作成する方法と、この機能を使用する理由について説明します。

### <a name="xbox-live-unity-plugin"></a>Xbox Live Unity プラグイン

Unity の Xbox Live プラグインには、Xbox Live への署名、統計情報、フレンド リスト、クラウド ストレージ、およびランキングをタイトルに追加するためのサポートが含まれています。 について[は、ビデオ](https://youtu.be/fVQZ-YgwNpY)をし、 [GitHub パッケージをダウンロード](https://aka.ms/UnityPlugin)を開始します。

### <a name="one-dev-question"></a>1 つのデベロッパー質問

デベロッパー質問の 1 つのビデオ シリーズの長い Microsoft 開発者は一連の Windows の開発、チームのカルチャと履歴に関する質問について説明します。

* [Windows の開発と履歴に関する Raymond Chen](https://www.youtube.com/playlist?list=PLWs4_NfqMtoxjy3LrIdf2oamq1coolpZ7)

* [Windows の開発と履歴に関する Larry Osterman](https://www.youtube.com/playlist?list=PLWs4_NfqMtoyPUkYGpJU0RzvY6PBSEA4K)

* [プログレッシブ Web アプリで Aaron グスタフソン](https://www.youtube.com/playlist?list=PLWs4_NfqMtoyPHoI-CIB71mEq-om6m35I)

* [Chris Heilmann webhint ツール](https://www.youtube.com/playlist?list=PLWs4_NfqMtow00LM-vgyECAlMDxx84Q2v)

## <a name="samples"></a>サンプル

### <a name="customer-orders-database"></a>顧客注文データベース

[顧客注文データベースのサンプル](https://github.com/Microsoft/Windows-appsample-customers-orders-database)[データ グリッド](https://docs.microsoft.com/windows/communitytoolkit/controls/datagrid)、 [NavigationView](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.navigationview)、[拡張](https://docs.microsoft.com/windows/communitytoolkit/controls/expander)などの新しいコントロールを使用して更新されました。

### <a name="customer-database-tutorial"></a>顧客データベース チュートリアル

[顧客データベース チュートリアル](../enterprise/customer-database-tutorial.md)では、顧客の一覧を管理するための基本的な UWP アプリを作成し、概念とエンタープライズ開発で便利なプラクティスを紹介します。 紹介の UI 要素を実装して、ローカルの SQLite データベースに対して操作を追加して、さらに移動する場合は、残りの部分のリモート データベースに接続するための緩やかなガイダンスを提供します。

### <a name="photo-editor-cwinrt"></a>フォト エディター、C++/WinRT

[フォト エディター サンプル アプリ](https://github.com/Microsoft/Windows-appsample-photo-editor)の開発の紹介、 [、C++/WinRT](../cpp-and-winrt-apis/intro-to-using-cpp-with-winrt.md)言語プロジェクションです。 アプリでは、**画像**ライブラリから写真を取得し、関連する写真効果で選択のイメージを編集することができます。

### <a name="windows-machine-learning"></a>Windows Machine Learning

[Windows の機械学習](https://github.com/Microsoft/Windows-Machine-Learning)リポジトリでは、最新の Windows 10 SDK を使用する更新されており、c#、C++、および JavaScript で記述されたサンプルが含まれています。

### <a name="xaml-hosting-api"></a>XAML をホストしている API

[XAML をホストしている API のサンプル](https://github.com/Microsoft/Windows-appsample-Xaml-Hosting)では、API (XAML 諸島とも呼ばれます) をホストしている UWP XAML を使用して、さまざまなシナリオを強調表示する Win32 デスクトップ アプリです。 プロジェクトには、ギャラリー スタイルのプレゼンテーションの Windows Ink、メディア プレーヤー、ナビゲーション ビュー コントロールが組み込まれています。 一般の外側では、使用量を制御するサンプルもで XAML とネイティブ Windows イベント/メッセージ、および基本的な XAML データ バインディングを処理します。