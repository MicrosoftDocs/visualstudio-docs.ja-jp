---
title: ソリューションの親コンテナー フォルダーの作成 | Microsoft Docs
description: ソース管理プラグイン API バージョン 1.2 を使用して、ソリューション内のすべての Web プロジェクトに対して 1 つのルート ソース管理ターゲットを指定する方法を説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- solutions, creating parent containers
- source control plug-ins, creating parent containers
ms.assetid: 961e68ed-2603-4479-a306-330eda2b2efa
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 2c9b3b5c01e9c1ad5de9fbb0a44398d3f7963295
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105056841"
---
# <a name="create-parent-container-folders-for-solutions"></a>ソリューションの親コンテナー フォルダーを作成する
ソース管理プラグイン API バージョン 1.2 では、ユーザーが、ソリューション内のすべての Web プロジェクトに対して 1 つのルート ソース管理ターゲットを指定できます。 この 1 つのルートは、スーパー統合ルート (SUR) と呼ばれます。

 ソース管理プラグイン API バージョン 1.1 では、ユーザーがマルチプロジェクト ソリューションをソース管理に追加すると、各 Web プロジェクトに対して 1 つのソース管理ターゲットを指定するようにユーザーが求められました。

## <a name="new-capability-flags"></a>新しい機能フラグ
 `SCC_CAP_CREATESUBPROJECT`

 `SCC_CAP_GETPARENTPROJECT`

## <a name="new-functions"></a>新しい関数
- [SccCreateSubProject](../../extensibility/scccreatesubproject-function.md)

- [SccGetParentProjectPath](../../extensibility/sccgetparentprojectpath-function.md)

 ソリューションをソース管理に追加するとき、ほとんどの場合、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE によって SUR フォルダーが作成されます。 具体的には、次の場合に行われます。

- プロジェクトがファイル共有 Web プロジェクトです。

- プロジェクトとソリューション ファイルのドライブが異なります。

- プロジェクトとソリューション ファイルの共有が異なります。

- プロジェクトが (ソース管理ソリューションに) 個別に追加されました。

[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] では、SUR フォルダーの名前を拡張子なしのソリューション名と同じにすることをお勧めします。 次の表に、2 つのバージョンの動作をまとめています。

|特徴量|ソース管理プラグイン API バージョン 1.1|ソース管理プラグイン API バージョン 1.2|
|-------------| - | - |
|SCC へのソリューションの追加|SccInitialize()<br /><br /> SccGetProjPath()<br /><br /> SccGetProjPath()<br /><br /> SccOpenProject()|SccInitialize()<br /><br /> SccGetProjPath()<br /><br /> SccCreateSubProject()<br /><br /> SccCreateSubProject()<br /><br /> SccOpenProject()|
|ソース管理されているソリューションへのプロジェクトの追加|SccGetProjPath()<br /><br /> OpenProject()|SccGetParentProjectPath()<br /><br /> SccOpenProject()<br /><br />  **注:** Visual Studio では、ソリューションが SUR の直接の子であることが前提とされます。|

## <a name="examples"></a>例
 2 つの例を次の表に示します。 どちらのケースでも、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ユーザーは、*user_choice* にターゲットを指定するまで、ソース管理されているソリューションのターゲット場所の指定を求められます。 user_choice が指定されると、ソース管理ターゲットの指定をユーザーに求めずに、ソリューションと 2 つのプロジェクトが追加されます。

|ソリューションの内容|ディスク上の場所|データベースの既定の構造|
|-----------------------|-----------------------|--------------------------------|
|*sln1.sln*<br /><br /> Web1<br /><br /> Web2|*C:\Solutions\sln1*<br /><br /> *C:\Inetpub\wwwroot\Web1*<br /><br /> \\\server\wwwroot$\Web2|$/<user_choice>/sln1<br /><br /> $/<user_choice>/C/Web1<br /><br /> $/<user_choice>/Web2|
|*sln1.sln*<br /><br /> Web1<br /><br /> Win1|*C:\Solutions\sln1*<br /><br /> *D:\Inetpub\wwwroot\Web1*<br /><br /> *C:\solutions\sln1\Win1*|$/<user_choice>/sln1<br /><br /> $/<user_choice>/D/web1<br /><br /> $/<user_choice>/sln1/win1|

 SUR フォルダーとサブフォルダーは、操作が取り消されてもエラーが原因で失敗しても、関係なく作成されます。 これらは、キャンセルまたはエラー条件で自動的に削除されることはありません。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] が既定でバージョン 1.1 の動作になるのは、ソース管理プラグインによって `SCC_CAP_CREATESUBPROJECT` および `SCC_CAP_GETPARENTPROJECT` 機能フラグが返されない場合です。 また、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] のユーザーは、次のキーの値を *dword:00000001* に設定して、バージョン 1.1 の動作に戻すことを選択できます。

 **[HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\8.0\SourceControl] DoNotCreateSolutionRootFolderInSourceControl** = *dword:00000001*

## <a name="see-also"></a>こちらもご覧ください
- [ソース管理プラグイン API バージョン 1.2 の新機能](../../extensibility/internals/what-s-new-in-the-source-control-plug-in-api-version-1-2.md)
