---
title: 従来の言語サービスの自動書式 | Microsoft Docs
description: 既知のコード コンストラクターの入力を開始するとコードのスニペットが自動的に挿入される、従来の言語サービスの自動書式について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- language services, automatic formatting
ms.assetid: c210fc94-77bd-4694-b312-045087d8a549
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: a08a56a6820917b3a954c162b1875430875c7585
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105086275"
---
# <a name="automatic-formatting-in-a-legacy-language-service"></a>従来の言語サービスの自動書式
自動書式を使用すると、ユーザーが既知のコード コンストラクターの入力を開始したときに、言語サービスによってコードのスニペットが自動的に挿入されます。

## <a name="automatic-formatting-behavior"></a>自動書式の動作
 たとえば、*if* と入力すると、言語サービスによって一致する中かっこが自動的に挿入されます。または、ENTER キーを押すと、前の行で新しいスコープが開かれたかどうかに応じて、新しい行の挿入ポイントが適切なインデント レベルになります。

 言語サービスの残りの部分に使用されるコマンド フィルターは、自動書式にも使用できます。 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.HighlightMatchingBrace%2A> を呼び出して、対応する中かっこを強調表示することもできます。

## <a name="see-also"></a>関連項目
- [従来の言語サービスを開発する](../../extensibility/internals/developing-a-legacy-language-service.md)
