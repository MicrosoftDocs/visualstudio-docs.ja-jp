---
title: カスタム ツール | Microsoft Docs
description: ツールをプロジェクト内の項目に関連付けて、ファイルが保存されるたびにそのツールを実行するカスタム ツールを、Visual Studio で作成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSPackages, custom tools
- tools [Visual Studio], custom
- custom tools
ms.assetid: d669f154-9b23-48b6-b9f6-7419c8dd61a6
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: d714822605178382ec2ef3574db617f7986cf888
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105091046"
---
# <a name="custom-tools"></a>カスタム ツール
"*カスタム ツール*" を使用すると、プロジェクト内の項目にツールを関連付けて、ファイルが保存されるたびにそのツールを実行することができます。 特定のカスタム ツール ("*単一ファイル ジェネレーター*" と呼ばれることもあります) は、データからコードを生成したり、その逆を行ったりするために頻繁に使用されます。 たとえば、単一ファイル ジェネレーターは、 *.settings* および *.resx* ファイルから [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] および [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] ソース コードを作成します。 生成されたソース コードは、 *.settings* および *.resx* ファイル内のデータへの厳密に型指定されたアクセスを提供します。 [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] および [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] プロジェクトの種類ではカスタム ツールがサポートされています。 [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] プロジェクトの種類ではサポートされていません。 独自のプロジェクトの種類で、カスタム ツールをサポートすることもできます。

 カスタム ツールは、`IVsSingleFileGenerator` インターフェイスを実装する登録済みのコンポーネントです。

 カスタム ツールは `ProjectItem` インターフェイス オブジェクトに関連付けられており、デザイナーやエディターに似ています。 カスタム ツールは、`ProjectItem` によって表されるファイルを入力として受け取り、ファイル名が `DefaultExtension` メソッドによって提供される新しいファイルを書き込みます。

## <a name="in-this-section"></a>このセクションの内容
- [単一ファイル ジェネレーターの実装](../../extensibility/internals/implementing-single-file-generators.md)

 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator> インターフェイスを使用してカスタム ツールを実装する方法について説明します。

- [単一ファイル ジェネレーターの登録](../../extensibility/internals/registering-single-file-generators.md)

 カスタム ツールのすべてのレジストリ エントリについて説明します。

- [ビジュアル デザイナーに型を公開する](../../extensibility/internals/exposing-types-to-visual-designers.md)

 プロジェクト システムが、ビジュアル デザイナーで一時的なポータブル実行可能 (PE) ファイルを介して生成されたクラスと型にアクセスするためのサポートを提供する方法について説明します。

- [プロジェクト項目のプロパティの保存](../../extensibility/persisting-the-property-of-a-project-item.md)

 ソース ファイルの作成者などのプロジェクト項目のプロパティを、プロジェクト ファイルに保存する方法について説明します。

## <a name="reference"></a>関連項目
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator> 1 つの入力ファイルを、コンパイルしたりプロジェクトに追加したりできる 1 つの出力ファイルに変換する、<xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator> の詳細について説明します。

 <xref:EnvDTE.ProjectItem> プロジェクト内の項目を表す `ProjectItem` インターフェイスについて説明します。

 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator.DefaultExtension%2A> 出力ファイル名に指定されたファイル名拡張子を取得する、`DefaultExtension` メソッドについて詳しく説明します。

## <a name="related-sections"></a>関連項目
- [プロジェクトを拡張する](../../extensibility/extending-projects.md)

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] プロジェクトおよびソリューションを使用してコード ファイルとリソース ファイルを編成する方法、またソース管理を実装する方法について説明します。
