---
title: コード化された UI テストの構造 | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-devops-test
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- coded UI tests
ms.assetid: 9c5d82fc-3fb7-4bb1-a9ac-ac1fa3a4b500
caps.latest.revision: 25
ms.author: gewarren
manager: douge
ms.openlocfilehash: 7595a967a6dae091da6c5a7613a27c602cc1381e
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2018
ms.locfileid: "49202749"
---
# <a name="anatomy-of-a-coded-ui-test"></a>コード化された UI テストの構造
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

コード化された UI テスト プロジェクトでコード化された UI テストを作成すると、ソリューションに複数のファイルが追加されます。 このトピックでは、コード化された UI テストの例を使用して、これらのファイルを参照します。  
  
 **必要条件**  
  
-   Visual Studio Enterprise  
  
## <a name="contents-of-a-coded-ui-test"></a>コード化された UI テストの内容  
 コード化された UI テストを作成すると、**[コード化された UI テスト ビルダー]** によってテスト対象のユーザー インターフェイスのマップが作成されるほか、すべてのテストのテスト メソッド、パラメーター、およびアサーションも作成されます。 また、各テストのクラス ファイルも作成されます。  
  
|ファイル|目次|編集可能かどうか|  
|----------|--------------|---------------|  
|[UIMap.Designer.cs](#UIMapDesignerFile)|[宣言セクション](#UIMapDesignerFile)<br /><br /> [UIMap クラス](#UIMapClass) (部分クラス、自動生成)<br /><br /> [メソッド](#UIMapMethods)<br /><br /> [Properties](#UIMapProperties)|いいえ|  
|[UIMap.cs](#UIMapCS)|[UIMap クラス](#UIMapCS) (部分クラス)|はい|  
|[CodedUITest1.cs](#CodedUITestCS)|[CodedUITest1 クラス](#CodedUITestCS)<br /><br /> [メソッド](#CodedUITestMethods)<br /><br /> [Properties](#CodedUITestProperties)|はい|  
|[UIMap.uitest](#UIMapuitest)|テストに使用する UI の XML マップ。|いいえ|  
  
###  <a name="UIMapDesignerFile"></a> UIMap.Designer.cs  
 このファイルには、テストの作成時に **[コード化された UI テスト ビルダー]** によって自動的に作成されるコードが含まれます。 このファイルはテストに変更があるたびに再作成されるため、ファイル内のコードに対して追加や変更はできません。  
  
#### <a name="declarations-section"></a>宣言セクション  
 このセクションには、次に示す Windows UI の宣言が含まれています。  
  
```csharp  
using System;  
using System.CodeDom.Compiler;  
using System.Collections.Generic;  
using System.Drawing;  
using System.Text.RegularExpressions;  
using System.Windows.Input;  
using Microsoft.VisualStudio.TestTools.UITest.Extension;  
using Microsoft.VisualStudio.TestTools.UITesting;  
using Microsoft.VisualStudio.TestTools.UITesting.WinControls;  
using Microsoft.VisualStudio.TestTools.UnitTesting;  
using Keyboard = Microsoft.VisualStudio.TestTools.UITesting.Keyboard;  
using Mouse = Microsoft.VisualStudio.TestTools.UITesting.Mouse;  
using MouseButtons = System.Windows.Forms.MouseButtons;  
```  
  
 <xref:Microsoft.VisualStudio.TestTools.UITesting.WinControls> 名前空間は、Windows ユーザー インターフェイス (UI) 用に含まれています。 Web ページ UI 用の名前空間は <xref:Microsoft.VisualStudio.TestTools.UITesting.HtmlControls>、Windows Presentation Foundation UI 用の名前空間は <xref:Microsoft.VisualStudio.TestTools.UITesting.WpfControls> です。  
  
####  <a name="UIMapClass"></a>UIMap クラス  
 ファイルの次のセクションは、<xref:Microsoft.VisualStudio.TestTools.UITest.Common.UIMap.UIMap> クラスです。  
  
```  
[GeneratedCode("Coded UITest Builder", "10.0.21221.0")]  
public partial class UIMap  
```  
  
 このクラスに適用される <xref:System.CodeDom.Compiler.GeneratedCodeAttribute> からクラス コードが始まり、部分クラスとして宣言されます。 この属性は、このファイル内のすべてのクラスに対しても同様に適用されます。 このクラスのコードをより多く格納できるその他のファイルとして `UIMap.cs` がありますが、これについては後で説明します。  
  
 生成された `UIMap` クラスには、テストの記録時に指定された各メソッドのコードが含まれています。  
  
```  
public void LaunchCalculator()  
public void AddItems()  
public void VerifyTotal()  
public void CleanUp()  
```  
  
 <xref:Microsoft.VisualStudio.TestTools.UITest.Common.UIMap.UIMap> クラスのこの部分には、メソッドに必要な各プロパティに対して生成されたコードも含まれています。  
  
```  
public virtual LaunchCalculatorParams LaunchCalculatorParams  
public virtual AddItemsParams AddItemsParams  
public virtual VerifyTotalExpectedValues VerifyTotalExpectedValues  
public virtual CalculateItemsParams CalculateItemsParams  
public virtual VerifyMathAppTotalExpectedValues   
    VerifyMathAppTotalExpectedValues  
public UIStartMenuWindow UIStartMenuWindow  
public UIRunWindow UIRunWindow  
public UICalculatorWindow UICalculatorWindow  
public UIStartWindow UIStartWindow  
public UIMathApplicationWindow UIMathApplicationWindow  
```  
  
#####  <a name="UIMapMethods"></a>UIMap メソッド  
 各メソッドは、`AddItems()` メソッドに似た構造を持ちます。 これについては、次のコードの後に詳しく説明します。このコードは、わかりやすくするために改行を加えて表記しています。  
  
```  
/// <summary>  
/// AddItems - Use 'AddItemsParams' to pass parameters into this method.  
/// </summary>  
public void AddItems()  
{  
    #region Variable Declarations  
    WinControl uICalculatorDialog =   
        this.UICalculatorWindow.UICalculatorDialog;  
    WinEdit uIItemEdit =   
        this.UICalculatorWindow.UIItemWindow.UIItemEdit;  
    #endregion  
  
    // Type '{NumPad7}' in 'Calculator' Dialog  
    Keyboard.SendKeys(uICalculatorDialog,   
        this.AddItemsParams.UICalculatorDialogSendKeys,   
        ModifierKeys.None);  
  
    // Type '{Add}{NumPad2}{Enter}' in 'Unknown Name' text box  
    Keyboard.SendKeys(uIItemEdit,   
        this.AddItemsParams.UIItemEditSendKeys,   
        ModifierKeys.None);  
}  
```  
  
 各メソッド定義の概要コメントで、そのメソッドのパラメーター値のために使用するクラスを示しています。 この場合は、`AddItemsParams` クラスです。このクラスは `UIMap.cs` ファイルの後半で定義されているほか、`AddItemsParams` プロパティによって返される値の型でもあります。  
  
 メソッド コードの先頭にあるのは `Variable Declarations` 領域です。ここでは、メソッドで使用される UI オブジェクトのローカル変数が定義されます。  
  
 このメソッドでは、`UIItemWindow` と `UIItemEdit` の両方が、`UIMap.cs` ファイルの後半で定義されている `UICalculatorWindow` クラスを使用してアクセスされるプロパティです。  
  
 その次の行では、`AddItemsParams` オブジェクトのプロパティを使用して、キーボードから電卓アプリケーションにテキストを送信しています。  
  
 `VerifyTotal()` メソッドはこれとよく似た構造を持ち、さらに次のアサーション コードが含まれています。  
  
```  
// Verify that 'Unknown Name' text box's property 'Text' equals '9. '  
Assert.AreEqual(  
    this.VerifyTotalExpectedValues.UIItemEditText,   
    uIItemEdit.Text);  
```  
  
 テキスト ボックス名は不明として表示されます。これは、Windows の電卓アプリケーションではこのコントロールの名前が一般に公開されていないためです。 実際の値が予期される値と一致しない場合は <xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert.AreEqual%2A?displayProperty=fullName> メソッドが失敗し、その結果、テストが失敗します。 また、予期される値には小数点が含まれ、その後にスペースが続くことにも注意してください。 このテストの機能を変更する必要が生じた場合は、この小数点とスペースを許可する必要があります。  
  
#####  <a name="UIMapProperties"></a>UIMap プロパティ  
 この各プロパティのコードは、クラス全体でも特に標準的なコードです。 次の `AddItemsParams` プロパティのコードは、`AddItems()` メソッドで使用されます。  
  
```  
public virtual AddItemsParams AddItemsParams  
{  
    get  
    {  
        if ((this.mAddItemsParams == null))  
        {  
            this.mAddItemsParams = new AddItemsParams();  
        }  
        return this.mAddItemsParams;  
    }  
}  
```  
  
 このプロパティでは、`mAddItemsParams` というプライベート ローカル変数を使用して、値を返す前にその値を保持します。 返されるオブジェクトのプロパティ名とクラス名は同じです。 このクラスは、`UIMap.cs` ファイルの後半で定義されます。  
  
 プロパティによって返される各クラスは、同様の構成になっています。 `AddItemsParams` クラスを次に示します。  
  
```  
/// <summary>  
/// Parameters to be passed into 'AddItems'  
/// </summary>  
[GeneratedCode("Coded UITest Builder", "10.0.21221.0")]  
public class AddItemsParams  
{  
    #region Fields  
    /// <summary>  
    /// Type '{NumPad7}' in 'Calculator' Dialog  
    /// </summary>  
    public string UICalculatorDialogSendKeys = "{NumPad7}";  
  
    /// <summary>  
    /// Type '{Add}{NumPad2}{Enter}' in 'Unknown Name' text box  
    /// </summary>  
    public string UIItemEditSendKeys = "{Add}{NumPad2}{Enter}";  
    #endregion  
}  
```  
  
 `UIMap.cs` ファイル内のすべてのクラスと同様に、このクラスも <xref:System.CodeDom.Compiler.GeneratedCodeAttribute> で始まります。 この小さなクラスの内部は、前述した `UIMap.AddItems()` メソッドで使用される <xref:Microsoft.VisualStudio.TestTools.UITesting.Keyboard.SendKeys%2A?displayProperty=fullName> メソッドのパラメーターとして使用する文字列を定義する `Fields` 領域です。 これらのパラメーターを使用するメソッドの呼び出し前に、この文字列フィールド内の値を置き換えるためのコードを記述できます。  
  
###  <a name="UIMapCS"></a>UIMap.cs  
 既定では、このファイルにはメソッドやプロパティを持たない `UIMap` 部分クラスが含まれています。  
  
#### <a name="uimap-class"></a>UIMap クラス  
 ここでは、<xref:Microsoft.VisualStudio.TestTools.UITest.Common.UIMap.UIMap> クラスの機能を拡張するためのカスタム コードを作成できます。 このファイルで作成するコードは、テストが変更されるたびに **[コード化された UI テスト ビルダー]** によって再生成されることはありません。  
  
 <xref:Microsoft.VisualStudio.TestTools.UITest.Common.UIMap.UIMap> クラスのすべての部分から、<xref:Microsoft.VisualStudio.TestTools.UITest.Common.UIMap.UIMap> の他のすべての部分のメソッドやプロパティを使用できます。  
  
###  <a name="CodedUITestCS"></a>CodedUITest1.cs  
 このファイルは **[コード化された UI テスト ビルダー]** によって生成されますが、テストが変更されるたびに再作成されることはありません。したがって、このファイルではコードを変更できます。 ファイルの名前は、テストに対して作成時に指定した名前から生成されます。  
  
#### <a name="codeduitest1-class"></a>CodedUITest1 クラス  
 既定では、このファイルには 1 つのクラスのみの定義が含まれています。  
  
```  
[CodedUITest]  
public class CodedUITest1  
```  
  
 T:Microsoft.VisualStudio.TestTools.UITesting.CodedUITestAttribute が自動的にクラスに適用され、テスト フレームワークがこれをテストの拡張機能として認識できるようになります。 また、このクラスが部分クラスではないという点にも注意してください。 すべてのクラス コードがこのファイルに含まれています。  
  
#####  <a name="CodedUITestProperties"></a>CodedUITest1 プロパティ  
 このクラスには、ファイルの末尾にある 2 つの既定のプロパティが含まれています。 これらのプロパティは変更できません。  
  
```  
/// <summary>  
/// Gets or sets the test context which provides  
/// information about and functionality for the current test run.  
///</summary>  
public TestContext TestContext  
public UIMap UIMap  
```  
  
#####  <a name="CodedUITestMethods"></a> CodedUITest1 メソッド  
 既定では、このクラスに含まれているメソッドは 1 つだけです。  
  
```  
public void CodedUITestMethod1()  
```  
  
 このメソッドは、テストの記録時に指定した各 `UIMap` メソッドを呼び出します ([UIMap クラス](#UIMapClass)に関するセクションを参照)。  
  
 `Additional test attributes` というタイトルの領域には、コメント解除した場合、2 つの省略可能なメソッドが含まれます。  
  
```  
// Use TestInitialize to run code before running each test   
[TestInitialize()]  
public void MyTestInitialize()  
{  
    // To generate code for this test, select "Generate Code for Coded   
    // UI Test" from the shortcut menu and select one of the menu items.  
    // For more information on generated code, see   
    // http://go.microsoft.com/fwlink/?LinkId=179463  
  
    // You could move this line from the CodedUITestMethod1() method  
    this.UIMap.LaunchCalculator();  
}  
  
// Use TestCleanup to run code after each test has run  
[TestCleanup()]  
public void MyTestCleanup()  
{  
    // To generate code for this test, select "Generate Code for Coded   
    // UI Test" from the shortcut menu and select one of the menu items.  
    // For more information on generated code, see   
    // http://go.microsoft.com/fwlink/?LinkId=179463  
  
    // You could move this line from the CodedUITestMethod1() method  
    this.UIMap.CloseCalculator();  
}  
```  
  
 `MyTestInitialize()` メソッドには、<xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestInitializeAttribute> が適用されています。これにより、テスト フレームワークは、他のテスト メソッドより前にこのメソッドを呼び出します。 同様に、`MyTestCleanup()` メソッドには、<xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestCleanupAttribute> が適用されいます。これにより、テスト フレームワークは、他のすべてのテスト メソッドが呼び出された後にこのメソッドを呼び出します。 これらのメソッドの使用は任意です。 このテストでは、`CodedUITest1Method1()` からではなく、`UIMap.LaunchCalculator()` メソッドは `MyTestInitialize()` から、`UIMap.CloseCalculator()` メソッドは `MyTestCleanup()` から、それぞれ呼び出すことができます。  
  
 <xref:Microsoft.VisualStudio.TestTools.UITesting.CodedUITestAttribute> を使用して、このクラスにさらにメソッドを追加した場合、テスト フレームワークは各メソッドをテストの一部として呼び出します。  
  
###  <a name="UIMapuitest"></a>UIMap.uitest  
 これは、コード化された UI テストの記録およびそのすべての部分の構造を表す XML ファイルです。 アクションとクラス、およびクラスのメソッドとプロパティが含まれます。 [UIMap.Designer.cs](#UIMapDesignerFile) ファイルには、テストの構造を再現し、テスト フレームワークへの接続を可能にするために、コード化された UI ビルダーによって生成されたコードが含まれています。  
  
 `UIMap.uitest` ファイルは直接編集できません。 ただし、コード化された UI ビルダーを使用してテストを変更することはできます。これにより、`UIMap.uitest` ファイルと [UIMap.Designer.cs](#UIMapDesignerFile) ファイルが自動的に変更されます。  
  
## <a name="see-also"></a>関連項目  
 <xref:Microsoft.VisualStudio.TestTools.UITest.Common.UIMap.UIMap>   
 <xref:Microsoft.VisualStudio.TestTools.UITesting.WinControls>   
 <xref:Microsoft.VisualStudio.TestTools.UITesting.HtmlControls>   
 <xref:Microsoft.VisualStudio.TestTools.UITesting.WpfControls>   
 <xref:System.CodeDom.Compiler.GeneratedCodeAttribute>   
 <xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert.AreEqual%2A?displayProperty=fullName>   
 <xref:Microsoft.VisualStudio.TestTools.UITesting.Keyboard.SendKeys%2A?displayProperty=fullName>   
 <xref:Microsoft.VisualStudio.TestTools.UITesting.CodedUITestAttribute>   
 <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestInitializeAttribute>   
 <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestCleanupAttribute>   
 [UI オートメーションを使用してコードをテストする](../test/use-ui-automation-to-test-your-code.md)   
 [コード化された UI テストを作成する](../test/use-ui-automation-to-test-your-code.md#VerifyingCodeUsingCUITCreate)   
 [コード化された UI テストのベスト プラクティス](../test/best-practices-for-coded-ui-tests.md)   
 [複数の UI マップでの大規模アプリケーションのテスト](../test/testing-a-large-application-with-multiple-ui-maps.md)   
 [コード化された UI テストと操作の記録でサポートされている構成とプラットフォーム](../test/supported-configurations-and-platforms-for-coded-ui-tests-and-action-recordings.md)



