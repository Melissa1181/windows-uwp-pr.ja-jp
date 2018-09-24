---
author: stevewhims
description: C++/WinRT 機能と、多くの時間と労力を実装やコレクションに合格するときに保存する基底クラスを提供します。
title: コレクション、C++/WinRT
ms.author: stwhi
ms.date: 08/24/2018
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: windows 10、uwp、標準、c++、cpp、winrt、プロジェクション、コレクション
ms.localizationpriority: medium
ms.openlocfilehash: 1ef6fbfab45197c868296186363c168a6c443247
ms.sourcegitcommit: a160b91a554f8352de963d9fa37f7df89f8a0e23
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/21/2018
ms.locfileid: "4126347"
---
# <a name="collections-with-cwinrtwindowsuwpcpp-and-winrt-apisintro-to-using-cpp-with-winrt"></a>コレクションと[、C++/WinRT](/windows/uwp/cpp-and-winrt-apis/intro-to-using-cpp-with-winrt)

> [!NOTE]
> **一部の情報はリリース前の製品に関する事項であり、正式版がリリースされるまでに大幅に変更される可能性があります。 ここに記載された情報について、Microsoft は明示または黙示を問わずいかなる保証をするものでもありません。**

内部では、Windows ランタイムのコレクションでは、単純な移動部分の多くがあります。 コレクション オブジェクトを Windows ランタイム関数に渡すか、独自のコレクションのプロパティとコレクション型を実装する場合は、関数と基底クラスでは、C++/WinRT をサポートします。 これらの機能は、手の複雑さを解消し、時間と労力で、多くのオーバーヘッドを保存します。

> [!IMPORTANT]
> このトピックで説明されている機能は、 [Windows 10 SDK プレビュー ビルド 17661](https://www.microsoft.com/software-download/windowsinsiderpreviewSDK)をインストールした場合に利用可能な以降できます。

[**IVector**](/uwp/api/windows.foundation.collections.ivector_t_)は、要素の任意のランダム アクセス コレクションによって実装された Windows ランタイム インターフェイスです。 **IVector**を実装する場合は、 [**IIterable**](/uwp/api/windows.foundation.collections.iiterable_t_)、 [**IVectorView**](/uwp/api/windows.foundation.collections.ivectorview_t_)、 [**IIterator**](/uwp/api/windows.foundation.collections.iiterator_t_)を実装する必要がありますがも。 入力する*必要がある*カスタム コレクション場合でも、多くの作業です。 **Std::vector** ( **std::map**、または**std::unordered_map**) 内のデータがあり、Windows ランタイム API に渡すことがすべて実行する場合、必要しますが、あるが可能であれば、作業のレベルを避けるため。 回避すること*は*できる限り、ためと、C++/WinRT では、わずかな労力で効率的にし、コレクションを作成できます。

## <a name="helper-functions-for-collections"></a>コレクションのヘルパー関数

### <a name="general-purpose-collection-empty"></a>空の汎用的なコレクション

汎用的なコレクションを実装する型の新しいオブジェクトを取得するには、 [**winrt::single_threaded_vector**](/uwp/cpp-ref-for-winrt/single-threaded-vector)関数テンプレートを呼び出すことができます。 [**IVector**](/uwp/api/windows.foundation.collections.ivector_t_)の場合、としてオブジェクトが返され、これによって、返されるオブジェクトの関数とプロパティを呼び出すインターフェイスが。

```cppwinrt
...
#include <winrt/Windows.Foundation.Collections.h>
#include <iostream>
using namespace winrt;
...
int main()
{
    init_apartment();

    Windows::Foundation::Collections::IVector<int> coll{ winrt::single_threaded_vector<int>() };
    coll.Append(1);
    coll.Append(2);
    coll.Append(3);

    for (auto const& el : coll)
    {
        std::cout << el << std::endl;
    }

    Windows::Foundation::Collections::IVectorView<int> view{ coll.GetView() };
}
```

上記のコード例で示すように、コレクションを作成した後の要素を追加、反復処理し、して一般 API から受信したすべての Windows ランタイム コレクション オブジェクトと同様に、オブジェクトを扱うできます。 コレクションを固定表示が必要な場合に示す[**IVector::GetView**](/uwp/api/windows.foundation.collections.ivector-1.getview)を呼び出すことができます。 前に示したパターン&mdash;のコレクションの作成と&mdash;が、データを渡すか、API からデータを取得する単純なシナリオに適しています。 **IVector**の場合、または、 **IVectorView**に渡すことができます、任意の場所、 [**IIterable**](/uwp/api/windows.foundation.collections.iiterable_t_)に期待されます。

### <a name="general-purpose-collection-primed-from-data"></a>データから先読み汎用のコレクション

また上記のコード例で表示される**追加**の呼び出しのオーバーヘッドを回避できます。 ソースのデータが既にまたは Windows ランタイムのコレクション オブジェクトを作成する前に設定することができます。 その方法を以下に示します。

```cppwinrt
auto coll1{ winrt::single_threaded_vector<int>({ 1,2,3 }) };

std::vector<int> values{ 1,2,3 };
auto coll2{ winrt::single_threaded_vector<int>(std::move(values)) };

for (auto const& el : coll2)
{
    std::cout << el << std::endl;
}
```

**Winrt::single_threaded_vector**にデータを含む一時オブジェクトを渡すことができますと同様に`coll1`額。 **Std::vector** (されませんにアクセスして、もう一度と仮定します) を移動するか、関数にします。 どちらの場合も、関数に、*右辺値*を渡しています。 これにより、効率的にして、データのコピーを回避するために、コンパイラができます。 *Rvalue*について詳しく知りたい場合は、[値のカテゴリとへの参照](cpp-value-categories.md)を参照してください。

XAML アイテム コントロールをコレクションにバインドする場合は、そのできます。 ただし、 [**ItemsControl.ItemsSource**](/uwp/api/windows.ui.xaml.controls.itemscontrol.itemssource)プロパティを正しく設定する必要が型の**IVector** **IInspectable** (または、相互運用性の種類[**IBindableObservableVector**](/uwp/api/windows.ui.xaml.interop.ibindableobservablevector)など) の値に設定に注意してください。 バインディング用の適切な種類のコレクションを作成して要素を追加するコード例を以下に示します。

```cppwinrt
auto bookSkus{ winrt::single_threaded_vector<Windows::Foundation::IInspectable>() };
bookSkus.Append(make<Bookstore::implementation::BookSku>(L"Moby Dick"));
```

データから、Windows ランタイムのコレクションを作成し、何かをコピーすることがなくすべての API に渡すことでビューを準備できます。

```cppwinrt
std::vector<float> values{ 0.1f, 0.2f, 0.3f };
IVectorView<float> view{ winrt::single_threaded_vector(std::move(values)).GetView() };
```

上記の例では、コレクションを作成*できます*にバインドする XAML アイテム コントロールです。コレクションが監視可能なはありません。

### <a name="observable-collection"></a>監視可能なコレクション

*監視可能な*コレクションを実装する型の新しいオブジェクトを取得するには、任意の要素型と[**winrt::single_threaded_observable_vector**](/uwp/cpp-ref-for-winrt/single-threaded-observable-vector)関数テンプレートを呼び出します。 監視可能なコレクションを XAML アイテム コントロールへのバインドに適したするには、要素の型として**IInspectable**を使用します。

[**IObservableVector**](/uwp/api/windows.foundation.collections.iobservablevector_t_)の場合、として、オブジェクトが返され、はインターフェイスを経由する (またはバインドされているコントロール)、返されるオブジェクトの関数とプロパティを呼び出します。

```cppwinrt
auto bookSkus{ winrt::single_threaded_observable_vector<Windows::Foundation::IInspectable>() };
```

詳細の詳細とコード例では、ユーザーのバインディングに関するインターフェイス (UI) を制御監視可能なコレクションには、「 [XAML アイテム コントロール: c++ へのバインド/WinRT コレクション](binding-collection.md)します。

### <a name="associative-collection-map"></a>連想コレクション (マップ)

説明した 2 つの関数のバージョンを連想コレクションがあります。

- [**Winrt::single_threaded_map**](/uwp/cpp-ref-for-winrt/single-threaded-map)関数テンプレートは、 [**IMap**](/uwp/api/windows.foundation.collections.imap_k_v_)として監視可能な非連想コレクションを返します。
- [**Winrt::single_threaded_observable_map**](/uwp/cpp-ref-for-winrt/single-threaded-observable-map)関数テンプレートは、 [**IObservableMap**](/uwp/api/windows.foundation.collections.iobservablemap_k_v_)として監視可能な連想コレクションを返します。

型**std::map**または**std::unordered_map**の*右辺値*関数に渡すことによってこれらのコレクションにデータを必要に応じて素数ことができます。

```cppwinrt
auto coll1{
    winrt::single_threaded_map<winrt::hstring, int>(std::map<winrt::hstring, int>{
        { L"AliceBlue", 0xfff0f8ff }, { L"AntiqueWhite", 0xfffaebd7 }
    })
};

std::map<winrt::hstring, int> values{
    { L"AliceBlue", 0xfff0f8ff }, { L"AntiqueWhite", 0xfffaebd7 }
};
auto coll2{ winrt::single_threaded_map<winrt::hstring, int>(std::move(values)) };
```

### <a name="single-threaded"></a>シングル スレッド

「シングル スレッド」これらの関数の名前には、すべての同時実行を提供しないことを示します&mdash;スレッド セーフが不明、つまり、します。 スレッドの言及は、これらの関数から返されたオブジェクトはすべてアジャイルであるために、アパートメントに関連する (を参照してください[アジャイル オブジェクトでは、C++/WinRT](agile-objects.md))。 オブジェクトは、シングル スレッドですだけです。 する方が適切な方法の 1 つのデータや他のアプリケーション バイナリ インターフェイス (ABI) に通過する場合。

## <a name="base-classes-for-collections"></a>コレクションの基本クラス

場合は、完全な柔軟性は、独自のカスタム コレクションを実装する、ありますハード方法は、これを回避するために必要があります。 たとえば、これは、ベクトルのカスタム ビューがどのように *、C++ のサポートなし/WinRT の基底クラス*します。

```cppwinrt
...
using namespace winrt;
using namespace Windows::Foundation::Collections;
...
struct MyVectorView :
    implements<MyVectorView, IVectorView<float>, IIterable<float>>
{
    // IVectorView
    float GetAt(uint32_t const) { ... };
    uint32_t GetMany(uint32_t, winrt::array_view<float>) const { ... };
    bool IndexOf(float, uint32_t&) { ... };
    uint32_t Size() { ... };

    // IIterable
    IIterator<float> First() const { ... };
};
...
IVectorView<float> view{ winrt::make<MyVectorView>() };
```

代わりに、カスタム ベクトルのビューを[**winrt::vector_view_base**](/uwp/cpp-ref-for-winrt/vector-view-base)構造体のテンプレートから派生し、データを保持するコンテナーを公開する**get_container**関数を実装するはるかに簡単です。

```cppwinrt
struct MyVectorView2 :
    implements<MyVectorView2, IVectorView<float>, IIterable<float>>,
    winrt::vector_view_base<MyVectorView2, float>
{
    auto& get_container() const noexcept
    {
        return m_values;
    }

private:
    std::vector<float> m_values{ 0.1f, 0.2f, 0.3f };
};
```

**Get_container**によって返されるコンテナーするその**winrt::vector_view_base** **開始**と**終了**のインターフェイスを提供する必要がありますが想定されます。 上記の例のように、 **std::vector**を提供します。 ただし、独自のカスタム コンテナーを含む、同じコントラクトを満たすすべてのコンテナーを返すことができます。

```cppwinrt
struct MyVectorView3 :
    implements<MyVectorView3, IVectorView<float>, IIterable<float>>,
    winrt::vector_view_base<MyVectorView3, float>
{
    auto get_container() const noexcept
    {
        struct container
        {
            float const* const first;
            float const* const last;

            auto begin() const noexcept
            {
                return first;
            }

            auto end() const noexcept
            {
                return last;
            }
        };

        return container{ m_values.data(), m_values.data() + m_values.size() };
    }

private:
    std::array<float, 3> m_values{ 0.2f, 0.3f, 0.4f };
};
```

これらは、基底クラス C + + WinRT がカスタム コレクションを実装するために提供します。

### [<a name="winrtvectorviewbase"></a>winrt::vector_view_base](/uwp/cpp-ref-for-winrt/vector-view-base)

上記のコード例を参照してください。

### [<a name="winrtvectorbase"></a>winrt::vector_base](/uwp/cpp-ref-for-winrt/vector-base)

```cppwinrt
struct MyVector :
    implements<MyVector, IVector<float>, IVectorView<float>, IIterable<float>>,
    winrt::vector_base<MyVector, float>
{
    auto& get_container() const noexcept
    {
        return m_values;
    }

    auto& get_container() noexcept
    {
        return m_values;
    }

private:
    std::vector<float> m_values{ 0.1f, 0.2f, 0.3f };
};
```

### [<a name="winrtobservablevectorbase"></a>winrt::observable_vector_base](/uwp/cpp-ref-for-winrt/observable-vector-base)

```cppwinrt
struct MyObservableVector :
    implements<MyObservableVector, IObservableVector<float>, IVector<float>, IVectorView<float>, IIterable<float>>,
    winrt::observable_vector_base<MyObservableVector, float>
{
    auto& get_container() const noexcept
    {
        return m_values;
    }

    auto& get_container() noexcept
    {
        return m_values;
    }

private:
    std::vector<float> m_values{ 0.1f, 0.2f, 0.3f };
};
```

### [<a name="winrtmapviewbase"></a>winrt::map_view_base](/uwp/cpp-ref-for-winrt/map-view-base)

```cppwinrt
struct MyMapView :
    implements<MyMapView, IMapView<winrt::hstring, int>, IIterable<IKeyValuePair<winrt::hstring, int>>>,
    winrt::map_view_base<MyMapView, winrt::hstring, int>
{
    auto& get_container() const noexcept
    {
        return m_values;
    }

private:
    std::map<winrt::hstring, int> m_values{
        { L"AliceBlue", 0xfff0f8ff }, { L"AntiqueWhite", 0xfffaebd7 }
    };
};
```

### [<a name="winrtmapbase"></a>winrt::map_base](/uwp/cpp-ref-for-winrt/map-base)

```cppwinrt
struct MyMap :
    implements<MyMap, IMap<winrt::hstring, int>, IMapView<winrt::hstring, int>, IIterable<IKeyValuePair<winrt::hstring, int>>>,
    winrt::map_base<MyMap, winrt::hstring, int>
{
    auto& get_container() const noexcept
    {
        return m_values;
    }

    auto& get_container() noexcept
    {
        return m_values;
    }

private:
    std::map<winrt::hstring, int> m_values{
        { L"AliceBlue", 0xfff0f8ff }, { L"AntiqueWhite", 0xfffaebd7 }
    };
};
```

### [<a name="winrtobservablemapbase"></a>winrt::observable_map_base](/uwp/cpp-ref-for-winrt/observable-map-base)

```cppwinrt
struct MyObservableMap :
    implements<MyObservableMap, IObservableMap<winrt::hstring, int>, IMap<winrt::hstring, int>, IMapView<winrt::hstring, int>, IIterable<IKeyValuePair<winrt::hstring, int>>>,
    winrt::observable_map_base<MyObservableMap, winrt::hstring, int>
{
    auto& get_container() const noexcept
    {
        return m_values;
    }

    auto& get_container() noexcept
    {
        return m_values;
    }

private:
    std::map<winrt::hstring, int> m_values{
        { L"AliceBlue", 0xfff0f8ff }, { L"AntiqueWhite", 0xfffaebd7 }
    };
};
```

## <a name="important-apis"></a>重要な API
* [ItemsControl.ItemsSource プロパティ](/uwp/api/windows.ui.xaml.controls.itemscontrol.itemssource)
* [IObservableVector インターフェイス](/uwp/api/windows.foundation.collections.iobservablevector_t_)
* [IVector インターフェイス](/uwp/api/windows.foundation.collections.ivector_t_)
* [winrt::map_base 構造体テンプレート](/uwp/cpp-ref-for-winrt/map-base)
* [winrt::map_view_base 構造体テンプレート](/uwp/cpp-ref-for-winrt/map-view-base)
* [winrt::observable_map_base 構造体テンプレート](/uwp/cpp-ref-for-winrt/observable-map-base)
* [winrt::observable_vector_base 構造体テンプレート](/uwp/cpp-ref-for-winrt/observable-vector-base)
* [winrt::single_threaded_observable_map 関数テンプレート](/uwp/cpp-ref-for-winrt/single-threaded-observable-map)
* [winrt::single_threaded_map 関数テンプレート](/uwp/cpp-ref-for-winrt/single-threaded-map)
* [winrt::single_threaded_observable_vector 関数テンプレート](/uwp/cpp-ref-for-winrt/single-threaded-observable-vector)
* [winrt::single_threaded_vector 関数テンプレート](/uwp/cpp-ref-for-winrt/single-threaded-vector)
* [winrt::vector_base 構造体テンプレート](/uwp/cpp-ref-for-winrt/vector-base)
* [winrt::vector_view_base 構造体テンプレート](/uwp/cpp-ref-for-winrt/vector-view-base)

## <a name="related-topics"></a>関連トピック
* [値のカテゴリとへの参照](cpp-value-categories.md)
* [XAML アイテム コントロール: C++/WinRT コレクションへのバインド](binding-collection.md)