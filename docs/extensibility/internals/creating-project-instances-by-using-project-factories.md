---
title: プロジェクト ファクトリを使用したプロジェクト インスタンスの作成 | Microsoft Docs
description: Visual Studio 統合開発環境 (IDE) でプロジェクト ファクトリを使用して、プロジェクト クラス インスタンスを作成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project factories
- projects [Visual Studio SDK], project factories
ms.assetid: 94c90012-8669-459c-af8e-307ac242c8c4
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 40b7c3fbe5b5b7fd59fe0e57376290181f3e9a20
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105056801"
---
# <a name="create-project-instances-by-using-project-factories"></a>プロジェクト ファクトリを使用したプロジェクト インスタンスの作成
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] のプロジェクト タイプでは、*プロジェクト ファクトリ* を使用して、プロジェクト オブジェクトのインスタンスが作成されます。 プロジェクト ファクトリは、共同作成可能な COM オブジェクトの標準クラス ファクトリに似ています。 ただし、プロジェクト オブジェクトは共同作成可能ではありません。これらは、プロジェクト ファクトリを使用してのみ作成できます。

 ユーザーが [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] で既存のプロジェクトを読み込むか、新しいプロジェクトを作成するときに、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE によって、VSPackage に実装されているプロジェクト ファクトリが呼び出されます。 新しいプロジェクト オブジェクトによって、**ソリューション エクスプローラー** を設定するのに十分な情報が IDE に提供されます。 新しいプロジェクト オブジェクトでは、IDE によって開始された関連するすべての UI 操作をサポートするために必要なインターフェイスも用意されます。

 プロジェクト内のクラスに <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory> インターフェイスを実装できます。 通常、それは独自のモジュール内に配置されます。

 所有者による集計をサポートするプロジェクトは、そのプロジェクト ファイルで所有者キーを永続化する必要があります。 所有者キーを持つプロジェクトで <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory.CreateProject%2A> メソッドが呼び出されると、所有されているプロジェクトによってその所有者キーがプロジェクト ファクトリ GUID に変換され、その後、このプロジェクト ファクトリで `CreateProject` メソッドが呼び出され実際の作成が行われます。

## <a name="create-an-owned-project"></a>所有されているプロジェクトの作成
 所有者による所有されているプロジェクトの作成には、次の 2 つのフェーズがあります。

1. <xref:Microsoft.VisualStudio.Shell.Interop.IVsOwnedProjectFactory.PreCreateForOwner%2A> メソッドを呼び出す。 これにより、所有されているプロジェクトには、入力制御 `IUnknown` に基づいて集計されたプロジェクト オブジェクトを作成する機会が与えられます。 所有されているプロジェクトによって、内部 `IUnknown` および集計されたオブジェクトが所有者プロジェクトに渡されます。 これにより、所有されているプロジェクトに、内部 `IUnknown` を格納する機会が与えられます。

2. <xref:Microsoft.VisualStudio.Shell.Interop.IVsOwnedProjectFactory.InitializeForOwner%2A> メソッドを呼び出す。 所有されていないプロジェクトの場合のように、`IVsProjectFactory::CreateProject` が呼び出されるのではなく、このメソッドが呼び出されると、所有されているプロジェクトによってすべてのインスタンス化が行われます。 通常、入力 `VSOWNEDPROJECTOBJECT` 列挙は、集計された所有されているプロジェクトです。 所有されているプロジェクトでは、この変数を使用して、そのプロジェクト オブジェクトが既に作成されている (cookie が NULL ではない) のか、それとも作成する必要がある (cookie が NULL である) のかを判断できます。

   プロジェクト タイプは、共同作成可能な COM オブジェクトの CLSID と同様に、一意のプロジェクト GUID によって識別されます。 通常、1 つのプロジェクト ファクトリによって、1 つのプロジェクト タイプのインスタンスの作成が処理されますが、1 つのプロジェクト ファクトリで 1 つ以上のプロジェクト タイプ GUID を処理することもできます。

   プロジェクト タイプは、特定のファイル名拡張子に関連付けられています。 ユーザーが既存のプロジェクト ファイルを開こうとしたとき、またはテンプレートを複製して新しいプロジェクトを作成しようとしたとき、IDE によって、ファイルの拡張子が使用され、対応するプロジェクト GUID が特定されます。

   IDE によって、新しいプロジェクトを作成する必要があるのか、それとも特定のタイプの既存のプロジェクトを開く必要があるのかが判断されると、 **[HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\8.0\Projects]** の下にあるシステム レジストリの情報が使用され、必要なプロジェクト ファクトリを実装している VSPackage が検索されます。 この VSPackage が IDE によって読み込まれます。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.SetSite%2A> メソッドでは、VSPackage によって <xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterProjectTypes.RegisterProjectType%2A> メソッドが呼び出され、そのプロジェクト ファクトリが IDE に登録される必要があります。

   `IVsProjectFactory` インターフェイスの主要なメソッドは <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory.CreateProject%2A> です。これは、既存のプロジェクトを開く、新しいプロジェクトを作成するという 2 つのシナリオを処理します。 ほとんどのプロジェクトでは、そのプロジェクトの状態はプロジェクト ファイルに格納されます。 通常、新しいプロジェクトの作成では、`CreateProject` メソッドに渡されたテンプレート ファイルのコピーが作成され、そのコピーが開かれます。 既存のプロジェクトは、`CreateProject` メソッドに渡されたプロジェクト ファイルを直接開くことによってインスタンス化されます。 `CreateProject` メソッドでは、必要に応じてユーザーに追加の UI 機能を表示できます。

   プロジェクトで使用するファイルがないこともあります。その場合、代わりに、そのプロジェクトの状態を、データベースや Web サーバーなどのファイル システム以外のストレージ メカニズムに格納できます。 この場合、プロジェクト データを識別するために、`CreateProject` メソッドに渡されるファイル名パラメーターは、実際は、ファイル システム パスではなく、一意の文字列 (URL) です。 `CreateProject` に渡されたテンプレート ファイルをコピーして、実行予定の適切な構築シーケンスをトリガーする必要はありません。

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsOwnedProjectFactory>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterProjectTypes>
- [チェック リスト: 新しいプロジェクト タイプの作成](../../extensibility/internals/checklist-creating-new-project-types.md)
