---
title: Office ソリューションの共同開発
description: 複数の開発者が、他の Visual Studio プロジェクトで共同作業するのと同じように Office プロジェクトを操作できるようにする方法について説明します。
ms.custom: SEO-VS-2020
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
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 028530014afdc78ab6c9c0483c3d443195383793
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99942309"
---
# <a name="collaborative-development-of-office-solutions"></a>Office ソリューションの共同開発
  複数の開発者は、他の Visual Studio プロジェクトで共同作業するのと同じように Office プロジェクトを操作することができます。 Visual Studio では、Microsoft Office が異なる場所にインストールされている場合でも、各コンピューター上の Office インストールの場所を正しく検索します。 ただし、知っておくべき重要な考慮事項がいくつかあります。

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

## <a name="debug-properties-are-not-shared"></a>デバッグ プロパティは共有されない
 デバッグ プロパティは、ソース管理で複数のユーザー間では共有されません。 Visual Basic や Visual C# のプロジェクトでは、デバッグ プロパティはユーザー固有のファイル (*ProjectName*.vbproj.user または *ProjectName*.csproj.user) に格納され、このファイルはソース管理下にありません。 複数のユーザーがデバッグを実行する場合は、各自が手動でデバッグ プロパティを入力する必要があります。

 プロジェクトがソース管理内ではなくネットワーク共有に置かれている場合は、共同作業を行う開発者がソリューションを開いてアセンブリをテストできるように、いくつかの追加手順を実行する必要があります。

## <a name="source-control-requires-checking-out-all-files"></a>ソース管理ではすべてのファイルのチェックアウトが必要
 プロジェクトにソース管理を使用する場合は、コード ファイル (*ThisDocument*、*ThisWorkbook*、*ThisAddIn* など) を変更するたびに、**ソリューション エクスプローラー** でそのコード ファイルの下にあるすべてのファイル (既定で非表示になっているファイルも含む) をチェックアウトする必要があります。 最上位のコード ファイルのみをチェックアウトすると、変更内容が失われる可能性があります。

 変更を行った後は、それらのすべてのファイルをチェックインし直します。 プロジェクト内の非表示のコード ファイルについて詳しくは、「[Visual Studio 環境における Office プロジェクト](../vsto/office-projects-in-the-visual-studio-environment.md)」を参照してください。

## <a name="security-for-informal-collaboration-on-a-network"></a>ネットワーク上での非公式の共同作業のセキュリティ
 ネットワークの場所 (\\\\*Servername*\\*Sharename* など) にあるすべてのドキュメント レベルのソリューションでは、使用している Microsoft Office アプリケーション内の信頼されたフォルダー一覧に、完全修飾された場所を追加する必要があります。 メイン フォルダーの下にサブディレクトリを含める (厳密には、信頼されたフォルダー一覧にデバッグおよびビルド フォルダーを追加する) オプションを選択します。 この方法の詳細については、「[ドキュメントへの信頼の付与](../vsto/granting-trust-to-documents.md)」を参照してください。

 ビルド時に自動的に生成される一時的な証明書は、パスワードで保護されません。 それらの証明書には、開発者のログイン名とその他の個人情報が含まれています。 一時的な証明書で署名されたカスタマイズを配置した場合、他のユーザーがこの情報にアクセスできる可能性があります。

## <a name="see-also"></a>関連項目
- [Office ソリューションをセキュリティで保護する](../vsto/securing-office-solutions.md)
- [Office ソリューションを設計して作成する](../vsto/designing-and-creating-office-solutions.md)
- [Office ソリューションのビルド](../vsto/building-office-solutions.md)
