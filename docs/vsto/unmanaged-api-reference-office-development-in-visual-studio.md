---
title: アンマネージド API リファレンス (Visual Studio での Office 開発)
description: アンマネージド API リファレンスは、マネージド VSTO アドインの読み込みに使用されます。また、このインターフェイスを実装することで、独自の VSTO アドイン ローダー コンポーネントを作成できます。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 08/14/2019
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office development in Visual Studio, reference
- Office development in Visual Studio, unmanaged API reference
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: cac9e2d01b47e0088543aeabcaeff30853314157
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99908547"
---
# <a name="unmanaged-api-reference-office-development-in-visual-studio"></a>アンマネージド API リファレンス (Visual Studio での Office 開発)

2007 Microsoft Office システム以降の Office アプリケーションでは、[IManagedAddin インターフェイス](../vsto/imanagedaddin-interface.md)を使用して、[!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] に組み込まれている VSTO アドイン ローダー コンポーネントに呼び出します。 このコンポーネントは、マネージド VSTO アドインの読み込みに使用されます。また、このインターフェイスを実装することで、独自の VSTO アドイン ローダー コンポーネントを作成できます。

[!include[Add-ins note](includes/addinsnote.md)]

## <a name="in-this-section"></a>このセクションの内容

[IManagedAddin インターフェイス](../vsto/imanagedaddin-interface.md)

Office アプリケーションでマネージド VSTO アドインの読み込みやアンロードを行うために実装できる COM インターフェイスです。
