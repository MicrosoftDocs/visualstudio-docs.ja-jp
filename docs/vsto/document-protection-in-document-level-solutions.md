---
title: ドキュメント レベルのソリューションにおけるドキュメントの保護
description: ドキュメント レベルのプロジェクトで Microsoft Office Word および Microsoft Office Excel の保護機能を使用する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- restricted permissions [Office development in Visual Studio]
- permissions [Office development in Visual Studio]
- workbooks [Office development in Visual Studio], restricted permissions
- Office documents [Office development in Visual Studio], restricted permissions
- documents [Office development in Visual Studio], restricted permissions
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: ddfe9d70cafc6acf7526c8819cb9ae3f46ea8022
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99910550"
---
# <a name="document-protection-in-document-level-solutions"></a>ドキュメント レベルのソリューションにおけるドキュメントの保護
  ドキュメント レベルのプロジェクトで Microsoft Office Word および Microsoft Office Excel の保護機能を使用することができます。 これらの機能は、認可されていないユーザーがドキュメントの保護された部分を変更できないようにします。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

 Excel を使用する場合、デザイナーでブックを開いているときに保護をオンまたはオフにできます。 Word を使用する場合、デザイナーの外部でのみ保護を有効にすることができます。 Word と Excel の両方で、実行時にプログラムによって保護を有効または無効にすることができます。

 デザイナーで開かれているドキュメントでドキュメント保護が有効になっていると、すべてのコントロールが **[ツールボックス]** から削除されるか、使用できなくなります。また、 **[データ ソース]** ウィンドウからドキュメントに何もドラッグすることはできません。

## <a name="serverdocument-and-protected-documents"></a>ServerDocument と保護されたドキュメント
 ドキュメントが保護されている場合、ドキュメントの外部からデータ キャッシュにアクセスすることはできません。 <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> クラスを使用して、保護されたドキュメントにキャッシュされているデータを取得または操作したり、<xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> クラスの他のメソッドを使用したりすることはできません。

## <a name="word-document-protection-in-the-designer"></a>デザイナーでの Word 文書の保護
 Visual Studio で Word 文書またはテンプレートを開いているときに保護を追加した場合、デザイナーでの保護の適用を開始することはできません。 ドキュメントは Visual Studio で開かれている間はデザイン モードであり、保護の適用を開始する前に実行モードになっている必要があります。

 ただし、保護が有効になっている既存の Word 文書を使用するプロジェクトを作成した場合、デザイナーで開かれている間、ドキュメントは保護されます。 ドキュメントの保護された部分を編集することはできませんが、コード エディターでコードを記述してドキュメントを自動化することはできます。 また、Visual Studio でドキュメントを開いているときに保護が有効になっている場合は、プロジェクトをビルドできません。

 ドキュメントを編集してプロジェクトをビルドできるように、デザイナーでドキュメントが開いている間は保護をオフにすることができます。 デバッグ中にデザイナーでコピーの保護を無効にすることはできません。デバッグ中に開かれるドキュメントは、デザイナーで開いているものとは別のコピーです (出力コピーは、Visual Basic の *\bin* ディレクトリ、C# の場合は *\bin\debug* ディレクトリに格納されます)。

 デザイナーで開くドキュメントのコピーを保護するには、Visual Studio でプロジェクトを終了し、プロジェクト ディレクトリにあるドキュメントのコピーを開いて、保護を有効にします。

## <a name="enforce-word-document-protection-on-build"></a>ビルド時の Word 文書保護の適用
 Visual Studio では、ビルド処理中に Word 文書とテンプレートの保護の適用が開始されます。これにより、ドキュメントがデバッグ用に開かれたときに保護が有効になります。 ドキュメントは空のパスワードで保護されています。

 ビルド中に保護が有効にするのは、例外を発生させたりアプリケーションの動作を変更させる可能性のあるコードがドキュメントの <xref:Microsoft.Office.Tools.Word.Document.Startup> イベントに存在する場合に、このコードを正しくデバッグできるようにするためです。 ドキュメントを開いた後で保護を有効にした場合、初期化コードをデバッグまたはテストすることはできません。

## <a name="setting-the-password"></a>パスワードの設定
 Visual Studio では自動的に保護が有効になりますが、既定ではパスワードは提供されません。 ドキュメント保護にパスワードを設定する場合は、ソリューションを配置する前に追加する必要があります。 パスワードを追加すると、認可されたユーザーがドキュメントから保護を除去できるようになります。パスワードがないと、保護を簡単に除去できません。 パスワードの設定の詳細については、特定の Office アプリケーションのヘルプを参照してください。

## <a name="see-also"></a>関連項目
- [方法: プログラムによって文書および文書の一部を保護する](../vsto/how-to-programmatically-protect-documents-and-parts-of-documents.md)
- [Office 開発のサンプルとチュートリアル](../vsto/office-development-samples-and-walkthroughs.md)
- [Information Rights Management とマネージド コード拡張機能の概要](../vsto/information-rights-management-and-managed-code-extensions-overview.md)
- [Office ドキュメントのパスワード保護](../vsto/password-protection-on-office-documents.md)
- [方法: アクセス許可が制限されたドキュメントの背後でのコードの実行を許可する](../vsto/how-to-permit-code-to-run-behind-documents-with-restricted-permissions.md)
- [Office ソリューションを設計して作成する](../vsto/designing-and-creating-office-solutions.md)
