---
title: プロジェクト サブタイプの初期化シーケンス | Microsoft Docs
description: 複数のプロジェクト サブタイプによって集約されたプロジェクト システム用の Visual Studio 環境での初期化シーケンスについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project subtypes, initialization sequence
ms.assetid: f657f8c3-5e68-4308-9971-e81e3099ba29
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 88a8aa39c513ed6317a6b57509810e16a58f192b
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105069544"
---
# <a name="initialization-sequence-of-project-subtypes"></a>プロジェクト サブタイプの初期化シーケンス
環境では、<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory.CreateProject%2A> の基本プロジェクト ファクトリ実装を呼び出すことによってプロジェクトを構築します。 プロジェクト サブタイプの構築は、プロジェクト ファイルの拡張子のプロジェクト タイプ GUID の一覧が空ではないと環境によって判断された時点で開始します。 プロジェクト ファイル拡張子とプロジェクト GUID により、プロジェクトが [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] と [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] のどちらのプロジェクト タイプであるかが指定されます。 たとえば、.vbproj 拡張子と {F184B08F-C81C-45F6-A57F-5ABD9991F28F} は [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] プロジェクトを識別します。

## <a name="environments-initialization-of-project-subtypes"></a>環境でのプロジェクト サブタイプの初期化
 次の手順では、複数のプロジェクト サブタイプによって集約されたプロジェクト システムの初期化シーケンスについて詳しく説明します。

1. 環境で基本プロジェクトの <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory.CreateProject%2A> が呼び出され、プロジェクトでそのプロジェクト ファイルを解析している間、集約プロジェクト タイプの GUID リストが `null` ではないことが環境によって検出されます。 プロジェクトでは、そのプロジェクトの直接作成を中止します。

2. プロジェクトでは <xref:Microsoft.VisualStudio.Shell.Interop.SVsCreateAggregateProject> サービスに対して `QueryService` を呼び出し、環境での <xref:Microsoft.VisualStudio.Shell.Interop.IVsCreateAggregateProject.CreateAggregateProject%2A> メソッドの実装を使用してプロジェクト サブタイプを作成します。 このメソッド内では、環境によって、最も外側のプロジェクト サブタイプを起点に、プロジェクト タイプ GUID のリストを順次処理しつつ、<xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProjectFactory.PreCreateForOuter%2A>、<xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProject.SetInnerProject%2A>、<xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProject.InitializeForOuter%2A> の各メソッドの実装に対して再帰的な関数呼び出しを行います。

     以下、初期化手順の詳細を示します。

    1. 環境での <xref:Microsoft.VisualStudio.Shell.Interop.IVsCreateAggregateProject.CreateAggregateProject%2A> メソッドの実装により、次の関数宣言を使用して `HrCreateInnerProj` メソッドが呼び出されます。

         \<CodeContentPlaceHolder>0</CodeContentPlaceHolder>

         この関数の最初の (つまり、最も外側のプロジェクト サブタイプに対する) 呼び出し時に、パラメーター `pOuter` と `pOwner` が `null` として渡され、関数は最も外側のプロジェクト サブタイプ `IUnknown` を `pOuter` に設定します。

    2. 次に、環境によって、リスト内の 2 番目のプロジェクト タイプ GUID を使用して `HrCreateInnerProj` 関数が呼び出されます。 この GUID は、集約シーケンスで基本プロジェクトに向かってステップインする、内側から 2 番目のプロジェクト サブタイプに対応します。

    3. この時点で、`pOuter` は最も外側のプロジェクト サブタイプの `IUnknown` を指しており、`HrCreateInnerProj` は <xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProjectFactory.PreCreateForOuter%2A> の実装を呼び出し、続いて <xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProject.SetInnerProject%2A> の実装を呼び出します。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProjectFactory.PreCreateForOuter%2A> メソッドでは、最も外側のプロジェクト サブタイプ `pOuter` の制御側 `IUnknown` を渡します。 被所有プロジェクト (内側のプロジェクト サブタイプ) では、集約プロジェクト オブジェクトをここに作成する必要があります。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProject.SetInnerProject%2A> メソッドの実装では、集約中である内側のプロジェクトの `IUnknown` へのポインターを渡します。 これらの 2 つのメソッドは集計オブジェクトを作成します。実装では、COM の集約ルールに従って、プロジェクト サブタイプが自分自身への参照カウントを保持する結果にならないようにする必要があります。

    4. `HrCreateInnerProj` は <xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProjectFactory.PreCreateForOuter%2A> の実装を呼び出します。 このメソッドでは、プロジェクト サブタイプがその初期化処理を行います。 たとえば、<xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProject.InitializeForOuter%2A> でソリューション イベントを登録できます。

    5. `HrCreateInnerProj` は、リスト内の最後の GUID (基本プロジェクト) に到達するまで再帰的に呼び出されます。 これらの呼び出しごとに、c から d までの手順が繰り返されます。 `pOuter` は、集約の各レベルの最も外側のプロジェクト サブタイプ `IUnknown` を指します。

## <a name="example"></a>例

次の例は、プログラムによるプロセスを、<xref:Microsoft.VisualStudio.Shell.Interop.IVsCreateAggregateProject.CreateAggregateProject%2A> メソッドが環境によって実装される場合の近似表現で詳しく示しています。 このコードは単なる例です。コンパイルは想定されておらず、わかりやすくするためにすべてのエラー チェックを省いています。

```cpp
HRESULT CreateAggregateProject
(
    LPCOLESTR lpstrGuids,
    LPCOLESTR pszFilename,
    LPCOLESTR pszLocation,
    LPCOLESTR pszName,
    VSCREATEPROJFLAGS grfCreateFlags,
    REFIID iidProject,
    void **ppvProject)
{
    HRESULT hr = NOERROR;
    CComPtr<IUnknown> srpunkProj;
    CComPtr<IVsAggregatableProject> srpAggProject;
    CComBSTR bstrGuids = lpstrGuids;
    BOOL fCanceled = FALSE;
    *ppvProject = NULL;

    HrCreateInnerProj(
         bstrGuids, NULL, NULL, pszFilename, pszLocation,
         pszName, grfCreateFlags, &srpunkProj, &fCanceled);
    srpunkProj->QueryInterface(
        IID_IVsAggregatableProject, (void **)&srpAggProject));
    srpAggProject->OnAggregationComplete();
    srpunkProj->QueryInterface(iidProject, ppvProject);
}

HRESULT HrCreateInnerProj
(
    WCHAR *pwszGuids,
    IUnknown *pOuter,
    IVsAggregatableProject *pOwner,
    LPCOLESTR pszFilename,
    LPCOLESTR pszLocation,
    LPCOLESTR pszName,
    VSCREATEPROJFLAGS grfCreateFlags,
    IUnknown **ppInner,
    BOOL *pfCanceled
)
{
    HRESULT hr = NOERROR;
    CComPtr<IUnknown> srpInner;
    CComPtr<IVsAggregatableProject> srpAggInner;
    CComPtr<IVsProjectFactory> srpProjectFactory;
    CComPtr<IVsAggregatableProjectFactory> srpAggPF;
    GUID guid = GUID_NULL;
    WCHAR *pwszNextGuids = wcschr(pwszGuids, L';');
    WCHAR wszText[_MAX_PATH+150] = L"";

    if (pwszNextGuids)
    {
        *pwszNextGuids++ = 0;
    }

    CLSIDFromString(pwszGuids, &guid);
    GetProjectTypeMgr()->HrGetProjectFactoryOfGuid(
        guid, &srpProjectFactory);
    srpProjectFactory->QueryInterface(
        IID_IVsAggregatableProjectFactory,
        (void **)&srpAggPF);
    srpAggPF->PreCreateForOuter(pOuter, &srpInner);
    srpInner->QueryInterface(
        IID_IVsAggregatableProject, (void **)&srpAggInner);

    if (pOwner)
    {
        IfFailGo(pOwner->SetInnerProject(srpInner));
    }

    if (pwszNextGuids)
    {
        CComPtr<IUnknown> srpNextInner;
        HrCreateInnerProj(
            pwszNextGuids, pOuter ? pOuter : srpInner,
            srpAggInner, pszFilename, pszLocation, pszName,
            grfCreateFlags, &srpNextInner, pfCanceled);
    }

    return srpAggInner->InitializeForOuter(
        pszFilename, pszLocation, pszName, grfCreateFlags,
        IID_IUnknown, (void **)ppInner, pfCanceled);
}
```

## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualStudio.Shell.Flavor>
- [プロジェクト サブタイプ](../../extensibility/internals/project-subtypes.md)
