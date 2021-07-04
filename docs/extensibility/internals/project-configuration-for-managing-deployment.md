---
title: 展開の管理のためのプロジェクト構成 | Microsoft Docs
description: デバッグとインストールに必要な場所への展開と、Visual Studio でデプロイをサポートするプロジェクトをサポートする 2 つの方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- project configurations, managing deployment
- projects [Visual Studio SDK], configuration for managing deployment
ms.assetid: bd5940d9-d94d-4944-beda-4ec1ab2bbde5
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 3c6077665ccc3bbe5f87b91a1d2fc5636e08539d
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112899902"
---
# <a name="project-configuration-for-managing-deployment"></a>展開の管理のためのプロジェクト構成
展開は、デバッグとインストールのために、出力項目をビルド プロセスから必要な場所に物理的に移動する操作です。 たとえば、Web アプリケーションは、ローカル マシン上に構築されてから、サーバー上に配置される場合があります。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] では、プロジェクトを展開に関与させることができる 2 つの方法をサポートしています。

- 展開プロセスの対象として。

- 展開プロセスのマネージャーとして。

  ソリューションを展開する前に、まず展開プロジェクトを追加して展開オプションを構成する必要があります。 展開プロジェクトがまだ存在していない場合は、 **[ビルド]** メニューの **[ソリューションの展開]** を選択したとき、または右クリックしたときに作成するかどうかを確認するメッセージが表示されます。 **[はい]** をクリックすると、 **[リモート展開ウィザード]** プロジェクトが選択された状態で **[新しいプロジェクトの追加]** ダイアログ ボックスが開きます。

  リモート展開ウィザードでは、アプリケーションの種類 (Windows または Web)、含めるプロジェクト出力グループ、含めたいその他のファイル、および展開先のリモート コンピューターを入力するよう求められます。 ウィザードの最後のページには、選択したオプションの概要が表示されます。

  展開プロセスの対象となるプロジェクトでは、代替環境に移動する必要がある出力項目が生成されます。 これらの出力項目は、プロジェクトが出力をグループ化できるようにすることを主な目的とする <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg2> インターフェイスのパラメーターとして記述されています。 `IVsProjectCfg2` の実装に関する詳細については、「[出力のためのプロジェクト構成](../../extensibility/internals/project-configuration-for-output.md)」を参照してください。

  展開プロセスを管理する展開プロジェクトは、展開コマンドを有効にし、このコマンドが選択されると応答します。 展開プロジェクトは、展開を実行するために <xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg> インターフェイスを実装し、展開の状態イベントを報告するために <xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployStatusCallback> インターフェイスを呼び出します。

  構成により、ビルドまたは展開操作に影響を与える依存関係を指定できます。 ビルドまたは展開の依存関係は、構成自体がビルドまたは展開される前または後に、ビルドまたは展開する必要があるプロジェクトです。 プロジェクト間のビルドの依存関係は <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildDependency> インターフェイスで記述され、展開の依存関係は <xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployDependency> インターフェイスで記述されます。 詳細については、「[ビルドのためのプロジェクト構成](../../extensibility/internals/project-configuration-for-building.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [構成オプションの管理](../../extensibility/internals/managing-configuration-options.md)
- [ビルドのためのプロジェクト構成](../../extensibility/internals/project-configuration-for-building.md)
- [出力のためのプロジェクト構成](../../extensibility/internals/project-configuration-for-output.md)
