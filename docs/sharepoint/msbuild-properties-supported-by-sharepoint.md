---
title: SharePoint でサポートされている MSBuild のプロパティ |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, MSBuild properties
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 5470160c6b0af1af39238a14319ad497e1541a43
ms.sourcegitcommit: dcbb876a5dd598f2538e62e1eabd4dc98595b53a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/28/2019
ms.locfileid: "72985171"
---
# <a name="msbuild-properties-supported-by-sharepoint"></a>SharePoint でサポートされている MsBuild プロパティ
  VisualStudio ファイル、プロジェクトファイル、またはプロジェクトユーザーファイルで定義されているすべての [!INCLUDE[vstecmsbuild](../sharepoint/includes/vstecmsbuild-md.md)] プロパティは、[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] SharePoint プロジェクトで使用できます。 SharePoint では、プロジェクトによって提供される共通の [!INCLUDE[vstecmsbuild](../sharepoint/includes/vstecmsbuild-md.md)] プロパティに加えて、SharePoint プロジェクトに固有の追加のプロパティが定義されます。

 共通 [!INCLUDE[vstecmsbuild](../sharepoint/includes/vstecmsbuild-md.md)] プロパティの一覧については、「 [MSBuild プロジェクトの共通プロパティ](/previous-versions/dotnet/netframework-4.0/bb629394(v=vs.100))」を参照してください。 プログラミング言語でサポートされているプロパティの完全な一覧については、 *.targets*ファイル、プロジェクトファイル ( *.csproj*または *.vbproj*)、またはプロジェクトユーザーファイル ( *.csproj*または *.vbproj*) を参照してください。

## <a name="msbuild-properties-specific-to-sharepoint"></a>SharePoint に固有の MsBuild プロパティ
 次の表に、[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]の SharePoint プロジェクトに特に適用される [!INCLUDE[vstecmsbuild](../sharepoint/includes/vstecmsbuild-md.md)] のプロパティを示します。 その他のプロパティは存在しますが、内部で使用するためのものです。

|プロパティ名|説明|
|-------------------|-----------------|
|SharePointSiteUrl|SharePoint サイトへの [!INCLUDE[TLA2#tla_url](../sharepoint/includes/tla2sharptla-url-md.md)] を表す文字列です。|
|SandboxedSolution|ソリューションがサンドボックスソリューションであるかどうかを示すブール値。|
|ActiveDeploymentConfiguration|アクティブな配置構成。|
|IncludeAssemblyInPackage|アセンブリがパッケージファイルに含まれるかどうかを示すブール値です。|
|PreDeploymentCommand|配置前コマンドのステップで実行するコマンドを表す文字列値。|
|PostDeploymentCommand|配置後コマンドのステップで実行するコマンドを表す文字列値。|
|CustomBeforeSharePointTargets|[!INCLUDE[vstecmsbuild](../sharepoint/includes/vstecmsbuild-md.md)] ターゲットファイルのパスを表す文字列。 ターゲットファイルが存在し、定義されている場合は、SharePoint ターゲットデータの前にインポートされます。 このプロパティを使用すると、配布された SharePoint ターゲットファイルを変更せずにパッケージ関連のプロパティを事前することで、パッケージプロセスをカスタマイズできます。ただし、ターゲットファイルは、すべての SharePoint プロジェクトに適用されます。|
|CustomAfterSharePointTargets|[!INCLUDE[vstecmsbuild](../sharepoint/includes/vstecmsbuild-md.md)] ターゲットファイルのパスを表す文字列。 ターゲットファイルが存在し、定義されている場合は、すべての SharePoint ターゲットデータの後にインポートされます。 このプロパティを使用すると、配布された SharePoint ターゲットファイルを変更することなくパッケージ関連のプロパティとターゲットをオーバーライドすることにより、パッケージプロセスをカスタマイズできます。ただし、ターゲットファイルは、すべての SharePoint プロジェクトに適用されます。|
|LayoutPath|パッケージ化される各ファイルが *.wsp*ファイルに追加される前に一時的に配置されるルートディレクトリを表す文字列。 このパスは、BeforeLayout および AfterLayout ターゲットをオーバーライドしてパッケージ化するファイルを追加、削除、または変更するタイミングを把握するのに役立ちます。これは、 *.wsp*ファイルの内容を変更するために使用できるためです。|
|BasePackagePath|パッケージが配置されているフォルダーを表す文字列。 この値は、プロジェクトの出力ディレクトリ (Bin\debug など) を使用します。|
|PackageExtension|パッケージに追加するファイル名拡張子を表す文字列です。 既定値は wsp です。|
|AssemblyDeploymentTarget|プロジェクトアセンブリが SharePoint サーバー上に配置される場所を表す文字列。 この値は、GlobalAssemblyCache (既定値) または WebApplication です。 このプロパティは、プロパティウィンドウで設定することもできます。|
|PackageWithValidation|パッケージ化の前に検証を実行するかどうかを指定するブール値です。 このプロパティを使用すると、パッケージのビルド中に検証エラーを無視できます。|
|ValidatePackageDependsOn|ValidatePackage ターゲットの前に実行する追加のターゲットを定義する文字列。|
|TokenReplacementFileExensions|パッケージ化中にトークンが置き換えられるファイルを定義する文字列。|

## <a name="use-msbuild-properties-in-the-properties-page"></a>[プロパティ] ページで MsBuild のプロパティを使用する
 柔軟性を高めるために、SharePoint のプロパティ ページの **展開前のコマンドライン** ボックスと **配置後**のコマンド ボックスでハードコーディングされた文字列を使用する代わりに、sharepoint プロパティを引数として使用できます。 たとえば、SharePoint サイトに特定の [!INCLUDE[TLA2#tla_url](../sharepoint/includes/tla2sharptla-url-md.md)] 文字列を指定する代わりに、代わりに `$(SharePointSiteUrl)`を使用できます。

> [!NOTE]
> [!INCLUDE[vstecmsbuild](../sharepoint/includes/vstecmsbuild-md.md)] 変数構文 `$(`*propertyname*`)` または環境変数構文 `%`*propertyname*`%` を使用してプロパティを指定できます。

## <a name="see-also"></a>関連項目

- [MSBuild リファレンス](../msbuild/msbuild-reference.md)