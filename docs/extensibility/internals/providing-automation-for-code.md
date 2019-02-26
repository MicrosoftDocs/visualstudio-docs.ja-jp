---
title: オートメーション コードの提供 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- CodeModel object
ms.assetid: 21cb3e63-f25c-404b-bc1d-a32ad0fdd4d5
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: b3a7f1bc0f3394f0b7c0d882657d926ce11259a0
ms.sourcegitcommit: d0425b6b7d4b99e17ca6ac0671282bc718f80910
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/21/2019
ms.locfileid: "56596283"
---
# <a name="providing-automation-for-code"></a>コードのオートメーションの提供
コードのオートメーション モデルを作成する必要はありません。 環境の SDK では、そのため、サンプルは提供されません。 コード モデルを把握するには、次を参照してください。、<xref:EnvDTE.CodeModel>オブジェクト。

 コード モデルを実装するには、内部データ構造によって決定されるインターフェイスを実装する必要があります。 オブジェクトから派生する必要があります、`IDispatch`クラス。

 オブジェクトを拡張すると、<xref:EnvDTE.CodeModel>と<xref:EnvDTE.FileCodeModel>から利用できる、<xref:EnvDTE.Project>オブジェクトし、次のようになります。

- <xref:EnvDTE.Project.CodeModel%2A>

- <xref:EnvDTE.ProjectItem.FileCodeModel%2A>

 実装することができます、`CodeModel`または`FileCodeModel`から返すオブジェクトのインターフェイス、`Project`と<xref:EnvDTE.ProjectItem>オブジェクト。 このプロジェクト システムの適切なインターフェイスからの機能を提供します。

 メソッドやプロパティなどの機能を追加する場合をからは入手できず、標準`CodeModel`と`FileCodeModel`インターフェイスは、standard から継承するインターフェイスを作成します。 エンドユーザーが探しに知っていただけるように、プロジェクト システムでドキュメントを必ず。 標準のインターフェイスを返しますが、ユーザーが呼び出すことができます、`QueryInterface`メソッドまたは存在することがわかっている場合、インターフェイスにキャストします。

## <a name="see-also"></a>関連項目
- [オートメーション モデルの概要](../../extensibility/internals/automation-model-overview.md)