---
title: ソース管理プラグイン | Microsoft Docs
description: このセクションの記事では、ソース管理システムを Visual Studio に統合可能にする、インターフェイス仕様一式について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, reference
ms.assetid: 964980ca-21c5-4706-8535-6ea23e1c9cc9
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: a6788d738d37ac62156958acb15c1bcd5d536515
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105089954"
---
# <a name="source-control-plug-ins"></a>ソース管理プラグイン
ソース管理プラグイン SDK のリファレンス セクションには、ソース管理システムを [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] に統合可能にするインターフェイス仕様一式が含まれています。 この仕様では、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 統合開発環境 (IDE) とのインターフェイスとして、ソース管理プラグインが実装する必要のあるさまざまな関数とデータ型の構文とセマンティクスが指定されています。

## <a name="in-this-section"></a>このセクションの内容
- 「[ソース管理プラグイン API 関数](../extensibility/source-control-plug-in-api-functions.md)」では、ソース管理プラグイン API に準拠するためにソース管理プラグインが実装する必要がある関数の一覧を示します。

- 「[IDE によって実装されるコールバック関数](../extensibility/callback-functions-implemented-by-the-ide.md)」では、特定のコマンドが実行されている間に、ソース管理プラグインが IDE に情報を返すために使用する関数について説明します。

- 「[列挙子](../extensibility/enumerators.md)」では、ソース管理プラグインが認識する必要がある、ソース管理プラグイン API の列挙子データ型の一覧を示します。

- 「[機能フラグ](../extensibility/capability-flags.md)」では、プロバイダーの機能を示す `SCC_CAP_xxx` フラグについて説明します。

- 「[特定のコマンドで使用されるビットフラグ](../extensibility/bitflags-used-by-specific-commands.md)」では、特定のコマンドのコンテキストで役立つフラグの一覧を示します。

- 「[エラー コード](../extensibility/error-codes.md)」では、関数によって `SCCTRN` として返される一般的なエラー値の一覧を示します。

- 「[ソース管理プラグインを検索するためのキーとして使用される文字列](../extensibility/strings-used-as-keys-for-finding-a-source-control-plug-in.md)」では、レジストリにアクセスしてソース管理プラグインを検索するためのキーについて説明します。

- 「[MSSCCPRJ.SCC ファイル](../extensibility/mssccprj-scc-file.md)」では、IDE にとって不透明な情報を含むが、ソース管理プラグインによって、ソリューションまたはプロジェクトをバージョン管理内で検索するために使用される、クライアント側のファイルについて説明します。

- 「[ソース管理プラグインの実装のベストプラクティス](../extensibility/best-practices-for-implementing-a-source-control-plug-in.md)」では、ソース管理プラグイン API の実装時に憶えておく必要のある重要な技術情報のコレクションを提供します。

- 「[文字列の長さの制限](../extensibility/restrictions-on-string-lengths.md)」では、さまざまな関数で使用される文字列の長さに対する、ソース管理プラグイン API の制限事項について説明します。

- 「[用語集](../extensibility/source-control-plug-in-glossary.md)」では、ソース管理プラグイン SDK のドキュメントを読むときに便利な用語とその定義を提供します。

- 「[方法: ソース管理プラグインの互換性に関する警告をオフにする](../extensibility/how-to-turn-off-compatibility-warnings-for-source-control-plug-ins.md)」では、警告を無効にする方法を説明します。

## <a name="related-sections"></a>関連項目
- [ソース管理プラグインのサンプル](https://www.microsoft.com/download/details.aspx?id=55984)のページには、ソース管理プラグインの機能のサンプルが用意されています。

- 「[ソース管理プラグインのテスト ガイド](../extensibility/internals/test-guide-for-source-control-plug-ins.md)」では、ソース管理プラグインに関連するテスト手順を説明します。

- 「[ソース管理プラグインを作成する](../extensibility/internals/creating-a-source-control-plug-in.md)」では、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] ソース管理のユーザー インターフェイス (UI) の使用中にソース管理機能を提供するソース管理プラグインを作成する方法を説明します。

- 「[Visual Studio SDK リファレンス](../extensibility/visual-studio-sdk-reference.md)」では、参照トピックの一覧を示します。
