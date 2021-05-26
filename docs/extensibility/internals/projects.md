---
title: プロジェクト | Microsoft Docs
description: VSPackage で、プロジェクト タイプ、プロジェクト サブタイプ、およびカスタム ツールを含めることで Visual Studio プロジェクト システムを拡張する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- solutions [Visual Studio]
- custom tools [Visual Studio SDK]
- project subtypes [Visual Studio SDK]
- projects [Visual Studio SDK]
- project types [Visual Studio SDK]
ms.assetid: 237742e4-a638-4d5b-a9b3-6a69d627763c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 73f685707d6c9f7a8b40bb57c5207c6a538fd1f4
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105081023"
---
# <a name="projects"></a>プロジェクト
Visual Studio でプロジェクトとは、**ソリューション エクスプローラー** に表示されるソース コード ファイルやその他のリソースを整理するために開発者が使用するコンテナーです。 通常、プロジェクトは、ソース コード ファイルとリソース (ビットマップ ファイルなど) への参照を格納するファイルです (C# プロジェクトの .csproj ファイルなど)。 プロジェクトを使用すると、ソース コード、Web サービスやデータベースへの参照、およびその他のリソースの整理、ビルド、デバッグ、およびデプロイを実行することができます。 VSPackage では、"*プロジェクト タイプ*"、"*プロジェクト サブタイプ*"、および "*カスタム ツール*" という主に 3 つの方法で、Visual Studio プロジェクト システムを拡張できます。

## <a name="in-this-section"></a>このセクションの内容
- [プロジェクトの種類](../../extensibility/internals/project-types.md)

 "*プロジェクト タイプ*" では、プログラミング言語など、新しい種類のプロジェクトのサポートが追加されます。 たとえば、Visual Studio でサポートされている各言語には独自のプロジェクト タイプがあり、IronPython 統合サンプルには IronPython 言語のプロジェクト タイプが含まれています。 C# または Visual Basic 以外の言語に対しては、プロジェクト タイプを作成して、項目のビルド、デバッグ、デプロイ、および **ソリューション エクスプローラー** での表示方法をカスタマイズする必要があります。 詳細については、「[プロジェクトの種類](../../extensibility/internals/project-types.md)」を参照してください。

- [プロジェクト サブタイプ](../../extensibility/internals/project-subtypes.md)

 "*プロジェクト サブタイプ*" はプロジェクト タイプに基づいており、プロジェクトのビルド、デバッグ、およびデプロイの方法をカスタマイズするために使用できます。 Visual Studio では、スマート デバイス プロジェクトにプロジェクト サブタイプを使用します。新しくビルドされたプログラムを開発用コンピューターからターゲット デバイスにコピーすることによって、デプロイをカスタマイズします。 C# および Visual Basic プロジェクト タイプは、プロジェクト サブタイプの基礎として使用できますが、C++ プロジェクト タイプはできません。 プロジェクト サブタイプの基礎として、独自のプロジェクト タイプを使用することもできます。 詳細については、「[プロジェクト サブタイプ](../../extensibility/internals/project-subtypes.md)」を参照してください。

- [Web プロジェクト](../../extensibility/internals/web-projects.md)

 Web アプリケーションを作成する Web プロジェクトについて説明します。

- 「[新しいプロジェクトの生成: 内部的な処理、パート 1](../../extensibility/internals/new-project-generation-under-the-hood-part-one.md)」および「[新しいプロジェクトの生成: 内部的な処理、パート 2](../../extensibility/internals/new-project-generation-under-the-hood-part-two.md)」

 新しいプロジェクトを作成するときに実際に行われることについて説明します。

- [VSSDK のサンプル](https://github.com/Microsoft/VSSDK-Extensibility-Samples)には、プロジェクトとソリューションを処理する VSSDK のサンプルが含まれています。

## <a name="related-sections"></a>関連項目
- [Visual Studio SDK の内部](../../extensibility/internals/inside-the-visual-studio-sdk.md)

 Visual Studio 機能拡張のさまざまな側面について説明します。
