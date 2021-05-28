---
title: .NET 4.5 に移行する Office プロジェクトに必要な変更
description: ターゲット フレームワークを以前のバージョンの .NET Framework から .NET Framework 4 以降に変更する場合に、プロジェクトに加える必要がある変更について説明します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office projects [Office development in Visual Studio], migrating to .NET Framework 4
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 4fbe3c311e734cc076ab898544470c3e27e91795
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99943719"
---
# <a name="changes-required-for-office-projects-migrated-to-net-45"></a>.NET 4.5 に移行する Office プロジェクトに必要な変更

  Office プロジェクトのターゲット フレームワークを旧バージョンの .NET Framework から [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 以降に変更する場合は、ソリューションを開発用コンピューターとエンド ユーザーのコンピューターで実行できるようにするため、次のタスクを実行する必要があります。

- Visual Studio 2008 からアップグレードした場合は、プロジェクトから <xref:System.Security.SecurityTransparentAttribute> を削除します。

- 開発用コンピューターでプロジェクトを実行またはデバッグできるように、Visual Studio で **Clean** コマンドを実行します。

- プロジェクトの .NET Framework の必須コンポーネントを更新します。

- ターゲット フレームワークを変更する前に ClickOnce を使用してソリューションを配置した場合は、さらにエンド ユーザーがソリューションを再インストールする必要があります。

  これらの各タスクの詳細については、以下の対応するセクションを参照してください。

## <a name="remove-the-securitytransparent-attribute-from-projects-that-you-upgrade-from-visual-studio-2008"></a>Visual Studio 2008 からアップグレードするプロジェクトから SecurityTransparent 属性を削除する
 Visual Studio 2008 から Office プロジェクトをアップグレードした後で、プロジェクトのターゲット フレームワークが [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 以降に変更された場合は、プロジェクトから <xref:System.Security.SecurityTransparentAttribute> を削除する必要があります。 この属性は Visual Studio によって自動的に削除されません。 この属性を削除しないと、プロジェクトをコンパイルしたときにエラー メッセージが表示されます。

 Visual Studio でアップグレードされたプロジェクトのターゲット フレームワークを [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] または [!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)] に変更できる条件の詳細については、「[Office ソリューションのアップグレードと移行](../vsto/upgrading-and-migrating-office-solutions.md)」を参照してください。

#### <a name="to-remove-the-securitytransparentattribute"></a>SecurityTransparentAttribute を削除するには

1. Visual Studio でプロジェクトを開き、 **ソリューション エクスプローラー** を開きます。

2. **[プロパティ]** ノード (C# の場合) または **[マイ プロジェクト]** ノード (Visual Basic の場合) の下で、AssemblyInfo コード ファイルをダブルクリックしてコード エディターで開きます。

    > [!NOTE]
    > Visual Basic プロジェクトで AssemblyInfo コード ファイルを表示するには、 **ソリューション エクスプローラー** の **[すべてのファイルの表示]** ボタンをクリックする必要があります。

3. <xref:System.Security.SecurityTransparentAttribute> を探し、ファイルから削除するか、コメント アウトします。

    ```vb
    <Assembly: SecurityTransparent()>
    ```

    ```csharp
    [assembly: SecurityTransparent()]
    ```

## <a name="perform-the-clean-command-to-debug-or-run-a-project-on-the-development-computer"></a>開発用コンピューターでプロジェクトをデバッグまたは実行するために Clean コマンドを実行する
 Office プロジェクトをビルドした後でプロジェクトのターゲット フレームワークを [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 以降に変更する場合は、ターゲット フレームワークを変更した後、**Clean** コマンドを実行してからプロジェクトをビルドし直す必要があります。 **Clean** コマンドを実行しないと、対象が変更されたプロジェクトをデバッグまたは実行しようとしたときに <xref:System.Runtime.InteropServices.COMException> が発生します。

 **Clean** コマンドの詳細については、「[Office ソリューションのビルド](../vsto/building-office-solutions.md)」を参照してください。

## <a name="update-the-prerequisites-for-deployment"></a>配置する必須コンポーネントを更新する
 Office プロジェクトの対象を [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 以降に変更する場合は、 **[必須コンポーネント]** ダイアログ ボックスで .NET Framework の対応する必須コンポーネントを更新する必要があります。 そうしない場合は、ClickOnce 配置または InstallShield Limited Edition プロジェクトが以前のバージョンの .NET Framework をチェックし、インストールします。

 エンド ユーザーのコンピューターに配置する必須コンポーネントの更新の詳細については、「[方法: Office ソリューションを実行するための必須コンポーネントをエンド ユーザーのコンピューターにインストールする](/previous-versions/bb608608(v=vs.110))」を参照してください。

## <a name="reinstall-solutions-on-end-user-computers"></a>エンド ユーザーのコンピューターにソリューションを再インストールする
 ClickOnce を使用して .NET Framework 3.5 を対象とする Office ソリューションを配置してから、プロジェクトの対象を [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 以降に変更した場合、エンド ユーザーはソリューションをアンインストールし、再発行後のソリューションを再インストールする必要があります。 対象が変更されたソリューションを再発行し、エンド ユーザーのコンピューター上でソリューションが更新された場合は、エンド ユーザーが更新されたソリューションを実行したときに <xref:System.Runtime.InteropServices.COMException> が発生します。

## <a name="see-also"></a>こちらもご覧ください
- [Office ソリューションを .NET Framework 4 以降に移行する](../vsto/migrating-office-solutions-to-the-dotnet-framework-4-or-later.md)