---
title: Office ソリューションの共同開発
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office applications [Office development in Visual Studio], collaborative development
- Office development in Visual Studio, collaboration
- source control [Office development in Visual Studio]
- collaborative development [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 76c26a110d88d3dee8bf7540647ea0bfde4e7c4f
ms.sourcegitcommit: d0425b6b7d4b99e17ca6ac0671282bc718f80910
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/21/2019
ms.locfileid: "56635060"
---
# <a name="collaborative-development-of-office-solutions"></a>Office ソリューションの共同開発
  複数の開発者は、他の Visual Studio プロジェクトが共同作業と同じ方法で Office プロジェクトで作業できます。 Visual Studio では、別の場所で Office がインストールされている場合でも、各コンピューターに Microsoft Office のインストールが正常で検索します。 ただし、注意すべき重要な考慮事項があります。

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

## <a name="debug-properties-are-not-shared"></a>デバッグ プロパティは共有されません。
 デバッグ プロパティは、ソース管理下の複数のユーザー間では共有されません。 Visual Basic および Visual C＃ プロジェクトでは、デバッグ プロパティをユーザー固有のファイル (*ProjectName.vbproj.user* または*ProjectName.csproj.user*)に格納します。このファイルはソース管理下にはありません。 複数のユーザーがデバッグを実行する場合は、各自が手動でデバッグ プロパティを入力する必要があります。

 プロジェクトは、ソース管理ではなく、ネットワーク共有に格納されているが場合、ソリューションを開き、アセンブリをテストする共同開発者を有効にする追加の手順を実行する必要があります。

## <a name="source-control-requires-checking-out-all-files"></a>ソース管理では、すべてのファイルをチェック アウトが必要です。
 プロジェクトをソース管理を使用する場合、これをチェック アウトのすべてのファイル内のコード ファイルでする必要があります**ソリューション エクスプ ローラー** (など、 *ThisDocument*、 *ThisWorkbook*、または*ThisAddIn*コード ファイル)、コード ファイルを変更するたびにもファイルを既定では表示されません。 最上位のコード ファイルのみをチェックする場合、変更は失われます。

 変更を行った後でバックアップのすべてのファイルを確認してください。 プロジェクト内の非表示コード ファイルの詳細については、[Visual Studio 環境における Office プロジェクト](../vsto/office-projects-in-the-visual-studio-environment.md)を参照してください。

## <a name="security-for-informal-collaboration-on-a-network"></a>ネットワーク上の共同のセキュリティ
 ネットワーク上の場所 (\\ \\ *Servername*\\*Sharename* など)にあるすべてのドキュメントレベルのソリューションでは、作業している Microsoft Office アプリケーションの信頼できるフォルダの一覧に完全修飾場所を追加する必要があります。 メインフォルダーの下にサブディレクトリを含めるか、デバッグフォルダとビルドフォルダを信頼できるフォルダリストに追加するかを選択します。 これを行う方法の詳細については、[ドキュメントに信頼を付与](../vsto/granting-trust-to-documents.md)を参照してください。

 ビルド時に自動的に生成される一時的な証明書は、パスワードで保護されていません。 証明書には、開発者のログイン名と他の個人情報が含まれています。 一時的な証明書によって署名されているカスタマイズを配置する場合は、この情報にアクセスできない他のユーザー必要があります。

## <a name="see-also"></a>関連項目
- [セキュリティで保護された Office ソリューション](../vsto/securing-office-solutions.md)
- [Office ソリューションの設計と作成](../vsto/designing-and-creating-office-solutions.md)
- [Office ソリューションの構築](../vsto/building-office-solutions.md)
