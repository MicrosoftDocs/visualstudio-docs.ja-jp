---
title: コード メトリック - 保守容易性指数の範囲と意味
ms.date: 1/8/2021
description: Visual Studio のコード メトリックの保守容易性指数範囲メトリックについて説明します。
ms.topic: conceptual
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: aa825b439b75606da136635d5816ac3e19ea8392
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99860465"
---
# <a name="code-metrics---maintainability-index-range-and-meaning"></a>コード メトリック - 保守容易性指数の範囲と意味

質問: 保守容易性指数が 0 から 100 までの範囲に再設定されました。 これはどのように、そしてなぜ行われたのでしょうか?

このメトリックは、もともと次のように計算されていました: `Maintainability Index = 171 - 5.2 * ln(Halstead Volume) - 0.23 * (Cyclomatic Complexity) - 16.2 * ln(Lines of Code)`

この数式の使用は、範囲が 171 から無制限の負の値であることを意味していました。  コードが 0 に近づくほど、コードの保守が困難になることは明らかなので、0 のコードと負の値のコードの差は役に立ちませんでした。  負の値の有用性の低下と、このメトリックをできるだけ明確に保ちたいという意向の結果、0 以下のすべての指数を 0 として扱い、171 以下の範囲を 0 から 100 までにリベースすることにしました。 そのため、使用する数式は次のとおりです。

   `Maintainability Index = MAX(0,(171 - 5.2 * ln(Halstead Volume) - 0.23 * (Cyclomatic Complexity) - 16.2 * ln(Lines of Code))*100 / 171)`

これに加えて、しきい値を保守的に設定することにしました。  指数が赤を示している場合に、高い信頼度でコードに問題があると言えることが望まれました。  その結果、次のしきい値が設定されました。

しきい値については、ノイズ レベルを低く保つために、この 0 - 100 の範囲を 80 - 20 に分割することにし、疑わしいコードにのみフラグを設定しました。 次のしきい値が使用されています。

- 0 - 9 = 赤
- 10 - 19 = 黄色
- 20 - 100 = 緑
