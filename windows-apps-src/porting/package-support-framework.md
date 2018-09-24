---
author: normesta
Description: Fix issues that prevent your desktop application from running in an MSIX container
Search.Product: eADQiWindows 10XVcnh
title: デスクトップ アプリケーションから MSIX コンテナーで実行されるように問題を修正します。
ms.author: normesta
ms.date: 07/02/2018
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: Windows 10, UWP
ms.localizationpriority: medium
ms.openlocfilehash: 7e5119696498156d36ec63b16b1d76c00b03f4df
ms.sourcegitcommit: a160b91a554f8352de963d9fa37f7df89f8a0e23
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/21/2018
ms.locfileid: "4128387"
---
# <a name="apply-runtime-fixes-to-an-msix-package-by-using-the-package-support-framework"></a>パッケージのサポートのフレームワークを使用して MSIX パッケージにランタイムの修正プログラムを適用します。

パッケージのサポート フレームワークでは、修正プログラムの適用、既存の win32 アプリケーションをソース コードにアクセスしていないとき MSIX コンテナーで実行できるようにするために役立つオープン ソースのキットです。 パッケージのサポートのフレームワークには、最新のランタイム環境のベスト プラクティスに従って、アプリケーションが役立ちます。

詳細についてはを[パッケージのサポートのフレームワーク](https://docs.microsoft.com/windows/msix/package-support-framework-overview)を参照してください。

このガイドを支援するアプリケーションの互換性の問題を特定して、それらに対処する修正プログラムを検索し、適用され、ランタイムを拡張します。

<a id="identify" />

## <a name="identify-packaged-application-compatibility-issues"></a>パッケージ化されたアプリケーションの互換性の問題を特定します。

最初に、アプリケーションのパッケージを作成します。 次に、インストール、実行し、その動作を確認します。 互換性の問題を識別するのに役立ちますエラー メッセージを表示される可能性があります。 問題を特定するのに[プロセスのモニター](https://docs.microsoft.com/en-us/sysinternals/downloads/procmon)を使用することもできます。  一般的な問題は、作業ディレクトリとプログラムのパスのアクセス許可に関する前提条件をアプリケーションに関連します。

### <a name="using-process-monitor-to-identify-an-issue"></a>プロセスのモニターを使用して、問題を特定するには

[プロセスのモニター](https://docs.microsoft.com/en-us/sysinternals/downloads/procmon)は、アプリのファイルとレジストリの操作とその結果を監視するための強力なユーティリティです。  アプリケーションの互換性の問題について理解することができます。  プロセスのモニターを開いた後にフィルターを追加します (フィルター > フィルター.)、アプリケーションの実行可能ファイルからのイベントのみを含めます。

![ProcMon アプリ フィルター](images/desktop-to-uwp/procmon_app_filter.png)

イベントの一覧が表示されます。 これらのイベント、多くの単語**成功**を**結果**列に表示してされます。

![ProcMon イベント](images/desktop-to-uwp/procmon_events.png)

必要に応じて、のみエラーのみを表示するイベントをフィルター処理することができます。

![ProcMon 除外の成功](images/desktop-to-uwp/procmon_exclude_success.png)

ファイル システムへのアクセスの失敗が疑われる場合は、[System32/SysWOW64 またはパッケージのファイル パスの下である障害が発生したイベントを検索します。 フィルターを使っても役立ちますここでは、すぎます。 この一覧の下部に開始し、上方向にスクロールします。 この一覧の下部に表示されるエラーが発生した最も新しくします。 「アクセス拒否」などの文字列が含まれているエラーや"パス/名前が見つかりません"、ほとんどの注意を払うし、疑わしい外観がないことを無視します。 [PSFSample](https://github.com/Microsoft/MSIX-PackageSupportFramework/blob/master/samples/PSFSample/)では、2 つの問題があります。 次の図に表示される一覧でそれらの問題を確認できます。

![ProcMon Config.txt](images/desktop-to-uwp/procmon_config_txt.png)

この画像に表示される最初の問題、アプリケーションは、"C:\Windows\SysWOW64"パスにある"Config.txt"ファイルから読み取る失敗しています。 アプリケーションがそのパスを直接参照しようとしている可能性が高いことはできません。 ほとんどの場合、相対パスを使用して、そのファイルから読み取るしようと、既定で"System32/SysWOW64"は、アプリケーションの作業ディレクトリ。 これは、アプリケーションでは、パッケージのどこかに設定する現在の作業ディレクトリを想定を示しています。 Appx 内で見ると、実行可能ファイルと同じディレクトリにファイルが存在することを確認できます。

![アプリの Config.txt](images/desktop-to-uwp/psfsampleapp_config_txt.png)

2 番目の問題は、次の図が表示されます。

![ProcMon ログ ファイル](images/desktop-to-uwp/procmon_logfile.png)

この問題は、アプリケーションは、そのパッケージのパスを .log ファイルを記述する失敗しています。 これにより、ファイルのリダイレクト shim が役立つ場合がありますがお勧めします。

<a id="find" />

## <a name="find-a-runtime-fix"></a>ランタイムの修正プログラムを見つける

PSF には、ファイルのリダイレクト shim など、今すぐに使用できるランタイムの修正プログラムが含まれています。

### <a name="file-redirection-shim"></a>ファイルのリダイレクト Shim

書き込みまたは MSIX コンテナーで実行されるアプリケーションからアクセス可能ではないディレクトリ内のデータを読み取るしようとするたびにリダイレクトするのに[ファイルのリダイレクト Shim](https://github.com/Microsoft/MSIX-PackageSupportFramework/tree/develop/FileRedirectionShim)を使用することができます。

たとえば、アプリケーションが、アプリケーションの実行可能ファイルと同じディレクトリで公開されているログ ファイルに書き込む場合、は、ローカル アプリ データ ストアなどの別の場所にそのログ ファイルを作成する[ファイルのリダイレクト Shim](https://github.com/Microsoft/MSIX-PackageSupportFramework/tree/develop/FileRedirectionShim)を使用できます。

### <a name="runtime-fixes-from-the-community"></a>コミュニティからランタイムの修正プログラム

当社の[GitHub](https://github.com/Microsoft/MSIX-PackageSupportFramework/tree/develop)ページをコミュニティの投稿を確認してください。 他の開発者が自分のような問題を解決してされ、実行時の修正プログラムと共有できます。

## <a name="apply-a-runtime-fix"></a>ランタイムの修正プログラムを適用します。

Windows SDK から、次の手順に従って、いくつかの簡単なツールを使用して既存のランタイム修正を適用できます。

> [!div class="checklist"]
> * パッケージ レイアウト フォルダーを作成します。
> * パッケージのサポート フレームワーク ファイルを取得します。
> * パッケージに追加します。
> * パッケージ マニフェストの変更
> * 構成ファイルを作成します。

各タスクを見ていきましょう。

### <a name="create-the-package-layout-folder"></a>パッケージ レイアウト フォルダーを作成します。

.Appx ファイルが既にある場合の内容をパッケージのステージング領域として使用されるレイアウト フォルダーに展開できます。  これを行う、 **x64 ネイティブのツールのコマンド プロンプト for VS 2017**、または手動で実行可能ファイルの検索パスで SDK bin パス。

```
makeappx unpack /p PSFSamplePackage_1.0.60.0_AnyCPU_Debug.appx /d PackageContents

```

これにより、次のようになります。

![パッケージのレイアウト](images/desktop-to-uwp/package_contents.png)

.Appx ファイルは、開始時があるない、ゼロから、パッケージのフォルダーとファイルを作成できます。

### <a name="get-the-package-support-framework-files"></a>パッケージのサポート フレームワーク ファイルを取得します。

Visual Studio を使用して、PSF Nuget パッケージを取得できます。 スタンドアロン Nuget コマンド ライン ツールを使用して取得できます。

#### <a name="get-the-package-by-using-visual-studio"></a>Visual Studio を使ってパッケージを取得します。

Visual Studio で、ソリューションまたはプロジェクト ノードを右クリックし、Nuget パッケージの管理コマンドのいずれかを選択します。  検索**Microsoft.PackageSupportFramework** **PSF**上 Nuget.org パッケージを検索します。次に、インストールします。

#### <a name="get-the-package-by-using-the-command-line-tool"></a>コマンド ライン ツールを使用して、パッケージを取得します。

この場所から Nuget コマンド ライン ツールをインストール:https://www.nuget.org/downloadsします。 次に、Nuget コマンドラインからこのコマンドを実行します。

```
nuget install Microsoft.PackageSupportFramework
```

### <a name="add-the-package-support-framework-files-to-your-package"></a>パッケージのサポート フレームワーク ファイルをパッケージに追加します。

パッケージのディレクトリに必要な 32 ビットと 64 ビット PSF Dll と実行可能ファイルを追加します。 次の表をガイドとして使用してください。 また、必要な任意のランタイム修正が含まれています。 ここでは、ファイルのリダイレクトのランタイムの修正プログラムが必要です。

| アプリケーションの実行可能ファイルは、x64 | アプリケーションの実行可能ファイルは、x86 |
|-------------------------------|-----------|
| [ShimLauncher64.exe](https://github.com/Microsoft/MSIX-PackageSupportFramework/blob/master/ShimLauncher/readme.md) |  [ShimLauncher32.exe](https://github.com/Microsoft/MSIX-PackageSupportFramework/blob/master/ShimLauncher/readme.md) |
| [ShimRuntime64.dll](https://github.com/Microsoft/MSIX-PackageSupportFramework/blob/master/ShimRuntime/readme.md) | [ShimRuntime32.dll](https://github.com/Microsoft/MSIX-PackageSupportFramework/blob/master/ShimRuntime/readme.md) |
| [ShimRunDll64.exe](https://github.com/Microsoft/MSIX-PackageSupportFramework/blob/master/ShimRunDll/readme.md) | [ShimRunDll32.exe](https://github.com/Microsoft/MSIX-PackageSupportFramework/blob/master/ShimRunDll/readme.md) |

パッケージの内容は次のようになります。

![パッケージのバイナリ](images/desktop-to-uwp/package_binaries.png)

### <a name="modify-the-package-manifest"></a>パッケージ マニフェストの変更

テキスト エディターで、パッケージ マニフェストを開き、設定し、`Executable`の属性、`Application`要素 shim ランチャー実行可能ファイルの名前にします。  対象のアプリケーションのアーキテクチャがわかっている場合は、ShimLauncher32.exe または ShimLauncher64.exe は、適切なバージョンを選択します。  ない場合は、ShimLauncher32.exe は、どのようなケースで動作します。  次に例を示します。

```xml
<Package ...>
  ...
  <Applications>
    <Application Id="PSFSample"
                 Executable="ShimLauncher32.exe"
                 EntryPoint="Windows.FullTrustApplication">
      ...
    </Application>
  </Applications>
</Package>
```

### <a name="create-a-configuration-file"></a>構成ファイルを作成します。

ファイル名を作成``config.json``、そのファイルをパッケージのルート フォルダーに保存します。 交換した実行可能ファイルをポイントする config.json ファイルの宣言されているアプリの ID を変更します。 プロセスのモニターを使用してから得られる情報を使用して、したりすることことができますも作業ディレクトリを設定しファイルのリダイレクト shim を使用してパッケージ相対"PSFSampleApp"ディレクトリにある .log ファイルを読み取り/書き込みをリダイレクトします。

```json
{
    "applications": [
        {
            "id": "PSFSample",
            "executable": "PSFSampleApp/PSFSample.exe",
            "workingDirectory": "PSFSampleApp/"
        }
    ],
    "processes": [
        {
            "executable": "PSFSample",
            "shims": [
                {
                    "dll": "FileRedirectionShim.dll",
                    "config": {
                        "redirectedPaths": {
                            "packageRelative": [
                                {
                                    "base": "PSFSampleApp/",
                                    "patterns": [
                                        ".*\\.log"
                                    ]
                                }
                            ]
                        }
                    }
                }
            ]
        }
    ]
}
```
次に示します。 config.json スキーマのためのガイド

| 配列 | key | 値 |
|-------|-----------|-------|
| applications | id |  値を使用して、`Id`の属性、`Application`パッケージ マニフェスト内の要素です。 |
| applications | 実行可能 | 起動する実行可能ファイルへのパッケージ相対パス。 ほとんどの場合、変更する前に、パッケージ マニフェスト ファイルからこの値を取得できます。 値では、`Executable`の属性、`Application`要素です。 |
| applications | 作業ディレクトリ | (省略可能)起動するアプリケーションの作業ディレクトリとして使用するパッケージの相対パス。 この値を設定しない場合、オペレーティング システムを使用して、`System32`アプリケーションの作業ディレクトリとしてディレクトリ。 |
| プロセス | 実行可能 | ほとんどの場合の名前になります、`executable`削除パスとファイル拡張子を持つ上に構成されています。 |
| shim | dll | 読み込む shim .appx パッケージ相対パス。 |
| shim | config | (省略可能)Shim 配布リストの動作を制御します。 この値の正確な形式は、各 shim が解釈できるようにこの"blob"必要があるように、shim-shim によってごとに異なります。 |

`applications`、 `processes`、および`shims`キーは、配列です。 つまり、1 つ以上のアプリケーション、プロセス、および shim DLL を指定する config.json ファイルを使用することができます。


### <a name="package-and-test-the-app"></a>パッケージと、アプリのテスト

次に、パッケージを作成します。

```
makeappx pack /d PackageContents /p PSFSamplePackageFixup.appx
```

次に、署名します。

```
signtool sign /a /v /fd sha256 /f ExportedSigningCertificate.pfx PSFSamplePackageFixup.appx
```

詳細については、[パッケージが署名証明書を作成する方法について説明](https://docs.microsoft.com/en-us/windows/desktop/appxpkg/how-to-create-a-package-signing-certificate)し、 [signtool を使ってパッケージに署名する方法](https://docs.microsoft.com/en-us/windows/desktop/appxpkg/how-to-sign-a-package-using-signtool)をご覧ください。

PowerShell を使用して、パッケージをインストールします。

>[!NOTE]
> 最初にパッケージをアンインストールしてください。

```
powershell Add-AppxPackage .\PSFSamplePackageFixup.appx
```

アプリケーションを実行し、ランタイムの修正プログラムが適用されると、動作を確認します。  診断と必要に応じて、パッケージの手順を繰り返します。

### <a name="use-the-trace-shim"></a>トレース Shim を使用します。

パッケージ化されたアプリケーションの互換性の問題を診断するために別の手法では、トレース Shim を使用します。 この DLL は、PSF 付属であり、プロセスの監視と同様、アプリの動作の詳細な診断ビューを提供します。  アプリケーションの互換性の問題を表示するように設計します。  トレース Shim を使用して、DLL、パッケージを追加、config.json に次のフラグメントを追加し、パッケージ化し、およびインストールするアプリケーション。

```json
{
    "dll": "TraceShim.dll",
    "config": {
        "traceLevels": {
            "filesystem": "allFailures"
        }
    }
}
```

既定では、トレース Shim「期待」と考えられるエラーが除外されます。  たとえば、アプリケーションは無条件に既に存在するかどうか、結果を無視して確認することがなく、ファイルを削除しよう可能性があります。 サインアウトして、いくつかの予期しないエラーをフィルター処理を取得する可能性があります残念ながらの結果は、ファイルシステム関数からすべてのエラーを受信するオプトイン上記の例では、これがあります。 これはそれより前に Config.txt ファイルから読み取る失敗すると、メッセージ「ファイルが見つかりません」からわかっているためです。 これは、頻繁に確認されたでは、一般に予想するものと想定したエラーです。 実際にのみに予期しないエラーをフィルタ リングとその後にフォールバックするすべてのエラーも識別できない問題がある場合は、最初に可能性の最適なを勧めします。

既定では、トレース Shim からの出力を取得、アタッチされたデバッガーに送信されます。 この例では、おいない、デバッガーをアタッチすることが代わりにプログラムを使用して[デバッグ表示](https://docs.microsoft.com/en-us/sysinternals/downloads/debugview)sysinternals 出力を表示します。 アプリを実行すると、わかります同じエラー前とに、同じランタイムの修正プログラムから、マイクロソフトをポイントするとします。

![TraceShim ファイルが見つかりません](images/desktop-to-uwp/traceshim_filenotfound.png)

![TraceShim アクセスが拒否されました](images/desktop-to-uwp/traceshim_accessdenied.png)

## <a name="debug-extend-or-create-a-runtime-fix"></a>デバッグ、延長、または実行時の修正プログラムの作成

デバッグ ランタイムの修正プログラム、拡張ランタイムの修正プログラムを最初から作成に Visual Studio を使用することができます。 これらの操作を成功させる必要があります。

> [!div class="checklist"]
> * パッケージ プロジェクトを追加します。
> * ランタイムの修正プログラムのプロジェクトに追加します。
> * Shim ランチャー実行可能ファイルを起動するプロジェクトを追加します。
> * パッケージ プロジェクトを構成します。

完了したら、ソリューションにはこれのようになります。

![完成したソリューション](images/desktop-to-uwp/runtime-fix-project-structure.png)

この例では、各プロジェクトを見てみましょう。

| プロジェクト | 目的 |
|-------|-----------|
| DesktopApplicationPackage | このプロジェクトは、 [Windows アプリケーション パッケージ プロジェクト](desktop-to-uwp-packaging-dot-net.md)に基づいており、出力、MSIX パッケージ。 |
| Runtimefix | これは、実行時の修正プログラムとして機能する 1 つまたは複数の代替関数が含まれている C++ Dynamic-Linked ライブラリ プロジェクトです。 |
| ShimLauncher | これは、C++ 空のプロジェクトです。 このプロジェクトは、パッケージのサポート フレームワークのランタイム配布可能なファイルを収集する場所です。 実行可能ファイルを出力します。 その実行可能ファイルは、ソリューションを起動するときに実行する最初のものです。 |
| WinFormsDesktopApplication | このプロジェクトには、デスクトップ アプリケーションのソース コードが含まれています。 |

これらの種類のプロジェクトのすべてを含む完全なサンプルを見ると、 [PSFSample](https://github.com/Microsoft/MSIX-PackageSupportFramework/blob/master/samples/PSFSample/)を参照してください。

作成して、ソリューション内の各プロジェクトを構成する手順について説明しましょう。


### <a name="create-a-package-solution"></a>パッケージのソリューションを作成します。

デスクトップ アプリケーションのソリューションがない場合は、Visual Studio で新しい**空のソリューション**を作成します。

![空のソリューション](images/desktop-to-uwp/blank-solution.png)

あるすべてのアプリケーション プロジェクトに追加することもできます。

### <a name="add-a-packaging-project"></a>パッケージ プロジェクトを追加します。

**Windows アプリケーション パッケージ プロジェクト**がまだしていない場合は、いずれかを作成し、ソリューションに追加します。

![パッケージ プロジェクト テンプレート](images/desktop-to-uwp/package-project-template.png)

Windows アプリケーション パッケージ プロジェクトについて詳しくは、 [Visual Studio を使って、アプリケーションのパッケージ](desktop-to-uwp-packaging-dot-net.md)を参照してください。

**ソリューション エクスプ ローラー**では、パッケージ プロジェクトを右クリックして、選択**を編集**、およびこれをプロジェクト ファイルの下部に追加。

```
<Target Name="PSFRemoveSourceProject" AfterTargets="ExpandProjectReferences" BeforeTargets="_ConvertItems">
<ItemGroup>
  <FilteredNonWapProjProjectOutput Include="@(_FilteredNonWapProjProjectOutput)">
  <SourceProject Condition="'%(_FilteredNonWapProjProjectOutput.SourceProject)'=='<your runtime fix project name goes here>'" />
  </FilteredNonWapProjProjectOutput>
  <_FilteredNonWapProjProjectOutput Remove="@(_FilteredNonWapProjProjectOutput)" />
  <_FilteredNonWapProjProjectOutput Include="@(FilteredNonWapProjProjectOutput)" />
</ItemGroup>
</Target>
```

### <a name="add-project-for-the-runtime-fix"></a>ランタイムの修正プログラムのプロジェクトに追加します。

**ダイナミック リンク ライブラリ (DLL)** の C++ プロジェクトをソリューションに追加します。

![ランタイム ライブラリの修正](images/desktop-to-uwp/runtime-fix-library.png)

[プロジェクト]、[**プロパティ**を右クリックします。

プロパティ ページで、**標準的な C++ 言語**のフィールドを検索し、そのフィールドの横にあるドロップダウン リストで [、 **ISO C 17 標準 (//std:c では 17)** オプションです。

![ISO 17 オプション](images/desktop-to-uwp/iso-option.png)

そのプロジェクトを右クリックし、コンテキスト メニューで、 **Nuget パッケージの管理**オプションを選択します。 **すべて**のまたは**nuget.org****パッケージ ソース**オプションが設定されていることを確認します。

次にそのフィールドの設定アイコンをクリックします。

*PSF*検索 * Nuget パッケージをし、このプロジェクトにインストールします。

![nuget パッケージ](images/desktop-to-uwp/psf-package.png)

デバッグや、既存のランタイムの修正プログラムを拡張する場合は、このガイドの[ランタイムの修正プログラムを検索](#find)のセクションで説明したガイダンスを使用して、取得したランタイムの修正プログラム ファイルを追加します。

新しい修正プログラムを作成する場合は、追加しないでください何もこのプロジェクトにまだだけです。 お手伝いしますこのガイドの後半では、このプロジェクトに適切なファイルを追加します。 ここでは、ソリューションの設定が引き続きされます。

### <a name="add-a-project-that-starts-the-shim-launcher-executable"></a>Shim ランチャー実行可能ファイルを起動するプロジェクトを追加します。

C++**空のプロジェクト**のプロジェクトをソリューションに追加します。

![空のプロジェクト](images/desktop-to-uwp/blank-app.png)

このプロジェクトを前のセクションで説明されている同じガイダンスを使用して、 **PSF** Nuget パッケージを追加します。

開いている、**全般**設定] ページで、プロジェクトのプロパティ ページ**ターゲット名**プロパティに設定``ShimLauncher32``または``ShimLauncher64``によっては、アプリケーションのアーキテクチャ。

![shim ランチャー リファレンス](images/desktop-to-uwp/shim-exe-reference.png)

ランタイム修正プロジェクトへの参照をプロジェクトをソリューションに追加します。

![ランタイムの修正プログラムのリファレンス](images/desktop-to-uwp/reference-fix.png)

参照を右クリックし、[**プロパティ**] ウィンドウで、これらの値を適用します。

| プロパティ | 値 |
|-------|-----------|-------|
| ローカル コピーします。 | True |
| ローカル サテライト アセンブリをコピーします。 | True |
| 参照アセンブリの出力 | True |
| リンク ライブラリの依存関係 | False |
| リンク ライブラリの依存関係の入力 | False |

### <a name="configure-the-packaging-project"></a>パッケージ プロジェクトを構成します。

パッケージ プロジェクトで、**[アプリケーション]** フォルダーを右クリックして **[参照の追加]** を選びます。

![プロジェクト参照の追加](images/desktop-to-uwp/add-reference-packaging-project.png)

Shim ランチャー プロジェクトとデスクトップ アプリケーション プロジェクトを選択し、 **[ok]** ボタンをクリックします。

![デスクトップ プロジェクト](images/desktop-to-uwp/package-project-references.png)

>[!NOTE]
> アプリケーションにソース コードを持たない、shim ランチャー プロジェクトを選ぶだけです。 構成ファイルを作成するときに、実行可能ファイルを参照する方法紹介します。

**アプリケーション**のノードで shim ランチャー アプリケーションを右クリックし、**エントリ ポイントとして設定**します。

![エントリ ポイントの設定](images/desktop-to-uwp/set-startup-project.png)

という名前のファイルを追加``config.json``、パッケージ プロジェクトにコピーし、ファイルに次の json テキストを貼り付けます。 **コンテンツ**を**パッケージ アクション**プロパティを設定します。

```json
{
    "applications": [
        {
            "id": "",
            "executable": "",
            "workingDirectory": ""
        }
    ],
    "processes": [
        {
            "executable": "",
            "shims": [
                {
                    "dll": "",
                    "config": {
                    }
                }
            ]
        }
    ]
}
```
各キーの値を提供します。 次の表をガイドとして使用します。

| 配列 | key | 値 |
|-------|-----------|-------|
| applications | id |  値を使用して、`Id`の属性、`Application`パッケージ マニフェスト内の要素です。 |
| applications | 実行可能 | 起動する実行可能ファイルへのパッケージ相対パス。 ほとんどの場合、変更する前に、パッケージ マニフェスト ファイルからこの値を取得できます。 値では、`Executable`の属性、`Application`要素です。 |
| applications | 作業ディレクトリ | (省略可能)起動するアプリケーションの作業ディレクトリとして使用するパッケージの相対パス。 この値を設定しない場合、オペレーティング システムを使用して、`System32`アプリケーションの作業ディレクトリとしてディレクトリ。 |
| プロセス | 実行可能 | ほとんどの場合の名前になります、`executable`削除パスとファイル拡張子を持つ上に構成されています。 |
| shim | dll | Shim を読み込む DLL のパッケージ相対パス。 |
| shim | config | (省略可能)Shim 配布リストの動作を制御します。 この値の正確な形式は、各 shim が解釈できるようにこの"blob"必要があるように、shim-shim によってごとに異なります。 |

完了したら、``config.json``ファイルは次のようになります。

```json
{
  "applications": [
    {
      "id": "DesktopApplication",
      "executable": "DesktopApplication/WinFormsDesktopApplication.exe",
      "workingDirectory": "WinFormsDesktopApplication"
    }
  ],
  "processes": [
    {
      "executable": ".*App.*",
      "shims": [ { "dll": "RuntimeFix.dll" } ]
    }
  ]
}

```

>[!NOTE]
> `applications`、 `processes`、および`shims`キーは、配列です。 つまり、1 つ以上のアプリケーション、プロセス、および shim DLL を指定する config.json ファイルを使用することができます。

### <a name="debug-a-runtime-fix"></a>ランタイムの修正プログラムをデバッグします。

Visual Studio で f5 キーを押してデバッガーを起動します。  開始する最初のものは、次に、ターゲット デスクトップ アプリケーションを起動する shim ランチャー アプリケーションです。  ターゲットのデスクトップ アプリケーションをデバッグするには、手動で**デバッグ**を選択してデスクトップ アプリケーションのプロセスにアタッチする必要があります->**プロセスにアタッチ**し、アプリケーションのプロセスを選択します。 ネイティブ ランタイム修正 DLL を持つ .NET アプリケーションのデバッグを許可するには、マネージ コードとネイティブ コードの種類 (混在モードのデバッグ) を選択します。  

これ設定したら、デスクトップ アプリケーション コードとランタイムの修正プログラムのプロジェクトで数行のコードの横にブレークポイントを設定できます。 アプリケーションにソース コードがあるない場合、ランタイムの修正プログラムのプロジェクトで数行のコードの横にあるブレークポイントを設定することができます。

>[!NOTE]
> Visual Studio を使用する最も簡単な開発エクスペリエンスをデバッグするには、いくつかの制限があるときは、このガイドの後でについて説明します他のデバッグ手法を適用することができます。

## <a name="create-a-runtime-fix"></a>ランタイムの修正プログラムを作成します。

問題を解決する場合、代替関数を作成し、構成データを含む新しいランタイムの修正プログラムを作成することを解決する、ランタイムがない場合にかなっています。 各部分を見てみましょう。

### <a name="replacement-functions"></a>代替機能

まず、MSIX コンテナーでアプリケーションを実行するときに呼び出しが失敗する関数を識別します。 呼び出す代わりに、ランタイム マネージャーを希望する代替関数を作成できます。 これにより、関数の実装を最新のランタイム環境の規則に準拠している動作に置き換えることです。

Visual Studio で、このガイドで既に作成したランタイム修正プロジェクトを開きます。

宣言、``SHIM_DEFINE_EXPORTS``マクロの include ステートメントを追加し、`shim_framework.h`それぞれの上部にします。CPP ファイルは、実行時の修正プログラムの機能を追加します。

```c++
#define SHIM_DEFINE_EXPORTS
#include <shim_framework.h>
```
>[!IMPORTANT]
>確認、`SHIM_DEFINE_EXPORTS`マクロがインクルード ステートメントの前に表示されます。

同じ関数のシグネチャを持つ関数を作成しているが動作を変更します。 置換する関数の例を以下に示します、`MessageBoxW`関数です。

```c++
auto MessageBoxWImpl = &::MessageBoxW;
int WINAPI MessageBoxWShim(
    _In_opt_ HWND hwnd,
    _In_opt_ LPCWSTR,
    _In_opt_ LPCWSTR caption,
    _In_ UINT type)
{
    return MessageBoxWImpl(hwnd, L"SUCCESS: This worked", caption, type);
}

DECLARE_SHIM(MessageBoxWImpl, MessageBoxWShim);
```

呼び出し`DECLARE_SHIM`マップ、`MessageBoxW`新しい代替関数に機能します。 アプリケーションが呼び出すしようとしたとき、`MessageBoxW`関数が呼び出さ代替関数代わりにします。

#### <a name="protect-against-recursive-calls-to-functions-in-runtime-fixes"></a>ランタイムの修正プログラムの関数に再帰呼び出しからの保護します。

適用することが必要に応じて、`reentrancy_guard`を再帰的なランタイムの修正プログラムでの関数の呼び出しを保護する関数の種類。

代替の関数を作成するなど、`CreateFile`関数です。 実装を呼び出すことがあります、`CopyFile`が、実装、`CopyFile`関数を呼び出すことがあります、`CreateFile`関数です。 これは、無限再帰サイクルへの呼び出しのする可能性があります、`CreateFile`関数です。

ついて詳しくは`reentrancy_guard` [authoring.md](https://github.com/Microsoft/MSIX-PackageSupportFramework/blob/master/Authoring.md)を参照してください。

### <a name="configuration-data"></a>構成データ

構成データ、ランタイムの修正プログラムを追加する場合は、追加することを検討してください、``config.json``します。 そのにより使用でき、`ShimQueryCurrentDllConfig`にそのデータを簡単に解析します。 この例では、その構成ファイルからのブール値と文字列の値を解析します。

```c++
if (auto configRoot = ::ShimQueryCurrentDllConfig())
{
    auto& config = configRoot->as_object();

    if (auto enabledValue = config.try_get("enabled"))
    {
        g_enabled = enabledValue->as_boolean().get();
    }

    if (auto logPathValue = config.try_get("logPath"))
    {
        g_logPath = logPathValue->as_string().wstring();
    }
}
```

## <a name="other-debugging-techniques"></a>その他のデバッグ手法

Visual Studio では、最も簡単な開発とデバッグのエクスペリエンスを提供は制限があります。

まず、F5 デバッグと、.appx パッケージからインストールするのではなく、パッケージ レイアウト フォルダー パスからルーズ ファイルを展開することによって、アプリケーションが実行されます。  レイアウト フォルダー通常ありませんセキュリティの制限を同じパッケージのインストール フォルダーとして。 その結果、にくいかもしれませんランタイムの修正プログラムを適用する前にパッケージのパスへのアクセス拒否エラーを再現することもできます。

この問題に対処するには、f5 キーを押してルーズ ファイルの展開ではなく、.appx パッケージの展開を使用します。  .Appx パッケージ ファイルを作成するには、前述のよう、Windows SDK から[MakeAppx](https://docs.microsoft.com/en-us/windows/desktop/appxpkg/make-appx-package--makeappx-exe-)ユーティリティを使用します。 またはから、Visual Studio 内アプリケーション プロジェクト ノードを右クリックし、**ストア**を選択->**アプリ パッケージを作成**します。

Visual Studio の別の問題は、デバッガーを起動したすべての子プロセスにアタッチするための組み込みサポートがないことです。   Visual Studio によって起動後が手動で接続され、ターゲット アプリケーションのスタートアップ パス内のロジックをデバッグが困難になります。

この問題に対処するには、使用子プロセスをサポートしているデバッガーをアタッチします。  一般に、ターゲット アプリケーションにジャスト イン タイム (JIT) デバッガーをアタッチすることに注意してください。  これは、ほとんど JIT 技法 ImageFileExecutionOptions レジストリ キーを使用して、ターゲット アプリの代わりにデバッガーを起動するためです。  ターゲット アプリに ShimRuntime.dll を挿入するために使用 ShimLauncher.exe detouring メカニズムが損なわれるためです。  WinDbg、 [Debugging Tools for Windows](https://docs.microsoft.com/en-us/windows-hardware/drivers/debugger/index)に含まれているし、 [Windows SDK](https://developer.microsoft.com/en-US/windows/downloads/windows-10-sdk)から取得したサポート子プロセスをアタッチします。  サポート直接[起動して UWP アプリをデバッグ](https://docs.microsoft.com/en-us/windows-hardware/drivers/debugger/debugging-a-uwp-app-using-windbg#span-idlaunchinganddebuggingauwpappspanspan-idlaunchinganddebuggingauwpappspanspan-idlaunchinganddebuggingauwpappspanlaunching-and-debugging-a-uwp-app)します。

子プロセスとしてターゲット アプリケーションの起動をデバッグするには、開始``WinDbg``します。

```
windbg.exe -plmPackage PSFSampleWithFixup_1.0.59.0_x86__7s220nvg1hg3m -plmApp PSFSample
```

``WinDbg``プロンプト、子のデバッグを有効にして、適切なブレークポイントを設定します。

```
.childdbg 1
g
```
(ターゲット アプリケーションが開始され、デバッガーにするまで実行)

```
sxe ld fixup.dll
g
```
(修正の DLL が読み込まれるまで実行されません)

```
bp ...
```

>[!NOTE]
> [PLMDebug](https://docs.microsoft.com/en-us/windows-hardware/drivers/debugger/plmdebug)は起動時、アプリにデバッガーをアタッチするも使用でき、 [Debugging Tools for Windows](https://docs.microsoft.com/en-us/windows-hardware/drivers/debugger/index)にも含まれています。  ただし、WinDbg によって提供されるようになりました直接サポートよりも複雑です。

## <a name="support-and-feedback"></a>サポートとフィードバック

**質問に対する回答を見つける**

ご質問がある場合は、 Stack Overflow でお問い合わせください。 Microsoft のチームでは、これらの[タグ](http://stackoverflow.com/questions/tagged/project-centennial+or+desktop-bridge)をチェックしています。 [こちら](https://social.msdn.microsoft.com/Forums/en-US/home?filter=alltypes&sort=relevancedesc&searchTerm=%5BDesktop%20Converter%5D)から質問することもできます。