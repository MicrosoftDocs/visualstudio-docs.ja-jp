﻿---
title: Vsgdbg::vsgdbg (コンス トラクター) |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 670651e6-5e79-4845-b0c2-671beb7055a8
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: db51226c4d980359fd36ee5196e48d7fa4577a37
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62895144"
---
# <a name="vsgdbgvsgdbg-constructor"></a>VsgDbg::VsgDbg (コンストラクター)
指定されたブール値パラメーターに基づいて、既定でグラフィックス情報をアクティブにキャプチャして記録するようにグラフィックス診断のアプリ内コンポーネントを準備をするか、または準備しないで、`VsgDbg` クラスのインスタンスを構築します。

## <a name="syntax"></a>構文

```C++
VsgDbg(
  bDefaultInit
);
```

#### <a name="parameters"></a>パラメーター
 `bDefaultInit` グラフィックス情報をアクティブにキャプチャして記録するように、グラフィックス診断のアプリ内コンポーネントを準備することを指定する場合は `true`、この時点ではグラフィックス情報をアクティブにキャプチャして記録するようにアプリケーションを準備しないことを指定する場合は `false`。

## <a name="remarks"></a>Remarks
 コンス トラクターが呼び出された場合`bDefaultInit`に設定`true`、グラフィックス ログ ファイルのファイル名は、方法によって決まります`DONT_SAVE_VSGLOG_TO_TEMP`と`VSG_DEFAULT_RUN_FILENAME`する前にプリプロセッサ シンボルが定義されている`vsgcapture.h`アプリに含まれます。

 `bDefaultInit` が `false` に設定された状態でコンストラクターが呼び出された場合、後で `Init` 関数を呼び出して、グラフィックス情報をアクティブにキャプチャして記録するようにグラフィックス診断のアプリ内コンポーネントを準備できます。

## <a name="see-also"></a>関連項目
- [VsgDbg::~VsgDbg (デストラクター)](vsgdbg-tilde-vsgdbg-destructor.md)
- [Init](init.md)
- [DONT_SAVE_VSGLOG_TO_TEMP](dont-save-vsglog-to-temp.md)
- [VSG_DEFAULT_RUN_FILENAME](vsg-default-run-filename.md)
