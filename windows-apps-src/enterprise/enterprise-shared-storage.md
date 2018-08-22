---
author: mcleblanc
ms.assetid: B48E21AB-0EA5-444B-8333-393DD8D1B76D
title: エンタープライズ共有記憶域
description: エンタープライズ共有記憶域は、基幹業務アプリのデータ共有のための、ローカルのデータの場所を定義します。
ms.author: markl
ms.date: 02/08/2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: Windows 10, UWP
ms.openlocfilehash: 3f04d00da3fce4674f344129910917e9585e8723
ms.sourcegitcommit: 909d859a0f11981a8d1beac0da35f779786a6889
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.locfileid: "243067"
---
# <a name="enterprise-shared-storage"></a>エンタープライズ共有記憶域

共有記憶域は、2 つの場所で構成されています。この場所では、制限された機能 **enterpriseDeviceLockdown** とエンタープライズ証明書を持つアプリは、完全な読み取り/書き込みアクセスがあります。 **enterpriseDeviceLockdown** を使うと、アプリは、デバイスのロック ダウン API を利用したり、企業で共有している保存フォルダーにアクセスしたりすることができます。 API について詳しくは、「[**Windows.Embedded.DeviceLockdown**](http://go.microsoft.com/fwlink/?LinkId=699331) 名前空間」をご覧ください。  

これらの場所は、次のローカル ドライブに設定されます。
- \Data\SharedData\Enterprise\Persistent
- \Data\SharedData\Enterprise\Non-Persistent

## <a name="scenarios"></a>シナリオ

エンタープライズ共有記憶域は、次のシナリオをサポートします。

- 1 つのアプリの 1 つのインスタンス内、同じアプリの複数のインスタンス間、また適切な機能と証明書を持つ複数のアプリ間で、データを共有できます。
- ローカルのハード ドライブの \Data\SharedData\Enterprise\Persistent フォルダーにデータを保存でき、これはデバイスのリセット後も保持されます。
- モバイル デバイス管理 (MDM) サービスを使用して、デバイス上のファイルの読み取り、書き込み、削除などのファイル操作を行えます。 MDM サービスを使ったエンタープライズ共有記憶域の使用方法について詳しくは、「[EnterpriseExtFileSystem CSP](http://go.microsoft.com/fwlink/?LinkId=699333)」をご覧ください。

## <a name="access-enterprise-shared-storage"></a>エンタープライズ共有記憶域へのアクセス

次の例では、パッケージ マニフェストでエンタープライズ共有記憶域へのアクセス機能を宣言する方法、および Windows.Storage.StorageFolder クラスを使って共有保存フォルダーにアクセスする方法を示します。

アプリ パッケージ マニフェストに次の機能を含めます。

```xml
<Package
  xmlns="http://schemas.microsoft.com/appx/manifest/foundation/windows10"
  xmlns:mp="http://schemas.microsoft.com/appx/2014/phone/manifest"
  xmlns:uap="http://schemas.microsoft.com/appx/manifest/uap/windows10"
  xmlns:rescap="http://schemas.microsoft.com/appx/manifest/foundation/windows10/restrictedcapabilities"
  IgnorableNamespaces="uap mp rescap">

…

<Capabilities>
    <rescap:Capability Name="enterpriseDeviceLockdown"/>
</Capabilities>
```

共有データの場所にアクセスするには、アプリで次のコードを使います。

```csharp
using System;
using System.Collections.Generic;
using System.Diagnostics;
using Windows.Storage;

…

// Get the Enterprise Shared Storage folder.
var enterprisePersistentFolderRoot = @"C:\Data\SharedData\Enterprise\Persistent";

StorageFolder folder =
    await StorageFolder.GetFolderFromPathAsync(enterprisePersistentFolderRoot);

// Get the files in the folder.
IReadOnlyList<StorageFile> sortedItems =
    await folder.GetFilesAsync();

// Iterate over the results and print the list of files
// to the Visual Studio Output window.
foreach (StorageFile file in sortedItems)
    Debug.WriteLine(file.Name + ", " + file.DateCreated);
```
