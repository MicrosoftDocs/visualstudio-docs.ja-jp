---
title: クラス デザイナーの Visual C++ 列挙体
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Class Designer [Visual Studio], enumerations
ms.assetid: 11e90ba1-18cd-44f8-9e26-e3746a7a19d1
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- cplusplus
ms.openlocfilehash: f31f153183d0cdd809bd9dde9187ade32b20ddd2
ms.sourcegitcommit: 21d667104199c2493accec20c2388cf674b195c3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2019
ms.locfileid: "55939854"
---
# <a name="visual-c-enumerations-in-class-designer"></a>クラス デザイナーの Visual C++ 列挙体

**クラス デザイナー**では、C++ の `enum`、およびスコープを持つ `enum class` 型はサポートされていません。 例を次に示します。

```cpp
enum CardSuit {
   Diamonds = 1,
   Hearts = 2,
   Clubs = 3,
   Spades = 4
};

// or...
enum class CardSuit {
   Diamonds = 1,
   Hearts = 2,
   Clubs = 3,
   Spades = 4
};
```

クラス ダイアグラムにおける C++ 列挙体の図形の形状と動作は構造体の図形に似ていますが、ラベルが **[Enum]** または **[Enum class]** である点と、青ではなくピンクである点、および左と上の余白に色つきの枠がある点が異なります。 列挙体の図形も構造体の図形も、角が直角になっています。

`enum` 型の使用法の詳細については、「[列挙型](/cpp/cpp/enumerations-cpp)」を参照してください。

## <a name="see-also"></a>関連項目

- [Visual C++ コードの使用](working-with-visual-cpp-code.md)
- [列挙型](/cpp/cpp/enumerations-cpp)