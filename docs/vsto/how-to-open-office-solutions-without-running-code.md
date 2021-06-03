---
title: '方法: コードを実行せずに Office ソリューションを開く'
description: アセンブリ コードを実行せずに、マネージド コード拡張機能を含むドキュメントまたはブックを開く方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office solutions [Office development in Visual Studio], opening
- opening Office solutions
- bypassing assemblies
- solutions [Office development in Visual Studio], opening
- assemblies [Office development in Visual Studio], bypassing
- Office documents [Office development in Visual Studio, opening without running code
- documents [Office development in Visual Studio], opening without running code
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 99f1a01a745544e7e11e724db9c6eafacf0ca201
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99876590"
---
# <a name="how-to-open-office-solutions-without-running-code"></a>方法: コードを実行せずに Office ソリューションを開く
  マネージド コード拡張機能を使用して作成された Microsoft Office ソリューションは、エンド ユーザーの Office アプリケーションのセキュリティ設定が [高] に設定されている場合でも実行されます。 これは、.NET アセンブリ コードのセキュリティが Microsoft Office ではなく Microsoft .NET Framework によって管理されるためです。

 しかし、場合によってはコードを実行せずにドキュメントを開く必要があります。 たとえば、ドキュメントを開いたときに実行されるコードでその内容が変更されるが、コードで変更される前に、ドキュメントの表示方法を更新する必要がある場合があります。 また、特定の情報が含まれているドキュメントを他のユーザーに送信する必要がある場合や、コードを実行して内容を変更する必要がない場合もあります。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

 アセンブリ コードを実行せずにマネージド コード拡張機能を含むドキュメントまたはブックを開くには、いくつかの方法があります。

## <a name="to-bypass-the-assembly-by-using-the-shift-key"></a>Shift キーを使用してアセンブリをバイパスするには

- Word と Excel でドキュメントを開くときに初期化イベントが発生しないようにするため、**Shift** キーを押しながら **[ファイル]** メニューからドキュメントとブックを開きます。

    > [!NOTE]
    > **[はじめに]** 作業ウィンドウからドキュメントまたはブックを開くと、**Shift** キーを押したままにしてもコードはバイパスされません。 また、Shift キーを押したままにしても、ドキュメントが開いた後にイベントが発生するのを防ぐことはできません。

     この方法は、最初にコードの実行とドキュメント変更を行わずに、ドキュメントを開いて変更を行う必要がある場合に便利です。

## <a name="to-bypass-an-assembly-by-renaming-or-removing-it"></a>名前の変更または削除によってアセンブリをバイパスするには

- アセンブリが配置されているコンピューターに必要なアクセス許可がある場合は、アセンブリの名前を変更するか、アセンブリを削除して、ドキュメントまたはブックで検出できないようにすることができます。 この結果、Office ドキュメントが開かれるたびにエラーが発生します。

     ソリューションが複数のユーザーによって使用されている場合は、この方法によってすべてのユーザーに対してソリューションが実行されなくなります。 これは、コードまたは参照先のサーバーで問題が検出され、すべてのユーザーがそれを実行できないようにする場合に役立ちます。

## <a name="see-also"></a>関連項目
- [Office ソリューションをセキュリティで保護する](../vsto/securing-office-solutions.md)
- [Office ソリューションを配置する](../vsto/deploying-an-office-solution.md)
- [Office ソリューションを設計して作成する](../vsto/designing-and-creating-office-solutions.md)
- [Office ソリューションでのアプリケーション マニフェストと配置マニフェスト](../vsto/application-and-deployment-manifests-in-office-solutions.md)
