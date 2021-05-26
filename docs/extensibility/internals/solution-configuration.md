---
title: ソリューション構成 | Microsoft Docs
description: プロジェクト タイプでサポートされているソリューション構成を実装する方法について説明します。ソリューション構成により、開始 (F5) キーとビルド コマンドの動作が指示されます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- solution configurations
ms.assetid: f22cfc75-3e31-4e0d-88a9-3ca99539203b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: c6bf2694b26305cdaefefd61dc1119b7b019b12d
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105080789"
---
# <a name="solution-configuration"></a>ソリューション構成
ソリューション構成には、ソリューション レベルのプロパティが格納されます。 これらは、**開始** (F5) キーと **ビルド** コマンドの動作を指示します。 既定では、これらのコマンドはデバッグ構成をビルドして開始します。 どちらのコマンドも、ソリューション構成のコンテキストで実行されます。 つまり、ユーザーは F5 キーを押すことで、設定を通して構成されているアクティブなソリューションをビルドして開始することができます。 環境は、ビルドと実行の際に、プロジェクトではなくソリューション用に最適化するように設計されています。

 標準の Visual Studio ツール バーには、[開始] ボタンと、[開始] ボタンの右側にソリューション構成ドロップダウンが表示されます。 ユーザーはこのリストを使用して、F5 キーを押したときに開始する構成を選択したり、独自のソリューション構成を作成したり、既存の構成を編集したりできます。

> [!NOTE]
> ソリューション構成を作成または編集するための機能拡張インターフェイスはありません。 `DTE.SolutionBuild` を使用する必要があります。 ただし、ソリューションのビルドを管理するための機能拡張 API があります。 詳細については、「<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionBuildManager2>」を参照してください。

 プロジェクト タイプでサポートされているソリューション構成を実装する方法を次に示します。

- Project

   現在のソリューションに存在するプロジェクトの名前を表示します。

- 構成

   プロジェクト タイプでサポートされていてプロパティ ページに表示される構成のリストを提供するには、<xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2> を実装します。

   [構成] 列には、このソリューション構成でビルドするプロジェクト構成の名前が表示されます。矢印ボタンをクリックすると、すべてのプロジェクト構成が一覧表示されます。 このリストに入力するために、環境で <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2.GetCfgNames%2A> メソッドが呼び出されます。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2.GetCfgProviderProperty%2A> メソッドによって、プロジェクトが構成の編集をサポートしていることが示された場合は、[構成] 見出しの下に [新規] または [編集] の選択肢も表示されます。 これらの各選択肢からはダイアログ ボックスが起動され、プロジェクトの構成を編集するために `IVsCfgProvider2` インターフェイスのメソッドが呼び出されます。

   プロジェクトで構成がサポートされていない場合、[構成] 列は [なし] と表示して無効になります。

- プラットフォーム

   選択されたプロジェクト構成のビルド対象のプラットフォームが表示されます。矢印ボタンをクリックすると、そのプロジェクトで使用可能なすべてのプラットフォームが一覧表示されます。 このリストに入力するために、環境で <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2.GetPlatformNames%2A> メソッドが呼び出されます。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2.GetCfgProviderProperty%2A> メソッドによって、プロジェクトがプラットフォームの編集をサポートしていることが示された場合は、[プラットフォーム] 見出しの下に [新規] または [編集] の選択肢も表示されます。 これらの各選択肢からはダイアログ ボックスが起動され、プロジェクトの使用可能なプラットフォームを編集するために `IVsCfgProvider2` のメソッドが呼び出されます。

   プロジェクトでプラットフォームがサポートされていない場合、そのプロジェクトの [プラットフォーム] 列は [なし] と表示して無効になります。

- ビルド

   現在のソリューション構成によってプロジェクトがビルドされるかどうかを指定します。 選択されていないプロジェクトは、それに含まれているプロジェクトの依存関係にかかわらず、ソリューション レベルのビルド コマンドが呼び出されてもビルドされません。 ビルド対象として選択されていないプロジェクトは、ソリューションのデバッグ、実行、パッケージ化、およびデプロイには引き続き含まれます。

- デプロイ

   選択されたソリューション ビルド構成で開始コマンドまたはデプロイ コマンドが使用されたときに、プロジェクトがデプロイされるかどうかを指定します。 このフィールドのチェック ボックスは、プロジェクトがその <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg2> オブジェクトに <xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg> インターフェイスを実装することによってデプロイをサポートしている場合に使用可能になります。

  新しいソリューション構成が追加されると、ユーザーは標準ツール バーの [ソリューション構成] ドロップダウン リスト ボックスからその構成を選択して、ビルドまたは開始できます。

## <a name="see-also"></a>関連項目
- [構成オプションの管理](../../extensibility/internals/managing-configuration-options.md)
- [ビルドのためのプロジェクト構成](../../extensibility/internals/project-configuration-for-building.md)
- [プロジェクト構成オブジェクト](../../extensibility/internals/project-configuration-object.md)
