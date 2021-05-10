---
title: FxCopCmd エラー
ms.date: 10/19/2016
description: FxCopCmd コマンドが返すエラー コードについて説明します。 各コードが表すエラーの種類を示し、致命的なエラーを認識する方法を紹介します。
ms.custom: SEO-VS-2020
ms.topic: reference
helpviewer_keywords:
- FxCopCmd errors
ms.assetid: bb614ed0-1b7c-4b56-99ae-da50ef6cfef9
ms.author: mikejo
author: mikejo5000
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: efeabd85bbf2753dd3f5e37a43e0918b7f95d7fe
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99860218"
---
# <a name="fxcopcmd-tool-errors"></a>FxCopCmd ツールのエラー

FxCopCmd では、すべてのエラーが致命的であるとは見なされません。 部分的な分析を実行するために十分な情報が FxCopCmd に含まれる場合は、分析が実行され、発生したエラーが報告されます。 エラーコード (32 ビット整数) には、エラーに対応する、ビットごとの数値の組み合わせが含まれています。

次の表では、FxCopCmd によって返されるエラーコードについて説明しています。

|エラー|数値|
|-----------|-------------------|
|エラーなし|0x0|
|分析エラー|0x1|
|規則の例外|0x2|
|プロジェクトの読み込みエラー|0x4|
|アセンブリの読み込みエラー|0x8|
|規則ライブラリの読み込みエラー|0x10|
|インポート レポートの読み込みエラー|0x20|
|出力エラー|0x40|
|コマンド ライン スイッチのエラー|0x80|
|初期化エラー|0x100|
|アセンブリ参照エラー|0x200|
|BuildBreakingMessage|0x400|
|不明なエラー|0x1000000|

致命的なエラーに対して **分析エラー** が返されています。 これは、分析を完了できなかったことを示します。 該当する場合は、致命的なエラーの根底にある原因もエラー コードに含まれます。 次の状況では、致命的なエラーが発生します。

- 入力が不十分なため、分析を実行できませんでした。

- 分析によって、FxCopCmd で処理されない例外がスローされました。

- 指定されたプロジェクト ファイルが見つからないか、破損しています。

- 出力オプションが指定されていないか、ファイルに書き込めませんでした。

> [!NOTE]
> FxCopCmd のリターン コード "**アセンブリ参照エラー**" 0x200 自体は、エラーではなく、警告です。 このリターン コードは、間接参照が不足しているが、FxCopCmd でそれらを処理できたことを示します。 警告は、分析結果の一部が損なわれた可能性があることを意味します。 他のリターンコードとの組み合わせにより、"**アセンブリ参照エラー**" はエラーとして扱われます。

## <a name="see-also"></a>関連項目

- [コード分析のアプリケーション エラー](../code-quality/code-analysis-application-errors.md)
