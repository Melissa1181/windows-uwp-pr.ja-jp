---
author: mcleanbyron
ms.assetid: 8C63D33B-557D-436E-9DDA-11F7A5BFA2D7
description: "既存のアドオンの申請を更新するには、Windows ストア申請 API のこのメソッドを使います。"
title: "Windows ストア申請 API を使用したアドオンの申請の更新"
translationtype: Human Translation
ms.sourcegitcommit: 5f975d0a99539292e1ce91ca09dbd5fac11c4a49
ms.openlocfilehash: b7a8e1d39d5ee0a0858382b84ab00cc2c481da5d

---

# Windows ストア申請 API を使用したアドオンの申請の更新




既存のアドオン (アプリ内製品 (IAP) とも呼ばれます) 申請を更新するには、Windows ストア申請 API 内のこのメソッドを使います。 このメソッドを使って申請を正常に更新した後は、インジェストと公開のために[申請をコミット](commit-an-add-on-submission.md)する必要があります。

このメソッドが Windows ストア申請 API を使ったアドオンの申請の作成プロセスにどのように適合するかについては、「[アドオンの申請の管理](manage-add-on-submissions.md)」をご覧ください。

## 前提条件

このメソッドを使うには、最初に次の作業を行う必要があります。

* Windows ストア申請 API に関するすべての[前提条件](create-and-manage-submissions-using-windows-store-services.md#prerequisites)を満たします (前提条件がまだ満たされていない場合)。
* このメソッドの要求ヘッダーで使う [Azure AD アクセス トークンを取得](create-and-manage-submissions-using-windows-store-services.md#obtain-an-azure-ad-access-token)します。 アクセス トークンを取得した後、アクセス トークンを使用できるのは、その有効期限が切れるまでの 60 分間です。 トークンの有効期限が切れたら新しいトークンを取得できます。
* デベロッパー センター アカウントにアドオン申請を作成します。 この操作は、デベロッパー センター ダッシュボードまたは[アドオン申請の作成](create-an-add-on-submission.md)メソッドを使って実行できます。

>**注:**&nbsp;&nbsp;このメソッドは、Windows ストア申請 API を使用するアクセス許可が付与された Windows デベロッパー センター アカウントにのみ使用できます。 すべてのアカウントでこのアクセス許可が有効になっているとは限りません。

## 要求

このメソッドの構文は次のとおりです。 ヘッダーと要求本文の使用例と説明については、次のセクションをご覧ください。

| メソッド | 要求 URI                                                      |
|--------|------------------------------------------------------------------|
| PUT    | ```https://manage.devcenter.microsoft.com/v1.0/my/inappproducts/{inAppProductId}/submissions/{submissionId} ``` |

<span/>
 

### 要求ヘッダー

| ヘッダー        | 型   | 説明                                                                 |
|---------------|--------|-----------------------------------------------------------------------------|
| Authorization | string | 必須。 **Bearer** &lt;*トークン*&gt; という形式の Azure AD アクセス トークン。 |

<span/>

### 要求パラメーター

| 名前        | 型   | 説明                                                                 |
|---------------|--------|-----------------------------------------------------------------------------|
| inAppProductId | string | 必須。 申請を更新するアドオンのストア ID です。 ストア ID はデベロッパー センター ダッシュボードで取得でき、[アドオンを作成](create-an-add-on.md)または[アドオンの詳細を取得](get-all-add-ons.md)する要求に対する応答データに含まれます。  |
| submissionId | string | 必須。 更新する申請の ID です。 この ID は、[アドオン申請の作成](create-an-add-on-submission.md)要求の応答データに含まれており、デベロッパー センター ダッシュボードで確認できます。  |

<span/>

### 要求本文

要求本文には次のパラメーターがあります。

| 値      | 型   | 説明                                                                                                                                                                                                                                                                         |
|------------|--------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| contentType           | string  |  アドオンで提供されている[コンテンツの種類](../publish/enter-iap-properties.md#content-type)です。 次のいずれかの値を使用できます。 <ul><li>NotSet</li><li>BookDownload</li><li>EMagazine</li><li>ENewspaper</li><li>MusicDownload</li><li>MusicStream</li><li>OnlineDataStorage</li><li>VideoDownload</li><li>VideoStream</li><li>Asp</li><li>OnlineDownload</li></ul> |  
| keywords           | array  | アドオンの[キーワード](../publish/enter-iap-properties.md#keywords)の文字列を最大 10 個含む配列です。 アプリでは、これらのキーワードを使ってアドオンを照会できます。   |
| lifetime           | string  |  アドオンの有効期間です。 次のいずれかの値を使用できます。 <ul><li>Forever</li><li>OneDay</li><li>ThreeDays</li><li>FiveDays</li><li>OneWeek</li><li>TwoWeeks</li><li>OneMonth</li><li>TwoMonths</li><li>ThreeMonths</li><li>SixMonths</li><li>OneYear</li></ul> |
| listings           | object  | アドオンの表示内容を含むオブジェクトです。 詳しくは、「[表示リソース](manage-add-on-submissions.md#listing-object)」をご覧ください。  |
| pricing           | object  | アドオンの価格情報を含むオブジェクトです。 詳しくは、「[価格リソース](manage-add-on-submissions.md#pricing-object)」をご覧ください。  |
| targetPublishMode           | string  | 申請の公開モードです。 次のいずれかの値を使用できます。 <ul><li>Immediate</li><li>Manual</li><li>SpecificDate</li></ul> |
| targetPublishDate           | string  | *targetPublishMode* が SpecificDate に設定されている場合、ISO 8601 形式での申請の公開日です。  |
| tag           | string  |  アドオンの[タグ](../publish/enter-iap-properties.md#tag)です。   |
| visibility  | string  |  アドオンの可視性です。 次のいずれかの値を使用できます。 <ul><li>Hidden</li><li>Public</li><li>Private</li><li>NotSet</li></ul>  |

<span/>

### 要求の例

次の例は、アドオンの申請を更新する方法を示しています。

```json
PUT https://manage.devcenter.microsoft.com/v1.0/my/inappproducts/9NBLGGH4TNMP/submissions/1152921504621230023 HTTP/1.1
Authorization: Bearer <your access token>
Content-Type: application/json
{
  "contentType": "EMagazine",
  "keywords": [
    "books"
  ],
  "lifetime": "FiveDays",
  "listings": {
    "en": {
      "description": "English add-on description",
      "icon": {
        "fileName": "add-on-en-us-listing2.png",
        "fileStatus": "Uploaded"
      },
      "title": "Add-on Title (English)"
    },
    "ru": {
      "description": "Russian add-on description",
      "icon": {
        "fileName": "add-on-ru-listing.png",
        "fileStatus": "Uploaded"
      },
      "title": "Add-on Title (Russian)"
    }
  },
  "pricing": {
    "marketSpecificPricings": {
      "RU": "Tier3",
      "US": "Tier4",
    },
    "sales": [
      {
         "name": "Sale1",
         "basePriceId": "Free",
         "startDate": "2016-05-21T18:40:11.7369008Z",
         "endDate": "2016-05-22T18:40:11.7369008Z",
         "marketSpecificPricings": {
            "RU": "NotAvailable"
         }
      }
    ],
    "priceId": "Free"
  },
  "targetPublishDate": "2016-03-15T05:10:58.047Z",
  "targetPublishMode": "Immediate",
  "tag": "SampleTag",
  "visibility": "Public",
}
```

## 応答

次の例は、このメソッドが正常に呼び出された場合の JSON 応答本文を示しています。 応答本文には、更新された申請に関する情報が含まれています。 応答本文内の値について詳しくは、「[アドオンの申請のリソース](manage-add-on-submissions.md#add-on-submission-object)」をご覧ください。

```json
{
  "id": "1152921504621243680",
  "contentType": "EMagazine",
  "keywords": [
    "books"
  ],
  "lifetime": "FiveDays",
  "listings": {
    "en": {
      "description": "English add-on description",
      "icon": {
        "fileName": "add-on-en-us-listing2.png",
        "fileStatus": "Uploaded"
      },
      "title": "Add-on Title (English)"
    },
    "ru": {
      "description": "Russian add-on description",
      "icon": {
        "fileName": "add-on-ru-listing.png",
        "fileStatus": "Uploaded"
      },
      "title": "Add-on Title (Russian)"
    }
  },
  "pricing": {
    "marketSpecificPricings": {
      "RU": "Tier3",
      "US": "Tier4",
    },
    "sales": [
      {
         "name": "Sale1",
         "basePriceId": "Free",
         "startDate": "2016-05-21T18:40:11.7369008Z",
         "endDate": "2016-05-22T18:40:11.7369008Z",
         "marketSpecificPricings": {
            "RU": "NotAvailable"
         }
      }
    ],
    "priceId": "Free"
  },
  "targetPublishDate": "2016-03-15T05:10:58.047Z",
  "targetPublishMode": "Immediate",
  "tag": "SampleTag",
  "visibility": "Public",
  "status": "PendingCommit",
  "statusDetails": {
    "errors": [
      {
        "code": "None",
        "details": "string"
      }
    ],
    "warnings": [
      {
        "code": "ListingOptOutWarning",
        "details": "You have removed listing language(s): []"
      }
    ],
    "certificationReports": [
      {
      }
    ]
  },
  "fileUploadUrl": "https://productingestionbin1.blob.core.windows.net/ingestion/26920f66-b592-4439-9a9d-fb0f014902ec?sv=2014-02-14&sr=b&sig=usAN0kNFNnYE2tGQBI%2BARQWejX1Guiz7hdFtRhyK%2Bog%3D&se=2016-06-17T20:45:51Z&sp=rwl",
  "friendlyName": "Submission 2"
}
```

## エラー コード

要求を正常に完了できない場合、次の HTTP エラー コードのいずれかが応答に含まれます。

| エラー コード |  説明   |
|--------|------------------|
| 400  | 要求が無効なため、申請を更新できませんでした。 |
| 409  | アドオンの現在の状態が原因で申請を更新できませんでした。または、[Windows ストア申請 API で現在サポートされていない](create-and-manage-submissions-using-windows-store-services.md#not_supported)デベロッパー センター ダッシュボード機能がアドオンで使用されています。 |   

<span/>


## 関連トピック

* [Windows ストア サービスを使用した申請の作成と管理](create-and-manage-submissions-using-windows-store-services.md)
* [アドオンの申請の管理](manage-add-on-submissions.md)
* [アドオンの申請の取得](get-an-add-on-submission.md)
* [アドオンの申請の作成](create-an-add-on-submission.md)
* [アドオンの申請のコミット](commit-an-add-on-submission.md)
* [アドオンの申請の削除](delete-an-add-on-submission.md)
* [アドオンの申請の状態の取得](get-status-for-an-add-on-submission.md)



<!--HONumber=Aug16_HO5-->

