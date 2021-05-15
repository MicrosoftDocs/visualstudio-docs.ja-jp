---
title: 64 ビット アプリケーションの配置のための必要条件 | Microsoft Docs
description: 64 ビット プラットフォームでアプリケーションを ClickOnce 配置するための前提条件として使用できる再頒布可能パッケージについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- deploying applications [Visual Studio], 64-bit
- 64-bit [Visual Studio]
- 64-bit programming [Visual Studio]
- 64-bit applications [Visual Studio]
ms.assetid: 87399e20-5510-41e4-b5b7-4a87c5773f21
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: abc44c679e65cc49f6a491e9435fdaeffed5e9c8
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99893946"
---
# <a name="deploy-prerequisites-for-64-bit-applications"></a>64 ビット アプリケーションの配置のための必要条件
ClickOnce の配置では、 64 ビット プラットフォームのアプリケーションのインストールをサポートします。 対象プラットフォームは、32 ビット プラットフォームの場合は **x86**、AMD64 命令セットと EM64T 命令セットをサポートするコンピューターの場合は **x64**、64 ビットの Itanium プロセッサの場合は **Itanium** です。

## <a name="prerequisites"></a>必須コンポーネント
 64 ビット アプリケーションのインストール時の必須コンポーネントとして使用できる再頒布可能パッケージを次の表に示します。

 64 ビット コンポーネントを含まない必須コンポーネントを選択した場合、選択したパッケージは 64 ビット プラットフォームで使用できないことを示す警告が表示される可能性があります。

| 再頒布可能パッケージ | x64 サポート | IA64 サポート |
| - |-------------|--------------|
| [!INCLUDE[vsto_runtime](../deployment/includes/vsto_runtime_md.md)] | はい | いいえ |
| Visual C++ 2010 ランタイム ライブラリ (IA64) | いいえ | はい |
| Visual C++ 2010 ランタイム ライブラリ (x64) | はい | いいえ |
| Microsoft .NET Framework 4 (x86 および x64) | はい | |
| Microsoft .NET Framework 4 Client Profile (x86 および x64) | はい | |

## <a name="see-also"></a>関連項目
- [アプリケーション、サービス、およびコンポーネントの配置](../deployment/deploying-applications-services-and-components.md)
- [方法: ClickOnce アプリケーションと共に必須コンポーネントをインストールする](../deployment/how-to-install-prerequisites-with-a-clickonce-application.md)
- [64 ビット アプリケーション](/dotnet/framework/64-bit-apps)