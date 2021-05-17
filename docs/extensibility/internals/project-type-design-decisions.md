---
title: プロジェクト タイプのデザインの方針 | Microsoft Docs
description: 新しいプロジェクト タイプを作成して Visual Studio を拡張する前に、項目、プロジェクト ファイルの永続化、コミットメントのしくみについて、デザインの方針を決定します。この記事では、これらの方針について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project types, project file persistence
- project types, commitment mechanics
- project types, items
- project types, design decisions
ms.assetid: f68671fe-fd7a-4e56-a0b5-330b0f1fedb1
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 2f1a90082b0ba9d18336463b26cf72acea39851b
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105064310"
---
# <a name="project-type-design-decisions"></a>プロジェクト タイプのデザインの方針
新しいプロジェクト タイプを作成する前に、プロジェクト タイプに関連したデザインの方針をいくつか決定する必要があります。 プロジェクトに含める項目の種類、プロジェクト ファイルを永続化する方法、使用するコミットメント モデルを決定する必要があります。

## <a name="project-items"></a>プロジェクト アイテム
 プロジェクトでファイルまたは抽象オブジェクトを使用するでしょうか。 ファイルを使用する場合、参照ベースのファイルでしょうか、それともディレクトリベースのファイルでしょうか。 ファイルや抽象オブジェクトはローカルとリモートのどちらに置かれるでしょうか。

 プロジェクト内の項目は、ファイルの場合もあれば、(データベース リポジトリ内のオブジェクト、インターネット経由のデータ接続などの) より抽象的なオブジェクトの場合もあります。 項目がファイルの場合、プロジェクトは参照ベースまたはディレクトリベースのプロジェクトである可能性があります。

 参照ベースのプロジェクトでは、項目は複数のプロジェクトに出現する可能性があります。 ただし、項目が表す実際のファイルは、1 つのディレクトリにしか存在しません。 ディレクトリベースのプロジェクトでは、すべてのプロジェクト項目はディレクトリ構造に存在します。

 ローカル項目は、アプリケーションがインストールされているのと同じコンピューターに格納されます。 リモート項目は、ローカル ネットワーク内の別のサーバー、またはインターネット上の他の場所に格納できます。

## <a name="project-file-persistence"></a>プロジェクト ファイルの永続化
 データが格納されるのは一般的なフラット ファイル システムでしょうか、それとも構造化ストレージでしょうか。 ファイルを開くのに使用されるのは標準のエディターでしょうか、それともプロジェクト固有のエディターでしょうか。

 データを永続化するために、ほとんどのアプリケーションでは、データをファイルに保存して、ユーザーが情報を確認または変更する必要があるときに読み戻します。

 複合ファイルとも呼ばれる構造化ストレージは通常、複数のコンポーネント オブジェクトモデル (COM) オブジェクトで、永続化対象のデータを 1 つのファイルに格納する必要があるときに使用されます。 構造化ストレージを使用すると、複数の異なるソフトウェア コンポーネントが 1 つのディスク ファイルを共有できます。

 プロジェクト内の項目の永続性に関して、いくつかのオプションを考慮する必要があります。 次のオプションのいずれかを実行できます。

- 変更された時点で各ファイルを個別に保存する。

- 1 回の **保存** 操作で多数のトランザクションをキャプチャする。

- ローカルでファイルを保存してからサーバーに発行する。または、プロジェクト項目がリモート オブジェクトへのデータ接続を表している場合は、別の方法を使用して項目を保存する。

  永続化の詳細については、「[プロジェクトの永続化](../../extensibility/internals/project-persistence.md)」および「[プロジェクト項目のオープンと保存](../../extensibility/internals/opening-and-saving-project-items.md)」を参照してください。

## <a name="project-commitment-model"></a>プロジェクト コミットメント モデル
 永続化されたデータ オブジェクトは直接モードで開かれるでしょうか、それともトランザクション モードでしょうか。

 データ オブジェクトが直接モードで開かれると、データに加えられた変更は直ちに反映されるか、ユーザーが手動でファイルを保存したときに反映されます。

 トランザクション モードを使用してデータ オブジェクトが開かれると、変更はメモリ内の一時的な場所に保存され、ユーザーがファイルの保存を手動で選択するまでコミットされません。 その時点で、すべての変更がまとめて行われるか、一切の変更が行われないかのどちらかになります。

## <a name="see-also"></a>関連項目
- [チェックリスト: 新しいプロジェクト タイプの作成](../../extensibility/internals/checklist-creating-new-project-types.md)
- [プロジェクト項目のオープンと保存](../../extensibility/internals/opening-and-saving-project-items.md)
- [プロジェクトの永続化](../../extensibility/internals/project-persistence.md)
- [プロジェクト モデルの要素](../../extensibility/internals/elements-of-a-project-model.md)
- [プロジェクト モデルのコア コンポーネント](../../extensibility/internals/project-model-core-components.md)
- [プロジェクト タイプの作成](../../extensibility/internals/creating-project-types.md)
