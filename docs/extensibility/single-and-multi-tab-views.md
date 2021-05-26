---
title: 単一および複数タブのビュー |Microsoft Docs
description: コード エディター ウィンドウやフォーム デザイナーなど、複数のタブから成るビューをエディターで実装する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], custom - single and multi-tab views
ms.assetid: e3611704-349f-4323-b03c-f2b0a445d781
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 7c23693b5ae622912695c139714c7e818ed0e868
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105056325"
---
# <a name="single-and-multi-tab-views"></a>単一タブと複数タブのビュー
エディターでは、さまざまな種類のビューを作成できます。 1 つの例としてコード エディター ウィンドウがあり、他にはフォーム デザイナーがあります。

 複数のタブからなるビューは、複数のタブを持つビューです。 たとえば、HTML エディターの下部には、 **[デザイン]** と **[ソース]** の 2 つのタブがあり、それぞれ論理ビューです。 デザイン ビューには、レンダリングされた Web ページが表示されます。もう一方では、Web ページを構成する HTML が表示されます。

## <a name="accessing-physical-views"></a>物理ビューへのアクセス
 物理ビューでは、ドキュメント ビュー オブジェクトがホストされます。それぞれ、コードやフォームなど、バッファー内のデータのビューを表します。 その結果、各ドキュメント ビュー オブジェクトには物理ビュー (物理ビュー文字列と呼ばれるもので識別されます) と、通常は 1 つの論理ビューがあります。

 ただし、場合によっては、物理ビューに 2 つ以上の論理ビューを含めることができます。 例としては、サイドバイサイド ビューを備えた分割ウィンドウがあるエディターや、GUI/デザイン ビューとコードビハインド フォーム ビューを持つフォーム デザイナーがあります。

 エディターから使用可能なすべての物理ビューにアクセスできるようにするには、エディター ファクトリで作成できるドキュメント ビュー オブジェクトの種類ごとに一意の物理ビュー文字列を作成する必要があります。 たとえば、[!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] エディター ファクトリでは、コード ウィンドウとフォーム デザイナー ウィンドウのドキュメント ビュー オブジェクトを作成できます。

## <a name="creating-multi-tabbed-views"></a>複数のタブ付きビューの作成
 ドキュメント ビュー オブジェクトは、一意の物理ビュー文字列を使用して物理ビューに関連付けられている必要がありますが、複数のタブを物理ビュー内に配置することで、さまざまな方法でデータを表示することができます。 この複数タブの構成では、すべてのタブが同じ物理ビュー文字列に関連付けられていますが、各タブには異なる論理ビュー GUID が割り当てられています。

 エディター用の複数のタブ付きビューを作成するには、<xref:Microsoft.VisualStudio.Shell.Interop.IVsMultiViewDocumentView> インターフェイスを実装してから、作成した各タブに別の論理ビュー GUID (<xref:Microsoft.VisualStudio.Shell.Interop.LogicalViewID>) を関連付けます。

 Visual Studio HTML エディターは、複数のタブ付きビューを備えたエディターの一例です。 これには、 **[デザイン]** タブと **[ソース]** タブがあります。 これを有効にするため、 **[デザイン]** タブには `LOGICALVIEWID_TextView`、 **[ソース]** タブには `LOGICALVIEWID_Code`と、各タブに別の論理ビューが関連付けられています。

 適切な論理ビューを指定することにより、VSPackage から、フォームのデザイン、コードの編集、コードのデバッグなど、特定の目的に対応するビューにアクセスできます。 ただし、ウィンドウの 1 つは NULL 文字列によって識別される必要があり、これはプライマリ論理ビュー (`LOGVIEWID_Primary`) に対応する必要があります。

 次の表に、使用可能な論理ビューの値とその使用方法を示します。

|LOGVIEWID GUID|推奨される用途|
|--------------------|---------------------|
|`LOGVIEWID_Primary`|エディター ファクトリの既定/プライマリ ビュー。<br /><br /> すべてのエディター ファクトリでは、この値をサポートする必要があります。 このビューでは、物理ビュー文字列として NULL 文字列を使用する必要があります。 少なくとも 1 つの論理ビューをこの値に設定する必要があります。|
|`LOGVIEWID_Debugging`|デバッグ ビュー。 通常、`LOGVIEWID_Debugging` は `LOGVIEWID_Code` と同じビューにマップされます。|
|`LOGVIEWID_Code`|**コードの表示** コマンドによって起動されたビュー。|
|`LOGVIEWID_Designer`|**フォームの表示** コマンドによって起動されたビュー。|
|`LOGVIEWID_TextView`|テキスト エディター ビュー。 これは、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> にアクセスするための <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindow> を返すビューです。|
|`LOGVIEWID_UserChooseView`|使用するビューを選択するようにユーザーに求めます。|
|`LOGVIEWID_ProjectSpecificEditor`|**[プログラムから開く]** ダイアログ ボックスから次に渡されます<br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject.OpenItem%2A><br /><br /> ユーザーが "(プロジェクトの既定のエディター)" エントリを選択したときです。|

 論理ビュー GUID は拡張可能ですが、VSPackage で定義されている論理ビュー GUID のみを使用できます。

 シャットダウン時に、Visual Studio では、エディター ファクトリの GUID とドキュメント ウィンドウに関連付けられている物理ビュー文字列を保持します。これにより、ソリューションを再度開いたときにドキュメント ウィンドウを再び開くために使用できるようになります。 ソリューションが閉じられたときに開いていたウィンドウだけが、ソリューション (.suo) ファイルに保存されます。 これらの値は、<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.GetProperty%2A> メソッドの `propid` パラメーターで渡される `VSFPROPID_guidEditorType` と `VSFPROPID_pszPhysicalView` 値に対応します。

## <a name="example"></a>例
 このスニペットは、`IVsCodeWindow` を実装するビューに <xref:Microsoft.VisualStudio.Shell.Interop.LogicalViewID.TextView> オブジェクトを使用してアクセスする方法を示しています。 この場合、<xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShellOpenDocument> サービスが、ウィンドウフレームへのポインターを取得する <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenDocumentViaProject%2A> を呼び出し、`LOGVIEWID_TextView` を要求するために使用されます。 ドキュメント ビュー オブジェクトへのポインターは、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.GetProperty%2A> を呼び出し、`VSFPROPID_DocView` の値を指定することによって取得されます。 ドキュメント ビュー オブジェクトから、`IVsCodeWindow` のために `QueryInterface` が呼び出されます。 この場合は、テキスト エディターが返されるため、<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.GetProperty%2A> メソッドで返されるドキュメント ビュー オブジェクトがコード ウィンドウになります。

```cpp
HRESULT CFindTool::GotoFileLocation(const WCHAR * szFile, long iLine, long iStart, long iLen)
{
  HRESULT hr;
  if (NULL == szFile || !*szFile)
    return E_INVALIDARG;

  if (iLine == -1L)
    return S_FALSE;

  VSITEMID                  itemid;
  VARIANT                   var;
  RECT                      rc;
  IVsUIShellOpenDocument *  pOpenDoc    = NULL;
  IVsCodeWindow *           pCodeWin    = NULL;
  IVsTextView *             pTextView   = NULL;
  IVsUIHierarchy *          pHierarchy  = NULL;
  IVsWindowFrame *          pFrame      = NULL;
  IUnknown *                pUnk        = NULL;
  IVsHighlight *            pHighlight  = NULL;

  IfFailGo(CGlobalServiceProvider::HrQueryService(SID_SVsUIShellOpenDocument, IID_IVsUIShellOpenDocument, (void **)&pOpenDoc));
  IfFailGo(pOpenDoc->OpenDocumentViaProject(szFile, LOGVIEWID_TextView, NULL, &pHierarchy, &itemid, &pFrame));
  pFrame->Show();
  VariantInit(&var);
  IfFailGo(pFrame->GetProperty(VSFPROPID_DocView, &var));
  if (VT_UNKNOWN != var.vt) { hr = E_FAIL; goto Error; }
  pUnk = V_UNKNOWN(&var);
  if (NULL != pUnk)
  {
    IfFailGo(pUnk->QueryInterface(IID_IVsCodeWindow, (void **)&pCodeWin));
    if (SUCCEEDED(hr = pCodeWin->GetLastActiveView(&pTextView)) ||
        SUCCEEDED(hr = pCodeWin->GetPrimaryView(&pTextView)) )
    {
      pTextView->SetSelection(iLine, iStart, iLine, iStart + iLen);
      // uncover selection
      IfFailGo(pTextView->QueryInterface(IID_IVsHighlight, (void**)&pHighlight));
      IfFailGo(SUCCEEDED(pHighlight->GetHighlightRect(&rc)));
      UncoverSelectionRect(&rc);
    }
  }

Error:
  CLEARINTERFACE(pHighlight);
  CLEARINTERFACE(pTextView);
  CLEARINTERFACE(pCodeWin);
  CLEARINTERFACE(pUnk);
  CLEARINTERFACE(pFrame);
  CLEARINTERFACE(pOpenDoc);
  CLEARINTERFACE(pHierarchy);
  RedrawWindow(m_hwndResults, NULL, NULL, RDW_ERASE|RDW_FRAME|RDW_INVALIDATE|RDW_ALLCHILDREN);
  return hr;
}
```

## <a name="see-also"></a>関連項目
- [複数のドキュメント ビューのサポート](../extensibility/supporting-multiple-document-views.md)
- [方法: ビューをドキュメントデータに添付する](../extensibility/how-to-attach-views-to-document-data.md)
- [カスタム エディターとデザイナーの作成](../extensibility/creating-custom-editors-and-designers.md)
