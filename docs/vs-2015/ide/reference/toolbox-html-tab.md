---
title: ツールボックス、[HTML] タブ | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.toolbox.html
helpviewer_keywords:
- Toolbox, HTML tab
- HTML Designer, setting options
- HTML tab in Toolbox
ms.assetid: 9bfdd3b8-f5ac-4a5f-bdbf-c2b4e97641d8
caps.latest.revision: 18
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 31ee75c419870d9047b3892c668c5e4665850654
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2018
ms.locfileid: "49292074"
---
# <a name="toolbox-html-tab"></a>ツールボックス、[HTML] タブ
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

  
ツールボックスの **[HTML]** タブは、Web ページと Web フォームで使用するコンポーネントを提供します。 このタブを表示するには、まず、HTML デザイナーで編集するためのドキュメントを開きます。 **[表示]** メニューで **[ツールボックス]** をクリックし、ツールボックスの **[HTML]** タブをクリックします。  
  
 **[HTML]** タブでツールのインスタンスを作成するには、ドキュメントに追加するツールをダブルクリックするか、またはツールを選択して編集サーフェイスの目的の位置にドラッグします。  
  
## <a name="tasks"></a>[タスク]  
  
-   [方法: ツールボックス ウィンドウの管理](http://msdn.microsoft.com/en-us/a022c3fe-298c-4a59-a48f-b050da90ebc2)  
  
-   [方法: [ツールボックス] タブの操作](http://msdn.microsoft.com/en-us/21285050-cadd-455a-b1f5-a2289a89c4db)  
  
## <a name="ui-elements"></a>UI 要素  
 次のツールは、[HTML] タブで既定で使用できます。  
  
 **ポインター**  
 ![ASP.NET モバイル デザイナー HTMLpage ポインター](../../ide/reference/media/vxpointer.gif "vxPointer")  
  
 このツールは、任意の [ツールボックス] タブを開いたときに、既定で選択されます。 削除することはできません。 マウス ポインターを使用すると、オブジェクトをデザイン ビュー サーフェイスにドラッグしたり、サイズ変更したり、ページまたはフォーム上で位置を変更することができます。 詳しくは、「[方法: ツールボックス ウィンドウの管理](http://msdn.microsoft.com/en-us/a022c3fe-298c-4a59-a48f-b050da90ebc2)」および「[[ツールボックス] タブの操作方法](http://msdn.microsoft.com/en-us/21285050-cadd-455a-b1f5-a2289a89c4db)」をご覧ください。  
  
 **入力 (ボタン)**  
 ![HTML Web ページ ボタン](../../ide/reference/media/vxbutton.gif "vxButton")  
  
 `type="button"` の `input` 要素を挿入します。 表示されるテキストを変更するには、`name` プロパティを編集します。 既定では、`id="Button1"` は最初のボタンに挿入され、`id="Button2"` は 2 番目のボタンという具合に挿入されます。  
  
 **入力 (ボタン)** をデザイン ビュー サーフェイスにドラッグすると、次のように HTML マークアップがドキュメントに挿入されます。  
  
```  
<input id="Button1" type="button" value="Button" name="Button1">  
```  
  
 詳細については、次を参照してください[HTML Input コントロール](http://msdn.microsoft.com/library/2ba82c6b-dff7-4b73-b1c2-9e76a48a69de)、 [HtmlInputButton サーバー コントロール宣言構文](http://msdn.microsoft.com/en-us/99ccf7fb-7e2a-4ba1-bcd9-981b619a16aa)、 [NIB: 方法: スクリプトの作成とイベント ハンドラーの編集](http://msdn.microsoft.com/en-us/69d71d13-c68b-4ecd-869b-a42edf6d1f6d)、 。[ボタンの Web サーバー コントロールのコンテンツ マップ](http://msdn.microsoft.com/library/66b3ce28-3b93-4f0a-951f-42fb5bb5fddf)、 <xref:System.Web.UI.HtmlControls.HtmlInputButton>、 <xref:System.Web.UI.HtmlControls.HtmlButton>、および<xref:System.Web.UI.WebControls.Button>します。  
  
 **入力 (リセット)**  
 ![HTMLpageResetButton スクリーンショット](../../ide/reference/media/vxreset.gif "vxReset")  
  
 `type="reset"` の `input` 要素を挿入します。 表示されるテキストを変更するには、`name` プロパティを編集します。 既定では、`id="Reset1"` は最初のリセット ボタンに挿入され、`id="Reset2"` は 2 番目のリセット ボタンという具合に挿入されます。  
  
 **入力 (リセット)** をデザイン ビュー サーフェイスにドラッグすると、次のように HTML マークアップがドキュメントに挿入されます。  
  
```  
<input id="Reset1" type="reset" value="Reset" name="Reset1">  
```  
  
 詳細については、次を参照してください。 [HTML Input コントロール](http://msdn.microsoft.com/library/2ba82c6b-dff7-4b73-b1c2-9e76a48a69de)、 [HtmlInputReset サーバー コントロール宣言構文](http://msdn.microsoft.com/en-us/cfc1f1fb-d33a-464d-9bb5-204e66174979)、 <xref:System.Web.UI.HtmlControls.HtmlInputButton>、および<xref:System.Web.UI.WebControls.Button>します。  
  
 **入力 (送信)**  
 ![HTMLpageToolbarSubmitButton スクリーンショット](../../ide/reference/media/vxsubmit.gif "vxSubmit")  
  
 `type="submit"` の `input` 要素を挿入します。 表示されるテキストを変更するには、`name` プロパティを編集します。 既定では、`id="Submit1"` は最初の送信ボタンに挿入され、`id="Submit2"` は 2 番目の送信ボタンという具合に挿入されます。  
  
 **入力 (送信)** をデザイン ビュー サーフェイスにドラッグすると、次のように HTML マークアップがドキュメントに挿入されます。  
  
```  
<input id="Submit1" type="submit" value="Submit" name="Submit1">  
```  
  
 詳細については、次を参照してください。 [HTML Input コントロール](http://msdn.microsoft.com/library/2ba82c6b-dff7-4b73-b1c2-9e76a48a69de)、 [HtmlInputSubmit サーバー コントロール宣言構文](http://msdn.microsoft.com/en-us/eef2a157-f184-4ce9-b256-d1eacc7930f2)、 <xref:System.Web.UI.HtmlControls.HtmlInputButton>、および<xref:System.Web.UI.WebControls.Button>します。  
  
 **入力 (テキスト)**  
 ![HTMLpageToolbarTextField スクリーンショット](../../ide/reference/media/vxtextfield.gif "vxTextfield")  
  
 ドキュメントに `type="text"` の `input` 要素を挿入します。 表示される既定のテキストを変更するには、`value` 属性を編集します。 既定では、`id="Text1"` は最初のテキスト フィールドに挿入され、`id="Text2"` は 2 番目のテキスト フィールドという具合に挿入されます。  
  
 **入力 (テキスト)** をデザイン ビュー サーフェイスにドラッグすると、次のように HTML マークアップがドキュメントに挿入されます。  
  
```  
<input id="Text1" TYPE="text" value="Text Field" name="Text1">  
```  
  
 詳細については、次を参照してください[HTML Input コントロール](http://msdn.microsoft.com/library/2ba82c6b-dff7-4b73-b1c2-9e76a48a69de)、 [HtmlInputText サーバー コントロール宣言構文](http://msdn.microsoft.com/en-us/87060d90-a11c-434d-9fc9-b03a8487041e)、 [TextBox Web サーバー コントロールの概要](http://msdn.microsoft.com/library/ab354bc1-f23a-48fc-93d8-d4d7c1b7396f)、 <xref:System.Web.UI.HtmlControls.HtmlInputText>、と。<xref:System.Web.UI.WebControls.TextBox>.  
  
> [!IMPORTANT]
>  すべてのユーザー入力を検証することをお勧めします。 詳細については、「[ASP.NET Web ページにおけるユーザー入力の検証](http://msdn.microsoft.com/library/4ad3dacb-89e0-4cee-89ac-40a3f2a85461)」を参照してください。  
  
 **入力 (ファイル)**  
 ![HTML ページ ファイル フィールド](../../ide/reference/media/vxfilefield.gif "vxFilefield")  
  
 ドキュメントに `type="file"` の `input` 要素を挿入します。 既定では、`id="File1"` は最初のファイル フィールドに挿入され、`id="File2"` は 2 番目のファイル フィールドという具合に挿入されます。  
  
 **入力 (ファイル)** をデザイン ビュー サーフェイスにドラッグすると、次のように HTML マークアップがドキュメントに挿入されます。  
  
```  
<input id="File1" type="file" name="File1">  
```  
  
 詳細については、次を参照してください。 [HTML Input コントロール](http://msdn.microsoft.com/library/2ba82c6b-dff7-4b73-b1c2-9e76a48a69de)、 [HtmlInputFile サーバー コントロール宣言構文](http://msdn.microsoft.com/en-us/a817b4a0-056f-4c17-a696-b9fdcde43db6)、および<xref:System.Web.UI.HtmlControls.HtmlInputFile>します。  
  
> [!IMPORTANT]
>  すべてのユーザー入力を検証することをお勧めします。 詳細については、「[ASP.NET Web ページにおけるユーザー入力の検証](http://msdn.microsoft.com/library/4ad3dacb-89e0-4cee-89ac-40a3f2a85461)」を参照してください。  
  
 **入力 (パスワード)**  
 ![Visual Studio パスワード フィールド](../../ide/reference/media/vxpassword.gif "vxPassword")  
  
 `type="password"` の `input` 要素を挿入します。 既定では、`id="Password1"` は最初のパスワード フィールドに挿入され、`id="Password2"` は 2 番目のパスワード フィールドという具合に挿入されます。  
  
 **入力 (パスワード)** をデザイン ビュー サーフェイスにドラッグすると、次のように HTML マークアップがドキュメントに挿入されます。  
  
```  
<input id="Password1" type="password" name="Password1">  
```  
  
 詳細については、「[HTML Input コントロール](http://msdn.microsoft.com/library/2ba82c6b-dff7-4b73-b1c2-9e76a48a69de)」、「[HtmlInputPassword Server Control Declarative Syntax](http://msdn.microsoft.com/en-us/df703dd0-1624-4e5a-a547-c97f2f331b9f)」 (HtmlInputPassword サーバー コントロール宣言構文)、「[方法 : パスワード入力のための TextBox Web サーバー コントロールを設定する](http://msdn.microsoft.com/library/5b5069f3-64a1-435a-aee6-da263f4e6310)」、および「[チュートリアル : Web フォーム ページにおけるユーザーの入力の検証](http://msdn.microsoft.com/library/7141d6ba-34f3-410b-b5cd-2102a24cb436)」を参照してください。  
  
> [!IMPORTANT]
>  アプリケーションでユーザー名とパスワードを送信する場合、転送を暗号化するため、Secure Sockets Layer (SSL) を使用するように Web サイトを構成する必要があります。 詳細については、「[IIS Operations Guide](http://go.microsoft.com/fwlink/?linkid=47856)」 (IIS 操作ガイド) の「Securing Connections with SSL」 (SSL で接続を保護する) を参照してください。 また、すべてのユーザー入力を検証することをお勧めします。 詳細については、「[ASP.NET Web ページにおけるユーザー入力の検証](http://msdn.microsoft.com/library/4ad3dacb-89e0-4cee-89ac-40a3f2a85461)」を参照してください。  
  
 **入力 (チェック ボックス)**  
 ![HTML Web ページ ツールボックス チェック ボックス オプション](../../ide/reference/media/vxcheckbox.gif "vxCheckbox")  
  
 `type="checkbox"` の `input` 要素を挿入します。 表示されるテキストを変更するには、`name` プロパティを編集します。 既定では、`id="Checkbox1"` は最初のチェック ボックスに挿入され、`id="Checkbox2"` は 2 番目のチェック ボックスという具合に挿入されます。  
  
 **入力 (チェック ボックス)** をデザイン ビュー サーフェイスにドラッグすると、次のように HTML マークアップがドキュメントに挿入されます。  
  
```  
<input id="Checkbox1" type="checkbox" name="Checkbox1">   
```  
  
 詳細については、次を参照してください[HTML Input コントロール](http://msdn.microsoft.com/library/2ba82c6b-dff7-4b73-b1c2-9e76a48a69de)、 [HtmlInputCheckBox サーバー コントロール宣言構文](http://msdn.microsoft.com/en-us/4a509586-89d8-4ccf-a0b8-b9160ce6e4a6)、[チェック ボックスをオンおよび CheckBoxList Web サーバー コントロールの概要](http://msdn.microsoft.com/library/3028dfd3-e2c5-451d-9150-d02c8ffb92bf)、。<xref:System.Web.UI.HtmlControls.HtmlInputCheckBox>、および<xref:System.Web.UI.WebControls.CheckBox>します。  
  
 **入力 (ラジオ)**  
 ![VisualStudioHTMLpageRadioButton スクリーンショット](../../ide/reference/media/vxradio.gif "vxRadio")  
  
 `type="radio"` の `input` 要素を挿入します。 表示されるテキストを変更するには、`name` プロパティを編集します。 既定では、`id="Radio1"` は最初のラジオ ボタンに挿入され、`id="Radio2"` は 2 番目のラジオ ボタンという具合に挿入されます。  
  
 **入力 (ラジオ)** をデザイン ビュー サーフェイスにドラッグすると、次のように HTML マークアップがドキュメントに挿入されます。  
  
```  
<input id="Radio1" type="radio" name="Radio1">  
```  
  
 詳細については、次を参照してください[HTML Input コントロール](http://msdn.microsoft.com/library/2ba82c6b-dff7-4b73-b1c2-9e76a48a69de)、 [HtmlInputRadioButton サーバー コントロール宣言構文](http://msdn.microsoft.com/en-us/6e60ff63-cc57-46ef-bf96-e829e204ba33)、 [RadioButton コントロールおよび RadioButtonList Web サーバー コントロール概要。](http://msdn.microsoft.com/library/20eb383c-4b59-432b-bba3-e9d785107747)、 <xref:System.Web.UI.HtmlControls.HtmlInputRadioButton>、および<xref:System.Web.UI.WebControls.RadioButton>します。  
  
 **入力 (非表示)**  
 ![HTML ページ非表示項目](../../ide/reference/media/vxhidden.gif "vxhidden")  
  
 `type="hidden"` の `input` 要素を挿入します。 既定では、`id="Hidden1"` は最初の非表示フィールドに挿入され、`id="Hidden2"` は 2 番目の非表示フィールドという具合に挿入されます。  
  
 **入力 (非表示)** をデザイン ビュー サーフェイスにドラッグすると、次のように HTML マークアップがドキュメントに挿入されます。  
  
```  
<input id="Hidden1" type="hidden" name="Hidden1">   
```  
  
 詳細については、次を参照してください。 [HTML Input コントロール](http://msdn.microsoft.com/library/2ba82c6b-dff7-4b73-b1c2-9e76a48a69de)、 [HtmlInputHidden サーバー コントロール宣言構文](http://msdn.microsoft.com/en-us/4194e44d-1d74-4bfc-9cc7-743a2e1ea5f9)、および<xref:System.Web.UI.HtmlControls.HtmlInputHidden>します。  
  
 **テキスト領域**  
 ![HTMLpage ツール バー テキスト領域](../../ide/reference/media/vxtextarea.gif "vxTextarea")  
  
 `textarea` 要素を挿入します。 テキスト領域のサイズを変更するか、スクロール バーを使用して表示領域を超える長さのテキストを表示することができます。 表示される既定のテキストを変更するには、`value` 属性を編集します。 既定では、`id="textarea1"` は最初のテキスト領域に挿入され、`id=" textarea 2"` は 2 番目のテキスト領域という具合に挿入されます。  
  
 **テキスト領域**をデザイン ビュー サーフェイスにドラッグすると、次のように HTML マークアップがドキュメントに挿入されます。  
  
```  
<textarea id=" textarea 1 name=" textarea 1" rows=2 cols=20></textarea>   
```  
  
 詳細については、次を参照してください。 [HtmlTextArea サーバー コントロール宣言構文](http://msdn.microsoft.com/en-us/5a103ffa-235b-4452-ba2b-a4fb8ba8cb87)、 <xref:System.Web.UI.HtmlControls.HtmlTextArea>、および<xref:System.Web.UI.WebControls.TextBox>します。  
  
> [!IMPORTANT]
>  すべてのユーザー入力を検証することをお勧めします。 詳細については、「[ASP.NET Web ページにおけるユーザー入力の検証](http://msdn.microsoft.com/library/4ad3dacb-89e0-4cee-89ac-40a3f2a85461)」を参照してください。  
  
 **テーブル**  
 ![HTMLpageToolbarTable スクリーンショット](../../ide/reference/media/vxtable.gif "vxTable")  
  
 `table` 要素を挿入します。  
  
 **テーブル**をデザイン ビュー サーフェイスにドラッグすると、次のように HTML マークアップがドキュメントに挿入されます。  
  
```  
<table cellspacing="1" width="75%" border=1> <tr><td></td></tr></table>   
```  
  
 詳細については、次を参照してください。 [HtmlTable サーバー コントロール宣言構文](http://msdn.microsoft.com/en-us/625b06d8-0f69-4112-a1d4-8ef2a9fbcda9)、 [Table、TableRow、TableCell Web サーバー コントロールの概要](http://msdn.microsoft.com/library/2fbd0582-cf69-4c8d-9e35-21f35e2cee1a)、 <xref:System.Web.UI.HtmlControls.HtmlTable>、および<xref:System.Web.UI.WebControls.Table>します。  
  
 **イメージ**  
 ![HTML ページ イメージ項目](../../ide/reference/media/vximage.gif "vxImage")  
  
 `img` 要素を挿入します。 この要素を編集して、要素の `src` と `alt` テキストを指定します。  
  
 **イメージ**をデザイン ビュー サーフェイスにドラッグすると、次のように HTML マークアップがドキュメントに挿入されます。  
  
```  
<img alt="" src="">  
```  
  
 詳細については、次を参照してください。 [HtmlImage サーバー コントロール宣言構文](http://msdn.microsoft.com/en-us/528430e8-ced1-47d1-8db2-942e734a61f6)、[イメージ Web サーバー コントロールの概要](http://msdn.microsoft.com/library/096a8d8d-58ee-4ee8-ab82-6594a0f3a0a9)、 <xref:System.Web.UI.HtmlControls.HtmlImage>、 <xref:System.Web.UI.HtmlControls.HtmlInputImage>、および<xref:System.Web.UI.WebControls.Image>します。  
  
 **選択**  
 ![HTML ページ ツールボックス ドロップダウン](../../ide/reference/media/vxdropdown.gif "vxDropdown")  
  
 `select` 要素のドロップダウン リスト (`size` 属性なし) を挿入します。 既定では、`id="select1"` は最初のリスト ボックスに挿入され、`id="select2"` は 2 番目のリスト ボックスという具合に挿入されます。  
  
 **選択**をデザイン ビュー サーフェイスにドラッグすると、次のように HTML マークアップがドキュメントに挿入されます。  
  
```  
<select id="select1" name="select1"><option selected></option></select>  
```  
  
 サイズ プロパティの値を増やすことで、複数行の `select` 要素を作成できます。  
  
 詳細については、次を参照してください[HtmlSelect サーバー コントロール宣言構文](http://msdn.microsoft.com/en-us/ee93bdec-b343-441a-a8ff-56ffcafe9ae5)、 [NIB: 方法: スクリプトの作成とイベント ハンドラーの編集](http://msdn.microsoft.com/en-us/69d71d13-c68b-4ecd-869b-a42edf6d1f6d)、 [DropDownList Web サーバー コントロールの概要](http://msdn.microsoft.com/library/517dd1a4-8df3-4c9f-8c89-1549a1aee608)。、 [ListBox Web サーバー コントロールの概要](http://msdn.microsoft.com/library/c08ee025-787a-408d-858e-a4a5fdb61d97)、 <xref:System.Web.UI.HtmlControls.HtmlSelect>、および<xref:System.Web.UI.WebControls.DropDownList>します。  
  
 **水平線**  
 ![HTML ページの水平線項目](../../ide/reference/media/vxhorizontal.gif "vxHorizontal")  
  
 `hr` 要素を挿入します。 線の太さを太くするには、`size` 属性を編集します。  
  
 **水平線**をデザイン ビュー サーフェイスにドラッグすると、次のように HTML マークアップがドキュメントに挿入されます。  
  
```  
<hr width="100%" size=1>   
```  
  
 詳細については、「[HTML Horizontal Rule コントロール](http://msdn.microsoft.com/library/bf6df0a8-9844-404d-8a9a-3455b0180f2f)」を参照してください。  
  
 **Div**  
 ![HTML ページ ラベル](../../ide/reference/media/vxlabel.gif "vxLabel")  
  
 `ms_positioning="FlowLayout"` 属性を含む `div` 要素を挿入します。 幅と高さを除き、この項目はフロー レイアウト パネルと同じです。 `div` 要素内に含まれるテキストを書式設定するには、`class="stylename"` 属性を開始タグに追加します。  
  
 **Div** をデザイン ビュー サーフェイスにドラッグすると、次のように HTML マークアップがドキュメントに挿入されます。  
  
```  
<div ms_positioning="FlowLayout" style="width: 70px; position: relative; height: 15px">Label</div>  
```  
  
 詳細については、次を参照してください。 [HTML Div コントロール](http://msdn.microsoft.com/library/585fa702-4408-4af1-a92b-68d77ee5e995)、 [Label Web サーバー コントロールの概要](http://msdn.microsoft.com/library/990558d1-4b22-4f28-b100-78a434b3c5ac)、および<xref:System.Web.UI.WebControls.Label>します。  
  
## <a name="see-also"></a>関連項目  
 [ツールボックス](../../ide/reference/toolbox.md)   
 [[標準] タブ (ツールボックス)](http://msdn.microsoft.com/library/35e9320d-fcbd-474b-8b8f-55705e9a1870)   
 [HTML コントロール](http://msdn.microsoft.com/library/83bc6f7e-a2b5-4fe9-9a34-eb34aef673be)



