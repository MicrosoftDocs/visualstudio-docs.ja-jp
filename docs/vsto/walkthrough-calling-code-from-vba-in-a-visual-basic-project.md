---
title: 'チュートリアル: Visual Basic プロジェクトのコードを VBA から呼び出す'
description: ドキュメント内の Visual Basic for Applications (VBA) コードから Microsoft Word 用のドキュメント レベルのカスタマイズ内のメソッドを呼び出す方法について説明します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio], Visual Basic for Applications and
- ThisDocument class
- Word [Office development in Visual Studio], calling code from VBA
- Visual Basic [Office development in Visual Studio], calling code from VBA
- VBA [Office development in Visual Studio], calling code in document-level customizations
- Office documents [Office development in Visual Studio, Visual Basic for Applications and
- calling code from VBA
- document-level customizations [Office development in Visual Studio], calling code
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: f4fe056f70e0af03809b43d60968bd8a1a50bf08
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107824485"
---
# <a name="walkthrough-call-code-from-vba-in-a-visual-basic-project"></a>チュートリアル: Visual Basic プロジェクトのコードを VBA から呼び出す
  このチュートリアルでは、ドキュメント内の Visual Basic for Applications (VBA) コードから Microsoft Office Word 用のドキュメント レベルのカスタマイズ内のメソッドを呼び出す方法を示します。 このプロシージャには次の 3 つの基本的な手順が含まれます。 `ThisDocument` ホスト項目クラスにメソッドを追加する、VBA コードにメソッドを公開する、および、ドキュメント内の VBA コードからメソッドを呼び出す、の 3 つです。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

 このチュートリアルでは具体的には Word を使用していますが、チュートリアルで示されるコンセプトは Excel のドキュメント レベルのプロジェクトにも適用されます。

 このチュートリアルでは、次の作業について説明します。

- VBA コードが含まれるドキュメントを作成する。

- Word のセキュリティ センターを使用して、ドキュメントの場所を信頼する。

- `ThisDocument` ホスト項目クラスにメソッドを追加する。

- VBA コードにメソッドを公開する。

- VBA コードからメソッドを呼び出す。

> [!NOTE]
> 次の手順で参照している Visual Studio ユーザー インターフェイス要素の一部は、お使いのコンピューターでは名前や場所が異なる場合があります。 これらの要素は、使用している Visual Studio のエディションや独自の設定によって決まります。 詳細については、「[Visual Studio IDE のカスタマイズ](../ide/personalizing-the-visual-studio-ide.md)」を参照してください。

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを実行するには、次のコンポーネントが必要です。

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- Microsoft Word

## <a name="create-a-document-that-contains-vba-code"></a>VBA コードが含まれるドキュメントを作成する
 最初の手順では、単純な VBA マクロを含むマクロ対応のドキュメントを作成します。 そのドキュメントに基づいた Visual Studio プロジェクトを作成する前に、ドキュメントに VBA プロジェクトを含める必要があります。 含めないと、Visual Studio は VBA プロジェクトを変更して、VBA コードがカスタマイズ アセンブリを呼び出せるようにすることができません。

 使用する VBA コードを含むドキュメントが既にある場合は、この手順を省略できます。

### <a name="to-create-a-document-that-contains-vba-code"></a>VBA コードが含まれるドキュメントを作成するには

1. Word を起動します。

2. 作業中のドキュメントを **DocumentWithVBA** という名前で、Word の **マクロ有効文書 (\*.docm)** として保存します。 このブックは、デスクトップなどの便利な場所に保存します。

3. リボンの **[開発]** タブをクリックします。

    > [!NOTE]
    > **[開発]** タブが表示されていない場合は、最初にこれを表示する必要があります。 詳細については、「[方法: [開発者] タブをリボンに表示する](../vsto/how-to-show-the-developer-tab-on-the-ribbon.md)」を参照してください。

4. **[コード]** グループの **[Visual Basic]** をクリックします。

     Visual Basic エディターが開きます。

5. **[プロジェクト]** ウィンドウで、 **[ThisDocument]** をダブルクリックします。

     `ThisDocument` オブジェクトのコード ファイルが開きます。

6. コード ファイルに次の VBA コードを追加します。 このコードは何も実行しない単純な関数を定義します。 この関数の唯一の目的は、VBA プロジェクトがドキュメント内に確実に存在するようにすることです。 これは、このチュートリアルの後の手順に必要です。

    ```vb
    Sub EmptySub()
    End Sub
    ```

7. ドキュメントを保存して、Word を終了します。

## <a name="create-the-project"></a>プロジェクトを作成する
 これで、先ほど作成したマクロ対応のドキュメントを使用する、Word のドキュメント レベルのプロジェクトを作成できます。

### <a name="to-create-a-new-project"></a>新しいプロジェクトを作成するには

1. [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]を起動します。

2. **[ファイル]** メニューの **[新規作成]** をポイントし、 **[プロジェクト]** をクリックします。 IDE が Visual Basic 開発設定を使用するように設定されている場合は、 **[ファイル]** メニューの **[新しいプロジェクト]** をクリックします。

3. テンプレート ウィンドウで、 **[Visual Basic]** を展開してから、 **[Office/SharePoint]** を展開します。

4. **[Office アドイン]** ノードを選択します。

5. プロジェクト テンプレートのリストで、 **[Word 2010 ドキュメント]** または **[Word 2013 ドキュメント]** プロジェクトを選択します。

6. **[名前]** ボックスに、 **「CallingCodeFromVBA」** と入力します。

7. **[OK]** をクリックします。

     **Visual Studio Tools for Office プロジェクト ウィザード** が開きます。

8. **[既存のドキュメントをコピーする]** を選択し、 **[既存のドキュメントの完全なパス]** ボックスで、先ほど作成した **DocumentWithVBA** ドキュメントの場所を指定します。 独自のマクロ対応ドキュメントを使用している場合は、代わりにそのドキュメントの場所を指定します。

9. **[完了]** をクリックします。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] はデザイナーで **DocumentWithVBA** ドキュメントを開き、 **ソリューション エクスプローラー** に **CallingCodeFromVBA** プロジェクトを追加します。

## <a name="trust-the-location-of-the-document"></a>ドキュメントの場所を信頼する
 ソリューションのコードをドキュメント内の VBA コードに公開する前に、実行するドキュメント内の VBA を信頼する必要があります。 これを行うには、いくつかの方法があります。 このチュートリアルでは、Word の **セキュリティ センター** で、ドキュメントの場所を信頼します。

### <a name="to-trust-the-location-of-the-document"></a>ドキュメントの場所を信頼するには

1. Word を起動します。

2. **[ファイル]** タブをクリックします。

3. **[Word のオプション]** ボタンをクリックします。

4. [カテゴリ] ウィンドウで **[セキュリティ センター]** をクリックします。

5. 詳細ウィンドウで **[セキュリティ センターの設定]** をクリックします。

6. [カテゴリ] ウィンドウで **[信頼できる場所]** をクリックします。

7. 詳細ウィンドウで **[新しい場所の追加]** をクリックします。

8. **[Microsoft Office の信頼できる場所]** ダイアログ ボックスで、 **CallingCodeFromVBA** プロジェクトを含むフォルダーを参照します。

9. **[この場所のサブフォルダも信頼する]** を選択します。

10. **[Microsoft Office の信頼できる場所]** ダイアログ ボックスで、 **[OK]** をクリックします。

11. **[セキュリティ センター]** ダイアログ ボックスで **[OK]** をクリックします。

12. **[Word のオプション]** ダイアログ ボックスで **[OK]** をクリックします。

13. Word を終了します。

## <a name="add-a-method-to-the-thisdocument-class"></a>ThisDocument クラスにメソッドを追加する
 VBA プロジェクトのセットアップができたので、今度は VBA コードから呼び出すことのできる `ThisDocument` ホスト項目クラスにメソッドを追加します。

### <a name="to-add-a-method-to-the-thisdocument-class"></a>ThisDocument クラスにメソッドを追加するには

1. **ソリューション エクスプローラー** で **ThisDocument.vb** を右クリックし、 **[コードの表示]** をクリックします。

     コード エディターで **ThisDocument** ファイルが開きます。

2. `ThisDocument` クラスに次のメソッドを追加します。 このメソッドは、ドキュメントの先頭に 2 行 2 列の表を作成します。 パラメーターは、最初の行に表示されるテキストを指定します。 このチュートリアルの後半では、ドキュメント内の VBA コードからこのメソッドを呼び出します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/CallingCodeFromVBA/ThisDocument.vb" id="Snippet1":::

3. プロジェクトをビルドします。

## <a name="expose-the-method-to-vba-code"></a>メソッドを VBA コードに公開する
 `CreateTable` メソッドをドキュメント内の VBA コードに公開するには、 **ホスト項目の** EnableVbaCallers `ThisDocument` プロパティを **True** に設定します。

### <a name="to-expose-the-method-to-vba-code"></a>メソッドを VBA コードに公開するには

1. **ソリューション エクスプローラー** で、 **ThisDocument.vb** をダブルクリックします。

     デザイナーで **DocumentWithVBA** ファイルが開きます。

2. **[プロパティ]** ウィンドウで、 **EnableVbaCallers** プロパティを選択し、値を **True** に変更します。

3. 表示されるメッセージで **[OK]** をクリックします。

4. プロジェクトをビルドします。

## <a name="call-the-method-from-vba-code"></a>VBA コードからメソッドを呼び出す
 これで、ドキュメント内の VBA コードから `CreateTable` メソッドを呼び出せます。

> [!NOTE]
> このチュートリアルでは、プロジェクトのデバッグ中に VBA コードをドキュメントに追加します。 Visual Studio はビルド出力フォルダー内のドキュメントをメイン プロジェクト フォルダーからのドキュメントのコピーで置き換えるので、このドキュメントに追加したすべての VBA コードは次にプロジェクトをビルドすると上書きされます。 VBA コードを保存したい場合は、プロジェクト フォルダー内のドキュメントにコピーします。 詳細については、「[VBA とドキュメント レベルのカスタマイズを結合する](../vsto/combining-vba-and-document-level-customizations.md)」を参照してください。

### <a name="to-call-the-method-from-vba-code"></a>VBA コードからメソッドを呼び出すには

1. **F5** キーを押してプロジェクトを実行します。

2. **[開発者]** タブで、 **[コード]** グループの、 **[Visual Basic]** をクリックします。

     Visual Basic エディターが開きます。

3. **[挿入]** メニューで **[モジュール]** をクリックします。

4. 次のコードを新しいモジュールに追加します。

     このコードはカスタマイズ アセンブリの `CreateTable` メソッドを呼び出します。 マクロは `CallVSTOAssembly` オブジェクトの `ThisDocument` プロパティを使用して、このメソッドにアクセスします。 このプロパティは、このチュートリアルで先ほど **EnableVbaCallers** プロパティを設定したときに自動的に生成されたものです。

    ```vb
    Sub CreateTable()
        Call ThisDocument.CallVSTOAssembly.CreateTable("Employee Name", "Start Date")
    End Sub
    ```

5. **F5** キーを押します。

6. 新しい表がドキュメントに追加されたことを確認します。

7. 変更を保存せずに Word を終了します。

## <a name="next-steps"></a>次のステップ
 Office ソリューションでの VBA からのコード呼び出しについて詳しくは、次のトピックを参照してください。

- VBA から Visual C# カスタマイズのコードを呼び出します。 このプロセスは、Visual Basic のプロセスとは異なります。 詳細については、「[チュートリアル: Visual C&#35; プロジェクトのコードを VBA から呼び出す](../vsto/walkthrough-calling-code-from-vba-in-a-visual-csharp-project.md)」を参照してください。

- VBA から VSTO アドインのコードを呼び出します。 詳細については、「[チュートリアル: VSTO アドイン内のコードを VBA から呼び出す](../vsto/walkthrough-calling-code-in-a-vsto-add-in-from-vba.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [VBA とドキュメント レベルのカスタマイズを結合する](../vsto/combining-vba-and-document-level-customizations.md)
- [ドキュメント レベルのカスタマイズのプログラミング](../vsto/programming-document-level-customizations.md)
- [方法: Visual Basic プロジェクトのコードを VBA に公開する](../vsto/how-to-expose-code-to-vba-in-a-visual-basic-project.md)
- [方法: Visual C&#35; プロジェクトのコードを VBA に公開する](../vsto/how-to-expose-code-to-vba-in-a-visual-csharp-project.md)
- [チュートリアル : Visual C&#35; プロジェクトのコードを VBA から呼び出す](../vsto/walkthrough-calling-code-from-vba-in-a-visual-csharp-project.md)
