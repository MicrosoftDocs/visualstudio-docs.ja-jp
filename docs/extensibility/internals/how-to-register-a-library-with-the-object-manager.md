---
title: '方法: オブジェクト マネージャーへのライブラリの登録 | Microsoft Docs'
description: クラス ビューやオブジェクト ブラウザーなどの参照ツールでシンボルを表示できるように、Visual Studio のオブジェクト マネージャーにライブラリを登録する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- libraries, registering with object manager
- IVsLibrary2 interface, registering library with object manager
- IVsSimpleLibrary2 interface, registering library with object manager
- IVsObjectManager2 interface, registering library with object manager
- libraries, symbol-browsing tools
ms.assetid: f124dd05-cb0f-44ad-bb2a-7c0b34ef4038
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: b83b68af4c026c40aca7969068ad015a61d64321
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105086067"
---
# <a name="how-to-register-a-library-with-the-object-manager"></a>方法: オブジェクト マネージャーへのライブラリの登録
**クラス ビュー**、**オブジェクト ブラウザー**、**呼び出しブラウザー**、**シンボルの検索結果** などのシンボル参照ツールを使用すると、プロジェクトまたは外部コンポーネントのシンボルを表示できます。 シンボルには、名前空間、クラス、インターフェイス、メソッド、およびその他の言語要素が含まれます。 ライブラリによってこれらのシンボルが追跡され、ツールにデータを事前設定する [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] オブジェクト マネージャーに公開されます。

 オブジェクト マネージャーでは、使用可能なすべてのライブラリが追跡されます。 シンボル参照ツールにシンボルを提供する前に、各ライブラリをオブジェクト マネージャーに登録する必要があります。

 通常は、VSPackage の読み込み時にライブラリを登録します。 ただし、必要に応じて別のタイミングで行うことができます。 VSPackage を停止するときにライブラリの登録を解除します。

 ライブラリを登録するには、<xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectManager2.RegisterLibrary%2A> メソッドを使用します。 マネージド コード ライブラリの場合は、<xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectManager2.RegisterSimpleLibrary%2A> メソッドを使用します。

 ライブラリの登録を解除するには、<xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectManager2.UnregisterLibrary%2A> メソッドを使用します。

 オブジェクト マネージャー (<xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectManager2>) への参照を取得するには、<xref:Microsoft.VisualStudio.Shell.Interop.SVsObjectManager> のサービス ID を `GetService` メソッドに渡します。

## <a name="register-and-unregister-a-library-with-the-object-manager"></a>オブジェクト マネージャーへのライブラリの登録と登録解除

### <a name="to-register-a-library-with-the-object-manager"></a>オブジェクト マネージャーにライブラリを登録するには

1. ライブラリを作成します。

    ```vb
    Private m_CallBrowserLibrary As CallBrowser.Library = Nothing
    Private m_nLibraryCookie As UInteger = 0
    ' Create Library.
    m_CallBrowserLibrary = New CallBrowser.Library()
    ```

    ```csharp
    private CallBrowser.Library m_CallBrowserLibrary = null;
    private uint m_nLibraryCookie = 0;
    // Create Library.
    m_CallBrowserLibrary = new CallBrowser.Library();

    ```

2. <xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectManager2> 型のオブジェクトへの参照を取得し、<xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectManager2.RegisterSimpleLibrary%2A> メソッドを呼び出します。

    ```vb
    Private Sub RegisterLibrary()
        If m_nLibraryCookie <> 0 Then
            Throw New Exception("Library already registered with Object Manager")
        End If

        ' Obtain a reference to IVsObjectManager2 type object.
        Dim objManager As IVsObjectManager2 = TryCast(GetService(GetType(SVsObjectManager)), IVsObjectManager2)
        If objManager Is Nothing Then
            Throw New NullReferenceException("GetService failed for SVsObjectManager")
        End If

        Try
            Dim hr As Integer = objManager.RegisterSimpleLibrary(m_CallBrowserLibrary, m_nLibraryCookie)
            Microsoft.VisualStudio.ErrorHandler.ThrowOnFailure(hr)
        Catch e As Exception
            ' Code to handle any CLS-compliant exception.
            Trace.WriteLine(e.Message)
            Throw
        End Try
    End Sub
    ```

    ```csharp
    private void RegisterLibrary()
    {
        if (m_nLibraryCookie != 0)
            throw new Exception("Library already registered with Object Manager");

        // Obtain a reference to IVsObjectManager2 type object.
        IVsObjectManager2 objManager =
                          GetService(typeof(SVsObjectManager)) as IVsObjectManager2;
        if (objManager == null)
            throw new NullReferenceException("GetService failed for SVsObjectManager");

        try
        {
            int hr =
                objManager.RegisterSimpleLibrary(m_CallBrowserLibrary,
                                                 out m_nLibraryCookie);
                Microsoft.VisualStudio.ErrorHandler.ThrowOnFailure(hr);
        }
        catch (Exception e)
        {
            // Code to handle any CLS-compliant exception.
            Trace.WriteLine(e.Message);
            throw;
        }
    }

    ```

### <a name="to-unregister-a-library-with-the-object-manager"></a>オブジェクト マネージャーのライブラリの登録を解除するには

1. <xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectManager2> 型のオブジェクトへの参照を取得し、<xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectManager2.UnregisterLibrary%2A> メソッドを呼び出します。

    ```vb
    Private Sub UnregisterLibrary()
        If m_nLibraryCookie <> 0 Then
            ' Obtain a reference to IVsObjectManager2 type object.
            Dim objManager As IVsObjectManager2 = TryCast(GetService(GetType(SVsObjectManager)), IVsObjectManager2)
            If objManager Is Nothing Then
                Throw New NullReferenceException("GetService failed for SVsObjectManager")
            End If

            Try
                objManager.UnregisterLibrary(m_nLibraryCookie)
            Catch e As Exception
                ' Code to handle any CLS-compliant exception.
                Trace.WriteLine(e.Message)
                Throw
            Finally
                m_nLibraryCookie = 0
            End Try
        End If
    End Sub
    ```

    ```csharp
    private void UnregisterLibrary()
    {
        if (m_nLibraryCookie != 0)
        {
            // Obtain a reference to IVsObjectManager2 type object.
            IVsObjectManager2 objManager = GetService(typeof(SVsObjectManager)) as IVsObjectManager2;
            if (objManager == null)
                throw new NullReferenceException("GetService failed for SVsObjectManager");

            try
            {
                objManager.UnregisterLibrary(m_nLibraryCookie);
            }
            catch (Exception e)
            {
                // Code to handle any CLS-compliant exception.
                Trace.WriteLine(e.Message);
                throw;
            }
            finally
            {
                m_nLibraryCookie = 0;
            }
        }
    }

    ```

## <a name="see-also"></a>関連項目
- [従来の言語サービスの機能拡張](../../extensibility/internals/legacy-language-service-extensibility.md)
- [シンボル参照ツールのサポート](../../extensibility/internals/supporting-symbol-browsing-tools.md)
- [方法: ライブラリによって提供されるシンボルのリストをオブジェクト マネージャーに公開する](../../extensibility/internals/how-to-expose-lists-of-symbols-provided-by-the-library-to-the-object-manager.md)
