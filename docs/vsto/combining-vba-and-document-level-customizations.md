---
title: VBA とドキュメントレベルのカスタマイズを結合する
description: Microsoft Office Word または Excel 用のドキュメントレベルのカスタマイズの一部であるドキュメント内で Visual Basic for Applications (VBA) コードを使用する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- VST.VBAInterop.InvalidAssemblyVersion
- VST.VBAInterop.ProjectLoadFailure
- VST.VBAInterop.MissingGUID
- VST.VBAInterop.EnableComCallers
- VST.VBAInterop.PersistVBACode
- VST.VBAInterop.ReferenceAssemblyFromVBA
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio], Visual Basic for Applications and
- VBA [Office development in Visual Studio]
- Office documents [Office development in Visual Studio], Visual Basic for Applications and
- VBA [Office development in Visual Studio], about VBA and document-level customizations
- managed code [Office development in Visual Studio], Visual Basic for Applications and
- document-level customizations [Office development in Visual Studio], Visual Basic for Applications and
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 1c5f66042dad7051c856aa6158ea0a666a81e9b4
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99938526"
---
# <a name="combine-vba-and-document-level-customizations"></a>VBA とドキュメントレベルのカスタマイズを結合する
  Microsoft Office Word または Microsoft Office Excel 用のドキュメント レベル カスタマイズの一部であるドキュメント内で Visual Basic for Applications (VBA) コードを使用できます。 カスタマイズ アセンブリからドキュメント内の VBA コードを呼び出したり、ドキュメント内の VBA コードがカスタマイズ アセンブリのコードを呼び出せるようにプロジェクトを構成したりすることができます。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

## <a name="behavior-of-vba-code-in-a-document-level-customization"></a>ドキュメントレベルのカスタマイズでの VBA コードの動作
 Visual Studio でプロジェクトを開くと、ドキュメントはデザイン モードで開かれます。 ドキュメントがデザイン モードのときは VBA コードは実行しないので、VBA コードを実行しないでドキュメントとコードを作業できます。

 ソリューションを実行すると、VBA およびカスタマイズ アセンブリの両方のイベント ハンドラーがドキュメント内で生成されたイベントを取得し、両方のコード セットが実行します。 どちらのコードが先に実行するかは、事前にはわかりません。個別のケースごとにテストして判断する必要があります。 2 つのコード セットを慎重に調整およびテストしないと、予期しない結果になる可能性があります。

## <a name="call-vba-code-from-the-customization-assembly"></a>カスタマイズ アセンブリから VBA コードを呼び出す
 Word 文書のマクロおよび Excel ブックのマクロと関数を、呼び出すことができます。 そのためには、次のいずれかのメソッドを使用します。

- Word の場合: <xref:Microsoft.Office.Interop.Word.Application> クラスの <xref:Microsoft.Office.Interop.Word._Application.Run%2A> メソッドを呼び出します。

- Excel の場合: <xref:Microsoft.Office.Interop.Excel._Application.Run%2A> クラスの <xref:Microsoft.Office.Interop.Excel.Application> メソッドを呼び出します。

  いずれのメソッドも、1 番目のパラメーターは呼び出すマクロまたは関数の名前を示し、残りの省略可能なパラメーターではマクロまたは関数に渡すパラメーターを指定します。 1 番目のパラメーターは、Word と Excel で形式が異なる場合があります。

- Word の場合、1 番目のパラメーターは、テンプレート、モジュール、およびマクロ名の任意の組み合わせが可能な文字列です。 ドキュメントの名前を指定した場合、コードは、任意のドキュメントの任意のマクロではなく、現在のコンテキストに関連するドキュメントのマクロのみを実行できます。

- Excel の場合、1 番目のパラメーターでは、マクロ名を指定する文字列、関数の場所を示す <xref:Microsoft.Office.Interop.Excel.Range> 、または登録された DLL (XLL) 関数の登録者 ID を渡すことができます。 文字列を渡した場合、文字列はアクティブなシートのコンテキストで評価されます。

  次のコード例では、Excel のドキュメント レベル プロジェクトから `MyMacro` という名前のマクロを呼び出す方法を示します。 この例では、 `MyMacro` は `Sheet1`で定義されているものとします。

```vb
Globals.Sheet1.Application.Run("MyMacro")
```

```csharp
Globals.Sheet1.Application.Run("MyMacro", missing, missing, missing,
    missing, missing, missing, missing, missing, missing, missing,
    missing, missing, missing, missing, missing, missing, missing,
    missing, missing, missing, missing, missing, missing, missing,
    missing, missing, missing, missing, missing, missing);
```

> [!NOTE]
> Visual C# で省略可能なパラメーターの代わりにグローバル `missing` 変数を使用する方法については、「[Office ソリューションのコードを記述する](../vsto/writing-code-in-office-solutions.md)」を参照してください。

## <a name="call-code-in-document-level-customizations-from-vba"></a>VBA からドキュメントレベルのカスタマイズ内のコードを呼び出す
 ドキュメント内の Visual Basic for Applications (VBA) コードがカスタマイズ アセンブリのコードを呼び出すことができるように、Word または Excel のドキュメント レベル プロジェクトを構成できます。 これは、次のシナリオで役立ちます。

- 同じドキュメントに関連付けられているドキュメント レベル カスタマイズ内の機能を使用して、ドキュメント内の既存の VBA コードを拡張する場合。

- ドキュメントで VBA コードを記述することによって、ドキュメント レベル カスタマイズ内で開発したサービスに、エンド ユーザーがアクセスできるようにする場合。

  Visual Studio の Office 開発ツールには、VSTO アドインと同様の機能が用意されています。VSTO アドインを開発している場合は、他の Microsoft Office ソリューションから VSTO アドインのコードを呼び出すことができます。 詳細については、「[他の Office ソリューションから VSTO アドインのコードを呼び出す](../vsto/calling-code-in-vsto-add-ins-from-other-office-solutions.md)」を参照してください。

> [!NOTE]
> この機能は、Word テンプレート プロジェクトでは使用できません。 Word 文書、Excel ブック、または Excel テンプレートの各プロジェクトでのみ使用できます。

## <a name="requirements"></a>必要条件
 VBA コードでカスタマイズ アセンブリを呼び出すことができるためには、プロジェクトが次の要件を満たしている必要があります。

- ドキュメントは、次のいずれかのファイル名拡張子であることが必要です。

  - Word の場合: *.docm* または *.doc*

  - Excel の場合: *.xlsm*、 *.xltm*、 *.xls*、または *.xlt*

- ドキュメントは、VBA コードが含まれる VBA プロジェクトを既に含んでいる必要があります。

- ドキュメント内の VBA コードは、マクロの有効化をユーザーに確認することなく実行できる必要があります。 Word または Excel のセキュリティ センター設定の信頼できる場所の一覧に Office プロジェクトの場所を追加することによって、VBA コードの実行を信頼することができます。

- Office プロジェクトは、ユーザーが VBA に公開した 1 つ以上のパブリック メンバーを含むパブリック クラスを、1 つ以上含んでいる必要があります。

     メソッド、プロパティ、およびイベントを VBA に公開できます。 公開できるクラスは、ホスト項目クラス (Word の `ThisDocument` 、Excel の `ThisWorkbook` や `Sheet1` など) またはプロジェクト内で定義されている別のクラスです。 ホスト項目の詳細については、「[ホスト項目とホスト コントロールの概要](../vsto/host-items-and-host-controls-overview.md)」を参照してください。

## <a name="enable-vba-code-to-call-into-the-customization-assembly"></a>VBA コードでカスタマイズ アセンブリを呼び出せるようにする
 ドキュメント内の VBA コードにカスタマイズ アセンブリ内のメンバーを公開するには 2 つの方法があります。

- [!INCLUDE[vbprvb](../sharepoint/includes/vbprvb-md.md)] プロジェクトのホスト項目クラスのメンバーを VBA に公開できます。 そのためには、ホスト項目 (つまり、文書、ワークシート、ブック) をデザイナーで開いた状態にして、[ **プロパティ** ] ウィンドウでホスト項目の **EnableVbaCallers** プロパティを **True** に設定します。 VBA コードがクラスのメンバーを呼び出せるようにするために必要なすべての処理は、Visual Studio が自動的に実行します。

- Visual C# プロジェクトのパブリック クラスのメンバー、または [!INCLUDE[vbprvb](../sharepoint/includes/vbprvb-md.md)] プロジェクトの非ホスト項目クラスのメンバーを、VBA に公開できます。 この方法を使用すると、VBA に公開するクラスをいっそう自由に選択できますが、必要な手動手順も多くなります。

   そのためには、次の主要な手順を実行する必要があります。

  1. COM にクラスを公開します。

  2. プロジェクトでホスト項目クラスの **GetAutomationObject** メンバーをオーバーライドして、VBA に公開したクラスのインスタンスを返すようにします。

  3. プロジェクトでホスト項目クラスの **ReferenceAssemblyFromVbaProject** プロパティを **True** に設定します。 これにより、カスタマイズ アセンブリのタイプ ライブラリがアセンブリに埋め込まれ、タイプ ライブラリへの参照がドキュメントの VBA プロジェクトに追加されます。

  詳細については、「[方法: Visual Basic プロジェクトのコードを VBA に公開する](../vsto/how-to-expose-code-to-vba-in-a-visual-basic-project.md)」および「[方法: Visual C&#35; プロジェクトのコードを VBA に公開する](../vsto/how-to-expose-code-to-vba-in-a-visual-csharp-project.md)」を参照してください。

  **EnableVbaCallers** および **ReferenceAssemblyFromVbaProject** プロパティは、設計時にのみ [ **プロパティ** ] ウィンドウで使用できます。実行時には使用できません。 プロパティを表示するには、 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]でホスト項目のデザイナーを開きます。 これらのプロパティを設定した場合に Visual Studio で実行される具体的なタスクの詳細については、「[ホスト項目プロパティによって実行されるタスク](#PropertyTasks)」を参照してください。

> [!NOTE]
> ブックまたはドキュメントに VBA コードがまだ含まれていない場合、またはドキュメント内の VBA コードの実行が信頼されていない場合は、 **EnableVbaCallers** または **ReferenceAssemblyFromVbaProject** プロパティを **True** に設定するとエラー メッセージが表示されます。 これは、このような状況では、Visual Studio がドキュメントのVBA プロジェクトを変更できないためです。

## <a name="use-members-in-vba-code-to-call-into-the-customization-assembly"></a>VBA コードのメンバーを使用してカスタマイズ アセンブリを呼び出す
 VBA コードがカスタマイズ アセンブリを呼び出せるようにプロジェクトを構成すると、Visual Studio は次のメンバーをドキュメントの VBA プロジェクトに追加します。

- すべてのプロジェクトに対し、Visual Studio は `GetManagedClass`という名前のグローバル メソッドを追加します。

- [!INCLUDE[vbprvb](../sharepoint/includes/vbprvb-md.md)] プロパティを使用してホスト項目クラスのメンバーを公開した **プロパティ** プロジェクトの場合は、Visual Studio は `CallVSTOAssembly` という名前のプロパティも、VBA プロジェクトの `ThisDocument`、 `ThisWorkbook`、 `Sheet1`、 `Sheet2`、 or `Sheet3` モジュールに追加します。

  プロジェクトの VBA コードに公開したクラスのパブリック メンバーには、 `CallVSTOAssembly` プロパティまたは `GetManagedClass` メソッドを使用してアクセスできます。

> [!NOTE]
> ソリューションを開発および配置するとき、ドキュメントの複数の異なるコピーに VBA コードを追加できます。 詳細については、「[ドキュメントに VBA コードを追加するためのガイドライン](#Guidelines)」を参照してください。

### <a name="use-the-callvstoassembly-property-in-a-visual-basic-project"></a>Visual Basic プロジェクトで CallVSTOAssembly プロパティを使用する
 ホスト項目クラスに追加したパブリック メンバーにアクセスするには、 `CallVSTOAssembly` プロパティを使用します。 たとえば、次の VBA マクロは、Excel ブック プロジェクトの `MyVSTOMethod` クラスで定義されている `Sheet1` という名前のメソッドを呼び出します。

```vb
Sub MyMacro()
    Sheet1.CallVSTOAssembly.MyVSTOMethod()
End Sub
```

 カスタマイズ アセンブリを呼び出すには、 `GetManagedClass` メソッドを直接使うより、このプロパティを使う方が便利です。 `CallVSTOAssembly` は、VBA に公開されたホスト項目クラスを表すオブジェクトを返します。 返されるオブジェクトのメンバーおよびメソッド パラメーターは、IntelliSense に表示されます。

 `CallVSTOAssembly` プロパティには、次のコードのような宣言があります。 このコードでは、 `Sheet1` という名前の Excel ブック プロジェクトの `ExcelWorkbook1` ホスト項目クラスを VBA に公開してあるものとします。

```vb
Property Get CallVSTOAssembly() As ExcelWorkbook1.Sheet1
    Set CallVSTOAssembly = GetManagedClass(Me)
End Property
```

### <a name="use-the-getmanagedclass-method"></a>GetManagedClass メソッドを使用する
 グローバル `GetManagedClass` メソッドを使用するには、 **GetAutomationObject** メソッドのオーバーライドを含むホスト項目クラスに対応する VBA オブジェクトを渡します。 次に、返されたオブジェクトを使用して、VBA に公開されているクラスにアクセスします。

 たとえば、次の VBA マクロは、 `MyVSTOMethod` という名前の Excel ブック プロジェクトの `Sheet1` ホスト項目クラスで定義されている `ExcelWorkbook1`という名前のメソッドを呼び出します。

```vb
Sub CallVSTOMethod
    Dim VSTOSheet1 As ExcelWorkbook1.Sheet1
    Set VSTOSheet1 = GetManagedClass(Sheet1)
    VSTOSheet1.MyVSTOMethod
End Sub
```

 `GetManagedClass` メソッドの宣言は次のとおりです。

```vb
GetManagedClass(pdispInteropObject Object) As Object
```

 このメソッドは、VBA に公開されたクラスを表すオブジェクトを返します。 返されるオブジェクトのメンバーおよびメソッド パラメーターは、IntelliSense に表示されます。

## <a name="guidelines-for-adding-vba-code-to-the-document"></a><a name="Guidelines"></a> ドキュメントへの VBA コードの追加に関するガイドライン
 ドキュメントの複数の異なるコピーに、ドキュメント レベル カスタマイズを呼び出す VBA コードを追加できます。

 ソリューションの開発およびテスト時には、Visual Studio でのプロジェクトのデバッグまたは実行中に開かれるドキュメント (つまり、ビルド出力フォルダー内のドキュメント) に VBA コードを記述できます。 ただし、Visual Studio はビルド出力フォルダー内のドキュメントをメイン プロジェクト フォルダーからのドキュメントのコピーで置き換えるので、このドキュメントに追加したすべての VBA は次にプロジェクトをビルドすると上書きされます。

 ソリューションのデバッグまたは実行の間にドキュメントに追加した VBA コードを保存する必要がある場合は、プロジェクト フォルダーのドキュメントに VBA コードをコピーします。 ビルド プロセスの詳細については、「[office ソリューションのビルド](../vsto/building-office-solutions.md)」を参照してください。

 ソリューションを配置する準備ができたら、主に次の 3 つの場所のドキュメントに VBA コードを追加できます。

### <a name="in-the-project-folder-on-the-development-computer"></a>開発用コンピューターのプロジェクト フォルダー内
 ドキュメント内の VBA コードとカスタム コードの両方を完全に制御できる場合は、この場所が便利です。 ドキュメントは開発用コンピューター上にあるため、カスタム コードを変更する場合は VBA コードを簡単に変更できます。 このドキュメント コピーに追加した VBA コードは、ソリューションをビルド、デバッグ、公開してもドキュメントに残ります。

 ドキュメントがデザイナーで開かれているときは、ドキュメントに VBA コードを追加できません。 最初にデザイナーでドキュメントを閉じてから、Word または Excel で直接ドキュメントを開く必要があります。

> [!CAUTION]
> ドキュメントを開くと実行される VBA コードを追加した場合は、まれに、このコードによってドキュメントが破壊されたり、デザイナーでドキュメントが開かなくなってしまったりする可能性があります。

### <a name="in-the-publish-or-installation-folder"></a>公開フォルダーまたはインストール フォルダー内
 場合によっては、公開フォルダーまたはインストール フォルダーのドキュメントに VBA コードを追加するのが適切な場合があります。 たとえば、Visual Studio がインストールされていないコンピューターを使用する別の開発者によって VBA コードが作成およびテストされる場合、このオプションを選択することがあります。

 ユーザーが公開フォルダーからソリューションを直接インストールする場合、ソリューションを公開するたびにドキュメントに VBA コードを追加する必要があります。 Visual Studio は、ソリューションが公開される公開場所のドキュメントを上書きします。

 ユーザーが公開フォルダーとは異なるインストール フォルダーからソリューションをインストールする場合は、ソリューションを公開するたびにドキュメントに VBA コードを追加する必要はありません。 公開の更新を公開フォルダーからインストール フォルダーに移動する準備ができたら、ドキュメント以外のすべてのファイルをインストール フォルダーにコピーします。

### <a name="on-the-end-user-computer"></a>エンド ユーザーのコンピューター上
 ドキュメント レベル カスタマイズで提供されるサービスを呼び出す VBA 開発者がエンド ユーザーである場合、ドキュメントのコピーの `CallVSTOAssembly` プロパティまたは `GetManagedClass` メソッドを使用して、コードの呼び出し方法をユーザーに伝えることができます。 ソリューションに対して更新プログラムを発行しても、エンド ユーザー コンピューター上のドキュメントの VBA コードは上書きされません。これは、更新プログラムの発行によってドキュメントが変更されることはないためです。

## <a name="tasks-performed-by-the-host-item-properties"></a><a name="PropertyTasks"></a> ホスト項目プロパティによって実行されるタスク
 **EnableVbaCallers** および **ReferenceAssemblyFromVbaProject** プロパティを使用するとき、Visual Studio は異なるタスク セットを実行します。

### <a name="enablevbacallers"></a>プロパティ
 Visual Basic プロジェクトでホスト項目の **EnableVbaCallers** プロパティを **True** に設定すると、Visual Studio は次のタスクを実行します。

1. <xref:Microsoft.VisualBasic.ComClassAttribute> および <xref:System.Runtime.InteropServices.ComVisibleAttribute> 属性をホスト項目クラスに追加します。

2. ホスト項目クラスの **GetAutomationObject** メソッドをオーバーライドします。

3. ホスト項目の **ReferenceAssemblyFromVbaProject** プロパティを **True** に設定します。

   **EnableVbaCallers** プロパティを **False** に戻すと、Visual Studio は次のタスクを実行します。

4. <xref:Microsoft.VisualBasic.ComClassAttribute> および <xref:System.Runtime.InteropServices.ComVisibleAttribute> 属性を `ThisDocument` クラスから削除します。

5. **GetAutomationObject** メソッドをホスト項目クラスから削除します。

   > [!NOTE]
   > Visual Studio は、自動的には **ReferenceAssemblyFromVbaProject** プロパティの設定を **False** に戻しません。 このプロパティは、[ **プロパティ** ] ウィンドウを使用して手動で **False** に設定できます。

### <a name="referenceassemblyfromvbaproject"></a>ReferenceAssemblyFromVbaProject
 Visual Basic または Visual C# プロジェクトでホスト項目の **ReferenceAssemblyFromVbaProject** プロパティを **True** に設定すると、Visual Studio は次のタスクを実行します。

1. カスタマイズ アセンブリのタイプ ライブラリを生成し、タイプ ライブラリをアセンブリに埋め込みます。

2. 次のタイプ ライブラリへの参照をドキュメントの VBA プロジェクトに追加します。

   - カスタマイズ アセンブリのタイプ ライブラリ。

   - Microsoft Visual Studio Tools for Office Execution Engine 9.0 のタイプ ライブラリ。 このタイプ ライブラリは [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]に含まれます。

   **ReferenceAssemblyFromVbaProject** プロパティを **False** に戻すと、Visual Studio は次のタスクを実行します。

3. ドキュメントの VBA プロジェクトから、タイプ ライブラリの参照を削除します。

4. アセンブリから埋め込まれているタイプ ライブラリを削除します。

## <a name="troubleshoot"></a>トラブルシューティング
 次の表では、一般的なエラーと、エラーを修正するための提案を示します。

|エラー|提案される解決策|
|-----------|----------------|
|**EnableVbaCallers** または **ReferenceAssemblyFromVbaProject** プロパティを設定した後、ドキュメントに VBA プロジェクトが含まれていない、またはドキュメント内の VBA プロジェクトに対するアクセス許可がないことを示すエラー メッセージが表示される。|プロジェクト内のドキュメントに少なくとも 1 つの VBA マクロが含まれていること、VBA プロジェクトに実行するための十分な信頼があること、および VBA プロジェクトがパスワードによって保護されていないことを確認します。|
|**EnableVbaCallers** または **ReferenceAssemblyFromVbaProject** プロパティを設定した後、<xref:System.Runtime.InteropServices.GuidAttribute> 宣言が存在しないか破損していることを示すエラー メッセージが表示されます。|<xref:System.Runtime.InteropServices.GuidAttribute> 宣言がプロジェクトの *AssemblyInfo.cs* または *AssemblyInfo.vb* ファイルにあること、およびこの属性に有効な GUID が設定されていることを確認します。|
|**EnableVbaCallers** または **ReferenceAssemblyFromVbaProject** プロパティを設定した後、<xref:System.Reflection.AssemblyVersionAttribute> によって指定されたバージョン番号が無効であることを示すエラー メッセージが表示されます。|プロジェクトの *AssemblyInfo.cs* または *AssemblyInfo.vb* ファイルに含まれる <xref:System.Reflection.AssemblyVersionAttribute> 宣言に、有効なアセンブリ バージョン番号が設定されていることを確認します。 有効なアセンブリのバージョン番号については、 <xref:System.Reflection.AssemblyVersionAttribute> クラスを参照してください。|
|カスタマイズ アセンブリの名前を変更した後、カスタマイズ アセンブリを呼び出す VBA コードが動作を停止する。|VBA コードに公開した後でカスタマイズ アセンブリの名前を変更すると、ドキュメントの VBA プロジェクトとカスタマイズ アセンブリの間のリンクが切れます。 この問題を解決するには、プロジェクトで **ReferenceFromVbaAssembly** プロパティを **False** に変更した後、 **True** に戻して、VBA コード内にある古いアセンブリ名への参照を新しいアセンブリ名に置き換えます。|

## <a name="see-also"></a>関連項目
- [方法: Visual Basic プロジェクトのコードを VBA に公開する](../vsto/how-to-expose-code-to-vba-in-a-visual-basic-project.md)
- [方法: Visual C&#35; プロジェクトでコードを VBA に公開する](../vsto/how-to-expose-code-to-vba-in-a-visual-csharp-project.md)
- [チュートリアル: Visual Basic プロジェクトのコードを VBA から呼び出す](../vsto/walkthrough-calling-code-from-vba-in-a-visual-basic-project.md)
- [チュートリアル : Visual C&#35; プロジェクトのコードを VBA から呼び出す](../vsto/walkthrough-calling-code-from-vba-in-a-visual-csharp-project.md)
- [Office ソリューションを設計して作成する](../vsto/designing-and-creating-office-solutions.md)
- [Visual Studio での VBA ソリューションと Office ソリューションの比較](../vsto/vba-and-office-solutions-in-visual-studio-compared.md)
- [プログラムのドキュメントレベルのカスタマイズ](../vsto/programming-document-level-customizations.md)
