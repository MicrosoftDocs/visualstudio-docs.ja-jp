---
title: プロジェクト タイプを作成する状況 |Microsoft Docs
description: ユーザーのために Visual Studio をカスタマイズするために新しいプロジェクト タイプが必要かどうかを判断する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project types, conditions for creating
ms.assetid: 26adc860-ee4a-4f5c-95e1-e41b207dd7e6
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 427c35a03f9d0cb11667ca9eaf88f144d018f620
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105074302"
---
# <a name="when-to-create-project-types"></a>プロジェクト タイプを作成する状況
新しいプロジェクト タイプを作成すると、ユーザー向けに [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] をカスタマイズするための基盤が提供されます。 ただし、すべての [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] カスタマイズに新しいプロジェクト タイプの作成が必要なわけではありません。 次のガイドラインは、自身のシナリオに新しいプロジェクト タイプが必要かどうかを判断するのに役立ちます。

## <a name="create-a-new-project-type"></a>新しいプロジェクト タイプを作成する
 次の 1 つまたは複数の方法で動作するように [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] をカスタマイズする場合は、プロジェクト タイプを作成する必要があります。

- ビルド、配置、構成、ソース管理に参加する。

- デバッグのサポートを提供する。

- **ソリューション エクスプローラー** でプロジェクト項目を表示する。

- **[プロジェクトを開く]** または **[新しいプロジェクト]** ダイアログ ボックスを使用する。

- プロジェクトの入れ子をサポートする。

## <a name="extend-an-existing-project-type"></a>既存のプロジェクト タイプを拡張する
 次の方法で [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] を使用できる新しいプロジェクト タイプを作成して、既存のプロジェクト タイプの動作を変更または拡張することができます。たとえば、[!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] プロジェクトのビルド プロセスを変更します。

- 複数のファイルを 1 つの単位として操作する。

- サブ項目の階層として 1 つのファイルを表示する。

- エディターの周囲にコマンド コンテキストを表示します。

- エディターのサービス コンテキストを表示する。

## <a name="use-an-existing-project-type"></a>既存のプロジェクト タイプを使用する
 新しいプロジェクトの作成が必要ない場合があります。 次の表に、プロジェクト タイプを作成する必要がないタスクを示します。

|タスク|説明|
|----------|-----------------|
|コマンドの処理|VSPackage はコマンドを処理できます。|
|エディターのビルド|カスタム エディターを登録できます。 詳細については、「[Document Windows and Editors](/previous-versions/bb165691(v=vs.100))」を参照してください。|
|ウィンドウの所有|新しいプロジェクト タイプを追加せずに、ツール ウィンドウとドキュメント ウィンドウの両方を作成できます。|
|プロパティ ウィンドウでのプロパティの公開|すべてのオブジェクトがプロパティを公開できます。|

## <a name="create-a-project-subtype"></a>プロジェクトのサブタイプを作成する
 プロジェクトのサブタイプを使用して、新しいプロジェクト タイプを作成することなく、マネージド プロジェクト タイプを拡張することができます。 プロジェクトのサブタイプは、COM 集計を使用して、Microsoft [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] または [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] で記述されたマネージド プロジェクトを拡張します。 COM 集計を使用すると、マネージド プロジェクト システムの実装の大部分を再利用しながら、集計やサポート インターフェイスの使用を通じて特定のシナリオ向けのカスタマイズを行うことができます。 プロジェクトのサブタイプの詳細については、「[プロジェクト サブタイプ](../../extensibility/internals/project-subtypes.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [Document Windows and Editors](/previous-versions/bb165691(v=vs.100))
- [チェックリスト: 新しいプロジェクト タイプの作成](../../extensibility/internals/checklist-creating-new-project-types.md)
- [Visual Studio での階層](../../extensibility/internals/hierarchies-in-visual-studio.md)