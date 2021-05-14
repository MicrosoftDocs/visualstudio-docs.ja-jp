---
title: IntelliSenseHostFlags | Microsoft Docs
description: IntelliSenseHostFlags 列挙型により、IntelliSense ホスト フラグを指定します。 この記事では、列挙値について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- IntellisenseHostFlags
helpviewer_keywords:
- IntelliSense, IntellisenseHostFlags enumeration
- IntellisenseHostFlags enumeration
ms.assetid: 0930640b-eb84-48ef-a8f7-d4268f55c99c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 83a3911670a10710ad6ae5cd6496fb76af6c27bb
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105079138"
---
# <a name="intellisensehostflags"></a>IntelliSenseHostFlags
IntelliSense ホスト フラグを指定します。

## <a name="syntax"></a>構文

```cpp
enum IntellisenseHostFlags
{
    IHF_READONLYCONTEXT      = 0x00000001
    IHF_NOSEPARATESUBJECT    = 0x00000002
    IHF_SINGLELINESUBJECT    = 0x00000004
    IHF_FORCECOMMITTOCONTEXT = 0x00000008
    IHF_OVERTYPE             = 0x00000010
};
```

### <a name="parameters"></a>パラメーター

|メンバー|説明|
|-------------|-----------------|
|`IHF_READONLYCONTEXT`|コンテキスト バッファーは読み取り専用です。|
|`IHF_NOSEPARATESUBJECT`|件名のテキストはありません。 コンテキスト バッファーには IntelliSense ターゲットが含まれています (`!IHF_READONLYCONTEXT` を意味します)。|
|`IHF_SINGLELINESUBJECT`|件名のテキストは複数行に対応していません。|
|`IHF_FORCECOMMITTOCONTEXT`|`CanCommitIntoReadOnlyBuffer` と同じ。|
|`IHF_OVERTYPE`|(件名またはコンテキストでの) 編集は、上書きモードで実行する必要があります。|

## <a name="requirements"></a>必要条件
 SingleFileeditor.idl

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.TextManager.Interop>
