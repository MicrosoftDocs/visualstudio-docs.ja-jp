---
title: プロジェクト タイプの基本情報 | Microsoft Docs
description: プロジェクト タイプを作成する必要がある場合と、プロジェクト サブタイプを使用して既存のプロジェクト タイプを拡張できる場合について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- project types [Visual Studio SDK]
ms.assetid: 09991589-2300-430e-b6a4-7f2b95fe676f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 051e7b76edd4559914307459fdcbdf1b7c0b600e
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112903558"
---
# <a name="project-type-essentials"></a>プロジェクト タイプの基本情報
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] には、[!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] や [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] などの言語に対応した複数のプロジェクト タイプが含まれています。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] では、独自のプロジェクト タイプを作成することもできます。

 カスタムのコマンド、エディター、またはツール ウィンドウを [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] に追加するだけの場合は、新しいプロジェクト タイプを作成しなくてもかまいません。 詳細については、次のトピックを参照してください。

- [コマンド、メニュー、およびツール バー](../../extensibility/internals/commands-menus-and-toolbars.md)

- [エディターと言語サービスの拡張機能](../../extensibility/editor-and-language-service-extensions.md)

- [ツール ウィンドウの拡張とカスタマイズ](../../extensibility/extending-and-customizing-tool-windows.md)

  同様に、提供された [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] および [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] プロジェクト タイプの動作をカスタマイズする場合は、プロジェクト サブタイプを使用して行うことができます。 詳細については、「[プロジェクト サブタイプ](../../extensibility/internals/project-subtypes.md)」を参照してください。

  次の項目の 1 つ以上をサポートする場合は、[!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] と [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] 以外の言語に基づいたプロジェクト用の新しいプロジェクト タイプを作成する必要があります。

- Build

- デプロイ

- 複数の構成

- ソース管理

- デバッグ

- ソリューション エクスプローラーのプロジェクト項目

- **[プロジェクトを開く]** または **[新しいプロジェクト]** ダイアログ ボックス

- プロジェクトの入れ子化

- プロジェクト タイプの機能の詳細については、以下を参照してください。

- プロジェクト タイプは VSPackage 内のオブジェクトであり、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] で期待される一連のインターフェイスを実装するものです。 C# を使用してプロジェクト タイプを開発する場合、必要なインターフェイスは Managed Package Framework プロジェクト クラスによって実装されるため、その実装を継承できます。 詳細については、「[マネージド パッケージ フレームワークを使用したプロジェクト タイプの実装 (C#)](../../extensibility/internals/using-the-managed-package-framework-to-implement-a-project-type-csharp.md)」を参照してください。

- C++ 開発者にとっては、HierUtil ライブラリ内のクラスが同様の役割を果たします。 詳細については、[ビルド内にありません: HierUtil7 プロジェクト クラスを使用したプロジェクト タイプの実装 (C++)](/previous-versions/bb166212(v=vs.100)) に関するページを参照してください。

- プロジェクト タイプでは、.exe または .dll アセンブリにビルドされる一般的なソース コード ファイル以外のデータをサポートできます。 たとえば、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] データベース プロジェクトでは、ディスクに格納されているスクリプトおよびクエリ ファイルへの参照が含まれ、データベースに対してスクリプトやクエリを実行するためのコマンドを **ソリューション エクスプローラー** に追加しますが、プロジェクトではビルド動作をサポートしていません。 詳細については、「[プロジェクト項目のオープンと保存](../../extensibility/internals/opening-and-saving-project-items.md)」を参照してください。

- プロジェクト タイプでは、ファイルを使用する必要は一切ありません。 たとえば、プロジェクト タイプでは、そのデータのすべてをデータベースに格納できます。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] では、プロジェクトおよびプロジェクト項目のデータを永続化する方法について、全面的な制御をプロジェクト タイプに認めています。 詳細については、「[プロジェクト タイプのデザインの方針](../../extensibility/internals/project-type-design-decisions.md)」を参照してください。

- プロジェクト タイプでは、*プロジェクト ファクトリ* を提供する必要があります。これは、特定のプロジェクト タイプに基づいたプロジェクトを開くか作成するよう [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] に指示が出されるたびに、そのプロジェクト タイプのインスタンスを作成するオブジェクトです。 詳細については、「[プロジェクト ファクトリを使用したプロジェクト インスタンスの作成](../../extensibility/internals/creating-project-instances-by-using-project-factories.md)」を参照してください。

- プロジェクト タイプでは、プロジェクトおよびプロジェクト項目のテンプレートを提供する必要があります。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] では、ユーザーが新しいプロジェクトを作成したり、新しい項目を既存のプロジェクトに追加したりするときにテンプレートを使用します。 詳細については、「[プロジェクトおよびプロジェクト項目テンプレートの追加](../../extensibility/internals/adding-project-and-project-item-templates.md)」を参照してください。

- プロジェクト タイプでは、デバッグやリリースなどの複数の構成をサポートできます。 ユーザーは、指定されたプロパティ ページを使用して、プロジェクトのさまざまな構成を変更できます。 詳細については、「[構成オプションの管理](../../extensibility/internals/managing-configuration-options.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [プロジェクト タイプの配置](../../extensibility/internals/deploying-project-types.md)