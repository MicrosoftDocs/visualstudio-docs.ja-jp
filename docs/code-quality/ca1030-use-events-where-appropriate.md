---
title: CA1030:適切な場所にイベントを使用します
ms.date: 03/11/2019
ms.topic: reference
f1_keywords:
- UseEventsWhereAppropriate
- CA1030
helpviewer_keywords:
- CA1030
- UseEventsWhereAppropriate
ms.assetid: ea051367-deeb-40f9-9b65-eb818f1e133a
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 28d71fbfc10532f7c9420ea7e847ef4c29b88854
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/24/2019
ms.locfileid: "71236076"
---
# <a name="ca1030-use-events-where-appropriate"></a>CA1030:適切な場所にイベントを使用します

|||
|-|-|
|TypeName|UseEventsWhereAppropriate|
|CheckId|CA1030|
|カテゴリ|Microsoft.Design|
|互換性に影響する変更点|なし|

## <a name="cause"></a>原因

メソッド名は、次のいずれかで始まります。

- アドオン
- RemoveOn
- 起動
- 発生

既定では、この規則は外部から参照できるメソッドのみを参照しますが、これは[構成可能](#configurability)です。

## <a name="rule-description"></a>規則の説明

この規則では、通常はイベントに使用される名前を持つメソッドを検出します。 イベントは、オブザーバーまたはパブリッシュ/サブスクライブデザインパターンに従います。これらは、あるオブジェクトの状態の変更を他のオブジェクトに伝達する必要があるときに使用されます。 明確に定義された状態変更に応答してメソッドが呼び出された場合、メソッドはイベントハンドラーによって呼び出される必要があります。 メソッドを呼び出すオブジェクトは、メソッドを直接呼び出すのではなく、イベントを発生させる必要があります。

イベントの一般的な例としては、ボタンのクリックなどのユーザー操作によってコードのセグメントが実行されるユーザーインターフェイスアプリケーションがあります。 .NET イベントモデルは、ユーザーインターフェイスに限定されていません。 状態の変更を1つ以上のオブジェクトに伝達する必要があるすべての場所で使用する必要があります。

## <a name="how-to-fix-violations"></a>違反の修正方法

オブジェクトの状態が変化したときにメソッドが呼び出された場合は、.NET イベントモデルを使用するようにデザインを変更することを検討してください。

## <a name="when-to-suppress-warnings"></a>警告を非表示にする場合

メソッドが .NET イベントモデルで動作しない場合は、この規則からの警告を非表示にします。

## <a name="configurability"></a>かつ

この規則を[FxCop アナライザー](install-fxcop-analyzers.md) (レガシ分析ではなく) から実行している場合は、ユーザー補助に基づいて、この規則を実行するコードベースの部分を構成できます。 たとえば、パブリックでない API サーフェイスに対してのみルールを実行するように指定するには、プロジェクトの editorconfig ファイルに次のキーと値のペアを追加します。

```ini
dotnet_code_quality.ca1030.api_surface = private, internal
```

このオプションは、この規則、すべての規則、またはこのカテゴリのすべての規則 (デザイン) に対してのみ構成できます。 詳細については、「 [FxCop アナライザーの構成](configure-fxcop-analyzers.md)」を参照してください。
