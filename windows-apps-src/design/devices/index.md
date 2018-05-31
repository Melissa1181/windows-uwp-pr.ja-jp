---
author: mijacobs
Description: Getting to know the devices that support Universal Windows Platform (UWP) apps will help you offer the best user experience for each form factor.
title: ユニバーサル Windows プラットフォーム (UWP) アプリ用デバイスの基本情報
ms.assetid: 7665044E-F007-495D-8D56-CE7C2361CDC4
label: Device primer
template: detail.hbs
keywords: デバイス, 入力, 操作
ms.author: mijacobs
ms.date: 02/08/2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
ms.localizationpriority: medium
ms.openlocfilehash: 4c36e60d0435db6536ea7bb0eee3011937668cb7
ms.sourcegitcommit: f9a4854b6aecfda472fb3f8b4a2d3b271b327800
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
ms.locfileid: "1395391"
---
#  <a name="device-primer-for-universal-windows-platform-uwp-apps"></a>ユニバーサル Windows プラットフォーム (UWP) アプリ用デバイスの基本情報



![Windows デバイス](images/device-primer/device-primer-ramp.png)

ユニバーサル Windows プラットフォーム (UWP) アプリをサポートするデバイスを理解すると、各フォーム ファクター向けの最適なユーザー エクスペリエンスを提供するために役立ちます。 特定のデバイス向けのアプリを設計するときは、アプリがデバイスにどのように表示されるか、そのデバイスでアプリがいつどこでどのように使われるか、ユーザーがそのデバイスをどのように操作するかについて、特に考慮する必要があります。

## <a name="pcs-and-laptops"></a>PC とノート PC


Windows PC とノート PC には、多種多様なデバイスと画面サイズがあります。 一般に、PC やノート PC は電話やタブレットより多くの情報を表示できます。

画面サイズ
-   13" 以上

![PC](images/device-primer/device-primer-desktop.png)

一般的な使い方
-   デスクトップとノート PC のアプリは共有で使われますが、一度に使うことができるのは 1 人のユーザーだけであり、通常は長時間使われます。

UI に関する考慮事項
-   アプリは、ユーザーが決めたウィンドウ表示のサイズにすることができます。 ウィンドウのサイズによっては、1 ～ 3 つのフレームを表示できます。 大型のモニターでは、アプリは 3 つを超えるフレームを表示できます。

-   アプリをデスクトップまたはノート PC で使う場合、ユーザーがアプリのファイルを制御できます。 アプリの設計者は、アプリのコンテンツを管理するメカニズムを必ず用意してください。 [名前を付けて保存] や [最近使ったファイル] などのコマンドや機能を含めることを検討してください。

-   システムの戻るボタンはオプションです。 アプリの開発者が表示するように選択した場合、アプリのタイトル バーに表示されます。

入力
-   マウス
-   キーボード
-   タッチ (ノート PC とオールインワン型デスクトップ)。
-   Xbox コントローラーなどのゲームパッドが使われることがあります。

デバイスの標準的な機能
-   カメラ
-   マイク

## <a name="tablets-and-2-in-1s"></a>タブレットと 2 in 1


超軽量のタブレット コンピューターは、タッチスクリーン、カメラ、マイク、および加速度計を備えています。 タブレットの画面サイズは、通常は 7 ～ 13.3 インチです。 2 in 1 デバイスは、構成によって (通常は、画面をたたむか直立させて切り替えます)、タブレットまたはキーボードとマウスを使ったノート PC として利用できます。

画面サイズ
- タブレットの場合、7 ～ 13.3 インチ
- 2 in 1 の場合は 13.3 インチ以上

![タブレット デバイス](images/device-primer/device-primer-tablet.png)

一般的な使い方
-   タブレットは、約 80% がその所有者によって使われ、残りの約 20% が共有されています。
-   最も一般的なのは、自宅でテレビを視聴しているときのコンパニオン デバイスとして使うことです。
-   電話とファブレットよりも長い時間使われます。
-   テキストは一気に入力されます。

UI に関する考慮事項
-   タブレットは、横方向でも縦方向でも一度に 2 つのフレームを表示できます。
-   システムの戻るボタンはナビゲーション バーに配置されます。

入力
-   タッチ
-   スタイラス
-   外部キーボード (ときどき)
-   マウス (ときどき)
-   音声 (ときどき)

デバイスの標準的な機能
-   カメラ
-   マイク
-   移動センサー (複数)
-   位置センサー (複数)

> [!NOTE]
> PC の考慮事項のほとんどが 2 in 1 にも当てはまります。

## <a name="xbox-and-tv"></a>Xbox とテレビ

ソファーに座りながらゲームパッドやリモコンを使って部屋の反対側にあるテレビを操作することを、**10 フィート エクスペリエンス**といいます。 通常は画面から約 10 フィート (約 3 m) の距離に座るため、このように呼ばれています。 この場合、たとえば PC の操作 (*2 フィート* エクスペリエンスと呼ばれます) には見られない、特有の課題があります。 テレビ画面に接続し、ゲームパッドやリモコンを使うこともある Xbox One やその他のデバイス向けアプリを開発している場合、この点を常に意識しておく必要があります。

10 フィート エクスペリエンスを提供する UWP アプリの設計は、ここに記載されているその他のデバイス カテゴリでの設計とは非常に異なります。 詳しくは、「[Xbox およびテレビ向け設計](designing-for-tv.md)」をご覧ください。

画面サイズ
- 24 インチ以上

![Xbox とテレビ](images/device-primer/device-primer-tv-and-xbox.png)

一般的な使い方
- 多くの場合は、複数のユーザーが共有して使用しますが、1 人だけで使用することもよくあります。
- 通常は長時間使われます。
- 最もよく使用される場所は自宅で、一か所に据え置かれます。
- ゲームパッドやリモコンを使ってのテキスト入力は時間がかかるため、テキスト入力が求められることはほとんどありません。
- 画面の向きは固定されています。
- 通常、一度に 1 つのアプリのみを実行しますが、画面の端にアプリをスナップできる場合があります (Xbox など)。

UI に関する考慮事項
- アプリのサイズは、他のアプリが画面の端にスナップされていない限り、通常は変化しません。
- システムの戻るボタン、ほとんどの Xbox アプリで提供される便利な機能で、ゲームパッドの B ボタンを使用してアクセスします。
- 通常、ユーザーは画面から約 10 フィート (約 3 m) の距離に座るため、読み取れるように十分な大きさで明瞭な UI が必要です。

入力
- ゲームパッド (Xbox コントローラーなど)
- リモコン
- 音声 (Kinect やヘッドセットを使用する場合)

デバイスの標準的な機能
- カメラ (Kinect を使用する場合)
- マイク (Kinect やヘッドセットを使用する場合)
- 移動センサー (Kinect を使用する場合)

## <a name="phones-and-phablets"></a>電話とファブレット


すべてのコンピューティング デバイスの中で最も広く使われている電話では、限られた画面領域と基本的な入力方法を使って、さまざまな操作を行うことができます。 電話にはさまざまなサイズがあり、大きい電話はファブレットと呼ばれます。 ファブレットでのアプリのエクスペリエンスは、電話でのエクスペリエンスと似ていますが、画面領域が大きくなることで、コンテンツ操作時に重要な変更が可能になります。

互換性のある Windows 10 Mobile デバイスの新しいエクスペリエンスである電話用 Continuum を使用すると、ユーザーが電話をモニターに接続し、マウスやキーボードを使用して、その電話をノート PC のように使うことができます。 詳しくは、「[電話用 Continuum](http://go.microsoft.com/fwlink/p/?LinkID=699431)」をご覧ください。

画面サイズ
-   電話の場合、4" ～ 5"
-   ファブレットの場合、5.5" ～ 7"

![Windows Phone](images/device-primer/device-primer-phablet.png)

一般的な使い方
-   主に縦向きで使われます。これはほとんどの場合、片手で電話を持つのが簡単であること、その方法で完全に電話を操作できることが理由ですが、写真やビデオの表示、本の閲覧、テキストの作成など、横向きが適切なエクスペリエンスもあります。
-   ほとんどの場合、そのデバイスの所有者である 1 人のユーザーによって使われます。
-   常に手近にあり、通常はポケットやバッグに入れられます。
-   短時間使われます。
-   ユーザーは、電話を使うときによくマルチタスクを実行します。
-   テキストは一気に入力されます。

UI に関する考慮事項
-   電話の画面の小さいサイズでは、横方向でも縦方向でも、一度に 1 つのフレームのみを表示できます。 電話のすべての階層型ナビゲーション パターンでは「ドリルダウン」モデルを使い、ユーザーが単一フレームの UI レイヤーを移動するようにします。

-   電話と同じように、縦モードのファブレットには、一度に 1 つのフレームのみを表示できます。 ただし、ファブレットで使うことができる画面領域は大きいため、ユーザーはファブレットを横方向に回転させてそのまま保持することで、2 つのアプリ フレームを同時に表示できます。

-   横方向と縦方向の両方で、スクリーン キーボードが表示されているときに、アプリ バーを表示するための十分な画面領域があることを確認します。

入力
-   タッチ
-   音声

デバイスの標準的な機能
-   マイク
-   カメラ
-   移動センサー (複数)
-   位置センサー (複数)

 

## <a name="surface-hub-devices"></a>Surface Hub デバイス


Microsoft Surface Hub は、複数のユーザーによる同時使用のために設計された大画面のチーム コラボレーション デバイスです。

画面サイズ
-   55" および 84"

![Surface Hub](images/device-primer/device-primer-surfacehub3.png)

一般的な使い方
-   Surface Hub 上のアプリは、会議などで短時間共有して使われます。

-   ほとんどの場合、Surface Hub デバイス固定された状態で使われ、移動することはめったにありません。

UI に関する考慮事項
-   Surface Hub 上のアプリは 4 つの状態のいずれかで表示されます。全画面 (標準の全画面表示)、バックグラウンド (アプリの実行中に非表示になり、タスク スイッチャーで利用可能)、フィル (利用可能なステージ エリアを使う固定表示)、スナップ (ステージの右端または左端を使う可変表示) です。
-   スナップ モードまたはフィル モードでは、Skype サイドバーが表示され、アプリは横方向に縮小されます。
-   システムの戻るボタンはオプションです。 アプリの開発者が表示するように選択した場合、アプリのタイトル バーに表示されます。

入力
-   タッチ
-   ペン
-   音声
-   キーボード (スクリーン/リモート)
-   タッチパッド (リモート)

デバイスの標準的な機能
-   カメラ
-   マイク

 

## <a name="windows-iot-devices"></a>Windows IoT デバイス


Windows IoT デバイスは、最新クラスのデバイスであり、主に小型のエレクトロニクス、センサー、接続機能が物理オブジェクト内に埋め込まれたものです。 通常、これらのデバイスはネットワークまたはインターネット経由で接続され、感知した実際のデータについて報告します。場合によっては、それに対して処理を実行することもあります。 デバイスには、画面がない場合 ("ヘッドレス" デバイスとも呼ばれます) と、一般的に 3.5" 以下の小さい画面に接続される場合 ("ヘッド付き" デバイスとも呼ばれます) があります。

画面サイズ
-   3.5" 以下
-   一部のデバイスには画面がない

![IoT デバイス](images/device-primer/device-primer-iot-device.png)

一般的な使い方
-   通常、ネットワークまたはインターネット経由で接続されており、感知した実際のデータについて報告します。場合によっては、それに対して処理を実行することもあります。
-   これらのデバイスは電話やその他の大型デバイスとは異なり、一度に 1 つのアプリケーションのみ実行できます。
-   常に操作するデバイスではありませんが、必要なときに利用でき、必要でないときに邪魔になりません。
-   アプリには専用のバック アフォーダンスはなく、これは開発者の責任です。

UI に関する考慮事項
-   "ヘッドレス "デバイスには画面がありません。
-   "ヘッド付き" デバイスの画面は最小限で、画面サイズと機能が制限されているため、必要なもののみが表示されます。
-   ほとんどの場合、向きはロックされるため、アプリでは 1 つの表示方向を考慮するだけで済みます。

入力
-   デバイスに応じて可変

デバイスの標準的な機能
-   デバイスに応じて可変