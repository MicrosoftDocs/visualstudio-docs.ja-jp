---
title: Web プロジェクトの基本情報 | Microsoft Docs
description: Web プロジェクトが Visual Studio で機能する仕組みの内部的な詳細について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- web projects, essentials
ms.assetid: ca2f4e43-322c-4431-8680-52da846940bc
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 9442dcdd460e1213c3c07ee87a5ea2e0d7099072
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105085703"
---
# <a name="web-project-essentials"></a>Web プロジェクトの基本情報
Web プロジェクトでは、Web アプリケーションを作成します。 Web プロジェクトを使用して、スマート Web ページを含む Web アプリケーションを作成できます。 スマート Web ページには、Web ページをオンデマンドでレンダリングするサーバー側コードがあります。

 [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] や [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] などの従来のプログラミング言語を使用してスマート Web ページを作成し、ユーザーから情報を収集して処理したり、データベースに情報を格納したりできます。

- 分離コード モデルでは、ファイル拡張子 .aspx または .asmx を持つ Web ページに、依存ソース コード ファイルが関連付けられます。 たとえば、hello.aspx には、依存ソース コード ファイル hello.aspx.cs が関連付けられる場合があります。

- スマート Web ページに関連付けられているサーバー側コードは、実行可能ファイルにコンパイルされて Web サイトの /bin フォルダーに配置されます。

- 特定の Web ページに関連付けられていないヘルパー クラスなどの追加のソース コード ファイルは、Web サイトの /App_Code フォルダーに配置されます。

  - Web サイト プロジェクト (WSP) では、スマート Web ページごとに 1 つの実行可能ファイルが生成されます。 /App_Code フォルダー内のソース コード ファイルから、追加の実行可能ファイルが生成されます。

  - Web アプリケーション プロジェクト (WAP) では、すべてのスマート Web ページのコードおよび /App_Code フォルダー内のすべてのソース ファイルを組み合わせた、1 つの実行可能ファイルが生成されます。

- Web プロジェクトのソリューション ファイルは、Web サイト自体とは別に配置されます。 既定では、ソリューション ファイルは \Documents and Settings\\*YourAccount*\My Documents\\ *\<Visual Studio ####>* \Projects\\*YourWebSite* に配置されます。

  > [!NOTE]
  > ソリューション ファイルを Web サイトに保持するには、ファイルをそこに移動して再度開きます。

- ソリューション ファイルのない Web サイトを Visual Studio で開くと、新しいソリューション ファイルが自動的に生成されます。

- Web プロジェクトにはプロジェクト ファイルがありません。 プロジェクト情報は、ソリューション ファイル、web.config ファイル、その他の場所に格納されます。

- Web プロジェクトにグローバル プロパティを追加すると、Web プロジェクトのソリューション フォルダーにストレージ ファイルが自動的に作成されます。

- Page ディレクティブまたは \<script runat="server"> タグを使用すると、スマート Web ページをサーバー側のプログラミング言語に関連付けることができます。

- また、Web ページには、任意のスクリプト言語で記述されたクライアント側スクリプト ブロックをいくつでも含めることができます。

- Web サイト プロジェクト システムは、プロジェクト テンプレートと項目テンプレートを追加し、[!INCLUDE[vwprvw](../../extensibility/internals/includes/vwprvw_md.md)] プロジェクトに登録することで実装されます。

- WAP システムは、プロジェクト サブタイプ (プロジェクト フレーバーとも呼ばれます) として実装されます。 WAP システムを作成するために、[!INCLUDE[vwprvw](../../extensibility/internals/includes/vwprvw_md.md)] プロジェクトに WAP サブタイプによってフレーバーが適用されます。 プロジェクトのサブタイプの詳細については、「[プロジェクト サブタイプ](../../extensibility/internals/project-subtypes.md)」を参照してください。

- スマート Web ページは、HTML とサーバー側のプログラミング言語を組み合わせたものです。 サーバー側の言語は、含まれる言語と呼ばれます。 含まれる言語をサポートするには、Web プロジェクト システムで <xref:Microsoft.VisualStudio.TextManager.Interop.IVsContainedLanguage> インターフェイス ファミリを実装する必要があります。

  - 含まれる言語をエディターでサポートするために、HTML 言語サービスでは、含まれる言語コードの表示を、含まれる言語サービスに委ねる必要があります。

  - エラー マーカー (赤の波線) は、常にコード エディターのプライマリ バッファーに作成する必要があります。

## <a name="see-also"></a>関連項目
- [Web プロジェクト](../../extensibility/internals/web-projects.md)
