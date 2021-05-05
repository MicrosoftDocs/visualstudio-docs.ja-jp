---
title: Azure のコマンド ライン ビルド | Microsoft Docs
description: Azure のコマンド ライン ビルド
author: ghogen
manager: jmartens
ms.workload: azure-vs
ms.topic: how-to
ms.date: 03/05/2017
ms.author: ghogen
ms.openlocfilehash: b60e076c50c9465f54c3c05dda0318f56fa5e9ae
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99844269"
---
# <a name="building-azure-projects-from-the-command-line"></a>コマンド ラインからの Azure プロジェクトのビルド
Microsoft Build Engine (MSBuild) を使用すると、Visual Studio がインストールされていないビルド ラボ環境で製品のビルドを構築できます。 MSBuild は、拡張可能で Microsoft が完全にサポートしている XML 形式をプロジェクト ファイルに使用します。 MSBuild ファイル形式を使用すると、1 つまたは複数のプラットフォームや構成でビルドが必要な項目を記述できます。

MSBuild はコマンド ラインで実行することもできます。このトピックでは、その方法について説明します。 コマンド ラインでプロパティを設定すると、プロジェクトの特定の構成を作成できます。 同様に、MSBuild がビルドするターゲットを定義することもできます。 コマンド ライン パラメーターおよび MSBuild の詳細については、「[MSBuild Command Line Reference (MSBuild コマンド ライン リファレンス)](../msbuild/msbuild-command-line-reference.md)」を参照してください。

## <a name="msbuild-parameters"></a>MSBuild パラメーター
パッケージを作成する最も簡単な方法は、 `/t:Publish` オプションを指定して MSBuild を実行することです。 既定では、プロジェクトのルート フォルダーに対して ディレクトリが作成されます (たとえば、`<ProjectDirectory>\bin\Configuration\app.publish\`)。 Azure プロジェクトをビルドすると、パッケージ ファイルとそれに対応する構成ファイルの 2 つのファイルが生成されます。

* パッケージ ファイル (`project.cspkg`)
* 構成ファイル (`ServiceConfiguration.TargetProfile.cscfg`)

既定では、各 Azure プロジェクトにはローカル (デバッグ) ビルド用に 1 つ、クラウド (ステージングまたは運用) ビルド用に 1 つのサービス構成ファイルが含まれています。 サービス構成ファイルは必要に応じて追加または削除できます。 Visual Studio 内でパッケージをビルドするときは、パッケージに含めるサービス構成ファイルを指定するよう求められます。 MSBuild を使用してパッケージをビルドする場合、既定でローカル サービス構成ファイルが含められます。 別のサービス構成ファイルを含めるには、MSBuild コマンドの `TargetProfile` プロパティ を設定します (`MSBuild /t:Publish /p:TargetProfile=ProfileName`)。

パッケージと構成ファイルの格納に別のディレクトリを使用する場合は、`/p:PublishDir=Directory\` オプションを使用してパスを設定します。その際、末尾に円記号の区切り記号を含めます。

## <a name="next-steps"></a>次のステップ
パッケージは、ビルド後に Azure にデプロイできます。
