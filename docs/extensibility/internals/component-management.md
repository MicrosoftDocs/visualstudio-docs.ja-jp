---
title: コンポーネント管理 | Microsoft Docs
description: Visual Studio で VSPackage インストーラーを作成するときに Windows インストーラー コンポーネントを管理する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- installation [Visual Studio SDK], components
- installation [Visual Studio SDK], file management
ms.assetid: 029bffa2-6841-4caa-a41a-442467e1aedc
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 9767af4c30957111526303600f9e8eda815b42f0
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105057092"
---
# <a name="component-management"></a>コンポーネント管理
Windows インストーラー内のタスクの単位は、Windows インストーラー コンポーネント (WIC または単にコンポーネントとも呼ばれます) と呼ばれます。 GUID により各 WIC が識別されます。これは、インストールの基本単位であり、Windows インストーラーを使用するセットアップの参照カウントです。

 いくつかの製品を使用して VSPackage インストーラーを作成することもできますが、この説明では Windows インストーラー ( *.msi*) ファイルを使用することを前提としています。 インストーラーを作成するときに、正しい参照カウントが常に発生するように、ファイルの配置を正しく管理する必要があります。 そうすると、インストールとアンインストールの組み合わせのシナリオでは、製品のバージョンによって相互に干渉したり、相互に侵入したりすることはありません。

 Windows インストーラーでは、参照カウントはコンポーネント レベルで発生します。 リソース (ファイル、レジストリ エントリなど) をコンポーネントに慎重に整理する必要があります。 さまざまなシナリオで役立つ、モジュール、機能、製品など、他のレベルの組織があります。 詳細については、「[Windows インストーラーの基本事項](../../extensibility/internals/windows-installer-basics.md)」を参照してください。

## <a name="guidelines-of-authoring-setup-for-side-by-side-installation"></a>サイド バイ サイド インストールのセットアップの作成に関するガイドライン

- バージョン間で共有されるファイルとレジストリ キーを独自のコンポーネントに作成します。

     これにより、次のバージョンで簡単に使用できるようになります。 たとえば、グローバルに登録されている型ライブラリ、ファイル拡張子、**HKEY_CLASSES_ROOT** に登録されているその他の項目などです。

- 共有コンポーネントを別々のマージ モジュールにグループ化します。

     この戦略は、サイド バイ サイド インストールを進めるために正しく作成するのに役立ちます。

- 同じ Windows インストーラー コンポーネントを複数のバージョンで使用して、共有ファイルとレジストリ キーをインストールします。

     別のコンポーネントを使用した場合、1 つのバージョンの VSPackage がアンインストールされ、別の VSPackage がまだインストールされている場合に、ファイルとレジストリ エントリはアンインストールされます。

- 同じコンポーネントにバージョン管理された項目と共有項目を混在させないでください。

     そうすると、グローバルな場所に共有アイテムを、またバージョン管理されたアイテムを分離された場所にインストールすることができなくなります。

- バージョン管理されたファイルを指す共有レジストリ キーがないようにします。

     ある場合、別のバージョンの VSPackage がインストールされていると、共有キーは上書きされます。 2 番目のバージョンを削除すると、キーがポイントしているファイルが消えます。

## <a name="see-also"></a>関連項目
- [共有 VSPackage と バージョン管理 VSPackage の選択](../../extensibility/choosing-between-shared-and-versioned-vspackages.md)
- [VSPackage のセットアップ シナリオ](../../extensibility/internals/vspackage-setup-scenarios.md)
