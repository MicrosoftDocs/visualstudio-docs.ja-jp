---
title: Outlook フォーム領域を作成するためのガイドライン
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- form regions [Office development in Visual Studio], guidelines
- icons [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: a962b1ae2bff7b9a954204485a6ee73a3b63eb7b
ms.sourcegitcommit: e98db44f3a33529b0ba188d24390efd09e548191
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/25/2019
ms.locfileid: "71255953"
---
# <a name="guidelines-to-create-outlook-form-regions"></a>Outlook フォーム領域を作成するためのガイドライン
  次に示す情報は、フォーム領域の最適化と、潜在的な問題の回避に役立ちます。

- [フォーム領域名を使用](#UsingFormRegions)します。

- [フォーム領域の継承を無効に](#DisablingInheritance)します。

- [型とメッセージクラス名について](#ClassNames)説明します。

- [閲覧ウィンドウの隣接フォーム領域をデザイン](#ReadingPane)します。

- [最適なアイコンサイズを使用](#UsingOptimal)します。

  フォーム領域の詳細については、「 [Outlook フォーム領域の作成](../vsto/creating-outlook-form-regions.md)」を参照してください。

  [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

## <a name="UsingFormRegions"></a>フォーム領域名を使用する
 フォーム領域は、いくつかの名前を使用して記述されます。 これらの名前の違いと、その名前がフォーム領域に与える影響を理解することが大切です。 次の表は、それぞれの名前の説明です。

|フォーム領域の名前|説明|
|----------------------|-----------------|
|フォーム領域の項目名|**[新しい項目の追加]** ダイアログ ボックスで **Outlook フォーム領域** のアイテムに指定した名前です。 これはフォーム領域コード ファイルの名前で、 **ソリューション エクスプローラー**に表示されます。|
|<xref:Microsoft.Office.Tools.Outlook.FormRegionManifest.FormRegionName%2A> プロパティ|この名前は、 **新しい Outlook フォーム領域** ウィザードの **[説明用のテキストを指定し、表示設定を選択します]** ページで指定します。 この名前は、 **[プロパティ]** ウィンドウに **FormRegionName** プロパティとして表示されます。<br /><br /> <xref:Microsoft.Office.Tools.Outlook.FormRegionManifest.FormRegionName%2A> プロパティを使用して、Outlook ユーザー インターフェイス (UI) のフォーム領域を識別するラベルを指定します。 分離フォーム領域の場合、この名前は Outlook アイテムのリボンにボタンとして表示されます。<br /><br /> 隣接フォーム領域の場合、この名前は、フォーム領域上のヘッダー テキストとして表示されます。|
|`Microsoft.Office.Tools.Outlook.FormRegionName` 属性|プロジェクトに **Outlook フォーム領域** アイテムを追加すると、Visual Studio によって、このプロパティはフォーム領域の完全修飾名に設定されます。 既定の完全修飾名は、VSTO アドインの名前にフォーム領域の名前を追加して、ドットで区切った名前に設定されます。たとえば、 `OutlookAddIn1.FormRegion1`のようになります。<br /><br /> この完全修飾名は、フォーム領域ファクトリ クラスの先頭にも属性として表示されます。<br /><br /> `Microsoft.Office.Tools.Outlook.FormRegionName` 属性を使用すると、Outlook VSTO アドインのすべてを通じてフォーム領域を一意に識別できます。フォーム領域アイテムの名前を変更しても、<xref:Microsoft.Office.Tools.Outlook.FormRegionManifest.FormRegionName%2A> プロパティを変更しても、`Microsoft.Office.Tools.Outlook.FormRegionName` 属性の値を変更することはできません。 この名前を変更するには、フォーム領域コード ファイルの `Microsoft.Office.Tools.Outlook.FormRegionName` 属性を変更する必要があります。|

## <a name="DisablingInheritance"></a>フォーム領域の継承を無効にする
 既定では、カスタム メッセージ クラスは、基本メッセージ クラスのすべてのフォーム領域の関連付けを継承します。 たとえば、`IPM.Task.Contoso` という名前のメッセージ クラスは `IPM.Task` から派生します。 そのため、`IPM.Task.Contoso` は `IPM.Task` のフォーム領域の関連付けを継承します。

 どの派生メッセージ クラスにもフォーム領域を関連付ける必要がない場合は、フォーム領域の <xref:Microsoft.Office.Tools.Outlook.FormRegionManifest.ExactMessageClass%2A> プロパティを **true**。 たとえば、隣接フォーム領域をに`IPM.Task`関連付けて、 <xref:Microsoft.Office.Tools.Outlook.FormRegionManifest.ExactMessageClass%2A>プロパティを**true**に設定した場合、フォーム領域は標準タスクフォームの下部にのみ追加されます。 フォーム領域は、標準タスク フォームのカスタマイズ バージョンの末尾には追加されません。

## <a name="ClassNames"></a>型とメッセージクラス名について
 Outlook アイテムの型名は、Outlook アイテムのメッセージ クラス名とは異なります。 たとえば、RSS アイテムの型名は `Microsoft.Office.Interop.Outlook.PostItem` です。 RSS アイテムのメッセージ クラス名は `IPM.Post.RSS` です。

 型名は、コード内の Outlook アイテムを参照するときに使用します。 型名の一覧については、「[フォーム領域を Outlook メッセージクラスに関連付ける](../vsto/associating-a-form-region-with-an-outlook-message-class.md)」を参照してください。

 **新しい Outlook フォーム領域ウィザード** の Outlook アイテムのメッセージ クラス名は、アイテムをフォーム領域に関連付けるときに使用します。 有効なメッセージクラス名の一覧については、「[フォーム領域を Outlook メッセージクラスに関連付ける](../vsto/associating-a-form-region-with-an-outlook-message-class.md)」を参照してください。

## <a name="ReadingPane"></a>閲覧ウィンドウの隣接フォーム領域をデザインする
 Outlook の閲覧ウィンドウを使用すると、アイテムを開かずに、Outlook アイテムをプレビューできます。 閲覧ウィンドウは、読み取り専用に設計されています。 そのため、隣接フォーム領域に追加するテキスト ボックスなどの入力コントロールは、閲覧ウィンドウでアイテムとフォーム領域を開いたときに、期待どおりに動作しないことがあります。

 たとえば、隣接フォーム領域を含むアイテムを閲覧ウィンドウで開くと、次のような状況が発生する可能性があります。

1. フォーム領域上のテキスト ボックスで、一部のテキストを選択します。

2. Del**キーを**押します。

3. テキスト ボックスで選択したテキスト部分でなく、メール アイテム全体が削除されます。

   隣接フォーム領域をデザインするときに、その領域に入力コントロールを含める場合は、閲覧ウィンドウ内のコントロールをテストして、正しく動作することを確認します。 期待どおりに動作しないコントロールを無効にするように、カスタム コードを追加することを検討してください。

   または、フォーム領域の <xref:Microsoft.Office.Tools.Outlook.FormRegionManifest.ShowInspectorRead%2A> プロパティを **False**。 この方法では、閲覧ウィンドウでフォーム領域が使用できなくなります。

## <a name="UsingOptimal"></a>最適なアイコンサイズを使用する
 **[プロパティ]** ウィンドウの **[Icons]** プロパティ グループでアイコンのプロパティを設定すると、フォーム領域に表示するアイコンを指定できます。 視覚的な品質を最高にするために、次のガイドラインを参考にしてください。

- **ページ** アイコンには、PNG (Portable Network Graphics) ファイルを使用します。

- **ウィンドウ** アイコンは 32 ピクセル × 32 ピクセルにする必要があります。

- その他のすべてのアイコンは 16 ピクセル × 16 ピクセルにする必要があります。

  **ページ** アイコンは、分離、置換、またはすべて置換のフォーム領域を含むアイテムについて、インスペクターのリボンに表示されます。

  **ウィンドウ**アイコンは、置換フォーム領域またはすべて置換フォーム領域を表示する開いているアイテムについて、通知領域および**Alt**+**Tab**ダイアログボックスに表示されます。

## <a name="see-also"></a>関連項目
- [実行時のフォーム領域へのアクセス](../vsto/accessing-a-form-region-at-run-time.md)
- [Outlook フォーム領域の作成](../vsto/creating-outlook-form-regions.md)
- [チュートリアル: Outlook フォーム領域のデザイン](../vsto/walkthrough-designing-an-outlook-form-region.md)
- [方法: フォーム領域を Outlook アドインプロジェクトに追加する](../vsto/how-to-add-a-form-region-to-an-outlook-add-in-project.md)
- [フォーム領域を Outlook メッセージクラスに関連付ける](../vsto/associating-a-form-region-with-an-outlook-message-class.md)
