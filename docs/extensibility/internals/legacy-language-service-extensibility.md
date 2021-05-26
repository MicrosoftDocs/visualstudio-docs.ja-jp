---
title: 従来の言語サービスの機能拡張 | Microsoft Docs
description: Visual Studio の従来の言語サービスの構造、実装、および機能拡張について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- language services
- Visual Studio, language services
ms.assetid: 2700cd4d-5f68-43fc-b62f-dc80c3f3aa85
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: f22d6997d932884e5aeb8d794b7884b40a8d5dab
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105074497"
---
# <a name="legacy-language-service-extensibility"></a>従来の言語サービスの機能拡張
言語サービスは、IDE でソース コードを編集するための言語固有のサポートを提供します。

 従来の言語サービスは VSPackage の一部として実装されていますが、言語サービス機能の新しい実装方法では MEF 拡張機能が使用されます。 言語サービスの新しい実装方法の詳細については、「[エディターと言語サービスの拡張機能](../../extensibility/editor-and-language-service-extensions.md)」を参照してください。

 このセクションでは、従来の言語サービスの構造と実装について説明します。

## <a name="in-this-section"></a>このセクションの内容
- [従来の言語サービスの移行](../../extensibility/internals/migrating-a-legacy-language-service.md)

 言語サービスを Visual Studio 2008 から最新バージョンに更新する方法について説明します。

- [従来の言語サービスの基本情報](../../extensibility/internals/legacy-language-service-essentials.md)

 言語サービスを開発してプログラミング言語を Visual Studio に統合する方法についての重要な情報を提供します。

- [従来の言語サービスの開発](../../extensibility/internals/developing-a-legacy-language-service.md)

 言語サービスの作成に役立つトピックへのリンクを示します。

- [従来の言語サービスでの構文の色分け表示](../../extensibility/internals/syntax-coloring-in-a-legacy-language-service.md)

 言語サービスでの構文の強調表示のサポートに関する情報を提供します。

- [従来の言語サービスの実装](../../extensibility/internals/implementing-a-legacy-language-service1.md)

 マネージド パッケージ フレームワーク (MPF) を使用して、完全な機能を備えた言語サービスをマネージド コードで実装する方法について説明します。

- [シンボル参照ツールのサポート](../../extensibility/internals/supporting-symbol-browsing-tools.md)

 IDE でシンボルのツリー ビューを参照できるようにするライブラリとツールについて説明します。

## <a name="related-sections"></a>関連項目
- [エディターと言語サービスの拡張機能](../../extensibility/editor-and-language-service-extensions.md)

 Visual Studio エディターの概要について説明します。

- [デバッグのための言語サービスのサポート](../../extensibility/internals/language-service-support-for-debugging.md)

 Visual Studio Debugging SDK に関する情報とリンクを示します。これには、プログラムのデバッグに使用されるデバッガー コンポーネントの作成とカスタマイズに必要な情報が含まれています。
