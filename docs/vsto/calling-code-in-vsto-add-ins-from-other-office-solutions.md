---
title: 他の Office ソリューションから VSTO アドインのコードを呼び出す
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- VBA [Office development in Visual Studio], calling code in application-level add-ins
- application-level add-ins [Office development in Visual Studio], calling code from other solutions
- calling add-in code
- add-ins [Office development in Visual Studio], calling code from other solutions
- interoperability [Office development in Visual Studio]
- calling code from VBA
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 584406098f058c17b3dd215dda9c8c4e9498cf46
ms.sourcegitcommit: e98db44f3a33529b0ba188d24390efd09e548191
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/25/2019
ms.locfileid: "71255329"
---
# <a name="call-code-in-vsto-add-ins-from-other-office-solutions"></a>他の Office ソリューションから VSTO アドインのコードを呼び出す
  VSTO アドイン内のオブジェクトは、他の Microsoft Office ソリューションを含む、他のソリューションに公開できます。 このことは、VSTO アドインが他のソリューションで使用可能なサービスを含む場合に便利です。 たとえば、Web サービスからの財務データに対して計算を実行する Microsoft Office Excel 用の VSTO アドインがある場合、他のソリューションは、実行時に Excel VSTO アドインを呼び出すことによって、これらの計算を実行できます。

 [!INCLUDE[appliesto_allapp](../vsto/includes/appliesto-allapp-md.md)]

 この処理には主に 2 つの手順があります。

- VSTO アドインで、オブジェクトを他のソリューションに公開します。

- もう 1 つのソリューションで、VSTO アドインにより公開されたオブジェクトにアクセスし、オブジェクトのメンバーを呼び出します。

## <a name="types-of-solutions-that-can-call-code-in-an-add-in"></a>アドインでコードを呼び出すことができるソリューションの種類
 VSTO アドインのオブジェクトは、次の種類のソリューションに公開できます。

- VSTO アドインと同じアプリケーション プロセスに読み込まれるドキュメント内の Visual Basic for Applications (VBA) コード。

- VSTO アドインと同じアプリケーション プロセスに読み込まれるドキュメント レベルのカスタマイズ。

- Visual Studio に含まれる Office プロジェクト テンプレートを使用して作成された他の VSTO アドイン。

- COM VSTO アドイン (つまり、 <xref:Extensibility.IDTExtensibility2> インターフェイスを直接実装する VSTO アドイン)。

- VSTO アドインとは異なるプロセスで実行中の任意のソリューション (こうした種類のソリューションは *アウト プロセス クライアント*とも呼ばれます)。 これらには、Windows フォームまたはコンソール アプリケーションなど、Office アプリケーションを自動化するアプリケーションと、異なるプロセスに読み込まれる VSTO アドインが含まれます。

## <a name="expose-objects-to-other-solutions"></a>オブジェクトを他のソリューションに公開する
 VSTO アドイン内のオブジェクトを他のソリューションに公開するには、VSTO アドインで次の手順を実行します。

1. 他のソリューションに公開するクラスを定義します。

2. <xref:Microsoft.Office.Tools.AddInBase.RequestComAddInAutomationService%2A> クラスの `ThisAddIn` メソッドをオーバーライドします。 他のソリューションに公開するクラスのインスタンスを返します。

### <a name="define-the-class-you-want-to-expose-to-other-solutions"></a>他のソリューションに公開するクラスを定義する
 少なくとも、公開するクラスはパブリックであり、 <xref:System.Runtime.InteropServices.ComVisibleAttribute> 属性の設定は **true**であり、 [IDispatch](/previous-versions/windows/desktop/api/oaidl/nn-oaidl-idispatch) インターフェイスを公開する必要があります。

 [IDispatch](/previous-versions/windows/desktop/api/oaidl/nn-oaidl-idispatch) インターフェイスを公開する推奨方法は以下の手順を実行することです。

1. 他のソリューションに公開するメンバーを宣言するインターフェイスを定義します。 このインターフェイスは、VSTO アドイン プロジェクトで定義できます。 ただし、クラスを非 VBA ソリューションに公開する場合、このインターフェイスを別のクラス ライブラリ プロジェクトで定義することを推奨します。そうすることで、VSTO アドインを呼び出すソリューションは VSTO アドイン プロジェクトを参照することなく、インターフェイスを参照できます。

2. このインターフェイスに属性を適用し、この属性をtrueに設定し<xref:System.Runtime.InteropServices.ComVisibleAttribute>ます。

3. クラスを変更して、このインターフェイスを実装します。

4. 属性をクラスに適用し、この属性を<xref:System.Runtime.InteropServices.ClassInterfaceType>列挙体の **[なし**] の値に設定します。 <xref:System.Runtime.InteropServices.ClassInterfaceAttribute>

5. このクラスをアウトプロセスクライアントに公開する場合は、次の手順も実行する必要があります。

   - <xref:System.Runtime.InteropServices.StandardOleMarshalObject>からクラスを派生させます。 詳細については、「[アウトプロセスクライアントにクラスを公開する](#outofproc)」を参照してください。

   - インターフェイスを定義するプロジェクトで、 **[COM の相互運用機能に登録]** プロパティを設定します。 このプロパティは、クライアントが事前バインディングを使用して VSTO アドインを呼び出すことができるようにする場合にのみ必要です。

   次のコード例は、他のソリューションによって呼び出し可能な `AddInUtilities` メソッドを持つ、 `ImportData` クラスを示します。 より大きなチュートリアルのコンテキストでこのコードを確認するには[、「チュートリアル:VSTO アドインのコードを VBA](../vsto/walkthrough-calling-code-in-a-vsto-add-in-from-vba.md)から呼び出します。

   [!code-csharp[Trin_AddInInteropWalkthrough #3](../vsto/codesnippet/CSharp/Trin_AddInInteropWalkthrough/AddInUtilities.cs#3)]
   [!code-vb[Trin_AddInInteropWalkthrough#3](../vsto/codesnippet/VisualBasic/Trin_AddInInteropWalkthrough/AddInUtilities.vb#3)]

### <a name="expose-classes-to-vba"></a>クラスを VBA に公開する
 上記の手順を実行すると、VBA コードはインターフェイス内で宣言するメソッドのみを呼び出すことができます。 VBA コードは、 <xref:System.Object>など、クラスが基本クラスから取得するメソッドを含め、クラス内の他のメソッドを呼び出すことはできません。

 また、 <xref:System.Runtime.InteropServices.ClassInterfaceAttribute>属性を<xref:System.Runtime.InteropServices.ClassInterfaceType>列挙体の autodispatch 値または autodispatch value に設定することによって、 [IDispatch](/previous-versions/windows/desktop/api/oaidl/nn-oaidl-idispatch)インターフェイスを公開することもできます。 インターフェイスを公開する場合は、メソッドを別のインターフェイスで宣言する必要はありません。 ただし、VBA コードは、 <xref:System.Object>など、基本クラスから取得されるメソッドを含め、クラス内の任意のパブリックおよび非静的メソッドを呼び出すことができます。 さらに、事前バインディングを使用するアウト プロセス クライアントはクラスを呼び出すことができません。

### <a name="outofproc"></a>アウトプロセスクライアントにクラスを公開する
 VSTO アドイン内のクラスをアウト プロセス クライアントに公開する場合、 <xref:System.Runtime.InteropServices.StandardOleMarshalObject> からクラスを派生させ、アウト プロセス クライアントが公開された VSTO アドイン オブジェクトを呼び出せるようにする必要があります。 そうしないと、アウト プロセス クライアントで公開されたオブジェクトのインスタンスを取得しようとしたとき、予期せずに失敗する可能性があります。

 このエラーは、Office アプリケーションのオブジェクトモデルへのすべての呼び出しをメイン UI スレッドで行う必要があるためですが、アウトプロセスクライアントからオブジェクトへの呼び出しは、任意の RPC (リモートプロシージャコール) スレッドに到着します。 .NET Framework における COM マーシャリング機構はスレッドを切り替えず、メイン UI スレッドではなく、受信 RPC スレッド上のオブジェクトに呼び出しをマーシャリングすることを試みます。 オブジェクトが <xref:System.Runtime.InteropServices.StandardOleMarshalObject>から派生するクラスのインスタンスである場合、オブジェクトへの受信呼び出しは、公開されたオブジェクトが作成されたスレッド、つまりホスト アプリケーションのメイン UI スレッドに自動的にマーシャリングされます。

 Office ソリューションでのスレッドの使用の詳細については、「 [office でのスレッドのサポート](../vsto/threading-support-in-office.md)」を参照してください。

### <a name="override-the-requestcomaddinautomationservice-method"></a>RequestComAddInAutomationService メソッドのオーバーライド
 次のコード例は、VSTO アドイン内の <xref:Microsoft.Office.Tools.AddInBase.RequestComAddInAutomationService%2A> クラスで `ThisAddIn` をオーバーライドする方法を示します。 この例では、他のソリューションに公開`AddInUtilities`するという名前のクラスを定義していることを前提としています。 より大きなチュートリアルのコンテキストでこのコードを確認するには[、「チュートリアル:VSTO アドインのコードを VBA](../vsto/walkthrough-calling-code-in-a-vsto-add-in-from-vba.md)から呼び出します。

 [!code-csharp[Trin_AddInInteropWalkthrough#1](../vsto/codesnippet/CSharp/Trin_AddInInteropWalkthrough/ThisAddIn.cs#1)]
 [!code-vb[Trin_AddInInteropWalkthrough#1](../vsto/codesnippet/VisualBasic/Trin_AddInInteropWalkthrough/ThisAddIn.vb#1)]

 VSTO アドインが読み込まれると、 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] は <xref:Microsoft.Office.Tools.AddInBase.RequestComAddInAutomationService%2A> メソッドを呼び出します。 ランタイムは、返されたオブジェクトを、VSTO アドインを表す<xref:Microsoft.Office.Core.COMAddIn>オブジェクトの comaddin オブジェクトプロパティに割り当てます。 この <xref:Microsoft.Office.Core.COMAddIn> オブジェクトは他の Office ソリューションおよび Office を自動化するソリューションで利用できます。

## <a name="access-objects-from-other-solutions"></a>他のソリューションからオブジェクトにアクセスする
 VSTO アドインで公開されたオブジェクトを呼び出すには、クライアント ソリューションで以下の手順を実行します。

1. 公開された VSTO アドインを表す <xref:Microsoft.Office.Core.COMAddIn> オブジェクトを取得します。 クライアントは、ホスト Office アプリケーションのオブジェクト モデル内の `Application.COMAddIns` プロパティを使用して、使用可能なすべての VSTO アドインにアクセスできます。

2. <xref:Microsoft.Office.Core.COMAddIn>オブジェクトの comaddin オブジェクトプロパティにアクセスします。 このプロパティは VSTO アドインから公開されたオブジェクトを返します。

3. 公開されたオブジェクトのメンバーを呼び出します。

   COMAddIn オブジェクトプロパティの戻り値の使用方法は、VBA クライアントと非 VBA クライアントで異なります。 アウト プロセス クライアントの場合、可能性のある競合状態を避けるために追加のコードが必要です。

### <a name="access-objects-from-vba-solutions"></a>VBA ソリューションからオブジェクトにアクセスする
 次のコード例では、VBA を使用して、VSTO アドインによって公開されているメソッドを呼び出す方法を示します。 この VBA マクロは、 **ExcelImportData**と`ImportData`いう名前の VSTO アドインで定義されているという名前のメソッドを呼び出します。 より大きなチュートリアルのコンテキストでこのコードを確認するには[、「チュートリアル:VSTO アドインのコードを VBA](../vsto/walkthrough-calling-code-in-a-vsto-add-in-from-vba.md)から呼び出します。

```vb
Sub CallVSTOMethod()
    Dim addIn As COMAddIn
    Dim automationObject As Object
    Set addIn = Application.COMAddIns("ExcelImportData")
    Set automationObject = addIn.Object
    automationObject.ImportData
End Sub
```

### <a name="access-objects-from-non-vba-solutions"></a>VBA 以外のソリューションからオブジェクトにアクセスする
 非 VBA ソリューションでは、実装するインターフェイスに COMAddIn オブジェクトのプロパティ値をキャストする必要があります。その後、インターフェイスオブジェクトで公開されているメソッドを呼び出すことができます。 次のコード例は、Visual Studio に含まれる Office Developer Tools を使用して作成された異なる VSTO アドインから `ImportData` メソッドを呼び出す方法を示します。

```vb
Dim addIn As Office.COMAddIn = Globals.ThisAddIn.Application.COMAddIns.Item("ExcelImportData")
Dim utilities As ExcelImportData.IAddInUtilities = TryCast( _
    addIn.Object, ExcelImportData.IAddInUtilities)
utilities.ImportData()
```

```csharp
object addInName = "ExcelImportData";
Office.COMAddIn addIn = Globals.ThisAddIn.Application.COMAddIns.Item(ref addInName);
ExcelImportData.IAddInUtilities utilities = (ExcelImportData.IAddInUtilities)addIn.Object;
utilities.ImportData();
```

 この例では、 `AddInUtilities` `IAddInUtilities`インターフェイスではなく、comaddin オブジェクトのプロパティの値をクラスにキャストしようとすると、がスロー <xref:System.InvalidCastException>されます。

## <a name="see-also"></a>関連項目
- [プログラム VSTO アドイン](../vsto/programming-vsto-add-ins.md)
- [チュートリアル: VSTO アドインのコードを VBA から呼び出す](../vsto/walkthrough-calling-code-in-a-vsto-add-in-from-vba.md)
- [Office ソリューションの開発](../vsto/developing-office-solutions.md)
- [方法: Visual Studio での Office プロジェクトを作成する](../vsto/how-to-create-office-projects-in-visual-studio.md)
- [VSTO アドインのアーキテクチャ](../vsto/architecture-of-vsto-add-ins.md)
- [機能拡張インターフェイスを使用した UI 機能のカスタマイズ](../vsto/customizing-ui-features-by-using-extensibility-interfaces.md)
