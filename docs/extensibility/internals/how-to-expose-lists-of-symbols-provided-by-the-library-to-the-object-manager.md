---
title: オブジェクト マネージャーに提供されるシンボルのリストを公開 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- IVsSimpleLibrary2 interface, lists of symbols
- IVsLibrary2 interface, lists of symbols
- symbols, call browser
- lists, symbols for the object manager
- symbols, exposing lists to the object manager
ms.assetid: 19757068-bdaa-4e7e-85d6-f8ce5026a859
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 19f426d60ea8ee3d9326fa9b13adfff115c169d5
ms.sourcegitcommit: 1fc6ee928733e61a1f42782f832ead9f7946d00c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "60061321"
---
# <a name="how-to-expose-lists-of-symbols-provided-by-the-library-to-the-object-manager"></a>方法: オブジェクト マネージャーにライブラリによって提供されるシンボルのリストを公開します。
シンボル参照ツール、**クラス ビュー**、**オブジェクト ブラウザー**、**呼び出しブラウザー**と**シンボルの検索結果**を新しいデータの要求を渡す[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]オブジェクト マネージャー。 オブジェクト マネージャーは、適切なライブラリを検索し、シンボルの新しいリストを要求します。 ライブラリの応答を要求されたデータを提供することで、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]オブジェクト マネージャーを介して、<xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2>インターフェイス。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]オブジェクト マネージャー メソッドを呼び出して、<xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2>データを取得するインターフェイスを使用して設定またはシンボル参照ツールのビューを更新します。

 ライブラリでは、ツールが呼び出され、ノードを展開すると、またはビューが更新されたとき、データの要求を取得することがあります。 シンボル参照ツールが初めて呼び出されると、オブジェクト マネージャーは、最上位レベルの一覧を提供するライブラリを要求します。 ユーザーは、一覧にノードを展開、ライブラリは、そのノードの下の子の一覧を提供します。 すべてのオブジェクト マネージャーの照会には、関心のある項目のインデックスが含まれています。 新しい一覧を表示するには、項目の数が、項目、その名前、アクセシビリティ、およびその他のプロパティの種類の一覧ではオブジェクト マネージャーを決定する必要があります。

> [!NOTE]
>  実装するシンボルのリストを提供する管理対象のコード例を以下に示します、<xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2>インターフェイス。 オブジェクト マネージャーでは、このインターフェイスでメソッドを呼び出して、取得したデータを使用して設定またはシンボル参照ツールを更新します。
>
>  ネイティブ コード シンボル プロバイダーの実装を使用して、<xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectList2>インターフェイス。

## <a name="to-provide-lists-of-symbols-to-the-object-manager"></a>オブジェクト マネージャーにシンボルのリストを提供するには

1. 実装することで、シンボルの一覧で項目の数を取得、<xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2.GetItemCount%2A>メソッド。 次の例では、オブジェクト マネージャーが、リスト内の項目の数に関する情報を取得する方法を示します。

    ```vb
    Protected m_Methods As System.Collections.Generic.SortedList(Of String, Method) = New System.Collections.Generic.SortedList(Of String, Method)()

    Public Function GetItemCount(ByRef pCount As UInteger) As Integer
        pCount = CUInt(m_Methods.Count)
        Return Microsoft.VisualStudio.VSConstants.S_OK
    End Function
    ```

    ```csharp
    protected System.Collections.Generic.SortedList<string, Method> m_Methods = new System.Collections.Generic.SortedList<string, Method>();

    public int GetItemCount(out uint pCount)
    {
        pCount = (uint)m_Methods.Count;
        return Microsoft.VisualStudio.VSConstants.S_OK;
    }

    ```

2. 実装することで、カテゴリおよび特定のリスト項目の属性に関する情報を取得、<xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2.GetCategoryField2%2A>メソッド。 指定された項目のカテゴリ、<xref:Microsoft.VisualStudio.Shell.Interop.LIB_CATEGORY>列挙体。 次の例では、オブジェクト マネージャーが特定のカテゴリの項目の属性を取得する方法を示します。

    ```vb
    Public Function GetCategoryField2(ByVal index As UInteger, ByVal Category As Integer, ByRef pfCatField As UInteger) As Integer
        pfCatField = 0

        Select Case CType(Category, LIB_CATEGORY)
            Case LIB_CATEGORY.LC_MEMBERTYPE
                pfCatField = CUInt(_LIBCAT_MEMBERTYPE.LCMT_METHOD)

            Case LIB_CATEGORY.LC_MEMBERACCESS
                Dim method As Method = m_Methods.Values(CInt(Fix(index)))

                If method.IsPublic Then
                    pfCatField = CUInt(_LIBCAT_MEMBERACCESS.LCMA_PUBLIC)
                ElseIf method.IsPrivate Then
                    pfCatField = CUInt(_LIBCAT_MEMBERACCESS.LCMA_PRIVATE)
                ElseIf method.IsFamily Then
                    pfCatField = CUInt(_LIBCAT_MEMBERACCESS.LCMA_PROTECTED)
                ElseIf method.IsFamilyOrAssembly Then
                    pfCatField = CUInt(_LIBCAT_MEMBERACCESS.LCMA_PROTECTED) Or CUInt(_LIBCAT_MEMBERACCESS.LCMA_PACKAGE)
                Else
                    ' Show everything else as internal.
                    pfCatField = CUInt(_LIBCAT_MEMBERACCESS.LCMA_PACKAGE)
                End If

            Case LIB_CATEGORY.LC_VISIBILITY
                pfCatField = CUInt(_LIBCAT_VISIBILITY.LCV_VISIBLE)

            Case LIB_CATEGORY.LC_LISTTYPE
                pfCatField = CUInt(_LIB_LISTTYPE.LLT_MEMBERS)

            Case Else
                Return Microsoft.VisualStudio.VSConstants.S_FALSE
        End Select
        Return Microsoft.VisualStudio.VSConstants.S_OK
    End Function
    ```

    ```csharp
    public int GetCategoryField2(uint index, int Category, out uint pfCatField)
    {
        pfCatField = 0;

        switch ((LIB_CATEGORY)Category)
        {
            case LIB_CATEGORY.LC_MEMBERTYPE:
                pfCatField = (uint)_LIBCAT_MEMBERTYPE.LCMT_METHOD;
                break;

            case LIB_CATEGORY.LC_MEMBERACCESS:
                {
                    Method method = m_Methods.Values[(int)index];

                    if (method.IsPublic)
                    {
                        pfCatField = (uint)_LIBCAT_MEMBERACCESS.LCMA_PUBLIC;
                    }
                    else if (method.IsPrivate)
                    {
                        pfCatField = (uint)_LIBCAT_MEMBERACCESS.LCMA_PRIVATE;
                    }
                    else if (method.IsFamily)
                    {
                        pfCatField = (uint)_LIBCAT_MEMBERACCESS.LCMA_PROTECTED;
                    }
                    else if (method.IsFamilyOrAssembly)
                    {
                        pfCatField = (uint)_LIBCAT_MEMBERACCESS.LCMA_PROTECTED |
                                     (uint)_LIBCAT_MEMBERACCESS.LCMA_PACKAGE;
                    }
                    else
                    {
                        // Show everything else as internal.
                        pfCatField = (uint)_LIBCAT_MEMBERACCESS.LCMA_PACKAGE;
                    }
                }
                break;

            case LIB_CATEGORY.LC_VISIBILITY:
                pfCatField = (uint)_LIBCAT_VISIBILITY.LCV_VISIBLE;
                break;

            case LIB_CATEGORY.LC_LISTTYPE:
                pfCatField = (uint)_LIB_LISTTYPE.LLT_MEMBERS;
                break;

            default:
                return Microsoft.VisualStudio.VSConstants.S_FALSE;
        }
        return Microsoft.VisualStudio.VSConstants.S_OK;
    }

    ```

3. 実装することによって指定されたリスト項目のテキスト表現を取得する、<xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2.GetTextWithOwnership%2A>メソッド。 次の例では、特定の項目の完全な名前を取得する方法を示します。

    ```vb
    Public Function GetTextWithOwnership(<System.Runtime.InteropServices.ComAliasNameAttribute("Microsoft.VisualStudio.OLE.Interop.ULONG")> ByVal index As UInteger, <System.Runtime.InteropServices.ComAliasNameAttribute("Microsoft.VisualStudio.Shell.Interop.VSTREETEXTOPTIONS")> ByVal tto As Microsoft.VisualStudio.Shell.Interop.VSTREETEXTOPTIONS, <System.Runtime.InteropServices.ComAliasNameAttribute("Microsoft.VisualStudio.OLE.Interop.WCHAR")> ByRef ppszText As String) As Integer
        ppszText = m_Methods.Values(CInt(Fix(index))).FullName
        Return Microsoft.VisualStudio.VSConstants.S_OK
    End Function
    ```

    ```csharp
    public int GetTextWithOwnership([System.Runtime.InteropServices.ComAliasNameAttribute("Microsoft.VisualStudio.OLE.Interop.ULONG")] uint index, [System.Runtime.InteropServices.ComAliasNameAttribute("Microsoft.VisualStudio.Shell.Interop.VSTREETEXTOPTIONS")] Microsoft.VisualStudio.Shell.Interop.VSTREETEXTOPTIONS tto, [System.Runtime.InteropServices.ComAliasNameAttribute("Microsoft.VisualStudio.OLE.Interop.WCHAR")] out string ppszText)
    {
        ppszText = m_Methods.Values[(int)index].FullName;
        return Microsoft.VisualStudio.VSConstants.S_OK;
    }

    ```

4. 実装することによって指定されたリスト項目のアイコンの情報を取得、<xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2.GetDisplayData%2A>メソッド。 アイコンは、型 (クラス、メソッド、およびなど)、およびリスト項目のアクセシビリティ (プライベート、パブリック、およびなど) を表します。 次の例では、特定の項目の属性に基づいてアイコンの情報を取得する方法を示します。

    ```vb
    Public Overridable Function GetDisplayData(ByVal index As UInteger, ByVal pData As Microsoft.VisualStudio.Shell.Interop.VSTREEDISPLAYDATA()) As Integer
        If pData Is Nothing Then
            Return Microsoft.VisualStudio.VSConstants.E_INVALIDARG
        End If

        Dim method As Method = m_Methods.Values(CInt(Fix(index)))

        Dim iImage As Integer = 12 * 6 ' See env\inc\OMGlyphs.h.

        Const OM_GLYPH_ACC_PUBLIC As Integer = 0
        Const OM_GLYPH_ACC_INTERNAL As Integer = 1
        Const OM_GLYPH_ACC_PROTECTED As Integer = 3
        Const OM_GLYPH_ACC_PRIVATE As Integer = 4

        If method.IsPublic Then
            iImage += OM_GLYPH_ACC_PUBLIC
        ElseIf method.IsPrivate Then
            iImage += OM_GLYPH_ACC_PRIVATE
        ElseIf method.IsFamily Then
            iImage += OM_GLYPH_ACC_PROTECTED
        ElseIf method.IsFamilyOrAssembly Then
            iImage += OM_GLYPH_ACC_PROTECTED
        Else
            iImage += OM_GLYPH_ACC_INTERNAL
        End If

        pData(0).Image = CUShort(iImage)
        pData(0).SelectedImage = CUShort(iImage)

        Return Microsoft.VisualStudio.VSConstants.S_OK
    End Function
    ```

    ```csharp
    public virtual int GetDisplayData(uint index, Microsoft.VisualStudio.Shell.Interop.VSTREEDISPLAYDATA[] pData)
    {
        if (pData == null)
        {
            return Microsoft.VisualStudio.VSConstants.E_INVALIDARG;
        }

        Method method = m_Methods.Values[(int)index];

        int iImage = 12 * 6;    // See env\inc\OMGlyphs.h.

        const int OM_GLYPH_ACC_PUBLIC = 0;
        const int OM_GLYPH_ACC_INTERNAL = 1;
        const int OM_GLYPH_ACC_PROTECTED = 3;
        const int OM_GLYPH_ACC_PRIVATE = 4;

        if (method.IsPublic)
        {
            iImage += OM_GLYPH_ACC_PUBLIC;
        }
        else if (method.IsPrivate)
        {
            iImage += OM_GLYPH_ACC_PRIVATE;
        }
        else if (method.IsFamily)
        {
            iImage += OM_GLYPH_ACC_PROTECTED;
        }
        else if (method.IsFamilyOrAssembly)
        {
            iImage += OM_GLYPH_ACC_PROTECTED;
        }
        else
        {
            iImage += OM_GLYPH_ACC_INTERNAL;
        }

        pData[0].Image = (ushort)iImage;
        pData[0].SelectedImage = (ushort)iImage;

        return Microsoft.VisualStudio.VSConstants.S_OK;
    }

    ```

5. 特定のリスト項目は実装することで拡張可能なかどうかに関する情報を取得、<xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2.GetExpandable3%2A>メソッド。 次の例では、特定の項目を展開するかどうかの情報を取得する方法を示します。

    ```vb
    Public Function GetExpandable(ByVal index As UInteger, ByRef pfExpandable As Integer) As Integer
        pfExpandable = Microsoft.VisualStudio.VSIP.Samples.CallBrowser.Constants.TRUE
        Return Microsoft.VisualStudio.VSConstants.S_OK
    End Function

    Public Function GetExpandable3(ByVal index As UInteger, ByVal ListTypeExcluded As UInteger, ByRef pfExpandable As Integer) As Integer
        Return GetExpandable(index, pfExpandable)
    End Function
    ```

    ```csharp
    public int GetExpandable(uint index, out int pfExpandable)
    {
        pfExpandable = Microsoft.VisualStudio.VSIP.Samples.CallBrowser.Constants.TRUE;
        return Microsoft.VisualStudio.VSConstants.S_OK;
    }

    public int GetExpandable3(uint index, uint ListTypeExcluded, out int pfExpandable)
    {
        return GetExpandable(index, out pfExpandable);
    }

    ```

6. 実装することで特定のリスト項目のシンボルの子リストを取得、<xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2.GetList2%2A>メソッド。 次の例は、子の指定した項目のシンボルの一覧を取得する方法を示します**呼び出す**または**呼び出し元**グラフ。

    ```vb
    ' Call graph list.
    Public Class CallsList
        Inherits ResultsList
        Implements Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2
        Public Sub New(ByVal library As Library)
            MyBase.New(library)
        End Sub

        Public Function GetList2(ByVal index As UInteger, ByVal ListType As UInteger, ByVal flags As UInteger, ByVal pobSrch As Microsoft.VisualStudio.Shell.Interop.VSOBSEARCHCRITERIA2(), ByRef ppList As Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2) As Integer
            Return MyBase.GetCallsList(index, ppList)
        End Function
    End Class

    ' Callers graph list.
    Public Class CallersList
        Inherits ResultsList
        Implements Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2
        Public Sub New(ByVal library As Library)
            MyBase.New(library)
        End Sub

        Public Function GetList2(ByVal index As UInteger, ByVal ListType As UInteger, ByVal flags As UInteger, ByVal pobSrch As Microsoft.VisualStudio.Shell.Interop.VSOBSEARCHCRITERIA2(), ByRef ppList As Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2) As Integer
            Return MyBase.GetCallersList(index, ppList)
        End Function
    End Class

    ' Call graph list.
    Public Function GetCallsList(ByVal index As UInteger, ByRef ppList As Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2) As Integer
        ppList = Nothing
        Dim callsList As ResultsList = New CallsList(m_Library)

        Dim method As Method = m_Methods.Values(CInt(Fix(index)))
        Dim strMethod As String = method.m_strPrototype

        Dim Calls As System.Collections.Generic.List(Of CallInstance) = m_Library.CallGraph.GetCallGraph(method)

        For i As Integer = 0 To Calls.Count - 1
            Dim caller As Method = Calls(i).m_Target
            callsList.AddMethod(caller)
        Next i

        ppList = CType(callsList, Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2)
        Return Microsoft.VisualStudio.VSConstants.S_OK
    End Function

    ' Callers graph list.
    Public Function GetCallersList(ByVal index As UInteger, ByRef ppList As Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2) As Integer
        ppList = Nothing
        Dim callersList As ResultsList = New CallersList(m_Library)

        Dim method As Method = m_Methods.Values(CInt(Fix(index)))
        Dim strMethod As String = method.m_strPrototype

        Dim Callers As System.Collections.Generic.List(Of CallInstance) = m_Library.CallGraph.GetCallersGraph(method)

        For i As Integer = 0 To Callers.Count - 1
            Dim caller As Method = Callers(i).m_Source
            callersList.AddMethod(caller)
        Next i

        ppList = CType(callersList, Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2)
        Return Microsoft.VisualStudio.VSConstants.S_OK
    End Function

    ' Get a child list of symbols for a given list item.
    Public Function GetList2(ByVal index As UInteger, ByVal ListType As UInteger, ByVal flags As UInteger, ByVal pobSrch As Microsoft.VisualStudio.Shell.Interop.VSOBSEARCHCRITERIA2(), ByRef ppList As Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2) As Integer
        ppList = Nothing

        Dim method As Method = m_Methods.Values(CInt(Fix(index)))
        Dim strMethod As String = method.m_strPrototype

        ' Determine if the list belongs to Call or Callers graphs.
        If CUInt(m_nFlags And CUInt(Microsoft.VisualStudio.Shell.Interop._VSOBSEARCHOPTIONS2.VSOBSO_CALLSFROM)) > 0 Then
            ' Build the list for the Call graph.
            Return MyBase.GetCallsList(index, ppList)
        ElseIf CUInt(m_nFlags And CUInt(Microsoft.VisualStudio.Shell.Interop._VSOBSEARCHOPTIONS2.VSOBSO_CALLSTO)) > 0 Then
            ' Build the list for the Callers graph.
            Return MyBase.GetCallersList(index, ppList)
        End If

        Return Microsoft.VisualStudio.VSConstants.E_FAIL
    End Function
    ```

    ```csharp
    // Call graph list.
    public class CallsList :
        ResultsList,
        Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2
    {
        public CallsList(Library library) :
            base(library)
        {
        }

        public int GetList2(uint index, uint ListType, uint flags, Microsoft.VisualStudio.Shell.Interop.VSOBSEARCHCRITERIA2[] pobSrch, out Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2 ppList)
        {
            return base.GetCallsList(index, out ppList);
        }
    }

    // Callers graph list.
    public class CallersList :
        ResultsList,
        Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2
    {
        public CallersList(Library library) :
            base(library)
        {
        }

        public int GetList2(uint index, uint ListType, uint flags, Microsoft.VisualStudio.Shell.Interop.VSOBSEARCHCRITERIA2[] pobSrch, out Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2 ppList)
        {
            return base.GetCallersList(index, out ppList);
        }
    }

    // Call graph list.
    public int GetCallsList(uint index, out Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2 ppList)
    {
        ppList = null;
        ResultsList callsList = new CallsList(m_Library);

        Method method = m_Methods.Values[(int)index];
        string strMethod = method.m_strPrototype;

        System.Collections.Generic.List<CallInstance> Calls = m_Library.CallGraph.GetCallGraph(method);

        for (int i = 0; i < Calls.Count; i++)
        {
            Method caller = Calls[i].m_Target;
            callsList.AddMethod(caller);
        }

        ppList = (Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2)(callsList);
        return Microsoft.VisualStudio.VSConstants.S_OK;
    }

    // Callers graph list.
    public int GetCallersList(uint index, out Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2 ppList)
    {
        ppList = null;
        ResultsList callersList = new CallersList(m_Library);

        Method method = m_Methods.Values[(int)index];
        string strMethod = method.m_strPrototype;

        System.Collections.Generic.List<CallInstance> Callers = m_Library.CallGraph.GetCallersGraph(method);

        for (int i = 0; i < Callers.Count; i++)
        {
            Method caller = Callers[i].m_Source;
            callersList.AddMethod(caller);
        }

        ppList = (Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2)(callersList);
        return Microsoft.VisualStudio.VSConstants.S_OK;
    }

    // Get a child list of symbols for a given list item.
    public int GetList2(uint index, uint ListType, uint flags, Microsoft.VisualStudio.Shell.Interop.VSOBSEARCHCRITERIA2[] pobSrch, out Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2 ppList)
    {
        ppList = null;

        Method method = m_Methods.Values[(int)index];
        string strMethod = method.m_strPrototype;

        // Determine if the list belongs to Call or Callers graphs.
        if ((uint)(m_nFlags & (uint)Microsoft.VisualStudio.Shell.Interop._VSOBSEARCHOPTIONS2.VSOBSO_CALLSFROM) > 0)
        {
            // Build the list for the Call graph.
            return base.GetCallsList(index, out ppList);
        }
        else if ((uint)(m_nFlags & (uint)Microsoft.VisualStudio.Shell.Interop._VSOBSEARCHOPTIONS2.VSOBSO_CALLSTO) > 0)
        {
            // Build the list for the Callers graph.
            return base.GetCallersList(index, out ppList);
        }

        return Microsoft.VisualStudio.VSConstants.E_FAIL;
    }

    ```

## <a name="see-also"></a>関連項目
- [シンボル参照ツールをサポートします。](../../extensibility/internals/supporting-symbol-browsing-tools.md)
- [方法: オブジェクト マネージャーにライブラリを登録します。](../../extensibility/internals/how-to-register-a-library-with-the-object-manager.md)
- [方法: ライブラリ内のシンボルを識別します。](../../extensibility/internals/how-to-identify-symbols-in-a-library.md)
- [従来の言語サービス拡張機能](../../extensibility/internals/legacy-language-service-extensibility.md)