---
title: インストールされているコード スニペットの一覧の取得 (レガシ) | Microsoft Docs
description: 特定の言語 GUID のすべてのコード スニペットを取得する方法について説明します。 これらのスニペットのショートカットを、IntelliSense の入力候補一覧に挿入できます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- snippets, retrieving list
- code snippets, retrieving list
- GetSnippets method
ms.assetid: 7d142f8b-35b1-44c4-a13e-f89f6460c906
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 051f356e7b6b6f1a92ba475617f48e5c6074f402
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112898875"
---
# <a name="walkthrough-getting-a-list-of-installed-code-snippets-legacy-implementation"></a>チュートリアル: インストールされているコード スニペットの一覧の取得 (従来の実装)
コード スニペットは、ソース バッファーに挿入できるコードの断片です。これは、メニュー コマンドを使用して (インストールされているコード スニペットの一覧から選択して) 行うか、IntelliSense 入力候補一覧からスニペットのショートカットを選択して行います。

 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsExpansionManager.EnumerateExpansions%2A> メソッドは、特定の言語 GUID のすべてのコード スニペットを取得します。 これらのスニペットのショートカットを、IntelliSense の入力候補一覧に挿入できます。

 Managed Package Framework (MPF) 言語サービスでのコード スニペットの実装について、詳しくは「[従来の言語サービスでのコード スニペットのサポート](../../extensibility/internals/support-for-code-snippets-in-a-legacy-language-service.md)」を参照してください。

### <a name="to-retrieve-a-list-of-code-snippets"></a>コード スニペットの一覧を取得するには

1. 次のコードは、特定の言語のコード スニペットの一覧を取得する方法を示しています。 結果は、<xref:Microsoft.VisualStudio.TextManager.Interop.VsExpansion> 構造体の配列に格納されます。 このメソッドは、静的な <xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A> メソッドを使用して、<xref:Microsoft.VisualStudio.TextManager.Interop.SVsTextManager> サービスから <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextManager> インターフェイスを取得します。 ただし、VSPackage に指定されたサービス プロバイダーを使用して <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider.QueryService%2A> メソッドを呼び出すこともできます。

    ```csharp
    using System;
    using System.Collections;
    using System.Runtime.InteropServices;
    using Microsoft.VisualStudio.Package;
    using Microsoft.VisualStudio.Shell;
    using Microsoft.VisualStudio.TextManager.Interop;

    [Guid("00000000-0000-0000-0000-000000000000")] //create a new GUID for the language service
    namespace TestLanguage
    {
        class TestLanguageService : LanguageService
        {
            private void GetSnippets(Guid languageGuid,
                                     ref ArrayList expansionsList)
            {
                IVsTextManager textManager = (IVsTextManager)Package.GetGlobalService(typeof(SVsTextManager));
                if (textManager != null)
                {
                    IVsTextManager2 textManager2 = (IVsTextManager2)textManager;
                    if (textManager2 != null)
                    {
                        IVsExpansionManager expansionManager = null;
                        textManager2.GetExpansionManager(out expansionManager);
                        if (expansionManager != null)
                        {
                            // Tell the environment to fetch all of our snippets.
                            IVsExpansionEnumeration expansionEnumerator = null;
                            expansionManager.EnumerateExpansions(languageGuid,
                            0,     // return all info
                            null,    // return all types
                            0,     // return all types
                            1,     // include snippets without types
                            0,     // do not include duplicates
                            out expansionEnumerator);
                            if (expansionEnumerator != null)
                            {
                                // Cache our expansions in a VsExpansion array
                                uint count   = 0;
                                uint fetched = 0;
                                VsExpansion expansionInfo = new VsExpansion();
                                IntPtr[] pExpansionInfo   = new IntPtr[1];

                                // Allocate enough memory for one VSExpansion structure. This memory is filled in by the Next method.
                                pExpansionInfo[0] = Marshal.AllocCoTaskMem(Marshal.SizeOf(expansionInfo));

                                expansionEnumerator.GetCount(out count);
                                for (uint i = 0; i < count; i++)
                                {
                                    expansionEnumerator.Next(1, pExpansionInfo, out fetched);
                                    if (fetched > 0)
                                    {
                                        // Convert the returned blob of data into a structure that can be read in managed code.
                                        expansionInfo = (VsExpansion)Marshal.PtrToStructure(pExpansionInfo[0], typeof(VsExpansion));

                                        if (!String.IsNullOrEmpty(expansionInfo.shortcut))
                                        {
                                            expansionsList.Add(expansionInfo);
                                        }
                                    }
                                }
                                Marshal.FreeCoTaskMem(pExpansionInfo[0]);
                            }
                        }
                    }
                }
            }
        }
    }
    ```

### <a name="to-call-the-getsnippets-method"></a>GetSnippets メソッドを呼び出すには

1. 次のメソッドは、解析操作の完了時に `GetSnippets` メソッドを呼び出す方法を示しています。 <xref:Microsoft.VisualStudio.Package.LanguageService.OnParseComplete%2A> メソッドは、理由 <xref:Microsoft.VisualStudio.Package.ParseReason> で開始した解析操作の後に呼び出されます。

> [!NOTE]
> パフォーマンス上の理由から、`expansionsList` 配列の一覧はキャッシュされます。 スニペットへの変更は、(たとえば、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] を停止して再起動することによって) 言語サービスを停止して再度読み込むまで、一覧に反映されません。

```csharp
class TestLanguageService : LanguageService
{
    private ArrayList expansionsList;

    public override void OnParseComplete(ParseRequest req)
    {
        if (this.expansionsList == null)
        {
            this.expansionsList = new ArrayList();
            GetSnippets(this.GetLanguageServiceGuid(),
                ref this.expansionsList);
        }
    }
}
```

### <a name="to-use-the-snippet-information"></a>スニペット情報を使用するには

1. 次のコードは、`GetSnippets` メソッドによって返されるスニペット情報の使用方法を示しています。 `AddSnippets` メソッドは、コード スニペットの一覧を事前設定するために使用される解析理由に応答して、パーサーから呼び出されます。 これは、完全な解析が最初に行われた後に発生する必要があります。

     `AddDeclaration` メソッドは、後で入力候補一覧に表示される宣言の一覧を構築します。

     `TestDeclaration` クラスには、宣言の種類に加えて、入力候補一覧に表示できるすべての情報が含まれています。

    ```csharp
    class TestAuthoringScope : AuthoringScope
    {
        public void AddDeclarations(TestDeclaration declaration)
        {
            if (m_declarations == null)
                m_declarations = new List<TestDeclaration>();
            m_declarations.Add(declaration);
         }
    }
    class TestDeclaration
    {
        private string m_name;
        private string m_description;
        private string m_type;

        public TestDeclaration(string name, string desc, string type)
        {
            m_name = name;
            m_description = desc;
            m_type = type;
        }

    class TestLanguageService : LanguageService
    {
        internal void AddSnippets(ref TestAuthoringScope scope)
        {
            if (this.expansionsList != null && this.expansionsList.Count > 0)
            {
                int count = this.expansionsList.Count;
                for (int i = 0; i < count; i++)
                {
                    VsExpansion expansionInfo = (VsExpansion)this.expansionsList[i];
                    scope.AddDeclaration(new TestDeclaration(expansionInfo.title,
                         expansionInfo.description,
                         "snippet"));
                }
            }
        }
    }

    ```

## <a name="see-also"></a>関連項目
- [従来の言語サービスでのコード スニペットのサポート](../../extensibility/internals/support-for-code-snippets-in-a-legacy-language-service.md)
