---
title: ソリューション ユーザー オプション (.Suo) ファイル | Microsoft Docs
description: ソリューション ユーザー オプション (.suo) ファイルについて説明します。このファイルでは、ユーザーごとのソリューション オプションが、バイナリ形式で格納された形で構造化ストレージ ファイルに含まれています。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- .suo files, VSPackages
- suo files, VSPackages
- solutions, .suo files
- solutions, user options
- solution user options (.suo) file
ms.assetid: 75258e0d-600d-4a3d-94f4-3d7ac12cb47c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 92e755053d3519212c27fd2567610baf189db309
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105069362"
---
# <a name="solution-user-options-suo-file"></a>ソリューション ユーザー オプション (.Suo) ファイル
ソリューション ユーザー オプション (.suo) ファイルには、ユーザーごとのソリューション オプションが含まれています。 このファイルをソース コード管理にチェックインしないでください。

 ソリューション ユーザー オプション (.suo) ファイルは、バイナリ形式で格納された構造化ストレージ (複合) ファイルです。 ユーザー情報の保存先はストリームですが、このストリームの名前が、.suo ファイル内の情報を識別するために使用されるキーになります。 ソリューション ユーザー オプション ファイルは、ユーザー設定を格納するために使用され、Visual Studio がソリューションを保存すると自動的に作成されます。

 環境で .suo ファイルが開かれると、現在読み込まれているすべての VSPackage が列挙されます。 VSPackage が <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionOpts> インターフェイスを実装する場合、環境は VSPackage に対して <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionOpts.LoadUserOptions%2A> メソッドを呼び出して、そのデータのすべてを .suo ファイルから読み込むよう求めます。

 VSPackage には、.suo ファイルに書き込んだ可能性があるストリームを把握しておく責任があります。 書き込んだストリームごとに、VSPackage は、<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence.LoadPackageUserOpts%2A> を通じて環境にコールバックして、ストリームの名前であるキーで識別される特定のストリームを読み込みます。 その後、環境は VSPackage にコールバックし、ストリームの名前と、<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence.LoadPackageUserOpts%2A> メソッドへの `IStream` ポインターを渡して、その特定のストリームを読み取ります。

 その時点で、`LoadUserOptions` がもう一度呼び出されて、読み取る必要がある .suo ファイルの別のセクションがあるかどうかが確認されます。 このプロセスは、.suo ファイル内のすべてのデータ ストリームが環境によって読み取られて処理されるまで続きます。

 ソリューションが保存されるか閉じられると、環境により、<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionOpts.SaveUserOptions%2A> メソッドへのポインターを指定して <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence.SavePackageSolutionProps%2A> メソッドが呼び出されます。 保存するバイナリ情報を含む `IStream` が <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionOpts.WriteUserOptions%2A> メソッドに渡されます。このメソッドは情報を .suo ファイルに書き込み、もう一度 `SaveUserOptions` メソッドを呼び出して、.suo ファイルに書き込む情報の別のストリームがあるかどうかを確認します。

 これらの 2 つのメソッド `SaveUserOptions` と `WriteUserOptions` は、.suo ファイルに保存される情報のストリームごとに、`IVsSolutionPersistence` へのポインターを渡して再帰的に呼び出されます。 これらは、.suo ファイルへの複数のストリームの書き込みを可能にするために、再帰的に呼び出されます。 このようにして、ユーザー情報はソリューションに永続化され、次にソリューションを開いたときにそこにあることが保証されます。

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionOpts>
- [ソリューション](../../extensibility/internals/solutions-overview.md)
