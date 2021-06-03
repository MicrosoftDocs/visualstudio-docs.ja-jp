---
title: SharePoint でサポートされている MSBuild プロパティ | Microsoft Docs
description: SharePoint でサポートされている、SharePoint に固有の MSBuild プロパティの名前と説明の一覧を示します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, MSBuild properties
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 20458cc7047e913e13f4594380d4b4946b44ec17
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99938513"
---
# <a name="msbuild-properties-supported-by-sharepoint"></a>SharePoint でサポートされている MSBuild プロパティ
  Microsoft.VisualStudio.SharePoint.targets ファイル、プロジェクト ファイル、またはプロジェクト ユーザー ファイルで定義されている [!INCLUDE[vstecmsbuild](../sharepoint/includes/vstecmsbuild-md.md)] プロパティはすべて、[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] SharePoint プロジェクトで使用できます。 SharePoint では、プロジェクトによって提供される一般的な [!INCLUDE[vstecmsbuild](../sharepoint/includes/vstecmsbuild-md.md)] プロパティに加え、SharePoint プロジェクトに固有の追加のプロパティも定義されています。

 一般的な [!INCLUDE[vstecmsbuild](../sharepoint/includes/vstecmsbuild-md.md)] プロパティの一覧については、「[MSBuild プロジェクトの共通プロパティ](/previous-versions/dotnet/netframework-4.0/bb629394(v=vs.100))」を参照してください。 お使いのプログラミング言語でサポートされているプロパティの完全な一覧については、 *.targets* ファイル、プロジェクト ファイル ( *.csproj* または *.vbproj*)、またはプロジェクト ユーザー ファイル (*csproj.user* または *.vbproj.user*) を参照してください。

## <a name="msbuild-properties-specific-to-sharepoint"></a>SharePoint に固有の MSBuild プロパティ
 次の表に、[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] の SharePoint プロジェクトに特に適用される [!INCLUDE[vstecmsbuild](../sharepoint/includes/vstecmsbuild-md.md)] プロパティの一覧を示します。 プロパティは他にもありますが、それらは内部で使用するためのものです。

|プロパティ名|説明|
|-------------------|-----------------|
|SharePointSiteUrl|SharePoint サイトの [!INCLUDE[TLA2#tla_url](../sharepoint/includes/tla2sharptla-url-md.md)] を表す文字列。|
|SandboxedSolution|ソリューションがサンドボックス ソリューションであるかどうかを示すブール値。|
|ActiveDeploymentConfiguration|アクティブな配置構成。|
|IncludeAssemblyInPackage|アセンブリがパッケージ ファイルに含まれるかどうかを示すブール値。|
|PreDeploymentCommand|配置前コマンド ステップで実行するコマンドを表す文字列値。|
|PostDeploymentCommand|配置後コマンド ステップで実行するコマンドを表す文字列値。|
|CustomBeforeSharePointTargets|[!INCLUDE[vstecmsbuild](../sharepoint/includes/vstecmsbuild-md.md)] ターゲット ファイルのパスを表す文字列。 このターゲット ファイルが存在し、定義されている場合は、すべての SharePoint ターゲット データの前にインポートされます。 このプロパティを使用すると、配布された SharePoint ターゲット ファイルを変更せずにパッケージ関連のプロパティを事前に定義することで、パッケージ プロセスをカスタマイズできます。ただし、このターゲット ファイルはすべての SharePoint プロジェクトに適用されます。|
|CustomAfterSharePointTargets|[!INCLUDE[vstecmsbuild](../sharepoint/includes/vstecmsbuild-md.md)] ターゲット ファイルのパスを表す文字列。 このターゲット ファイルが存在し、定義されている場合は、すべての SharePoint ターゲット データの後にインポートされます。 このプロパティを使用すると、配布された SharePoint ターゲット ファイルを変更しなくてもパッケージ関連のプロパティとターゲットをオーバーライドすることで、パッケージ プロセスをカスタマイズできます。ただし、このターゲット ファイルはすべての SharePoint プロジェクトに適用されます。|
|LayoutPath|パッケージ化される各ファイルが *.wsp* ファイルに追加される前に一時的に配置されるルート ディレクトリを表す文字列。 このパスは、BeforeLayout および AfterLayout ターゲットをオーバーライドして、パッケージ化されるファイルを追加、削除、または変更するタイミングを把握するのに役立ちます。これを使用して *.wsp* ファイルの内容を変更できるからです。|
|BasePackagePath|パッケージが配置されているフォルダーを表す文字列。 この値には、プロジェクトの出力ディレクトリ (Bin\debug など) が使用されます。|
|PackageExtension|パッケージに追加するファイル名拡張子を表す文字列。 既定値は wsp です。|
|AssemblyDeploymentTarget|SharePoint サーバー上のプロジェクト アセンブリの配置先を表す文字列。 その値は、GlobalAssemblyCache (既定値) または WebApplication です。 このプロパティは、[プロパティ] ウィンドウで設定することもできます。|
|PackageWithValidation|パッケージ化の前に検証を行うかどうかを指定するブール値。 このプロパティを使用すると、パッケージのビルド中に発生する検証エラーを無視できます。|
|ValidatePackageDependsOn|ValidatePackage ターゲットの前に実行する追加のターゲットを定義する文字列。|
|TokenReplacementFileExensions|パッケージ化の処理中にトークンが置き換えられるファイルを定義する文字列。|

## <a name="use-msbuild-properties-in-the-properties-page"></a>プロパティ ページで MSBuild プロパティを使用する
 柔軟性を高めるため、SharePoint の [プロパティ] ページの **[配置前コマンド ライン]** および **[配置後コマンド ライン]** ボックスでハードコーディングされた文字列を使用する代わりに、SharePoint プロパティを引数として使用できます。 たとえば、SharePoint サイトに対して特定の [!INCLUDE[TLA2#tla_url](../sharepoint/includes/tla2sharptla-url-md.md)] 文字列を指定する代わりに、`$(SharePointSiteUrl)` を使用できます。

> [!NOTE]
> プロパティの指定には、[!INCLUDE[vstecmsbuild](../sharepoint/includes/vstecmsbuild-md.md)] 変数の構文 `$(`*propertyName*`)` または環境変数の構文 `%`*propertyName*`%` を使用できます。

## <a name="see-also"></a>関連項目

- [MSBuild リファレンス](../msbuild/msbuild-reference.md)