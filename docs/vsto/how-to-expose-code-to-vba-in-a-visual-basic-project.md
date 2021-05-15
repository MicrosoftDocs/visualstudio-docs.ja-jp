---
title: '方法: Visual Basic プロジェクトのコードを VBA に公開する'
description: 2 種類のコードが相互に対話できるように、Visual Basic プロジェクトのコードを Visual Basic for Applications (VBA) コードに公開する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- VBA [Office development in Visual Studio], exposing code in document-level customizations
- document-level customizations [Office development in Visual Studio], exposing code
- Visual Basic [Office development in Visual Studio], exposing code to VBA
- exposing code to VBA
- host items [Office development in Visual Studio], exposing code to VBA
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 69ef8b47ac4038b466d0ebf859832bd4363403cd
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99913491"
---
# <a name="how-to-expose-code-to-vba-in-a-visual-basic-project"></a>方法: Visual Basic プロジェクトのコードを VBA に公開する
  2 種類のコードが相互に対話できるように、[!INCLUDE[vbprvb](../sharepoint/includes/vbprvb-md.md)] プロジェクトのコードを Visual Basic for Applications (VBA) コードに公開する方法について説明します。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

 Visual Basic のプロセスは、Visual C# のプロセスとは異なります。 詳細については、「[方法: Visual C&#35; プロジェクトのコードを VBA に公開する](../vsto/how-to-expose-code-to-vba-in-a-visual-csharp-project.md)」を参照してください。

 このプロセスは、ホスト項目クラスのコードと他のクラスのコードで異なります。

- [ホスト項目クラスでコードを公開する](#HostItemCode)

- [ホスト項目クラスに含まれていないコードを公開する](#NonHostItem)

## <a name="expose-code-in-a-host-item-class"></a><a name="HostItemCode"></a> ホスト項目クラスでコードを公開する
 VBA コードでホスト項目クラスの Visual Basic コードを呼び出せるようにするには、ホスト項目の **EnableVbaCallers** プロパティを **True** に設定します。

 ホスト項目クラスのメソッドを公開してから VBA から呼び出す方法を示すチュートリアルについては、「[チュートリアル: Visual Basic プロジェクトの VBA からコードを呼び出す](../vsto/walkthrough-calling-code-from-vba-in-a-visual-basic-project.md)」を参照してください。 ホスト項目の詳細については、「[ホスト項目とホスト コントロールの概要](../vsto/host-items-and-host-controls-overview.md)」を参照してください。

#### <a name="to-expose-code-in-a-host-item-to-vba"></a>ホスト項目のコードを VBA に公開する

1. マクロをサポートし、既に VBA コードが含まれている Word 文書、Excel ブック、または Excel テンプレートに基づくドキュメントレベルの [!INCLUDE[vbprvb](../sharepoint/includes/vbprvb-md.md)] プロジェクトを開くか、作成します。

     マクロをサポートするドキュメント ファイル形式の詳細については、「[VBA とドキュメントレベルのカスタマイズを結合する](../vsto/combining-vba-and-document-level-customizations.md)」を参照してください。

    > [!NOTE]
    > この機能は、Word テンプレート プロジェクトでは使用できません。

2. ドキュメント内の VBA コードが、ユーザーにマクロの有効化を求めることなく実行できることを確認します。 Word または Excel のセキュリティ センター設定の信頼できる場所の一覧に Office プロジェクトの場所を追加することによって、VBA コードの実行を信頼することができます。

3. VBA に公開するプロパティ、メソッド、またはイベントをプロジェクトのホスト項目クラスのいずれかに追加し、新しいメンバーを **Public** と宣言します。 クラスの名前は、アプリケーションによって異なります。

    - Word プロジェクトでは、ホスト項目クラスには既定で `ThisDocument` という名前が付けられます。

    - Excel プロジェクトでは、ホスト項目クラスには既定で `ThisWorkbook`、`Sheet1`、`Sheet2`、または `Sheet3` という名前が付けられます。

4. ホスト項目の **EnableVbaCallers** プロパティを **True** に設定します。 このプロパティは、デザイナーでホスト項目が開いているときに、 **[プロパティ]** ウィンドウで使用できます。

     このプロパティを設定すると、Visual Studio によって自動的に **ReferenceAssemblyFromVbaProject** プロパティが **True** に設定されます。

    > [!NOTE]
    > ブックまたはドキュメントに VBA コードがまだ含まれていない場合、またはドキュメント内の VBA コードの実行が信頼されていない場合は、**EnableVbaCallers** プロパティを **True** に設定するとエラー メッセージが表示されます。 これは、このような状況では、Visual Studio がドキュメントのVBA プロジェクトを変更できないためです。

5. 表示されるメッセージで **[OK]** をクリックします。 このメッセージは、[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] からプロジェクトを実行しているときにブックまたはドキュメントに VBA コードを追加すると、次回プロジェクトをビルドしたときに VBA コードが失われることを示しています。 これは、プロジェクトをビルドするたびに、ビルド出力フォルダー内のドキュメントが上書きされるためです。

     この時点で、VBA プロジェクトがアセンブリを呼び出すことができるように、Visual Studio によってプロジェクトが構成されます。 また、Visual Studio では、`CallVSTOAssembly` という名前のプロパティが、VBA プロジェクトの `ThisDocument`、`ThisWorkbook`、`Sheet1`、`Sheet2`、または `Sheet3` モジュールに追加されます。 このプロパティを使用して、VBA コードに公開したクラスのパブリック メンバーにアクセスできます。

6. プロジェクトをビルドします。

## <a name="expose-code-that-is-not-in-a-host-item-class"></a><a name="NonHostItem"></a> ホスト項目クラスに含まれていないコードを公開する
 VBA コードでホスト項目クラスに含まれていない Visual Basic コードを呼び出せるようにするには、コードを変更して VBA で認識されるようにします。

### <a name="to-expose-code-that-is-not-in-a-host-item-class-to-vba"></a>ホスト項目クラスに含まれていないコードを VBA に公開するには

1. マクロをサポートし、既に VBA コードが含まれている Word 文書、Excel ブック、または Excel テンプレートに基づくドキュメントレベルの [!INCLUDE[vbprvb](../sharepoint/includes/vbprvb-md.md)] プロジェクトを開くか、作成します。

     マクロをサポートするドキュメント ファイル形式の詳細については、「[VBA とドキュメントレベルのカスタマイズを結合する](../vsto/combining-vba-and-document-level-customizations.md)」を参照してください。

    > [!NOTE]
    > この機能は、Word テンプレート プロジェクトでは使用できません。

2. ドキュメント内の VBA コードが、ユーザーにマクロの有効化を求めることなく実行できることを確認します。 Word または Excel のセキュリティ センター設定の信頼できる場所の一覧に Office プロジェクトの場所を追加することによって、VBA コードの実行を信頼することができます。

3. VBA に公開するメンバーをプロジェクトのパブリック クラスに追加し、新しいメンバーを **public** と宣言します。

4. 次の <xref:System.Runtime.InteropServices.ComVisibleAttribute> 属性と <xref:Microsoft.VisualBasic.ComClassAttribute> 属性を、VBA に公開するクラスに適用します。 これらの属性により、VBA クラスでクラスが認識されるようになります。

    ```vb
    <Microsoft.VisualBasic.ComClass()> _
    <System.Runtime.InteropServices.ComVisibleAttribute(True)> _
    ```

5. プロジェクトでホスト項目クラスの **GetAutomationObject** メンバーをオーバーライドして、VBA に公開したクラスのインスタンスを返すようにします。 次のコード例では、`DocumentUtilities` という名前のクラスを VBA に公開することを前提としています。

    ```vb
    Protected Overrides Function GetAutomationObject() As Object
        Return New DocumentUtilities()
    End Function
    ```

6. [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] でドキュメント (Word の場合) またはワークシート (Excel の場合) デザイナーを開きます。

7. **[プロパティ]** ウィンドウで、 **ReferenceAssemblyFromVbaProject** プロパティを選択し、値を **True** に変更します。

    > [!NOTE]
    > ブックまたはドキュメントに VBA コードがまだ含まれていない場合、またはドキュメント内の VBA コードの実行が信頼されていない場合は、**ReferenceAssemblyFromVbaProject** プロパティを **True** に設定するとエラー メッセージが表示されます。 これは、このような状況では、Visual Studio がドキュメントのVBA プロジェクトを変更できないためです。

8. 表示されるメッセージで **[OK]** をクリックします。 このメッセージは、[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] からプロジェクトを実行しているときにブックまたはドキュメントに VBA コードを追加すると、次回プロジェクトをビルドしたときに VBA コードが失われることを示しています。 これは、プロジェクトをビルドするたびに、ビルド出力フォルダー内のドキュメントが上書きされるためです。

     この時点で、VBA プロジェクトがアセンブリを呼び出すことができるように、Visual Studio によってプロジェクトが構成されます。 また、Visual Studio では、`GetManagedClass` という名前のメソッドが VBA プロジェクトに追加されます。 VBA プロジェクト内の任意の場所からこのメソッドを呼び出して、VBA に公開したクラスにアクセスできます。

9. プロジェクトをビルドします。

## <a name="see-also"></a>関連項目
- [方法: Visual Studio で Office プロジェクトを作成する](../vsto/how-to-create-office-projects-in-visual-studio.md)
- [Office ソリューションを設計して作成する](../vsto/designing-and-creating-office-solutions.md)
- [VBA とドキュメントレベルのカスタマイズを結合する](../vsto/combining-vba-and-document-level-customizations.md)
- [チュートリアル: Visual Basic プロジェクトのコードを VBA から呼び出す](../vsto/walkthrough-calling-code-from-vba-in-a-visual-basic-project.md)
- [方法: Visual C&#35; プロジェクトでコードを VBA に公開する](../vsto/how-to-expose-code-to-vba-in-a-visual-csharp-project.md)
