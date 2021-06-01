---
title: '方法: C# プロジェクトのコードを VBA に公開する'
description: 2 種類のコードが相互に対話できるように、Visual C# プロジェクトのコードを Visual Basic for Applications (VBA) のコードに公開する方法について説明します。
ms.custom: seodec18, SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Visual C# [Office development in Visual Studio], exposing code to VBA
- VBA [Office development in Visual Studio], exposing code in document-level customizations
- document-level customizations [Office development in Visual Studio], exposing code
- exposing code to VBA
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 1df1eed4edec3efdbf93f4effc352b3d02656d04
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99889409"
---
# <a name="how-to-expose-code-to-vba-in-a-visual-c-project"></a>方法: Visual C# プロジェクトのコードを VBA に公開する
  Visual C# プロジェクトのコードを Visual Basic for Applications (VBA) のコードに公開して、2 種類のコードが相互に対話できるようにすることができます。

 Visual C# のプロセスは、Visual Basic のプロセスとは異なります。 詳細については、「[方法: Visual Basic プロジェクトのコードを VBA に公開する](../vsto/how-to-expose-code-to-vba-in-a-visual-basic-project.md)」を参照してください。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

## <a name="expose-code-in-a-visual-c-project"></a>Visual C# プロジェクトのコードを公開する
 VBA のコードで Visual C# プロジェクトのコードを呼び出せるようにするには、COM で認識できるようにコードを変更した後、デザイナーで **ReferenceAssemblyFromVbaProject** プロパティを **True** に設定します。

 VBA から Visual C# プロジェクトのメソッドを呼び出す方法を示すチュートリアルについては、「[チュートリアル: Visual C&#35; プロジェクトのコードを VBA から呼び出す](../vsto/walkthrough-calling-code-from-vba-in-a-visual-csharp-project.md)」を参照してください。

### <a name="to-expose-code-in-a-visual-c-project-to-vba"></a>Visual C# プロジェクトのコードを VBA に公開するには

1. マクロをサポートし、既に VBA コードが含まれている Word 文書、Excel ブック、または Excel テンプレートに基づくドキュメントレベルのプロジェクトを開くか、作成します。

    マクロをサポートするドキュメント ファイル形式の詳細については、「[VBA とドキュメントレベルのカスタマイズを結合する](../vsto/combining-vba-and-document-level-customizations.md)」を参照してください。

   > [!NOTE]
   > この機能は、Word テンプレート プロジェクトでは使用できません。

2. ドキュメント内の VBA コードが、ユーザーにマクロの有効化を求めることなく実行できることを確認します。 Word または Excel のセキュリティ センター設定の信頼できる場所の一覧に Office プロジェクトの場所を追加することによって、VBA コードの実行を信頼することができます。

3. VBA に公開するメンバーをプロジェクトのパブリック クラスに追加し、新しいメンバーを **public** と宣言します。

4. 次の <xref:System.Runtime.InteropServices.ComVisibleAttribute> 属性と <xref:System.Runtime.InteropServices.ClassInterfaceAttribute> 属性を、VBA に公開するクラスに適用します。 これらの属性によってクラスが COM で表示されるようになりますが、クラスのインターフェイスは生成されません。

   ```csharp
   [System.Runtime.InteropServices.ComVisible(true)]
   [System.Runtime.InteropServices.ClassInterface(
       System.Runtime.InteropServices.ClassInterfaceType.None)]
   ```

5. プロジェクトでホスト項目クラスの **GetAutomationObject** メンバーをオーバーライドして、VBA に公開したクラスのインスタンスを返すようにします。

   - ホスト項目クラスを VBA に公開する場合は、このクラスに属する **GetAutomationObject** メソッドをオーバーライドし、クラスの現在のインスタンスを返します。

     ```csharp
     protected override object GetAutomationObject()
     {
         return this;
     }
     ```

   - ホスト項目ではないクラスを VBA に公開する場合は、プロジェクトの任意のホスト項目の **GetAutomationObject** メソッドをオーバーライドし、非ホスト項目のクラスのインスタンスを返します。 たとえば、次のコードでは、`DocumentUtilities` という名前のクラスを VBA に公開することを想定しています。

     ```csharp
     protected override object GetAutomationObject()
     {
         return new DocumentUtilities();
     }
     ```

     ホスト項目の詳細については、「[ホスト項目とホスト コントロールの概要](../vsto/host-items-and-host-controls-overview.md)」を参照してください。

6. VBA に公開するクラスからインターフェイスを抽出します。 **[インターフェイスの抽出]** ダイアログ ボックスで、インターフェイス宣言に含めるパブリック メンバーを選択します。 詳細については、「[インターフェイスの抽出リファクタリング](../ide/reference/extract-interface.md)」を参照してください。

7. インターフェイス宣言に **public** キーワードを追加します。

8. インターフェイスに <xref:System.Runtime.InteropServices.ComVisibleAttribute> 属性を追加して、インターフェイスが COM に認識されるようにします。

   ```csharp
   [System.Runtime.InteropServices.ComVisible(true)]
   ```

9. [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] のデザイナーで文書 (Word の場合) またはワークシート (Excel の場合) を開きます。

10. **[プロパティ]** ウィンドウで、 **ReferenceAssemblyFromVbaProject** プロパティを選択し、値を **True** に変更します。

    > [!NOTE]
    > ブックまたは文書に VBA コードがまだ含まれていない場合、または文書内の VBA コードの実行が信頼されていない場合は、**ReferenceAssemblyFromVbaProject** プロパティを **True** に設定するとエラー メッセージが表示されます。 これは、このような状況では、Visual Studio がドキュメントのVBA プロジェクトを変更できないためです。

11. 表示されるメッセージで **[OK]** をクリックします。 このメッセージは、[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] からプロジェクトを実行しているときにブックまたは文書に VBA コードを追加すると、次回プロジェクトをビルドしたときに VBA コードが失われることを示しています。 これは、プロジェクトをビルドするたびに、ビルド出力フォルダー内のドキュメントが上書きされるためです。

     この時点で、VBA プロジェクトがアセンブリを呼び出すことができるように、Visual Studio によってプロジェクトが構成されます。 また、Visual Studio では、`GetManagedClass` という名前のメソッドが VBA プロジェクトに追加されます。 VBA プロジェクト内の任意の場所からこのメソッドを呼び出して、VBA に公開したクラスにアクセスできます。

12. プロジェクトをビルドします。

## <a name="see-also"></a>関連項目
- [方法: Visual Studio で Office プロジェクトを作成する](../vsto/how-to-create-office-projects-in-visual-studio.md)
- [Office ソリューションを設計して作成する](../vsto/designing-and-creating-office-solutions.md)
- [VBA とドキュメント レベルのカスタマイズを結合する](../vsto/combining-vba-and-document-level-customizations.md)
- [チュートリアル: Visual C&#35; プロジェクトのコードを VBA から呼び出す](../vsto/walkthrough-calling-code-from-vba-in-a-visual-csharp-project.md)
- [方法: Visual Basic プロジェクトのコードを VBA に公開する](../vsto/how-to-expose-code-to-vba-in-a-visual-basic-project.md)
