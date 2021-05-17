---
title: プロジェクト モデルの要素 | Microsoft Docs
description: プロジェクト モデルの要素について、および Visual Studio のすべてのプロジェクトのインターフェイスと実装で基本構造を共有する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], implementation considerations
- project models
- projects [Visual Studio SDK], elements
ms.assetid: a1dbe0dc-68da-45d7-8704-5b43ff7e4fc4
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 85b31996a7a0636f136e43531e69fe25c6d87d8f
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105061291"
---
# <a name="elements-of-a-project-model"></a>プロジェクト モデルの要素
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 内のすべてのプロジェクトのインターフェイスと実装は、基本構造 (プロジェクト タイプに応じたプロジェクト モデル) を共有します。 開発中の VSPackage であるプロジェクト モデルでは、設計上の決定事項に準拠し、IDE で提供されるグローバル機能に連携するオブジェクトを作成します。 たとえば、プロジェクト項目を永続化する方法を制御しますが、ファイルを永続化する必要があるという通知は制御しません。 開いているプロジェクト項目にフォーカスを移動し、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] メニュー バーの **[ファイル]** メニューの **[保存]** を選択した場合、プロジェクト タイプ コードで、IDE からのコマンドを先に取得し、ファイルを永続化し、ファイルがこれ以上変更されないという通知を IDE に送信する必要があります。

 VSPackage では、IDE インターフェイスにアクセスできるようにするサービスを通じて、IDE と対話します。 たとえば、特定のサービスを通じて、コマンドを監視およびルーティングし、プロジェクトで行われた選択に関するコンテキスト情報を提供します。 VSPackage に必要なすべてのグローバル IDE 機能は、サービスによって提供されます。 サービスの詳細については、「[方法: サービスを取得する](../../extensibility/how-to-get-a-service.md)」を参照してください。

 実装に関するその他の注意点:

- 1 つのプロジェクト モデルには、複数のプロジェクト タイプを含めることができます。

- プロジェクト タイプとアテンダント プロジェクト ファクトリは、GUID とは別に登録されます。

- ユーザーが [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] UI を使用して新しいプロジェクトを作成するときに、新しいプロジェクト ファイルを初期化するには、各プロジェクトにテンプレート ファイルまたはウィザードが必要です。 たとえば、[!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] テンプレートは最終的に .vcproj ファイルとなるものを初期化します。

  次の図は、一般的なプロジェクトの実装を構成する主要なインターフェイス、サービス、オブジェクトを示しています。 アプリケーションヘルパー (`HierUtil7`) を使用して、基になるオブジェクトやその他のプログラミング定型を作成できます。 `HierUtil7` アプリケーション ヘルパーの詳細については、「[HierUtil7 プロジェクトクラスを使用してプロジェクトの種類を実装する (C++)](/previous-versions/bb166212(v=vs.100))」を参照してください。

  ![Visual Studio プロジェクト モデル グラフィック](../../extensibility/internals/media/vsprojectmodel.gif "vsProjectModel") プロジェクト モデル

  上の図に一覧表示されているインターフェイスおよびサービスと、図に含まれていないその他のオプションのインターフェイスの詳細については、「[プロジェクト モデルのコア コンポーネント](../../extensibility/internals/project-model-core-components.md)」を参照してください。

  プロジェクトはコマンドをサポートできます。したがって、コマンド <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> コンテキスト GUID を使用してコマンド ルーティングに参加するには、インターフェイスを実装する必要があります。

## <a name="see-also"></a>関連項目
- [チェック リスト: 新しいプロジェクト タイプの作成](../../extensibility/internals/checklist-creating-new-project-types.md)
- [HierUtil7 プロジェクトクラスを使用してプロジェクトの種類を実装する (C++)](/previous-versions/bb166212(v=vs.100))
- [プロジェクト モデルのコア コンポーネント](../../extensibility/internals/project-model-core-components.md)
- [プロジェクト ファクトリを使用したプロジェクト インスタンスの作成](../../extensibility/internals/creating-project-instances-by-using-project-factories.md)
- [方法: サービスを取得する](../../extensibility/how-to-get-a-service.md)
- [プロジェクト タイプの作成](../../extensibility/internals/creating-project-types.md)