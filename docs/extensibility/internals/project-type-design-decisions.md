---
title: プロジェクトの種類の設計上の決定 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project types, project file persistence
- project types, commitment mechanics
- project types, items
- project types, design decisions
ms.assetid: f68671fe-fd7a-4e56-a0b5-330b0f1fedb1
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 7d6d1df2a3b2188360b0ee60480b4d6580ed8faf
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72725375"
---
# <a name="project-type-design-decisions"></a>プロジェクト タイプのデザインの方針
新しいプロジェクトの種類を作成する前に、プロジェクトの種類に関するいくつかの設計上の決定を行う必要があります。 プロジェクトに含める項目の種類、プロジェクトファイルを永続化する方法、および使用するコミットメントモデルを決定する必要があります。

## <a name="project-items"></a>プロジェクト項目
 プロジェクトでファイルまたは抽象オブジェクトを使用しますか? ファイルを使用する場合、これらは参照ベースまたはディレクトリベースのファイルになりますか。 ファイルまたは抽象オブジェクトはローカルとリモートのどちらになりますか。

 プロジェクト内の項目はファイルにすることも、データベースリポジトリ内のオブジェクトやインターネット経由のデータ接続など、より抽象的なオブジェクトにすることもできます。 項目がファイルの場合、プロジェクトは参照ベースまたはディレクトリベースのプロジェクトにすることができます。

 参照ベースのプロジェクトでは、複数のプロジェクトに項目を表示できます。 ただし、項目が表す実際のファイルは、1つのディレクトリにのみ存在します。 ディレクトリベースのプロジェクトでは、すべてのプロジェクト項目がディレクトリ構造に存在します。

 ローカル項目は、アプリケーションがインストールされているのと同じコンピューターに格納されます。 リモート項目は、ローカルネットワーク内の別のサーバー、またはインターネット上の他の場所に格納できます。

## <a name="project-file-persistence"></a>プロジェクトファイルの永続化
 データは共通のフラットファイルシステムまたは構造化ストレージに格納されますか。 標準エディターまたはプロジェクト固有のエディターを使用してファイルを開きますか?

 データを永続化するために、ほとんどのアプリケーションはデータをファイルに保存し、ユーザーが情報を確認または変更する必要があるときにそのデータを読み戻します。

 構造化ストレージ (複合ファイルとも呼ばれます) は、通常、複数のコンポーネントオブジェクトモデル (COM) オブジェクトが、永続化されたデータを1つのファイルに格納する必要がある場合に使用します。 構造化ストレージでは、複数の異なるソフトウェアコンポーネントが1つのディスクファイルを共有できます。

 プロジェクト内の項目の永続性に関して考慮する必要があるオプションがいくつかあります。 次のいずれかのオプションを実行できます。

- 各ファイルが変更されたときに個別に保存します。

- 複数のトランザクションを1回の**保存**操作でキャプチャします。

- ファイルをローカルに保存した後、サーバーに発行するか、アイテムがリモートオブジェクトへのデータ接続を表している場合は、別の方法を使用してプロジェクトアイテムを保存します。

  永続化の詳細については、「[プロジェクトの永続](../../extensibility/internals/project-persistence.md)化」と「[プロジェクト項目を開いて保存](../../extensibility/internals/opening-and-saving-project-items.md)する」を参照してください。

## <a name="project-commitment-model"></a>プロジェクトコミットメントモデル
 永続化されたデータオブジェクトは、直接モードまたはトランザクションモードで開くことができますか。

 データオブジェクトが直接モードで開かれると、データに加えられた変更が直ちに、またはユーザーが手動でファイルを保存したときに反映されます。

 トランザクションモードでデータオブジェクトを開くと、変更はメモリ内の一時的な場所に保存され、ユーザーが手動でファイルの保存を選択するまでコミットされません。 その時点で、すべての変更が同時に行われるか、変更は行われません。

## <a name="see-also"></a>関連項目
- [チェック リスト: 新しいプロジェクト タイプの作成](../../extensibility/internals/checklist-creating-new-project-types.md)
- [プロジェクト項目のオープンと保存](../../extensibility/internals/opening-and-saving-project-items.md)
- [プロジェクトの永続化](../../extensibility/internals/project-persistence.md)
- [プロジェクト モデルの要素](../../extensibility/internals/elements-of-a-project-model.md)
- [プロジェクト モデルのコア コンポーネント](../../extensibility/internals/project-model-core-components.md)
- [プロジェクト タイプの作成](../../extensibility/internals/creating-project-types.md)