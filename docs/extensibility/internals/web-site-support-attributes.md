---
title: Web サイト サポートの属性 | Microsoft Docs
description: Web サイト プロジェクトを使用して Visual Studio の機能を拡張するために必要な Web サイト サポートの属性について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- web site projects, registration
ms.assetid: 46d52e2c-ca2a-4bbd-8500-5b0129768aec
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 348fd16234e38cd7832ae18e7b28e6abe0bc63d9
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112901774"
---
# <a name="web-site-support-attributes"></a>Web サイト サポートの属性
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] Web サイト プロジェクトを拡張して、Web プログラミング言語のサポートを提供できます。 この言語は [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] に自身を登録して、その言語が選択されたときに **[新しい Web サイト]** ダイアログ ボックスにプロジェクト テンプレートを表示できるようにする必要があります。

IronPython Studio のサンプルには、Web サイト サポートが含まれています。 このサンプルには、IronPython を新しい Web プロジェクトの分離コード言語として登録するための次の属性クラスが含まれています。

## <a name="websiteprojectattribute"></a>WebSiteProjectAttribute
 この属性は、言語プロジェクトに適用されます。 これにより、 **[新しい Web サイト]** ダイアログ ボックスの **[言語]** 一覧にある Web プログラミング言語の一覧にその言語が追加されます。 たとえば、次のコードでは IronPython を一覧に追加します。

```
[WebSiteProject("IronPython", "Iron Python")]
public class PythonProjectPackage : ProjectPackage
```

 この属性ではまた、テンプレート フォルダーを指すテンプレート パスを設定することもできます。 テンプレート フォルダーの場所の詳細については、「[Web サイト サポートのテンプレート](../../extensibility/internals/web-site-support-templates.md)」を参照してください。

## <a name="websiteprojectrelatedfilesattribute"></a>WebSiteProjectRelatedFilesAttribute
 この属性は、言語プロジェクトに適用されます。 これにより、Web サイト プロジェクトでは、**ソリューション エクスプローラー** で、あるファイルの種類 (関連) を別のファイルの種類 (プライマリ) の下に入れ子にすることができます。

 たとえば、次のコードでは、IronPython の分離コード ファイルが .aspx ファイルに関連していることを指定します。 IronPython Web サイト ソリューションで新しい .aspx Web ページが作成されると、新しい .py ソース ファイルが生成され、.aspx ページの子ノードとして表示されます。

```
[WebSiteProjectRelatedFiles("aspx", "py")]
public class PythonProjectPackage : ProjectPackage
```

## <a name="provideintellisenseproviderattribute"></a>ProvideIntellisenseProviderAttribute
 この属性は、言語プロジェクト パッケージに適用されます。 これにより、その言語の IntelliSense プロバイダーが選択されます。

 たとえば、次のコードでは、<xref:Microsoft.VisualStudio.Shell.Interop.IVsIntellisenseProject> を実装する PythonIntellisenseProvider のインスタンスが、言語サービスを提供するために必要に応じて作成される必要があることを指定します。

```
[ProvideIntellisenseProvider(typeof(PythonIntellisenseProvider), "IronPythonCodeProvider", "Iron Python", ".py", "IronPython;Python", "IronPython")]
public class PythonPackage : Package, IOleComponent
```

 IVsIntellisenseProject の実装では、参照を処理し、コードを含む Web ページが要求されているが、キャッシュされていない場合に言語コンパイラを呼び出します。

## <a name="see-also"></a>関連項目
- [Web サイト サポート](../../extensibility/internals/web-site-support.md)
