---
author: stevewhims
description: このトピックにある現象のトラブルシューティングおよび対処法に関する表は、新しいコードを作成しているか既存のアプリを移植しているかにはかかわらず役立つ可能性があります。
title: C++/WinRT に関する問題のトラブルシューティング
ms.author: stwhi
ms.date: 04/10/2018
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: Windows 10、uwp、標準、c++、cpp、winrt、プロジェクション、トラブルシューティング、HRESULT、エラー
ms.localizationpriority: medium
ms.openlocfilehash: 21f5fc4773979b2d7940b85871264e27d56d29c4
ms.sourcegitcommit: ab92c3e0dd294a36e7f65cf82522ec621699db87
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
ms.locfileid: "1832266"
---
# <a name="troubleshooting-cwinrtwindowsuwpcpp-and-winrt-apisintro-to-using-cpp-with-winrt-issues"></a>[C++/WinRT](/windows/uwp/cpp-and-winrt-apis/intro-to-using-cpp-with-winrt) に関する問題のトラブルシューティング
> [!NOTE]
> **一部の情報はリリース前の製品に関する事項であり、正式版がリリースされるまでに大幅に変更される可能性があります。 本書に記載された情報について、Microsoft は明示または黙示を問わずいかなる保証をするものでもありません。**

> [!NOTE]
> 現在利用可能な C++/WinRT Visual Studio Extension (VSIX) (プロジェクト テンプレート サポートおよび C++/WinRT MSBuild プロパティとターゲットを提供) の詳細については、「[C++/WinRT の Visual Studio サポートと VSIX](intro-to-using-cpp-with-winrt.md#visual-studio-support-for-cwinrt-and-the-vsix)」を参照してください。

このトピックは、すぐに認識していただくための先行情報です。まだ必要としていない場合も同様です。 以下の症状のトラブルシューティングおよび対処法に関する表は、新しいコードを作成しているか既存のアプリを移植しているかにはかかわらず役立つ可能性があります。 移植中であり、進展させてプロジェクトのビルドおよび実行の段階に達することを急いでいる場合は、問題を引き起こしている重要でないコードにコメントアウトまたはスタブ挿入を適用して、一時的に進展させることができます。その後、元に戻ってその借りを解消することになります。

## <a name="tracking-down-xaml-issues"></a>XAML に関する問題の検出
XAML 解析例外は診断が難しい場合があります。特に、わかりやすいエラー メッセージが例外に含まれていない場合は、診断が難しくなります。 デバッガーが初回例外をキャッチするように構成されていることを確してください (早い段階で解析例外のキャッチを試行するため)。 デバッガーで例外変数を調べて、HRESULT やメッセージ内に役立つ情報が含まれているかどうかを確認できます。 また、XAML パーサーを使って、Visual Studio の出力ウィンドウを調べ、エラー メッセージの出力を確認することもできます。

アプリが終了し、XAML マークアップの解析中に処理不能な例外がスローされたことのみがわかっている場合、存在しないリソースへの (キーによる) 参照の結果である可能性があります。 または、UserControl、カスタム コントロール、カスタム レイアウト パネルの内部で例外がスローされたことも考えられます。 最終手段として、バイナリ分割を使うことができます。 XAML ページからマークアップのおよそ半分を削除し、アプリを再実行します。 これによって、エラーが削除した半分で発生しているか (いずれの場合でも、削除した部分はここで元に戻す必要があります)、または削除しなかった半分で発生しているかがわかります。 問題が特定されるまで、エラーを含む半分をさらに分割するプロセスを繰り返します。

## <a name="symptoms-and-remedies"></a>現象と対処法
| 現象 | 対処法 |
|---------|--------|
| 実行時に REGDB_E_CLASSNOTREGISTERED の HRESULT 値で例外がスローされます。 | このエラーの原因の 1 つは、Windows ランタイム コンポーネントを読み込むことができないことです。 コンポーネントの Windows ランタイム メタデータ ファイル (`.winmd`) の名前がコンポーネント バイナリ (`.dll`) の名前と同じであることを確認してください。この名前は、プロジェクトの名前、およびルート名前空間の名前でもあります。 また、Windows ランタイム メタデータとバイナリが、ビルド プロセスによって使用中のアプリの `Appx` フォルダに正しくコピーされていることを確認してください。 さらに、使用中のアプリの `AppxManifest.xml` (および `Appx` フォルダ内) に、アクティブ化可能なクラスとバイナリ名を正しく宣言している **&lt;InProcessServer&gt;** 要素が含まれていることを確認してください。 このエラーは、ローカルに実装されたランタイム クラスが、プロジェクションされた型の既定のコンストラクターによって誤ってインスタンス化された場合にも発生する可能性があります。 その場合にプロジェクションされた型を正しく使用する方法の詳細については、「[XAML コントロール、C++/WinRT プロパティへのバインド](binding-property.md)」を参照してください。 |
| C++ コンパイラーは、"*'implements_type': は、'&lt;プロジェクションされた型&gt;'* の直接的または間接的な基底クラスのメンバーではありません" というエラーを生成します。 | これは、実装型 (たとえば **MyRuntimeClass**) の未修飾名前空間名を使用して、その型のヘッダーを含めずに **make** を呼び出すと発生する可能性があります。 コンパイラーは、**MyRuntimeClass** をプロジェクションされた型として解釈します。 解決策は、実装型のヘッダーを含めることです (たとえば `MyRuntimeClass.h`)。 |
| C++ コンパイラーが、"*削除された関数を参照しようとしています*" というエラーを生成します。 | これは、**make** を呼び出し、テンプレート パラメーターとして渡す実装型の既定のコンストラクターが `= delete` である場合に発生する可能性があります。 実装型のヘッダー ファイルを編集し、`= delete` を `= default` に変更してください。 ランタイム クラスの IDL にコンストラクターを追加することもできます。 |
| [**INotifyPropertyChanged**](/uwp/api/windows.ui.xaml.data.inotifypropertychanged) を実装しましたが、XAML バインドが更新されません (そのため、UI が [**PropertyChanged**](/uwp/api/windows.ui.xaml.data.inotifypropertychanged.PropertyChanged) にサブスクライブしません)。 | XAML マークアップのバインド式で必ず `Mode=OneWay` (または TwoWay) を設定してください。 「[XAML コントロール: C++/WinRT プロパティへのバインド](binding-property.md)」を参照してください。 |
| XAML アイテム コントロールを監視可能なコレクションにバインドしていますが、実行時に "パラメーターが正しくありません" というメッセージで例外がスローされます。 | IDL および実装で、監視可能なコレクションを型 **Windows.Foundation.Collections.IVector<IInspectable>** として宣言します。 ただし、**Windows.Foundation.Collections.IObservableVector<T>** を実装するオブジェクトを返します。T は要素型です。 「[XAML アイテム コントロール: C++/WinRT コレクションへのバインド](binding-collection.md)」を参照してください。  |
| C++ コンパイラーが、"*'MyImplementationType_base&lt;MyImplementationType&gt;': 使用可能な適切な既定コンストラクターがありません*" という形式のエラーを生成します。|これは、非自明なコンストラクターを持つ型から派生させた場合に発生する可能性があります。 派生型のコンストラクターは、基本型のコンストラクターが必要とするパラメーターを渡す必要があります。 実証済みの例については、「[非自明なコンストラクタを持つ型からの派生](author-apis.md#deriving-from-a-type-that-has-a-non-trivial-constructor)」を参照してください。|
| C++ コンパイラーが、"*'const std::vector&lt;std::wstring,std::allocator&lt;_Ty&gt;&gt;' から 'const winrt::param::async_iterable&lt;winrt::hstring&gt; &'* に変換できません" というエラーを生成します。|これは、コレクションを予期している Windows ランタイム API に std::wstring の std::vector を渡すときに発生する可能性があります。 詳細については、「[標準的な C++ のデータ型と C++/WinRT](std-cpp-data-types.md)」を参照してください。|
| C++ コンパイラーが、"*'const std::vector&lt;winrt::hstring,std::allocator&lt;_Ty&gt;&gt;' から 'const winrt::param::async_iterable&lt;winrt::hstring&gt; &'* に変換できません" というエラーを生成します。|これは、コレクションを予期している非同期 Windows ランタイム API に winrt::hstring の std::vector を渡すときに、非同期呼び出し先へのベクトルのコピーも移動も行っていない場合に発生する可能性があります。 詳細については、「[標準的な C++ のデータ型と C++/WinRT](std-cpp-data-types.md)」を参照してください。|
| プロジェクトを開くときに、Visual Studio が "*プロジェクトのアプリケーションはインストールされていません*" というエラーを生成します。|まだ行っていない場合は、Visual Studio の **[新しいプロジェクト]** ダイアログから **C++ での開発用の Windows ユニバーサル ツール**をインストールする必要があります。 それでも問題が解決しない場合は、プロジェクトが C++/WinRT Visual Studio Extension (VSIX) に依存している可能性があります (「[C++/WinRT の Visual Studio サポートと VSIX](intro-to-using-cpp-with-winrt.md#visual-studio-support-for-cwinrt-and-the-vsix)」を参照)。|
| Windows アプリ認定キットのテストが、ランタイム クラスの 1 つについて、"*Windows 基底クラスから派生しません。すべての構成可能クラスは最終的に、Windows 名前空間内の型から派生する必要があります*" というエラーを生成します。|*アプリケーション内で宣言されている*各ランタイム クラスの最終的な基底クラスは、Windows.* 名前空間からの型である必要があります。 [**Windows.UI.Xaml.DependencyObject**](/uwp/api/windows.ui.xaml.dependencyobject) からビュー モデルを派生させることができます。 または、**DependencyObject** から派生したバインド可能な基底クラスを宣言し、それからビュー モデルを派生します。|
| C++ コンパイラーが、EventHandler または TypedEventHandler のデリゲート特殊化に関して "*WinRT 型である必要があります*" というエラーを生成します。|代わりに **winrt::delegate&lt;...T&gt;** を使用することを考慮してください。 「[C++/WinRT でのイベントの作成](author-events.md)」を参照してください。|
| C++ コンパイラーが、Windows ランタイムの非同期操作の特殊化に関して "*WinRT 型である必要があります*" というエラーを生成します。|代わりに並列パターン ライブラリ (PPL) の [**task**](https://msdn.microsoft.com/library/hh750113) を返すことを考慮してください。 「[同時実行操作と非同期操作](concurrency.md)」を参照してください。|
| C++ コンパイラーが、"*エラー C2220: 警告がエラーとして扱われました - 'オブジェクト' ファイルは生成されませんでした*" を生成します。|警告を解決するか、または **[C/C++]** > **[全般]** > **[警告をエラーとして扱う]** を **[いいえ (/WX-)]** に設定します。|
| オブジェクトが破棄された後で C++/WinRT オブジェクトのイベント ハンドラーが呼び出されるため、アプリがクラッシュします。|「[イベント ハンドラーでの *this* オブジェクトの使用](handle-events.md#using-the-this-object-in-an-event-handler)」を参照してください。|
| C++ コンパイラーが "*エラー C2338: これは弱参照サポート専用です*" を生成します。|**テンプレート引数として winrt::no_weak_ref** マーカー構造体を基底クラスに渡した型の、弱参照を要求しています。 「[弱参照サポートの除外](weak-references.md#opting-out-of-weak-reference-support)」を参照してください。|
| C++ リンカーが、C++/WinRT プロジェクションの Windows 名前空間ヘッダーに関して "*エラー LNK2019: 外部シンボルは未解決です*" を生成します (winrt 名前空間内)。|API は含まれているヘッダー内で事前宣言されていますが、その定義は含まれていないヘッダー内にあります。 API の名前空間で付けられた名前のヘッダーを含めてから、リビルドしてください。|