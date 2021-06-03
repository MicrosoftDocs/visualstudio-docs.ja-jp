---
title: 'チュートリアル: カスタム XML 部分へのコンテンツ コントロールのバインド'
description: Word のドキュメント レベルのカスタマイズで、コンテンツ コントロールを同じ文書内の XML データにバインドする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- PlainTextContentControl, binding to a custom XML part
- custom XML parts, binding to content controls
- content controls [Office development in Visual Studio], data binding
- data binding [Office development in Visual Studio], content controls
- DropDownListContentControl, binding items to a custom XML part
- DatePickerContentControl, binding to a custom XML part
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 6e4a10949f463cc769890b828ba39de30a9b4c1c
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107824576"
---
# <a name="walkthrough-bind-content-controls-to-custom-xml-parts"></a>チュートリアル: カスタム XML 部分へのコンテンツ コントロールのバインド
  このチュートリアルでは、Word のドキュメント レベルのカスタマイズで、コンテンツ コントロールを同じ文書内の XML データにバインドする方法を説明します。

 [!INCLUDE[appliesto_wdalldoc](../vsto/includes/appliesto-wdalldoc-md.md)]

 Word では、"*カスタム XML 部分*" と呼ばれる XML データを文書内に格納できます。 このデータの表示は、カスタム XML 部分の要素にコンテンツ コントロールをバインドすることによって制御できます。 このチュートリアルで例として示す文書のカスタム XML 部分には、従業員情報が格納されています。 この文書を開くと、XML 要素の値がコンテンツ コントロールに表示されます。 コンテンツ コントロール内のテキストに加えた変更は、カスタム XML 部分に保存されます。

 このチュートリアルでは、次の作業について説明します。

- デザイン時におけるドキュメント レベルのプロジェクトの Word 文書へのコンテンツ コントロールの追加

- XML データ ファイルと、コンテンツ コントロールにバインドする要素を定義する XML スキーマを作成する。

- デザイン時に XML スキーマを文書に添付する。

- 実行時に XML ファイルの内容を文書内のカスタム XML 部分に追加する。

- コンテンツ コントロールをカスタム XML 部分の要素にバインドする。

- <xref:Microsoft.Office.Tools.Word.DropDownListContentControl> を XML スキーマに定義された値にバインドする。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを実行するには、次のコンポーネントが必要です。

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- Microsoft Word

## <a name="create-a-new-word-document-project"></a>Word 文書プロジェクトを作成する
 このチュートリアルで使用する Word 文書を作成します。

### <a name="to-create-a-new-word-document-project"></a>Word 文書プロジェクトを作成するには

1. **EmployeeControls** という名前の Word 文書プロジェクトを作成します。 ソリューションの新しい文書を作成します。 詳細については、「[方法: Visual Studio で Office プロジェクトを作成する](../vsto/how-to-create-office-projects-in-visual-studio.md)」を参照してください。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] によって、デザイナーで新しい Word 文書が開き、**ソリューション エクスプローラー** に **EmployeeControls** プロジェクトが追加されます。

## <a name="add-content-controls-to-the-document"></a>文書にコンテンツ コントロールを追加する
 ユーザーが従業員に関する情報を表示または編集できる 3 種類のコンテンツ コントロールが含まれるテーブルを作成します。

### <a name="to-add-content-controls-to-the-document"></a>文書にコンテンツ コントロールを追加するには

1. [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] デザイナーでホストされている Word 文書のリボンで **[挿入]** タブを選択します。

2. **[表]** グループの **[表]** を選択し、2 列 3 行の表を挿入します。

3. 最初の列に次のようにテキストを入力します。

   ||
   |-|
   |**Employee Name**|
   |**Hire Date**|
   |**Title**|

4. 2 つ目の列の最初の行 (**Employee Name** の隣) を選択します。

5. リボンの **[開発]** タブを選択します。

   > [!NOTE]
   > **[開発]** タブが表示されていない場合は、最初にこれを表示する必要があります。 詳細については、「[方法: [開発者] タブをリボンに表示する](../vsto/how-to-show-the-developer-tab-on-the-ribbon.md)」を参照してください。

6. **[コントロール]** グループの **[テキスト]** ボタン ![PlainTextContentControl](../vsto/media/plaintextcontrol.gif "PlainTextContentControl") を選択し、最初のセルに <xref:Microsoft.Office.Tools.Word.PlainTextContentControl> を追加します。

7. 2 つ目の列の 2 つ目の行 (**Hire Date** の隣) を選択します。

8. **[コントロール]** グループの **[日付の選択]** ボタン ![DatePickerContentControl](../vsto/media/datepicker.gif "DatePickerContentControl") を選択し、2 番目のセルに <xref:Microsoft.Office.Tools.Word.DatePickerContentControl> を追加します。

9. 2 つ目の列の 3 つ目の行 ( **[Title]** の隣) を選択します。

10. **[コントロール]** グループの **[ドロップダウン リスト]** ボタン ![DropDownListContentControl](../vsto/media/dropdownlist.gif "DropDownListContentControl") を選択し、最後のセルに <xref:Microsoft.Office.Tools.Word.DropDownListContentControl> を追加します。

    これで、このプロジェクトのユーザー インターフェイスが完成しました。 ここでこのプロジェクトを実行すると、最初の行にテキストを入力し、2 つ目の行で日付を選択できます。 次の手順では、表示するデータを XML ファイル内の文書に添付します。

## <a name="create-the-xml-data-file"></a>XML データ ファイルを作成する
 通常は、ファイルやデータベースなどの外部ソースからカスタム XML 部分に格納する XML 文字列を取得する必要があります。 このチュートリアルでは、文書内のコンテンツ コントロールにバインドする要素でマークされた従業員データを含む、XML ファイルを作成します。 実行時に使用可能にするため、カスタマイズ アセンブリのリソースとして XML ファイルを埋め込みます。

#### <a name="to-create-the-data-file"></a>データ ファイルを作成するには

1. **[プロジェクト]** メニューの **[新しい項目の追加]** をクリックします。

     **[新しい項目の追加]** ダイアログ ボックスが表示されます。

2. **[テンプレート]** ペインで、 **[XML ファイル]** を選択します。

3. このファイルに **employees.xml** という名前を付け、 **[追加]** ボタンを選択します。

     コード エディターで **employees.xml** ファイルが開きます。

4. **employees.xml** ファイルの内容を次のテキストに置き換えます。

    ```xml
    <?xml version="1.0" encoding="utf-8" ?>
    <employees xmlns="http://schemas.microsoft.com/vsto/samples">
      <employee>
        <name>Karina Leal</name>
        <hireDate>1999-04-01</hireDate>
        <title>Manager</title>
      </employee>
    </employees>
    ```

5. **ソリューション エクスプローラー** で **employees.xml** ファイルを選択します。

6. **[プロパティ]** ウィンドウで **[ビルド アクション]** プロパティを選択し、値を **[埋め込まれたリソース]** に変更します。

     この操作によって、プロジェクトをビルドしたときに、XML ファイルがリソースとしてアセンブリに埋め込まれます。 これにより、実行時に XML ファイルの内容にアクセスできます。

## <a name="create-an-xml-schema"></a>XML スキーマを作成する
 コンテンツ コントロールをカスタム XML 部分の 1 つの要素にバインドする場合は、XML スキーマを使用する必要はありません。 ただし、<xref:Microsoft.Office.Tools.Word.DropDownListContentControl> を複数の値にバインドする場合は、前の手順で作成した XML データ ファイルを検証する XML スキーマを作成する必要があります。 XML スキーマには、`title` 要素に割り当てることができる値を定義します。 このチュートリアルの後半で、この要素に <xref:Microsoft.Office.Tools.Word.DropDownListContentControl> をバインドします。

#### <a name="to-create-an-xml-schema"></a>XML スキーマを作成するには

1. **[プロジェクト]** メニューの **[新しい項目の追加]** をクリックします。

     **[新しい項目の追加]** ダイアログ ボックスが表示されます。

2. **[テンプレート]** ペインで、 **[XML スキーマ]** を選択します。

3. このスキーマに **employees.xsd** という名前を付け、 **[追加]** ボタンを選択します。

     スキーマ デザイナーが開きます。

4. **ソリューション エクスプローラー** で、**employees.xsd** のショートカット メニューを開き、 **[コードの表示]** を選択します。

5. **employees.xsd** ファイルの内容を次のスキーマに置き換えます。

    ```xml
    <?xml version="1.0" encoding="utf-8" ?>
    <xs:schema xmlns="http://schemas.microsoft.com/vsto/samples"
        targetNamespace="http://schemas.microsoft.com/vsto/samples"
        xmlns:xs="http://www.w3.org/2001/XMLSchema"
        elementFormDefault="qualified">
      <xs:element name="employees" type="EmployeesType"></xs:element>
      <xs:complexType name="EmployeesType">
        <xs:all>
          <xs:element name="employee" type="EmployeeType"/>
        </xs:all>
      </xs:complexType>
      <xs:complexType name="EmployeeType">
        <xs:sequence>
          <xs:element name="name" type="xs:string" minOccurs="1" maxOccurs="1"/>
          <xs:element name="hireDate" type="xs:date" minOccurs="1" maxOccurs="1"/>
          <xs:element name="title" type="TitleType" minOccurs="1" maxOccurs="1"/>
        </xs:sequence>
      </xs:complexType>
      <xs:simpleType name="TitleType">
        <xs:restriction base="xs:string">
          <xs:enumeration value ="Engineer"/>
          <xs:enumeration value ="Designer"/>
          <xs:enumeration value ="Manager"/>
        </xs:restriction>
      </xs:simpleType>
    </xs:schema>
    ```

6. **[ファイル]** メニューの **[すべてを保存]** をクリックして、**employees.xml** ファイルおよび **employees.xsd** ファイルに加えた変更を保存します。

## <a name="attach-the-xml-schema-to-the-document"></a>XML スキーマを文書に添付する
 <xref:Microsoft.Office.Tools.Word.DropDownListContentControl> を `title` 要素の有効な値にバインドするためには、XML スキーマを文書に添付する必要があります。

### <a name="to-attach-the-xml-schema-to-the-document--word_15_short"></a>XML スキーマを文書に添付するには ([!INCLUDE[Word_15_short](../vsto/includes/word-15-short-md.md)])

1. デザイナーで **EmployeeControls.docx** をアクティブにします。

2. リボンの **[開発]** タブを選択し、 **[アドイン]** ボタンを選択します。

3. **[テンプレートとアドイン]** ダイアログ ボックスの **[XML スキーマ]** タブを選択し、 **[スキーマの追加]** ボタンを選択します。

4. プロジェクト ディレクトリを開き、前の手順で作成した **employees.xsd** スキーマを選択し、 **[開く]** ボタンを選択します。

5. **[スキーマの設定]** ダイアログ ボックスで **[OK]** ボタンを選択します。

6. **[OK]** ボタンを選択して **[テンプレートとアドイン]** ダイアログ ボックスを閉じます。

### <a name="to-attach-the-xml-schema-to-the-document-word-2010"></a>XML スキーマをドキュメントに添付するには (Word 2010)

1. デザイナーで **EmployeeControls.docx** をアクティブにします。

2. リボンの **[開発]** タブを選択します。

3. **[XML]** グループで、 **[スキーマ]** ボタンを選択します。

4. **[テンプレートとアドイン]** ダイアログ ボックスの **[XML スキーマ]** タブを選択し、 **[スキーマの追加]** ボタンを選択します。

5. プロジェクト ディレクトリを開き、前の手順で作成した **employees.xsd** スキーマを選択し、 **[開く]** ボタンを選択します。

6. **[スキーマの設定]** ダイアログ ボックスで **[OK]** ボタンを選択します。

7. **[OK]** ボタンを選択して **[テンプレートとアドイン]** ダイアログ ボックスを閉じます。

     **[XML データ構造]** 作業ウィンドウが開きます。

8. **[XML データ構造]** 作業ウィンドウを閉じます。

## <a name="add-a-custom-xml-part-to-the-document"></a>カスタム XML 部分を文書に追加する
 コンテンツ コントロールを XML ファイル内の要素にバインドするためには、XML ファイルの内容を文書内の新しいカスタム XML 部分に追加する必要があります。

### <a name="to-add-a-custom-xml-part-to-the-document"></a>カスタム XML 部分を文書に追加するには

1. **ソリューション エクスプローラー** で **ThisDocument.cs** または **ThisDocument.vb** のショートカット メニューを開き、 **[コードの表示]** を選択します。

2. `ThisDocument` クラスに次の宣言を追加します。 このコードでは、カスタム XML 部分を文書に追加するために使用する複数のオブジェクトを宣言しています。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/EmployeeControls/ThisDocument.cs" id="Snippet1":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/EmployeeControls/ThisDocument.vb" id="Snippet1":::

3. `ThisDocument` クラスに次のメソッドを追加します。 このメソッドは、アセンブリにリソースとして埋め込まれている XML データ ファイルの内容を取得し、それを XML 文字列として返します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/EmployeeControls/ThisDocument.cs" id="Snippet3":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/EmployeeControls/ThisDocument.vb" id="Snippet3":::

4. `ThisDocument` クラスに次のメソッドを追加します。 `AddCustomXmlPart` メソッドは、受け取った XML 文字列を含むカスタム XML 部分を作成します。

     カスタム XML 部分が一度だけ作成されるように、このメソッドは、一致する GUID を持つカスタム XML 部分が文書内に存在しない場合のみカスタム XML 部分を作成します。 このメソッドは、初めて呼び出されたときに、<xref:Microsoft.Office.Core._CustomXMLPart.Id%2A> プロパティの値を `employeeXMLPartID` 文字列に格納します。 `employeeXMLPartID` 文字列の値は、<xref:Microsoft.VisualStudio.Tools.Applications.Runtime.CachedAttribute> 属性によって宣言されているため、文書内に保持されます。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/EmployeeControls/ThisDocument.cs" id="Snippet4":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/EmployeeControls/ThisDocument.vb" id="Snippet4":::

## <a name="bind-the-content-controls-to-elements-in-the-custom-xml-part"></a>コンテンツ コントロールをカスタム XML 部分の要素にバインドする
 コンテンツ コントロールをカスタム XML 部分の要素にバインドするには、各コンテンツ コントロールの **XMLMapping** プロパティを使用します。

### <a name="to-bind-the-content-controls-to-elements-in-the-custom-xml-part"></a>コンテンツ コントロールをカスタム XML 部分の要素にバインドするには

1. `ThisDocument` クラスに次のメソッドを追加します。 このメソッドは、各コンテンツ コントロールをカスタム XML 部分の要素にバインドし、<xref:Microsoft.Office.Tools.Word.DatePickerContentControl> の日付表示形式を設定します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/EmployeeControls/ThisDocument.cs" id="Snippet5":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/EmployeeControls/ThisDocument.vb" id="Snippet5":::

## <a name="run-your-code-when-the-document-is-opened"></a>文書が開かれたときにコードを実行する
 カスタム XML 部分を作成し、文書が開かれたときにカスタム コントロールをデータにバインドします。

### <a name="to-run-your-code-when-the-document-is-opened"></a>文書が開かれたときにコードを実行するには

1. `ThisDocument_Startup` クラスの `ThisDocument` メソッドに次のコード行を追加します。 このコードでは、**employees.xml** ファイルから XML 文字列を取得し、それを文書内の新しいカスタム XML 部分に追加し、コンテンツ コントロールをカスタム XML 部分の要素にバインドします。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/EmployeeControls/ThisDocument.cs" id="Snippet2":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/EmployeeControls/ThisDocument.vb" id="Snippet2":::

## <a name="test-the-project"></a>プロジェクトをテストする
 文書を開くと、コンテンツ コントロールにカスタム XML 部分の要素のデータが表示されます。 <xref:Microsoft.Office.Tools.Word.DropDownListContentControl> をクリックすると、**employees.xsd** ファイルに定義された、`title` 要素の 3 つの有効な値のいずれかを選択できます。 コンテンツ コントロールに表示されたデータを編集すると、新しい値が文書内のカスタム XML 部分に保存されます。

### <a name="to-test-the-content-controls"></a>コンテンツ コントロールをテストするには

1. **F5** キーを押してプロジェクトを実行します。

2. 文書内に次のようなテーブルが表示されることを確認します。 2 つ目の列の文字列は、文書内のカスタム XML 部分の要素から取得されます。

    |列|[値]|
    |-|-|
    |**Employee Name**|**Karina Leal**|
    |**Hire Date**|**April 1, 1999**|
    |**Title**|**マネージャー**|

3. **Employee Name** セルの右側のセルを選択し、別の名前を入力します。

4. **Hire Date** セルの右側のセルを選択し、日付の選択で別の日付を選択します。

5. **Title** セルの右側のセルを選択し、ドロップダウン リストから別の項目を選択します。

6. 文書を保存して閉じます。

7. エクスプローラーで、プロジェクトの下にある *\bin\Debug* フォルダーを開きます。

8. **EmployeeControls.docx** のショートカット メニューを開き、 **[名前の変更]** を選択します。

9. ファイル名を **EmployeeControls.docx.zip** に変更します。

     **EmployeeControls.docx** 文書は Open XML 形式で保存されています。 この文書の拡張子を *.zip* に変更すると、文書の内容を確認できます。 オープン XML 形式の詳細については、技術文書「[Office (2007) Open XML ファイル形式の概要](/previous-versions/office/developer/office-2007/aa338205(v=office.12))」を参照してください。

10. **EmployeeControls.docx.zip** ファイルを開きます。

11. **customXml** フォルダーを開きます。

12. **item2.xml** のショートカット メニューを開き、 **[開く]** を選択します。

     このファイルには、文書に追加したカスタム XML 部分が含まれています。

13. `name`、`hireDate`、`title` の各要素に文書内のコンテンツ コントロールに入力した値が設定されていることを確認します。

14. **item2.xml** ファイルを閉じます。

## <a name="next-steps"></a>次のステップ
 コンテンツ コントロールの使用方法の詳細については、次の各トピックを参照してください。

- 用意されているすべてのコンテンツ コントロールを使用してテンプレートを作成できます。 詳細については、「[チュートリアル: コンテンツ コントロールを使用してテンプレートを作成する](../vsto/walkthrough-creating-a-template-by-using-content-controls.md)」を参照してください。

- 文書を閉じた状態でカスタム XML 部分のデータを変更できます。 その文書を次にユーザーが開いたときには、XML 要素にバインドされたコンテンツ コントロールに新しいデータが表示されます。

- コンテンツ コントロールを使用して文書の一部を保護できます。 詳細については、「[方法: コンテンツ コントロールを使用して文書の一部を保護する](../vsto/how-to-protect-parts-of-documents-by-using-content-controls.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [拡張オブジェクトを使用して Word を自動化する](../vsto/automating-word-by-using-extended-objects.md)
- [コンテンツ コントロール](../vsto/content-controls.md)
- [方法: Word 文書にコンテンツ コントロールを追加する](../vsto/how-to-add-content-controls-to-word-documents.md)
- [方法: コンテンツ コントロールを使用して文書の一部を保護する](../vsto/how-to-protect-parts-of-documents-by-using-content-controls.md)
- [ホスト項目とホスト コントロールの概要](../vsto/host-items-and-host-controls-overview.md)
- [ホスト項目とホスト コントロールのプログラム上の制限事項](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
- [実行時に Office ドキュメントにコントロールを追加する](../vsto/adding-controls-to-office-documents-at-run-time.md)
