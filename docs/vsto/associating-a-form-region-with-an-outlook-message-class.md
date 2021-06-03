---
title: フォーム領域を Outlook メッセージ クラスに関連付ける
description: フォーム領域を各アイテムのメッセージ クラスに関連付けることにより、そのフォーム領域を表示する Microsoft Office Outlook アイテムを指定する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- VSTO.NewFormRegionWizard.InvalidMessageClassName
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- FormRegionMessageClassAttribute
- form regions [Office development in Visual Studio], message classes
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: be3b789fabf00d853d447cb3489ef07a5b494fcd
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107826994"
---
# <a name="associate-a-form-region-with-an-outlook-message-class"></a>フォーム領域を Outlook メッセージ クラスに関連付ける
  フォーム領域を各アイテムのメッセージ クラスに関連付けることにより、そのフォーム領域を表示する Microsoft Office Outlook アイテムを指定することができます。 たとえば、メール アイテムの下部にフォーム領域を追加する場合は、フォーム領域を `IPM.Note` メッセージ クラスに関連付けることができます。

 フォーム領域をメッセージ クラスに関連付けるには、**新しい Outlook フォーム領域** ウィザードでメッセージ クラス名を指定するか、フォーム領域ファクトリ クラスに属性を適用します。

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

## <a name="understand-outlook-message-classes"></a>Outlook メッセージ クラスについて
 Outlook メッセージ クラスでは、Outlook アイテムの種類を識別します。 次の表に、これら 8 種類の標準のアイテムとそのメッセージ クラス名を示します。

|Outlook アイテムの種類|メッセージ クラス名|
|-----------------------|------------------------|
|AppointmentItem|`IPM.Appointment`|
|ContactItem|`IPM.Contact`|
|DistListItem|`IPM.DistList`|
|JournalItem|`IPM.Activity`|
|MailItem|`IPM.Note`|
|PostItem|`IPM.Post` または `IPM.Post.RSS`|
|TaskItem|`IPM.Task`|

 カスタム メッセージ クラスの名前を指定することもできます。 カスタム メッセージ クラスでは、Outlook で定義するカスタム フォームを識別します。

> [!NOTE]
> 置換およびすべて置換フォーム領域では、新しいカスタム メッセージ クラス名を指定できます。 既存のカスタム フォームのメッセージ クラス名を使用する必要はありません。 カスタム メッセージ クラスの名前は一意である必要があります。 名前が一意であることを確認する方法の 1 つは、\<*StandardMessageClassName*>.\<*Company*>.\<*MessageClassName*> のような名前付け規則を使用することです (例: `IPM.Note.Contoso.MyMessageClass`)。

## <a name="associate-a-form-region-with-an-outlook-message-class"></a>フォーム領域を Outlook メッセージ クラスに関連付ける
 フォーム領域をメッセージ クラスを関連付けるには、次の 2 つの方法があります。

- **新しい Outlook フォーム領域** ウィザードを使用します。

- クラス属性を適用します。

### <a name="use-the-new-outlook-form-region-wizard"></a>新しい Outlook フォーム領域ウィザードを使用する
 **新しい Outlook フォーム領域** ウィザードの最後のページでは、標準のメッセージ クラスを選択し、フォーム領域に関連付けるカスタム メッセージ クラスの名前を入力できます。

 フォーム領域によってフォーム全体またはフォームの既定のページが置き換えられるように設計されている場合、標準のメッセージ クラスは使用できません。 標準のメッセージ クラス名は、フォームに新しいページを追加したり、フォームの下部に追加されたりするフォームに対してのみ指定できます。 詳細については、「[方法: フォーム領域を Outlook アドイン プロジェクトに追加する](../vsto/how-to-add-a-form-region-to-an-outlook-add-in-project.md)」を参照してください。

 1 つ以上のカスタム メッセージ クラスを含めるには、 **[このフォーム領域を表示するカスタム メッセージ クラスを選択]** ボックスに名前を入力します。

 入力する名前は、次のガイドラインに準拠している必要があります。

- 完全修飾メッセージ クラス名 (例: "IPM.Note.Contoso") を使用します。

- 複数のメッセージ クラス名を区切るには、セミコロンを使用します。

- "IPM.Note" や "IPM.Contact" などの標準の Outlook メッセージ クラスは含めないでください。 "IPM.Note.Contoso" などのカスタム メッセージ クラスのみを含めます。

- 基本メッセージ クラスを単独で指定しないでください (例: "IPM")。

- メッセージ クラス名ごとに 256 文字を超えないようにしてください。

  **[完了]** をクリックすると、**新しい Outlook フォーム領域** ウィザードによって入力の形式が検証されます。

> [!NOTE]
> **新しい Outlook フォーム領域** ウィザードでは、指定したメッセージ クラス名が正しいか有効であるかは検証されません。

 ウィザードを完了すると、**新しい Outlook フォーム領域** ウィザードによって、指定したメッセージ クラス名を含むフォーム領域クラスに属性が適用されます。 これらの属性は手動で適用することもできます。

### <a name="apply-class-attributes"></a>クラス属性を適用する
 **新しい Outlook フォーム領域** ウィザードを完了した後で、フォーム領域を Outlook メッセージ クラスに関連付けることができます。 これを行うには、フォーム領域ファクトリ クラスに属性を適用します。

 次の例は、`myFormRegion` という名前のフォーム領域ファクトリ クラスに適用されている 2 つの <xref:Microsoft.Office.Tools.Outlook.FormRegionMessageClassAttribute> 属性を示しています。 最初の属性は、フォーム領域をメール メッセージ フォームの標準のメッセージ クラスに関連付けます。 2 番目の属性は、`IPM.Task.Contoso` という名前のカスタム メッセージ クラスにフォーム領域を関連付け ます。

 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_Outlook_FR_Attributes/FormRegion1.vb" id="Snippet1":::
 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_Outlook_FR_Attributes/FormRegion1.cs" id="Snippet1":::

 属性は、次のガイドラインに準拠している必要があります。

- カスタム メッセージ クラスの場合は、完全修飾メッセージ クラス名 (例: "IPM.Note.Contoso") を使用します。

- 基本メッセージ クラスを単独で指定しないでください (例: "IPM")。

- メッセージ クラス名ごとに 256 文字を超えないようにしてください。

- フォーム領域によってフォーム全体またはフォームの既定のページが置き換えられる場合は、標準のメッセージ クラスの名前を含めないでください。 標準のメッセージ クラス名は、フォームに新しいページを追加したり、フォームの下部に追加されたりするフォームに対してのみ指定できます。 詳細については、「[方法: フォーム領域を Outlook アドイン プロジェクトに追加する](../vsto/how-to-add-a-form-region-to-an-outlook-add-in-project.md)」を参照してください。

  プロジェクトをビルドすると、Visual Studio によってメッセージ クラス名の形式が検証されます。

> [!NOTE]
> Visual Studio では、指定したメッセージ クラス名が正しいか有効であるかは検証されません。

## <a name="see-also"></a>関連項目
- [実行時のフォーム領域へのアクセス](../vsto/accessing-a-form-region-at-run-time.md)
- [Outlook フォーム領域の作成](../vsto/creating-outlook-form-regions.md)
- [チュートリアル: Outlook フォーム領域のデザイン](../vsto/walkthrough-designing-an-outlook-form-region.md)
- [Outlook フォーム領域を作成するためのガイドライン](../vsto/guidelines-for-creating-outlook-form-regions.md)
- [フォーム名とメッセージ クラスの概要](/office/vba/outlook/Concepts/Forms/form-name-and-message-class-overview)
- [Outlook フォームとアイテムの連携のしくみ](/office/vba/outlook/Concepts/Forms/how-outlook-forms-and-items-work-together)
