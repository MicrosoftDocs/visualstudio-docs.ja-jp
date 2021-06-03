---
title: DSL 定義への拡張機能の追加
description: DSL 定義の拡張機能を使用して、ドメイン固有言語 (DSL) に対する拡張機能のパッケージを作成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
author: JoshuaPartlow
ms.author: joshuapa
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 1208c152534206a0ed2894fc0e41d844e0b77d47
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99861960"
---
# <a name="add-extensions-to-dsl-definitions"></a>DSL 定義に拡張機能を追加する

DSL 定義の拡張機能を使用して、ドメイン固有言語 (DSL) に対する拡張機能のパッケージを作成することができます。 DSL 拡張機能は、Visual Studio Integration Extension (VSIX) に含まれており、DSL と同じ方法でユーザーのコンピューターにインストールできます。 その他の機能は、実行時に動的に有効にしたり無効にしたりすることができます。 DSL は拡張機能用に明示的に設計されている必要はなく、拡張 DSL を変更することなく、後で、またはサード パーティが拡張機能を設計できます。

DSL 拡張機能には、次の機能を含めることができます。

- モデルおよびプレゼンテーション要素のプロパティ

- シェイプとコネクタのデコレーター

- クラス、リレーションシップ、シェイプ、コネクタ

- 検証制約

- ツールボックスの項目とタブ

拡張 DSL のユーザーは、追加機能のインスタンスを含むモデルを作成して保存できます。 モデルは、適切な拡張機能をインストールした他のユーザーが読み取ることができます。 拡張機能をインストールしていないユーザーは、追加機能を使用できませんが、追加機能を失うことなく、モデルを更新して保存することができます。

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]

## <a name="see-also"></a>関連項目

- [関連するブログ記事](https://devblogs.microsoft.com/devops/the-visual-studio-modeling-sdk-is-now-available-with-visual-studio-2017/)
