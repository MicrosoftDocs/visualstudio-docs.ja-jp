---
title: コードのオートメーションの提供 | Microsoft Docs
description: 内部データ構造によって決定されるインターフェイスの実装が必要なコード モデルを実装する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- CodeModel object
ms.assetid: 21cb3e63-f25c-404b-bc1d-a32ad0fdd4d5
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 57d5337ae088560bb94a6af39902e90b6af02686
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105060966"
---
# <a name="providing-automation-for-code"></a>コードのオートメーションの提供
コードのオートメーション モデルの作成は必要ありません。 環境 SDK には、それを行うためのサンプルが用意されていません。 コード モデルの詳細については、<xref:EnvDTE.CodeModel> オブジェクトを参照してください。

 コード モデルを実装するには、内部データ構造によって決定されるすべてのインターフェイスを実装する必要があります。 これらのオブジェクトは、`IDispatch` クラスから派生する必要があります。

 拡張するオブジェクト <xref:EnvDTE.CodeModel> と <xref:EnvDTE.FileCodeModel> は <xref:EnvDTE.Project> オブジェクトから使用でき、次のようになります。

- <xref:EnvDTE.Project.CodeModel%2A>

- <xref:EnvDTE.ProjectItem.FileCodeModel%2A>

 `Project` および <xref:EnvDTE.ProjectItem> オブジェクトから返すオブジェクトで `CodeModel` または `FileCodeModel` インターフェイスだけを実装することを選択できます。 このインターフェイスから、プロジェクト システムに適したすべての機能を提供します。

 標準の `CodeModel` および `FileCodeModel` インターフェイスからは使用できない機能 (メソッドやプロパティなど) を追加する場合は、標準インターフェイスから継承される独自のインターフェイスを作成します。 エンド ユーザーにその探し方がわかるように、それをプロジェクト システムで必ず文書化するようにしてください。 標準インターフェイスを返しますが、存在することがわかっていれば、ユーザーは `QueryInterface` メソッドを呼び出すか、またはそのインターフェイスにキャストすることができます。

## <a name="see-also"></a>関連項目
- [オートメーション モデルの概要](../../extensibility/internals/automation-model-overview.md)
