---
title: ソース管理プラグインの実装 - ベスト プラクティス
description: Visual Studio でソース管理プラグインを確実に実装する助けとするため、これらの技術的詳細を確認してください。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, best practices
- best practices, source control plug-ins
- source control [Visual Studio SDK], plug-ins
ms.assetid: 85e73b73-29dc-464f-8734-ed308742c435
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: d64f195d13aca75b3b037ff14401395c03bd3d29
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105097358"
---
# <a name="best-practices-for-implementing-a-source-control-plug-in"></a>ソース管理プラグインを実装するためのベスト プラクティス
以下の技術的詳細は、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] でソース管理プラグインを確実に実装する助けとなります。

## <a name="memory-management-issues"></a>メモリ管理に関する問題
 ほとんどの場合、呼び出し元である統合開発環境 (IDE) が、メモリの解放と割り当てを行います。 ソース管理プラグインは、呼び出し元が割り当てたバッファーで、文字列やその他の項目を返します。 例外については、発生場所となる特定の関数の説明に記載しています。

## <a name="arrays-of-file-names"></a>ファイル名の配列
 ファイルの配列が渡されるときには、ファイル名の切れ目のない配列としては渡されません。 これはファイル名へのポインターの配列として渡されます。 たとえば [SccGet](../extensibility/sccget-function.md) では、`lpFileNames` パラメーターによってファイル名が渡されますが、`lpFileNames` は実際には `char **` へのポインターです。 `lpFileNames`[0] は最初の名前へのポインター、`lpFileNames`[1] は 2 番目の名前へのポインターであり、これが続きます。

## <a name="large-model"></a>大きなモデル
 16 ビット オペレーティング システム上であっても、すべてのポインターが 32 ビットです。

## <a name="fully-qualified-paths"></a>完全修飾パス
 引数としてファイル名またはディレクトリを指定する場合は、末尾にバックスラッシュを付けず、完全修飾パスまたは UNC パスにする必要があります。 それが、基になっているソース管理システムの要件である場合は、ソース管理プラグインで、これらを相対パスに変換する必要があります。

## <a name="specify-a-fully-qualified-path-for-the-registered-dll"></a>登録される DLL の完全修飾パスを指定する
 IDE では、相対パス ( *.\NewProvider.DLL* など) から DLL を読み込まなくなっています。 DLL への完全なパスを指定する必要があります (*C:\Providers\NewProvider.DLL* など)。 この要件によって、未認可であったり偽装されていたりするソース管理 DLL の読み込みを防止し、IDE のセキュリティが強化されています。

## <a name="check-for-an-existing-vssci-plug-in-when-you-install-your-source-control-plug-in"></a>ソース管理プラグインをインストールするときに既存の VSSCI プラグインについて調べる
 ソース管理プラグインをインストールする予定のユーザーは、コンピューターに従来のソース管理プラグインを既にインストールしている場合があります。 関連するレジストリキーに既存の値があるかどうは、作成するプラグインのインストール (セットアップ) プログラムで判定する必要があります。 これらのキーが既に設定されている場合、インストール プログラムでは、そのプラグインを既定のソース管理プラグインとして登録するか、既にインストールされているものを置き換えるかをユーザーに確認する必要があります。

## <a name="error-result-codes-and-reporting"></a>エラーの結果コードとレポート
 ソース管理関数の `SCC_OK` リターン コードは、操作がすべてのファイルについて成功したことを示します。 操作が失敗した場合は、最後に発生したエラー コードが返されると予期されています。

 レポートに関する規則では、IDE でエラーが発生した場合は、それを報告する責任を負うのは IDE です。 ソース管理システムでエラーが発生した場合は、それを報告する責任を負うのはソース管理プラグインです。 たとえば、IDE からは "**現在どのファイルも選択されていません**" と報告されるのに対して、プラグインからは "**このファイルは既にチェックアウトされています**" と報告されます。

## <a name="the-context-structure"></a>コンテキスト構造体
 [SccInitialize](../extensibility/sccinitialize-function.md) の呼び出し中に、呼び出し元は `ppvContext` パラメーターを渡します。これは、void への初期化されていないハンドルです。 ソース管理プラグインでは、このパラメーターを無視することも、任意の種類の構造体を割り当てて、その構造体へのポインターを、渡されたポインターに入れることもできます。 IDE ではこの構造体は認識されませんが、この構造体へのポインターを、プラグイン内のその他の呼び出しすべてに渡します。 これによってプラグインに、有用なコンテキスト キャッシュ情報が提供されます。この情報を使用すると、グローバル変数を使用せずに複数の関数呼び出しにわたって存続するグローバル状態情報を維持できます。 プラグインは、[SccUninitialize](../extensibility/sccuninitialize-function.md) の呼び出しに関する構造体を解放する役割を担います。

 プラグインによって [SccInitialize](../extensibility/sccinitialize-function.md) に (具体的には `lpSccCaps` パラメーター内に) `SCC_CAP_REENTRANT` ビットが設定された場合、開いているすべてのプロジェクトを追跡するために複数のコンテキスト構造体が使用されます。

## <a name="bitflags-and-other-command-options"></a>ビットフラグとその他のコマンド オプション
 [SccGet](../extensibility/sccget-function.md) などの各コマンドに対して、IDE ではコマンドの動作を変更する多くのオプションを指定できます。

 API では、IDE による、`fOptions` パラメーターを通した特定のオプションの設定をサポートしてい ます。 これらのオプションについては、それらの影響を受けるコマンドと共に、「[特定のコマンドで使用されるビットフラグ](../extensibility/bitflags-used-by-specific-commands.md)」で説明されています。 これらは一般に、ユーザーにプロンプトが表示されないオプションです。

 ユーザーが構成できる設定オプションのほとんどは、ソース管理プラグイン間で大幅に異なるため、この方法では定義されません。したがって、推奨されるメカニズムは **[詳細設定]** ボタンです。 たとえば、 **[取得]** ダイアログ ボックスでは、IDE で認識されている情報のみが表示されますが、プラグインにこのコマンド用のオプションがある場合は、 **[詳細設定]** ボタンも表示されます。 ユーザーが **[詳細設定]** ボタンをクリックすると、IDE から [SccGetCommandOptions](../extensibility/sccgetcommandoptions-function.md) が呼び出されて、ソース管理プラグインで、ビットフラグや日付/時刻などの情報を求めるダイアログをユーザーに表示できるようになります。 プラグインからは、`SccGet` コマンドの実行時に返す構造体で、この情報が返されます。

## <a name="see-also"></a>関連項目
- [ソース管理プラグイン](../extensibility/source-control-plug-ins.md)
- [ソース管理プラグインの作成](../extensibility/internals/creating-a-source-control-plug-in.md)
