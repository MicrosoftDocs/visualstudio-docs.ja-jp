---
title: コード分析のアプリケーション エラー
ms.date: 11/04/2016
description: Visual Studio でマネージド コード分析ツールによって生成されるエラー メッセージについて説明します。 エラー コードとそれに対応する説明を示します。
ms.custom: SEO-VS-2020
ms.topic: reference
helpviewer_keywords:
- errors [Visual Studio ALM], code analysis
- code analysis, errors
- managed code, code analysis errors
- code analysis, policy errors
ms.assetid: d8fd9475-ac9b-4085-b5a3-b0c807922cac
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 0f5c217e8d043d0363b66a63c84c78829f640065
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99860582"
---
# <a name="code-analysis-application-errors"></a>コード分析のアプリケーション エラー

このセクションは、マネージド コード分析ツールによって生成されるエラー メッセージの参考資料です。

## <a name="in-this-section"></a>このセクションの内容

|コード|説明|
|-|-|
|[CA0001](ca0001.md)|マネージド コード分析ツール内で、予期されたエラー条件を示していない例外が発生しました。|
|[CA0051](ca0051.md)|規則が選択されていません。|
|[CA0052](ca0052.md)|分析するターゲットが選択されていません。|
|[CA0053](ca0053.md)|規則のアセンブリを読み込むことができませんでした。|
|[CA0054](ca0054.md)|カスタム規則アセンブリに含まれる XML リソースが無効です。|
|[CA0055](ca0055.md)|ファイル \<path> を読み込むことができませんでした。|
|[CA0056](ca0056.md)|プロジェクト ファイルに含まれている分析ツールのバージョンが正しくありません。|
|[CA0057](ca0057.md)|現在のターゲットと規則のセットに違反をマップできません。|
|[CA0058](ca0058.md)|参照先アセンブリを読み込むことができません。|
|[CA0059](ca0059.md)|コマンド ライン スイッチのエラー。|
|[CA0060](ca0060.md)|参照先アセンブリを間接的に読み込むことができません。|
|[CA0061](ca0061.md)|規則の '*RuleId*' が見つかりませんでした。|
|[CA0062](ca0062.md)|規則セット '*RuleSetName*' で参照されている規則 '*RuleId*' が見つかりませんでした。|
|[CA0063](ca0063.md)|ルール セット ファイル、またはその依存するルール セット ファイルのいずれかを読み込むことができませんでした。|
|[CA0064](ca0064.md)|指定されたルール セットに FxCop 規則が含まれていなかったため、分析は実行されませんでした。|
|[CA0065](ca0065.md)|サポートされていないメタデータ構造です。型 '*TypeName*' に、同じ名前 '*PropertyFieldName*' を持つプロパティとフィールドの両方が含まれています。|
|[CA0066](ca0066.md)|**/targetframeworkversion** に指定された値 '*VersionID*' は、認識されているバージョンではありません。|
|[CA0067](ca0067.md)|ディレクトリが見つかりません。|
|[CA0068](ca0068.md)|ターゲット アセンブリ '*AssemblyName*' のデバッグ情報が見つかりませんでした。|
|[CA0069](ca0069.md)|代替プラットフォームを使用しています。 *FrameworkVersion1* が見つかりませんでした。 代わりに *FrameworkVersion2* を使用しています。 最良の分析結果を得るために、正しいフレームワーク バージョンを必ずインストールしてください。|
|[CA0070](ca0070.md)|セキュリティのアクセス許可が原因で、アセンブリと型のどちらも読み込むことができません。|
|[CA0501](ca0501.md)|出力レポートを読み取ることができません。|
|[CA0502](ca0502.md)|サポートされていない言語です。|
|[CA0503](ca0503.md)|非推奨のプロパティです。 後継プロパティを使用してください。|
|[CA0504](ca0504.md)|規則ディレクトリは存在しないため、無視されました。|
|[CA0505](ca0505.md)|非推奨のプロパティです。 後継プロパティを使用してください。|
|[FxCopCmd エラー](fxcopcmd-errors.md)|マネージド コード分析のエラー。|

## <a name="related-sections"></a>関連項目

- [Code Analysis Policy Errors](../code-quality/code-analysis-policy-errors.md)
- [マネージド コードの品質の分析](../code-quality/code-analysis-for-managed-code-overview.md)
