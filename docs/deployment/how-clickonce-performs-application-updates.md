---
title: ClickOnce がアプリケーションの更新を実行するしくみ | Microsoft Docs
description: ClickOnce がファイル バージョン情報を使用してアプリケーションを更新するかどうかを決定する方法について説明します。 ClickOnce では、ファイルの部分置換を使用してダウンロードの冗長性を回避します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- updates, ClickOnce
- ClickOnce deployment, updates
- deploying applications [ClickOnce], application updates
ms.assetid: d54313c2-cf0c-420d-b151-99953a95f0bb
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: cdef39a0ab07d4cb9c9f42cf897bd7728934b88d
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99915744"
---
# <a name="how-clickonce-performs-application-updates"></a>ClickOnce がアプリケーションの更新を実行するしくみ
ClickOnce では、アプリケーションの配置マニフェストで指定されるファイル バージョン情報を使用して、アプリケーションのファイルを更新するかどうかを決定します。 更新が開始されると、ClickOnce は *ファイルの部分置換* と呼ばれる手法を使用して、アプリケーション ファイルの冗長的なダウンロードを回避します。

## <a name="file-patching"></a>ファイルの部分置換
 アプリケーションを更新する場合、ClickOnce では、ファイルが変更されていない限り、アプリケーションの新しいバージョンのすべてのファイルがダウンロードされることはありません。 代わりに、現在のアプリケーションのアプリケーション マニフェストで指定されたファイルのハッシュ署名を、新しいバージョンのマニフェスト内のシグネチャと比較します。 ファイルのシグネチャが異なる場合は、ClickOnce によって新しいバージョンがダウンロードされます。 シグネチャが一致する場合、ファイルはあるバージョンから次のバージョンへと変更されていません。 この場合、ClickOnce では既存のファイルをコピーし、新しいバージョンのアプリケーションで使用します。 この手法により、1 つまたは 2 つのファイルのみが変更された場合でも ClickOnce によってアプリケーション全体が再度ダウンロードされることがなくなります。

 ファイルの部分置換は、<xref:System.Deployment.Application.ApplicationDeployment.DownloadFileGroup%2A> メソッドと <xref:System.Deployment.Application.ApplicationDeployment.DownloadFileGroupAsync%2A> メソッドを使用して必要に応じてダウンロードされるアセンブリに対しても機能します。

 Visual Studio を使用してアプリケーションをコンパイルする場合、プロジェクト全体をリビルドするたびに、すべてのファイルに対して新しいハッシュ シグネチャが生成されます。 この場合、いくつかのアセンブリのみが変更された可能性があるにもかかわらず、すべてのアセンブリがクライアントにダウンロードされます。

 ファイルの部分置換は、データとしてマークされ、データ ディレクトリに格納されているファイルに対しては機能しません。 これらは、ファイルのハッシュ シグネチャに関係なく、常にダウンロードされます。 データ ディレクトリの詳細については、「[ClickOnce アプリケーションにおけるローカル データおよびリモート データへのアクセス](../deployment/accessing-local-and-remote-data-in-clickonce-applications.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [ClickOnce の更新方法の選択](../deployment/choosing-a-clickonce-update-strategy.md)
- [ClickOnce 配置ストラテジの選択](../deployment/choosing-a-clickonce-deployment-strategy.md)