---
title: ClickOnce キャッシュの概要 |Microsoft Docs
description: ClickOnce アプリケーション キャッシュについて説明します。ClickOnce アプリケーション キャッシュには、ClickOnce アプリケーションが格納されているクライアント コンピューター上の非表示ディレクトリが含まれます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- Windows applications, ClickOnce deployemtn
- ClickOnce applications, cache
- ClickOnce deployment, cache
ms.assetid: e379921e-9ef1-4326-bbf3-53ba67925526
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 12c14850717688b17caed2fbe7feb546e0ebdb6e
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99936172"
---
# <a name="clickonce-cache-overview"></a>ClickOnce キャッシュの概要
ローカルにインストールされているか、オンラインでホストされているすべての [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションは、クライアントコンピューターの [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーション *キャッシュ* に格納されます。 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] キャッシュは、現在のユーザーの Documents and Settings フォルダーの Local Settings ディレクトリにある非表示ディレクトリのファミリです。 このキャッシュには、アセンブリ、構成ファイル、アプリケーションとユーザーの設定、およびデータ ディレクトリを含む、アプリケーションのすべてのファイルが保持されます。 キャッシュは、アプリケーションのデータ ディレクトリの最新バージョンへの移行も行います。 データ移行の詳細については、「[ClickOnce アプリケーションにおけるローカル データおよびリモート データへのアクセス](../deployment/accessing-local-and-remote-data-in-clickonce-applications.md)」を参照してください。

 アプリケーション ストレージ用に単一の場所を提供することにより、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] ではアプリケーションの物理的なインストールを管理するタスクをユーザーから引き継ぎます。 キャッシュは、すべてのアプリケーションおよびその個別バージョンのアセンブリとデータ ファイルを相互に分離して保持することで、アプリケーションの分離にも役立ちます。 たとえば、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションをアップグレードすると、そのバージョンとそのデータ リソースにはキャッシュ内で独自のディレクトリが提供されます。

## <a name="cache-storage-quota"></a>キャッシュ ストレージ クォータ
 オンラインでホストされている [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションは、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] キャッシュのサイズを制限するクォータにより、占有できる容量が制限されます。 キャッシュ サイズは、すべてのユーザーのオンライン アプリケーションに適用されます。部分的に信頼されたオンライン アプリケーションは、クォータ容量の半分の占有に制限されます。 インストール済みのアプリケーションはキャッシュ サイズによって制限されず、キャッシュの制限に対してカウントされません。 すべての [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションについて、キャッシュには現在のバージョンと以前にインストールされたバージョンのみが保持されます。

 既定では、クライアント コンピューターには、オンライン [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーション用に 250 MB のストレージがあります。 データ ファイルは、この制限に対してカウントされません。 システム管理者は、レジストリ キー **HKEY_CURRENT_USER\Software\Classes\Software\Microsoft\Windows\CurrentVersion\Deployment\OnlineAppQuotaInKB** を変更することにより、特定のクライアント コンピューター上のこのクォータを拡大または縮小できます。これは、キャッシュサイズを KB 単位で表す DWORD 値です。 たとえば、キャッシュサイズを 50 MB に減らすには、この値を 51200 に変更します。

## <a name="see-also"></a>関連項目
- [ClickOnce アプリケーションにおけるローカル データおよびリモート データへのアクセス](../deployment/accessing-local-and-remote-data-in-clickonce-applications.md)