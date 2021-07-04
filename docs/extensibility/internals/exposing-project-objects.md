---
title: プロジェクト オブジェクトの公開 | Microsoft Docs
description: オートメーション インターフェイスを使用してプロジェクトにアクセスできるオートメーション オブジェクトを提供することによって、Visual Studio でカスタム プロジェクト タイプのオブジェクトを公開する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- project objects, exposing
- extensibility, project objects
ms.assetid: 5bb24967-434a-4ef4-87a0-2f3250c9e22d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: c3e89b4c80d64bedb77e68c648ba993794f8b658
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112898293"
---
# <a name="expose-project-objects"></a>プロジェクト オブジェクトの公開

カスタム プロジェクト タイプでは、オートメーション インターフェイスを使用してプロジェクトにアクセスできるようにするために、オートメーションオブジェクトを提供できます。 すべてのプロジェクト タイプは、<xref:EnvDTE.Solution> からアクセスされる標準の <xref:EnvDTE.Project> オートメーション オブジェクトを提供することが想定されています。このオブジェクトには、IDE で開いているすべてのプロジェクトのコレクションが含まれています。 プロジェクト内の各項目は、`Project.ProjectItems` を使用してアクセスされる <xref:EnvDTE.ProjectItem> オブジェクトによって公開されることが想定されています。 これらの標準オートメーション オブジェクトに加えて、プロジェクトではプロジェクト固有のオートメーション オブジェクトを提供することを選択できます。

`DTE.<customObjectName>` または `DTE.GetObject("<customObjectName>")` を使用してルート DTE オブジェクトから遅延バインディングにアクセスできる、カスタムのルートレベル オートメーション オブジェクトを作成できます。 たとえば、Visual C++ では、`DTE.VCProjects` または `DTE.GetObject("VCProjects")` を使用してアクセスできる *VCProjects* という C++ プロジェクト固有のプロジェクト コレクションを作成します。 プロジェクト タイプに対して一意である `Project.Object`、最派生オブジェクトに対してクエリを実行できる `Project.CodeModel`、および `ProjectItem.Object` や `ProjectItem.FileCodeModel` を公開する `ProjectItem` を作成することもできます。

一般的な規則として、プロジェクトではプロジェクト固有のカスタム プロジェクト コレクションを公開します。 たとえば、[!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] では、`DTE.VCProjects` または `DTE.GetObject("VCProjects")` を使用してアクセスできる C++ 固有のプロジェクト コレクションを作成します。 プロジェクト タイプに対して一意である `Project.Object`、最派生オブジェクトに対してクエリを実行できる `Project.CodeModel`、`ProjectItem.Object` を公開する `ProjectItem`、および `ProjectItem.FileCodeModel` を作成することもできます。

## <a name="to-contribute-a-vspackage-specific-object-for-a-project"></a>プロジェクトの VSPackage 固有のオブジェクトを投稿するには

1. VSPackage の *.pkgdef* ファイルに適切なキーを追加します。

     たとえば、C++ 言語プロジェクトの *.pkgdef* 設定を次に示します。

    ```
    [$RootKey$\Packages\{F1C25864-3097-11D2-A5C5-00C04F7968B4}\Automation]
    "VCProjects"=""
    [$RootKey$\Packages\{F1C25864-3097-11D2-A5C5-00C04F7968B4}\AutomationEvents]
    "VCProjectEngineEventsObject"=""
    ```

2. 次の例に示すように、<xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetAutomationObject%2A> メソッドのコードを実装します。

    ```cpp
    STDMETHODIMP CVsPackage::GetAutomationObject(
    /* [in]  */ LPCOLESTR       pszPropName,
    /* [out] */ IDispatch **    ppIDispatch)
    {
    ExpectedPtrRet(pszPropName);
    ExpectedPtrRet(ppIDispatch);
    *ppIDispatch = NULL;

        if (m_fZombie)
            return E_UNEXPECTED;

        if (_wcsicmp(pszPropName, g_wszAutomationProjects) == 0)
        {
            return GetAutomationProjects(ppIDispatch);
        }
        else if (_wcsicmp(pszPropName, g_wszAutomationProjectsEvents) == 0)
        {
            return CAutomationEvents::GetAutomationEvents(ppIDispatch);
        }
        else if (_wcsicmp(pszPropName, g_wszAutomationProjectItemsEvents) == 0)
        {
            return CAutomationEvents::GetAutomationEvents(ppIDispatch);
        }
        return E_INVALIDARG;
    }
    ```

     コードで、`g_wszAutomationProjects` はプロジェクト コレクションの名前です。 次のコード例に示すように、`GetAutomationProjects` メソッドは、`Projects` インターフェイスを実装するオブジェクトを作成し、呼び出し元オブジェクトへの `IDispatch` ポインターを返します。

    ```cpp
    HRESULT CVsPackage::GetAutomationProjects(/* [out] */ IDispatch ** ppIDispatch)
    {
        ExpectedPtrRet(ppIDispatch);
        *ppIDispatch = NULL;

        if (!m_srpAutomationProjects)
        {
            HRESULT hr = CACProjects::CreateInstance(&m_srpAutomationProjects);
            IfFailRet(hr);
            ExpectedExprRet(m_srpAutomationProjects != NULL);
        }
        return m_srpAutomationProjects.CopyTo(ppIDispatch);
    }
    ```

     オートメーション オブジェクトの一意の名前を選択します。 名前の競合は予測できません。また、複数のプロジェクト タイプで同じ名前を使用している場合は、競合するオブジェクト名が任意にスローされます。 オートメーション オブジェクトの名前には、企業名、またはその製品名に固有の特徴を含める必要があります。

     カスタム `Projects` コレクション オブジェクトは、プロジェクト オートメーション モデルの残りの部分に対する便利なエントリ ポイントです。 プロジェクト オブジェクトは、<xref:EnvDTE.Solution> プロジェクト コレクションからアクセスすることもできます。 コンシューマーに `Projects` コレクション オブジェクトを提供する適切なコードとレジストリ エントリを作成したら、実装でプロジェクト モデルの残りの標準オブジェクトを提供する必要があります。 詳細については、「[プロジェクトのモデリング](../../extensibility/internals/project-modeling.md)」を参照してください。

## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetAutomationObject%2A>
