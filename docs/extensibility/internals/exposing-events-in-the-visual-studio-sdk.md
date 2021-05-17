---
title: Visual studio SDK でのイベントの公開 | Microsoft Docs
description: プロジェクトとプロジェクト項目のイベントを公開する、Visual Studio SDK のメソッドとレジストリ エントリについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- events [Visual Studio], exposing
- automation [Visual Studio SDK], exposing events
ms.assetid: 70bbc258-c221-44f8-b0d7-94087d83b8fe
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 019efb11d7a31af875425888a1f70423bca76ca9
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105069804"
---
# <a name="expose-events-in-the-visual-studio-sdk"></a>Visual Studio SDK でイベントを公開する
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] では、オートメーションを使用してイベントをソース化できます。 プロジェクトとプロジェクト項目のイベントは、ソース化することをお勧めします。

 イベントは、オートメーション コンシューマーによって <xref:EnvDTE.DTEClass.Events%2A> オブジェクトまたは <xref:EnvDTE.DTEClass.GetObject%2A> (`GetObject("EventObjectName")` など) から取得されます。 環境により、`DISPATCH_METHOD` または `DISPATCH_PROPERTYGET` フラグを使用して `IDispatch::Invoke` が呼び出され、イベントが返されます。

 次のプロセスでは、VSPackage 固有のイベントがどのように返されるかを説明します。

1. 環境が起動します。

2. このメソッドは、すべての VSPackage の **Automation**、 **AutomationEvents**、および **AutomationProperties** キーの下にあるすべての値名をレジストリから読み取り、それらの名前をテーブルに格納します。

3. オートメーション コンシューマーは、この例では、`DTE.Events.AutomationProjectsEvents` または `DTE.Events.AutomationProjectItemsEvents` を呼び出します。

4. 環境により、テーブル内の文字列パラメーターが検出され、それに対応する VSPackage が読み込まれます。

5. 環境により、<xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetAutomationObject%2A> 呼び出しで渡される名前 (この例では、`AutomationProjectsEvents` または `AutomationProjectItemsEvents`) を使用してメソッドが呼び出されます。

6. VSPackage は、`get_AutomationProjectsEvents` や `get_AutomationProjectItemEvents` などのメソッドを含むルート オブジェクトを作成し、このオブジェクトに IDispatch ポインターを返します。

7. オートメーション呼び出しに渡された名前に基づいて、適切なメソッドが環境によって呼び出されます。

8. `get_` メソッドは、`IConnectionPointContainer` インターフェイスと `IConnectionPoint` インターフェイスの両方を実装する別の IDispatch ベースのイベント オブジェクト を作成し、このオブジェクトに `IDispatchpointer` を返します。

   オートメーションを使用してイベントを公開するには、<xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetAutomationObject%2A> に応答し、レジストリに追加する文字列を監視する必要があります。 基本的なプロジェクトのサンプルでは、この文字列は *BscProjectsEvents* と *BscProjectItemsEvents* です。

## <a name="registry-entries-from-the-basic-project-sample"></a>基本的なプロジェクトのサンプルのレジストリ エントリ
 ここでは、オートメーション イベントの値を、レジストリのどこに追加するかを示します。

 **[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0\Packages\\&lt;PkgGUID \> \AutomationEvents]**

 **AutomationProjectEvents** = `AutomationProjectEvents` オブジェクトを返します。

 **AutomationProjectItemEvents** = `AutomationProjectItemsEvents` オブジェクトを返します。

|名前|Type|Range|説明|
|----------|----------|-----------|-----------------|
|既定値 (@)|REG_SZ|未使用|未使用。 データ フィールドをドキュメントに使用できます。|
|*AutomationProjectsEvents*|REG_SZ|イベント プロジェクトの名前。|キー名のみが関連しています。 データ フィールドをドキュメントに使用できます。<br /><br /> この例は、基本的なプロジェクトのサンプルから取得したものです。|
|*AutomationProjectItemEvents*|REG_SZ|イベント プロジェクトの名前|キー名のみが関連しています。 データ フィールドをドキュメントに使用できます。<br /><br /> この例は、基本的なプロジェクトのサンプルから取得したものです。|

 いずれかのイベント オブジェクトがオートメーション コンシューマーによって要求された場合は、VSPackage がサポートするいずれかのイベントのメソッドを含むルート オブジェクトを作成してください。 環境により、このオブジェクトの適切な `get_` メソッドが呼び出されます。 たとえば、`DTE.Events.AutomationProjectsEvents` が呼び出されると、ルート オブジェクトの `get_AutomationProjectsEvents` メソッドが呼び出されます。

 ![Visual Studio プロジェクトのイベント](../../extensibility/internals/media/projectevents.gif "ProjectEvents") イベントのオートメーション モデル

 クラス `CProjectEventsContainer` は、*BscProjectsEvents* のソース オブジェクトを表し、`CProjectItemsEventsContainer` は、*BscProjectItemsEvents* のソース オブジェクトを表します。

 ほとんどのイベント オブジェクトはフィルター オブジェクトを受け取るため、ほとんどの場合、すべてのイベント要求に対して新しいオブジェクトを返す必要があります。 イベントを発生させるときは、このフィルターを調べて、イベント ハンドラーが呼び出されていることを確認します。

 *AutomationEvents.h* と *AutomationEvents.cpp* には、次の表に示すクラスの宣言と実装が含まれています。

|クラス|説明|
|-----------|-----------------|
|`CAutomationEvents`|`DTE.Events` オブジェクトから取得されたイベント ルート オブジェクトを実装します。|
|`CProjectsEventsContainer` および `CProjectItemsEventsContainer`|対応するイベントを発生させるイベント ソース オブジェクトを実装します。|

 次のコード例は、イベント オブジェクトの要求に応答する方法を示しています。

```cpp
STDMETHODIMP CVsPackage::GetAutomationObject(
    /* [in]  */ LPCOLESTR       pszPropName,
    /* [out] */ IDispatch **    ppIDispatch)
{
    ExpectedPtrRet(ppIDispatch);
    *ppIDispatch = NULL;

    if (_wcsicmp(pszPropName, g_wszAutomationProjects) == 0)
        //Is the requested name our Projects object?
    {
        return GetAutomationProjects(ppIDispatch);
        // Gets our Projects object.
    }
    else if (_wcsicmp(pszPropName, g_wszAutomationProjectsEvents) == 0)
        //Is the requested name our ProjectsEvents object?
    {
        return CAutomationEvents::GetAutomationEvents(ppIDispatch);
          // Gets our ProjectEvents object.
    }
    else if (_wcsicmp(pszPropName, g_wszAutomationProjectItemsEvents) == 0)  //Is the requested name our ProjectsItemsEvents object?
    {
        return CAutomationEvents::GetAutomationEvents(ppIDispatch);
          // Gets our ProjectItemsEvents object.
    }
    return E_INVALIDARG;
}
```

 上記のコードで `g_wszAutomationProjects` は、プロジェクト コレクション (*FigProjects*) の名前であり、`g_wszAutomationProjectsEvents` (*FigProjectsEvents*) および `g_wszAutomationProjectItemsEvents` (*FigProjectItemEvents*) は、VSPackage 実装からソース化されるプロジェクト イベントとプロジェクト項目イベントの名前です。

 イベント オブジェクトは、同じ中央の場所である `DTE.Events` オブジェクトから取得されます。 これにより、すべてのイベント オブジェクトがグループ化されるため、特定のイベントを検索するためにエンド ユーザーがオブジェクト モデル全体を参照する必要がなくなります。 これにより、システム全体のイベント用に独自のコードを実装する代わりに、特定の VSPackage オブジェクトを提供することが可能になります。 ただし、`ProjectItem` インターフェイスのイベントを検索する必要があるエンド ユーザーは、そのイベント オブジェクトの取得元がすぐにはわかりません。

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetAutomationObject%2A>
