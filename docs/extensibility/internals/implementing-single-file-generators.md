---
title: 単一ファイル ジェネレーターの実装 | Microsoft Docs
description: IVsSingleFileGenerator インターフェイスを実装するカスタム ツールを使用して、Visual Studio で Visual Basic および Visual C# プロジェクト システムを拡張する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- custom tools, implementing
- projects [Visual Studio SDK], extensibility
- projects [Visual Studio SDK], managed custom tools
ms.assetid: fe9ef6b6-4690-4c2c-872c-301c980d17fe
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: a46ebce9a554c90e23f9ce5f29680fc3ef86b337
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105085833"
---
# <a name="implementing-single-file-generators"></a>単一ファイル ジェネレーターの実装
カスタム ツール (単一ファイル ジェネレーターと呼ばれることもあります) を使用して、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] で [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] および [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] プロジェクト システムを拡張できます。 カスタム ツールは、<xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator> インターフェイスを実装する COM コンポーネントです。 カスタム ツールでは、このインターフェイスを使用して、1 つの入力ファイルが 1 つの出力ファイルに変換されます。 変換の結果は、ソース コードやその他の有用な出力です。 カスタム ツールによって生成されるコード ファイルの 2 つの例は、ビジュアル デザイナーでの変更に応じて生成されるコードと、Web サービス記述言語 (WSDL) を使用して生成されるファイルです。

 カスタム ツールが読み込まれたとき、または入力ファイルが保存されたときに、プロジェクト システムは <xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator.Generate%2A> メソッドを呼び出し、<xref:Microsoft.VisualStudio.Shell.Interop.IVsGeneratorProgress> コールバック インターフェイスへの参照を渡します。これにより、ツールは進行状況をユーザーに報告できるようになります。

 カスタム ツールによって生成される出力ファイルは、入力ファイルに対する依存関係と共にプロジェクトに追加されます。 カスタム ツールの <xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator.DefaultExtension%2A> の実装から返された文字列に基づいて、出力ファイルの名前がプロジェクト システムによって自動的に決定されます。

 カスタム ツールは、<xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator> インターフェイスを実装している必要があります。 必要に応じて、カスタム ツールで <xref:Microsoft.VisualStudio.OLE.Interop.IObjectWithSite> インターフェイスをサポートすると、入力ファイル以外のソースから情報を取得できます。 いずれの場合も、カスタム ツールを使用するには、システムまたは [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ローカル レジストリにあらかじめ登録する必要があります。 カスタム ツールの登録の詳細については、「[単一ファイル ジェネレーターの登録](../../extensibility/internals/registering-single-file-generators.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [ビジュアル デザイナーへのタイプの公開](../../extensibility/internals/exposing-types-to-visual-designers.md)
