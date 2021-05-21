---
title: 従来の言語サービスの登録 1 | Microsoft Docs
description: レジストリ キーとエントリを追加して、Visual Studio で VSPackage から従来の言語サービスを登録する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- language services [managed package framework], registering
ms.assetid: d33b08af-09e0-4c79-87b2-5536b27fbacf
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: d5fa94fbd514e5fb162bc569438197dd8c65444b
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105060771"
---
# <a name="registering-a-legacy-language-service-1"></a>従来の言語サービスの登録 1
Managed Package Framework (MPF) では、言語サービスは VSPackage で提供されており (「[VSPackages ](../../extensibility/internals/vspackages.md)」を参照してください)、レジストリ キーとエントリを追加して [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] に登録します。 この登録プロセスは、一部はインストール時に、一部は実行時に実行されます。

## <a name="register-the-language-service-by-using-attributes"></a>属性を使用して言語サービスを登録する
 言語サービスの登録には、次の属性を使用します。

- <xref:Microsoft.VisualStudio.Shell.ProvideServiceAttribute>

- <xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute>

- <xref:Microsoft.VisualStudio.Shell.ProvideLanguageExtensionAttribute>

- <xref:Microsoft.VisualStudio.Shell.ProvideLanguageCodeExpansionAttribute>

- <xref:Microsoft.VisualStudio.Shell.ProvideLanguageEditorOptionPageAttribute>

  これらの属性については、以下で説明します

### <a name="provideserviceattribute"></a>ProvideServiceAttribute
 この属性を使用すると、言語サービスをサービスとして登録できます。

### <a name="example"></a>例

```csharp
using Microsoft.VisualStudio.Shell;

namespace TestLanguagePackage
{
    [ProvideServiceAttribute(typeof(TestLanguageService),
                             ServiceName = "Test Language Service")]

    public class TestLanguagePackage : Package
    {
    }
}
```

### <a name="providelanguageserviceattribute"></a>ProvideLanguageServiceAttribute
 この属性を使用すると、言語サービスを言語サービスとして明示的に登録できます。 言語サービスで提供する機能を指定するオプションを設定できます。 この例は、言語サービスで提供できるオプションのサブセットを示しています。 言語サービス オプションの完全なセットについては、「<xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute>」を参照してください。

### <a name="example"></a>例

```csharp
using Microsoft.VisualStudio.Shell;

namespace TestLanguagePackage
{
    [ProvideLanguageServiceAttribute(typeof(TestLanguageService),
                             "Test Language",
                             106,             // resource ID of localized language name
                             CodeSense = true,             // Supports IntelliSense
                             RequestStockColors = false,   // Supplies custom colors
                             EnableCommenting = true,      // Supports commenting out code
                             EnableAsyncCompletion = true  // Supports background parsing
                             )]

    public class TestLanguagePackage : Package
    {
    }
}
```

### <a name="providelanguageextensionattribute"></a>ProvideLanguageExtensionAttribute
 この属性を使用すると、言語サービスをファイル拡張子に関連付けることができます。 どのプロジェクトでも、その拡張子を持つファイルが読み込まれるたびに言語サービスが開始され、ファイルの内容を表示するために使用されます。

### <a name="example"></a>例

```csharp
using Microsoft.VisualStudio.Shell;

namespace TestLanguagePackage
{
    [ProvideLanguageExtensionAttribute(typeof(TestLanguageService),
                                       ".Testext")]

    public class TestLanguagePackage : Package
    {
    }
}
```

### <a name="providelanguagecodeexpansionattribute"></a>ProvideLanguageCodeExpansionAttribute
 この属性を使用すると、コード拡張またはスニペット テンプレートを取得する場所を登録することができます。 この情報は、コード スニペットがソース ファイルに挿入されるときに、**コード スニペット ブラウザー** とエディターによって使用されます。

### <a name="example"></a>例

```csharp
using Microsoft.VisualStudio.Shell;

namespace TestLanguagePackage
{
    [ProvideLanguageCodeExpansionAttribute(
             typeof(TestLanguageService),
             "Test Language", // Name of language used as registry key.
             106,           // Resource ID of localized name of language service.
             "testlanguage",  // language key used in snippet templates.
             @"%InstallRoot%\Test Language\SnippetsIndex.xml",  // Path to snippets index
             SearchPaths = @"%InstallRoot%\Test Language\Snippets\%LCID%\Snippets\;" +
                           @"%TestDocs%\Code Snippets\Test Language\Test Code Snippets"
             )]

    public class TestLanguagePackage : Package
    {
    }
}
```

### <a name="providelanguageeditoroptionpageattribute"></a>ProvideLanguageEditorOptionPageAttribute
 この属性を使用すると、 **[オプション]** ダイアログ ボックスの **[テキスト エディター]** カテゴリの下に表示されるプロパティ ページを登録することができます。 言語サービスに表示されるページごとに、これらの属性のいずれかを使用してください。 ページをツリー構造で整理する必要がある場合は、追加の属性を使用してツリーの各ノードを定義します。

### <a name="example"></a>例
 この例は、 **[オプション]** と **[インデント]** の 2 つのプロパティ ページと、2 つ目のプロパティ ページを含む 1 つのノードを示しています。

```csharp
using Microsoft.VisualStudio.Shell;

namespace TestLanguagePackage
{
    [ProvideLanguageEditorOptionPageAttribute(
             "Test Language",  // Registry key name for language
             "Options",      // Registry key name for property page
             "#242",         // Localized name of property page
             OptionPageGuid = "{A2FE74E1-FFFF-3311-4342-123052450768}"  // GUID of property page
             )]
    [ProvideLanguageEditorOptionPageAttribute(
             "Test Language",  // Registry key name for language
             "Advanced",     // Registry key name for node
             "#243",         // Localized name of node
             )]
    [ProvideLanguageEditorOptionPageAttribute(
             "Test Language",  // Registry key name for language
             @"Advanced\Indenting",     // Registry key name for property page
             "#244",         // Localized name of property page
             OptionPageGuid = "{A2FE74E2-FFFF-3311-4342-123052450768}"  // GUID of property page
             )]

    public class TestLanguagePackage : Package
    {
    }
}
```

## <a name="proffer-the-language-service-at-run-time"></a>実行時に言語サービスを提供する
 言語パッケージが読み込まれたら、言語サービスの準備ができたことを [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] に伝える必要があります。 これを行うには、サービスを提供します。 これは、<xref:Microsoft.VisualStudio.Shell.Package.Initialize%2A> メソッドで実行します。 さらに、バックグラウンドでの解析を実行できるように、アイドル期間中に言語サービスを呼び出すタイマーを開始する必要があります。 このアイドル タイマーは、<xref:Microsoft.VisualStudio.Package.DocumentProperties> クラスを介して実装した場合、ドキュメントのプロパティを更新するためにも使用されます。 タイマーをサポートするには、パッケージで <xref:Microsoft.VisualStudio.OLE.Interop.IOleComponent> インターフェイスを実装する必要があります (完全に実装する必要があるのは <xref:Microsoft.VisualStudio.OLE.Interop.IOleComponent.FDoIdle%2A> メソッドのみであり、残りのメソッドからは既定値を返すことができます)。

### <a name="example"></a>例
 この例は、サービスを提供し、アイドル タイマーを提供するための一般的なアプローチを示しています。

```csharp

using System;
using System.Runtime.InteropServices;
using System.ComponentModel.Design;
using Microsoft.VisualStudio.Package;
using Microsoft.VisualStudio.Shell;
using Microsoft.VisualStudio.OLE.Interop;
using Microsoft.VisualStudio.TextManager.Interop;

namespace TestLanguagePackage
{
    [Microsoft.VisualStudio.Shell.ProvideService(typeof(TestLanguageService))]
    [Microsoft.VisualStudio.Shell.ProvideLanguageExtension(typeof(TestLanguageService), ".testext")]
    [Microsoft.VisualStudio.Shell.ProvideLanguageService(typeof(TestLanguageService), "Test Language", 0,
        AutoOutlining = true,
        EnableCommenting = true,
        MatchBraces = true,
        ShowMatchingBrace = true)]
    [Guid("00000000-0000-0000-0000-00000000000")] //provide a unique GUID for the package

    public class TestLanguagePackage : Package, IOleComponent
    {
        private uint m_componentID;

        protected override void Initialize()
        {
            base.Initialize();  // required

            // Proffer the service.
            IServiceContainer serviceContainer = this as IServiceContainer;
            TestLanguageService langService      = new TestLanguageService();
            langService.SetSite(this);
            serviceContainer.AddService(typeof(TestLanguageService),
                                        langService,
                                        true);

            // Register a timer to call our language service during
            // idle periods.
            IOleComponentManager mgr = GetService(typeof(SOleComponentManager))
                                       as IOleComponentManager;
            if (m_componentID == 0 && mgr != null)
            {
                OLECRINFO[] crinfo = new OLECRINFO[1];
                crinfo[0].cbSize            = (uint)Marshal.SizeOf(typeof(OLECRINFO));
                crinfo[0].grfcrf            = (uint)_OLECRF.olecrfNeedIdleTime |
                                              (uint)_OLECRF.olecrfNeedPeriodicIdleTime;
                crinfo[0].grfcadvf          = (uint)_OLECADVF.olecadvfModal |
                                              (uint)_OLECADVF.olecadvfRedrawOff |
                                              (uint)_OLECADVF.olecadvfWarningsOff;
                crinfo[0].uIdleTimeInterval = 1000;
                int hr = mgr.FRegisterComponent(this, crinfo, out m_componentID);
            }
        }

        protected override void Dispose(bool disposing)
        {
            if (m_componentID != 0)
            {
                IOleComponentManager mgr = GetService(typeof(SOleComponentManager))
                                           as IOleComponentManager;
                if (mgr != null)
                {
                    int hr = mgr.FRevokeComponent(m_componentID);
                }
                m_componentID = 0;
            }

            base.Dispose(disposing);
        }

        #region IOleComponent Members

        public int FDoIdle(uint grfidlef)
        {
            bool bPeriodic = (grfidlef & (uint)_OLEIDLEF.oleidlefPeriodic) != 0;
            // Use typeof(TestLanguageService) because we need to
            // reference the GUID for our language service.
            LanguageService service = GetService(typeof(TestLanguageService))
                                      as LanguageService;
            if (service != null)
            {
                service.OnIdle(bPeriodic);
            }
            return 0;
        }

        public int FContinueMessageLoop(uint uReason,
                                        IntPtr pvLoopData,
                                        MSG[] pMsgPeeked)
        {
            return 1;
        }

        public int FPreTranslateMessage(MSG[] pMsg)
        {
            return 0;
        }

        public int FQueryTerminate(int fPromptUser)
        {
            return 1;
        }

        public int FReserved1(uint dwReserved,
                              uint message,
                              IntPtr wParam,
                              IntPtr lParam)
        {
            return 1;
        }

        public IntPtr HwndGetWindow(uint dwWhich, uint dwReserved)
        {
            return IntPtr.Zero;
        }

        public void OnActivationChange(IOleComponent pic,
                                       int fSameComponent,
                                       OLECRINFO[] pcrinfo,
                                       int fHostIsActivating,
                                       OLECHOSTINFO[] pchostinfo,
                                       uint dwReserved)
        {
        }

        public void OnAppActivate(int fActive, uint dwOtherThreadID)
        {
        }

        public void OnEnterState(uint uStateID, int fEnter)
        {
        }

        public void OnLoseActivation()
        {
        }

        public void Terminate()
        {
        }

        #endregion
    }
}
```
