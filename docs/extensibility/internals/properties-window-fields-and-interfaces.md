---
title: プロパティ ウィンドウのフィールドとインターフェイス | Microsoft Docs
description: Visual Studio IDE 内でフォーカスのあるウィンドウに基づいて、プロパティ ウィンドウにどのような情報を表示するかを決定する選択について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Properties window, fields and interfaces
ms.assetid: 0328f0e5-2380-4a7a-a872-b547cb775050
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 9f445d31fe995321ad6ec334a5b6eb93570b8875
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105061031"
---
# <a name="properties-window-fields-and-interfaces"></a>プロパティ ウィンドウのフィールドとインターフェイス
**[プロパティ]** ウィンドウにどのような情報を表示するかを決定する選択のモデルは、IDE 内でフォーカスのあるウィンドウに基づいています。 すべてのウィンドウと、選択されたウィンドウ内のオブジェクトでは、その選択コンテキスト オブジェクトをグローバル選択コンテキストにプッシュできます。 環境では、あるウィンドウにフォーカスがあるときに、そのウィンドウ フレームの値でグローバル選択コンテキストを更新します。 フォーカスが変更されると、選択コンテキストも変更されます。

## <a name="tracking-selection-in-the-ide"></a>IDE での選択の追跡
 IDE によって所有されるウィンドウ フレームまたはサイトには、<xref:Microsoft.VisualStudio.Shell.Interop.STrackSelection> という名前のサービスがあります。 次の手順は、ユーザーがフォーカスを別の開いているウィンドウに変更するか、または **ソリューション エクスプローラー** で別のプロジェクト項目を選択することによって発生する選択の変更が、 **[プロパティ]** ウィンドウに表示される内容を変更するためにどのように実装されるかを示しています。

1. 選択されたウィンドウに配置されている VSPackage によって作成されたオブジェクトが、<xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider.QueryService%2A> を呼び出して <xref:Microsoft.VisualStudio.Shell.Interop.STrackSelection> で <xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection> を呼び出すようにします。

2. 選択されたウィンドウによって提供される選択コンテナーによって、独自の <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> オブジェクトが作成されます。 選択が変更されると、VSPackage は <xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection.OnSelectChange%2A> を呼び出して、環境内のすべてのリスナー ( **[プロパティ]** ウィンドウを含む) にその変更を通知します。 また、新しい選択に関連した階層と項目に関する情報へのアクセスも提供します。

3. <xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection.OnSelectChange%2A> を呼び出し、`VSHPROPID_BrowseObject` パラメーターで選択された階層項目を渡すと、<xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> オブジェクトが設定されます。

4. 要求された項目の [__VSHPROPID.VSHPROPID_BrowseObject](<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID.VSHPROPID_BrowseObject>) に対して [IDispatch インターフェイス](/previous-versions/windows/desktop/api/oaidl/nn-oaidl-idispatch)から派生したオブジェクトが返されると、環境では、それを <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> にラップします (次の手順を参照)。 この呼び出しが失敗した場合、環境では `IVsHierarchy::GetProperty` への 2 番目の呼び出しを行い、それを 1 つまたは複数の階層項目によって提供される選択コンテナー [__VSHPROPID.VSHPROPID_SelContainer](<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID.VSHPROPID_SelContainer>) に渡します。

    プロジェクト VSPackage では <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> を作成しません。それを実装している、環境によって提供されるウィンドウ VSPackage (**ソリューション エクスプローラー** など) が、代わりに <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> を構築するためです。

5. 環境では、<xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> のメソッドを呼び出して、 **[プロパティ]** ウィンドウに入力するための `IDispatch` インターフェイスに基づいたオブジェクトを取得します。

   **[プロパティ]** ウィンドウ内の値が変更されると、VSPackage では、その変更を要素の値に報告するために `IVsTrackSelectionEx::OnElementValueChangeEx` と `IVsTrackSelectionEx::OnSelectionChangeEx` を実装します。 その後、環境では <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell> または <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPointContainer> を呼び出して **[プロパティ]** ウィンドウに表示される情報をプロパティ値と同期された状態に維持します。 詳細については、「[プロパティ ウィンドウでのプロパティ値の更新](#updating-property-values-in-the-properties-window)」を参照してください。

   ある項目に関連したプロパティを表示するために **ソリューション エクスプローラー** でその別のプロジェクト項目を選択することに加えて、 **[プロパティ]** ウィンドウで使用可能なドロップダウン リストを使用して、フォームまたはドキュメント ウィンドウ内から別のオブジェクトを選択することもできます。 詳細については、「[プロパティ ウィンドウのオブジェクト一覧](../../extensibility/internals/properties-window-object-list.md)」を参照してください。

   情報が **[プロパティ]** ウィンドウ グリッドに表示される方法をアルファベット順からカテゴリ別に変更できるほか、可能な場合は、 **[プロパティ]** ウィンドウの適切なボタンをクリックすることによって、選択されたオブジェクトのプロパティ ページを開くこともできます。 詳細については、「[プロパティ ウィンドウのボタン](../../extensibility/internals/properties-window-buttons.md)」および「[プロパティ ページ](../../extensibility/internals/property-pages.md)」を参照してください。

   最後に、 **[プロパティ]** ウィンドウの下部には、 **[プロパティ]** ウィンドウ グリッドで選択されたフィールドの説明も表示されています。 詳細については、「[プロパティ ウィンドウからのフィールドの説明の取得](#getting-field-descriptions-from-the-properties-window)」を参照してください。

## <a name="updating-property-values-in-the-properties-window"></a><a name="updating-property-values-in-the-properties-window"></a> プロパティ ウィンドウでのプロパティ値の更新
**[プロパティ]** ウィンドウをプロパティ値の変更と同期するには、2 つの方法があります。 1 番目の方法は、<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell> インターフェイスを呼び出すことです。このインターフェイスは、環境によって用意されているツール ウィンドウやドキュメント ウィンドウのアクセスや作成を含む、基本的なウィンドウ操作機能へのアクセスを提供します。 次の手順は、この同期プロセスを説明したものです。

### <a name="updating-property-values-using-ivsuishell"></a>IVsUIShell を使ってプロパティ値を更新する

#### <a name="to-update-property-values-using-the-ivsuishell-interface"></a>IVsUIShell インターフェイスを使ってプロパティ値を更新するには

1. VSPackage、プロジェクト、エディターがツール ウィンドウまたはドキュメント ウィンドウを作成したり列挙したりする必要が生じた時点で、<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell> を (<xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell> サービスを通じて) 呼び出します。

2. <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.RefreshPropertyBrowser%2A> を実装することにより、<xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPointContainer> を実装したり <xref:Microsoft.VisualStudio.OLE.Interop.IPropertyNotifySink.OnChanged%2A> イベントを起動したりすることなく、 **[プロパティ]** ウィンドウをプロジェクト (または、 **[プロパティ]** ウィンドウによって参照されている他の任意の選択されたオブジェクト) のプロパティ変更と同期された状態に維持します。

3. <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> のメソッド <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.AdviseHierarchyEvents%2A> および <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.UnadviseHierarchyEvents%2A> を実装します。この 2 つのメソッドは、それぞれ、階層イベントのクライアント通知を設定および無効化します。これにより、階層で <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPointContainer> を実装する必要がなくなります。

### <a name="updating-property-values-using-iconnection"></a>IConnection を使ってプロパティ値を更新する
 **[プロパティ]** ウィンドウとプロパティ値の変更を同期する 2 番目の方法は、接続可能なオブジェクトに `IConnection` を実装することにより、発信インターフェイスの存在を示すことです。 プロパティ名をローカライズする場合は、オブジェクトを <xref:System.ComponentModel.ICustomTypeDescriptor> から派生させます。 <xref:System.ComponentModel.ICustomTypeDescriptor> の実装では、実装から返すプロパティ記述子を変更し、プロパティの名前を変更できます。 説明をローカライズするには、<xref:System.ComponentModel.DescriptionAttribute> から派生させた属性を作成し、Description プロパティをオーバーライドします。

#### <a name="considerations-in-implementing-the-iconnection-interface"></a>IConnection インターフェイスを実装する際の考慮事項

1. `IConnection` は、<xref:Microsoft.VisualStudio.OLE.Interop.IEnumConnectionPoints> インターフェイスを持つ列挙子サブオブジェクトへのアクセスを提供します。 また、すべての接続ポイント サブオブジェクトへのアクセスも提供し、それぞれは <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPoint> インターフェイスを実装します。

2. すべての参照オブジェクトは、<xref:Microsoft.VisualStudio.OLE.Interop.IPropertyNotifySink> イベントを実装する必要があります。 **[プロパティ]** ウィンドウは、 `IConnection`を通してイベントを設定することをお勧めします。

3. 接続ポイントは、<xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPoint.Advise%2A> の実装で許容される接続数 (1 つまたは複数) を制御します。 インターフェイスを 1 つのみ許容する接続ポイントでは、<xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPoint.EnumConnections%2A> メソッドから <xref:Microsoft.VisualStudio.VSConstants.E_NOTIMPL> を返すことができます。

4. クライアントは、`IConnection` インターフェイスを呼び出すことにより、<xref:Microsoft.VisualStudio.OLE.Interop.IEnumConnectionPoints> インターフェイスを持つ列挙子サブオブジェクトへのアクセスを取得できます。 その後、<xref:Microsoft.VisualStudio.OLE.Interop.IEnumConnectionPoints> インターフェイスを呼び出すと、各発信インターフェイス ID (IID) の接続ポイントを列挙することができます。

5. また、`IConnection` を呼び出すことにより、各発信 IID への <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPoint> インターフェイスを持つ接続ポイント サブオブジェクトへのアクセスを取得することもできます。 クライアントは、<xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPoint> インターフェイス経由で、接続可能なオブジェクトとそのクライアント独自の同期によるアドバイザリ ループを開始または終了します。クライアントはまた、<xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPoint> インターフェイスを呼び出して、認識している接続を列挙するための <xref:Microsoft.VisualStudio.OLE.Interop.IEnumConnections> インターフェイスを含む列挙子オブジェクトを取得することもできます。

## <a name="getting-field-descriptions-from-the-properties-window"></a><a name="getting-field-descriptions-from-the-properties-window"></a> プロパティ ウィンドウからのフィールドの説明の取得
**[プロパティ]** ウィンドウの下部にある説明領域に、選択したプロパティ フィールドに関連する情報が表示されます。 この機能は既定で有効になっています。 説明フィールドを非表示にするには、 **[プロパティ]** ウィンドウを右クリックし、 **[説明]** をクリックします。 これにより、メニュー ウィンドウの **[説明]** タイトルの横のチェック マークが削除されます。 同じ手順を行って **[説明]** の表示をオンに戻すことにより、フィールドを再度表示できます。

 説明フィールド内の情報は <xref:Microsoft.VisualStudio.OLE.Interop.ITypeInfo> から取得されます。 それぞれのメソッド、インターフェイス、コクラスなどには、タイプ ライブラリのローカライズされていない `helpstring` 属性を適用できます。 **[プロパティ]** ウィンドウでは、<xref:Microsoft.VisualStudio.OLE.Interop.ITypeInfo.GetDocumentation%2A> から文字列を取得します。

### <a name="to-specify-localized-help-strings"></a>ローカライズされたヘルプ文字列を指定するには

1. タイプ ライブラリ ( `helpstringdll` ) のライブラリ ステートメントに`typelib`属性を追加します。

   > [!NOTE]
   > この手順は、タイプ ライブラリがオブジェクト ライブラリ (.olb) ファイルにある場合は省略可能です。

2. 文字列の `helpstringcontext` 属性を指定します。 `helpstring` 属性を指定することもできます。

    これらの属性は、実際の.chm ファイルのヘルプ トピックに含まれる `helpfile` 属性と `helpcontext` 属性とは異なります。

   強調表示されているプロパティ名に対して表示される説明情報を取得するために、 **[プロパティ]** ウィンドウでは、選択されているプロパティの <xref:System.Runtime.InteropServices.ComTypes.ITypeInfo2.GetDocumentation2%2A> を呼び出し、出力文字列のための目的の `lcid` 属性を指定します。 内部的には、<xref:System.Runtime.InteropServices.ComTypes.ITypeInfo2> は `helpstringdll` 属性で指定された .dll ファイルを検索し、指定されたコンテキストと `lcid` 属性を使ってその .dll ファイル上に `DLLGetDocumentation` を呼び出します。

   `DLLGetDocumentation` の署名と実装は次のとおりです。

```cpp
STDAPI DLLGetDocumentation
(
   ITypeLib * /* ptlib */,
   ITypeInfo * /* ptinfo */,
   LCID /* lcid */,
   DWORD dwCtx,
   BSTR * pbstrHelpString
);
```

 `DLLGetDocumentation` 関数はDLL の .def ファイルで定義されているエクスポートである必要があります。

 内部的には、実際には DLL である .olb ファイルが作成されます。 この DLL には、1 つのリソース、タイプ ライブラリ (.tlb) ファイル、および 1 つのエクスポートされた `DLLGetDocumentation`関数が含まれます。

 .olb ファイルの場合は、 `helpstringdll` 属性は.tlb ファイル自体を含む同じファイルであるため省略可能です。

 したがって、 **[説明]** ウィンドウに表示する文字列を取得するために最低限必要な操作は、タイプ ライブラリに `helpstring` 属性を指定することです。 これらの文字列をローカライズする場合は、 `helpstringdll` (省略可能) 属性と `helpstringcontext` (必須) 属性を指定し、 `DLLGetDocumentation`を実装する必要があります

 idl の `helpstringcontext` 属性と `DLLGetDocumentation`によって取得したローカライズされた情報を取得する場合は、実装する必要のある追加のインターフェイスはありません。

 別の方法でプロパティのローカライズされた名前と説明の取得には、<xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing.GetLocalizedPropertyInfo%2A> を実装します。 このメソッドの実装に関する詳細については、「 [Properties Window Fields and Interfaces](../../extensibility/internals/properties-window-fields-and-interfaces.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [プロパティの拡張](../../extensibility/internals/extending-properties.md)
