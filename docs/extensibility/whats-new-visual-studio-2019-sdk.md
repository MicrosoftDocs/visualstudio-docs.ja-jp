---
title: Visual Studio 2019 SDK の新機能 | Microsoft Docs
description: Visual Studio SDK には、Visual Studio 2019 の新機能と更新された機能があります。これには、エディターの登録の機能強化が含まれています。
ms.custom: SEO-VS-2020
ms.date: 03/29/2019
ms.topic: conceptual
ms.assetid: 4a07607b-0c87-4866-acd8-6d68358d6a47
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 2d8e08136eb142e5e72c08e23860bf94f01dc87c
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105061902"
---
# <a name="whats-new-in-the-visual-studio-2019-sdk"></a>Visual Studio 2019 SDK の新機能

Visual Studio SDK には、Visual Studio 2019 の次の新機能と更新された機能があります。

## <a name="synchronously-autoloaded-extensions-warning"></a>同期的に自動読み込みされる拡張機能の警告

インストールされている拡張機能のいずれかが起動時に同期的に自動読み込みされた場合、ユーザーに警告が表示されるようになりました。 警告の詳細については、「[同期的に自動読み込みされた拡張機能](synchronously-autoloaded-extensions.md)」を参照してください。

## <a name="single-unified-visual-studio-sdk"></a>単一の統合された Visual Studio SDK

単一の NuGet パッケージ [Microsoft.VisualStudio.SDK](https://www.nuget.org/packages/microsoft.visualstudio.sdk) を使用して、すべての Visual Studio SDK 資産を取得できるようになりました。

## <a name="editor-registration-enhancements"></a>エディターの登録の機能強化

Visual Studio では、その登場以来、特定の拡張子 (.xaml や .rc など) に対するエディターのアフィニティ、または任意の拡張子 (.*) に適していることを宣言できるカスタム エディターの登録がサポートされています。 Visual Studio 2019 バージョン 16.1 以降では、エディターの登録のサポートが拡張されています。

### <a name="filenames"></a>ファイル名

エディターでは、特定のファイル拡張子のサポートを登録するだけでなく (またはその代わりに)、エディターのパッケージに新しい `ProvideEditorFilename` 属性を適用して、特定のファイル名をサポートすることを登録できます。

たとえば、すべての .json ファイルをサポートするエディターでは、次の `ProvideEditorExtension` 属性がそのパッケージに適用されます。

```cs
[ProvideEditorExtension(typeof(MyEditor), ".json", MyEditor.Priority)]
```

16.1 以降では、いくつかのよく知られた .json ファイルのみが MyEditor でサポートされている場合、代わりに次の `ProvideEditorFilename` 属性をそのパッケージに適用できます。

```cs
[ProvideEditorFilename(typeof(MyEditor), "particular.json", MyEditor.Priority)]
[ProvideEditorFilename(typeof(MyEditor), "special.json",    MyEditor.Priority)]
```

### <a name="uicontexts"></a>UIContexts

エディターには、それが有効になるケースを表す 1 つ以上の UIContexts を登録できます。 UIContexts は、エディターを登録するパッケージに `ProvideEditorUIContextAttribute` の 1 つ以上のインスタンスを適用することで登録されます。

エディターに UIContexts が登録されている場合:

- 指定された拡張子を持つファイルを開いたときに、登録されている UIContexts の少なくとも 1 つがアクティブな場合、そのエディターはエディターの検索に含まれます。
- 登録されているどの UIContexts もアクティブでない場合、そのエディターはエディターの検索に含まれません。

エディターに UIContexts が登録されていない場合、そのエディターは常にその拡張子のエディターの検索に含まれます。

たとえば、C# プロジェクトが開いているときにのみ使用できるエディターの場合は、`ProvideEditorUIContext` 属性を適用して、次のアフィニティを宣言できます。

```cs
[ProvideEditorUIContext(typeof(MyEditor), KnownUIContexts.CSharpProjectContext)]
```
