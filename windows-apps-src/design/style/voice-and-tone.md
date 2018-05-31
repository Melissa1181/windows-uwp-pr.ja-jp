---
author: QuinnRadich
title: ボイスとトーン
description: アプリのテキストを設計と融合させるには、適切なボイスとトーンを使用することが重要です。
keywords: UWP, Windows 10, ボイス, トーン, テキスト, 書き込み, 設計, UI, UX
ms.author: quradic
ms.date: 8/52/2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
ms.localizationpriority: medium
ms.openlocfilehash: 8c95359afb148c6c77f3297aaacd5cb55e366c51
ms.sourcegitcommit: db09dcb08da5995c46c2729896e56be3774ee5ba
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/05/2018
ms.locfileid: "1554542"
---
# <a name="voice-and-tone"></a>ボイスとトーン

詳細な操作手順から単純なヒントまで、テキストは、ほぼすべてのアプリに必要なコンポーネントです。 そのようなユーザー エクスペリエンスの基本的な部分として、テキストはアプリの設計を強化するものであり、アプリの目的と視覚的なプレゼンテーションが調和している必要があります。

あらゆるライティングと同様に、アプリのテキストを作成するときには、ボイスとトーンの選択についてじっくり考えることが必要です。 この 2 つはよく似ていますが異なります。ボイスは対象に対する姿勢であり、トーンはその実装であると考えることができます。 アプリ内にユーザー向けのテキストを書き込むときには、このボイスは常に友好的で自然であり、すぐにつながることができるものでなければなりません。 トーンは、一般的なガイドラインに従っており、アプリのボイスやニーズと調和している限り、より柔軟にすることができます。 適切な単語や語句を慎重に選択することにより、アプリのユーザー エクスペリエンスを向上させ、エラーの発生など、ユーザーにとってよくない状況において、ユーザーの負担を軽減し、少しでも快適なエクスペリエンスを提供できます。

## <a name="creating-a-friendly-natural-voice"></a>友好的で自然なボイスの作成

アプリのボイスは、その目的と設計を自然に、直感的に拡張したものです。 自分にとって心地よい言葉を選びます。それはユーザーにも心地よい言葉です。

役に立つ方法の 1 つは、アプリの架空のユーザーに話していると想像してみることです。 自分の知っている人、友人や家族、会社の同僚を思い浮かべてください。 このアプリをその人たちにどのように説明しますか。 その機能についてどのように説明しますか。操作の手順をどのように話しますか。 話をするときに主題に合わせてボイスとトーンの変えているように、ライティングでもこのような方法が適切です。

これに対して、まったく異なるアプリを説明する方法を想像してみることも役に立つ場合があります。 ゲームを作っている場合は、財務アプリやニュース アプリを説明するのにどのように話したり、書いたりするかを考えてみてください。 生産性を向上させるアプリを設計している場合、教育アプリについて説明する方法を想像してください。 さまざまなトピックについて話すときにどのような言葉や構造を使っているかを調べることによって、自分が記述しようとしている主題について、新しい見方ができるようになる場合があります。

さらに多くのアイデアを得るには、似たようなアプリを見てインスピレーションを得たり、Web で詳しいアドバイスを検索したりしてください。 適切なボイスを見つけることは多くの人が苦労している問題であるため、適切だと感じるものを決めるのが容易ではない場合も悩まないでください。

## <a name="general-tone-advice-for-uwp-apps"></a>UWP アプリ用のトーンに関する一般的なアドバイス

アプリ内の領域は限られているため、それを上手に使用することが重要です。 アプリで要求されている特定のトーンに関係なく、アプリのテキストを記述するときは、以下の原則を念頭に置くことをお勧めします。

#### <a name="lead-with-whats-important"></a>大切なことから説明する

テキストは、ユーザーが読んで一目で理解できる必要があります。 不要な前置きを付けて単語を長くしないでください。 重要なポイントが最も目立つようにします。常に、アイデアの中核部分を示した後で、説明を追加します。

**適切:** [フィルター] を選択して画像に効果を追加します。

**不適切:** 視覚効果や変更を画像に追加する場合は、[フィルター] を選択します。

#### <a name="clarity-is-key"></a>わかりやすさが重要

対象読者が慣れ親しんでいる言葉を使用してください。 通常、これは日常的な話し言葉を選択することを意味しますが、特殊な用途のアプリには独自の基準があります。 ユーザーがテキストを理解できないという状況は避ける必要があります。そのため、どのようなトーンを使用するか迷う場合は、わかりやすさを優先してください。

**適切:** [設定] を選んで、アプリで写真を保存する方法を変更します。

**不適切:** アプリの既定の動作は、[設定] メニューで構成することができます。

#### <a name="contractions-arent-a-problem"></a>短縮形は問題ない

短縮形は多くのユーザーが慣れ親しんだ、通常使用されている形式です。 短縮形を使わずに記述すると、アプリが堅苦しく、形式ばった印象になります。

**適切:** When you're happy with your image, press "save" to add it to your gallery (画像に問題がなければ、[保存] をクリックしてギャラリーに追加します). From there, you'll be able to share it with friends (ギャラリーから、友人と画像を共有できます).

**不適切:** When you are happy with your image, press "save" to add it to your gallery (画像に問題がなければ、[保存] をクリックしてギャラリーに追加します). From there, you will be able to share it with friends (ギャラリーから、友人と画像を共有できます).

#### <a name="emphasize-action"></a>アクションを強調する

アプリは、アクションによって定義されます。 ユーザーはアプリを使用するときにアクションを実行し、アプリはユーザーに応答するときにアクションを実行します。 アプリ全体のテキストで*能動態*を使用していることを確認します。 ユーザーや機能は、アクションが実行される対象ではなく、アクションを実行するものとして記述する必要があります。

**適切:** アプリを再起動して変更内容を表示します。

**不適切:** アプリが再起動されたときに、変更内容が適用されます。

#### <a name="short-and-sweet"></a>短く、わかりやすく

ユーザーはテキストをざっと見て、多くの場合、より大きな単語のブロック全体をスキップします。 必要な情報やプレゼンテーションを犠牲してはいけませんが、必要以上に語句を使用しないでください。 これは、短い文や語句を多用することを意味する場合もあれば、 長い文で単語や構造を慎重に選ぶことを意味する場合もあります。

**適切:** 申し訳ありませんが、画像をアップロードできませんでした。 もう一度この問題が発生した場合は、アプリを再起動してください。 心配しないでください。再起動すると画像が復元されます。

**不適切:** エラーが発生したため、画像をアップロードできませんでした。 もう一度やり直してください。この問題をもう一度が発生した場合は、アプリを再起動する必要があります。 心配は要りません。作業内容はローカルに保存されており、再起動すると復元されます。
