---
title: 従来の言語サービスの実装 1 | Microsoft Docs
description: マネージド パッケージ フレームワーク (MPF) を使用して、拡張言語サービス機能をサポートする従来の言語サービスを実装する方法について説明します。 パート 1/2。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- language services, managed
ms.assetid: df638f24-166d-4b80-be82-c9c39ca7a556
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 99e3f11a9ea60595b2372921702282c2bb4d8dcd
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105085911"
---
# <a name="implementing-a-legacy-language-service-1"></a>従来の言語サービスの実装 1
マネージド パッケージ フレームワーク (MPF) のクラスを使用すると、構文の強調表示、かっこの一致、IntelliSense の入力候補などのさまざまな機能をサポートする従来の言語サービスを実装できます。

 従来の言語サービスは VSPackage の一部として実装されていますが、言語サービス機能の新しい実装方法では MEF 拡張機能が使用されます。 言語サービスの新しい実装方法の詳細については、「[エディターと言語サービスの拡張機能](../../extensibility/editor-and-language-service-extensions.md)」を参照してください。

> [!NOTE]
> 新しいエディターの API をできるだけ早く使い始めることをお勧めします。 これにより、言語サービスのパフォーマンスが向上し、新しいエディター機能を利用できるようになります。

## <a name="in-this-section"></a>このセクションの内容
- [従来の言語サービスの概要](../../extensibility/internals/legacy-language-service-overview.md)

 MPF でサポートされている言語サービス機能の概要について説明します。

- [従来の言語サービスの実装](../../extensibility/internals/implementing-a-legacy-language-service2.md)

 MPF を使用して言語サービスを実装するために必要な事項について説明します。

- [従来の言語サービスの登録](../../extensibility/internals/registering-a-legacy-language-service1.md)

 MPF ベースの言語サービスを [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] に登録するために必要な手順について説明します。

- [従来の言語サービスのパーサーとスキャナー](../../extensibility/internals/legacy-language-service-parser-and-scanner.md)

 MPF を使用して言語サービスのすべての機能を実装するために必要な 2 つのパーサーについて説明します。

- [チュートリアル: 従来の言語サービスの作成](../../extensibility/internals/walkthrough-creating-a-legacy-language-service.md)

 VSPackage で MPF 言語サービスを実装するために必要な基本的な手順について説明します。

- [チュートリアル: インストールされているコード スニペットの一覧の取得 (従来の実装)](../../extensibility/internals/walkthrough-getting-a-list-of-installed-code-snippets-legacy-implementation.md)

 インストールされているコード スニペットの一覧を取得する方法を示します。

- [従来の言語サービスの機能](../../extensibility/internals/legacy-language-service-features1.md)

 MPF を使用して言語サービスのすべての機能を実装するために必要な作業について詳しく説明したトピックへのリンクを示します。
