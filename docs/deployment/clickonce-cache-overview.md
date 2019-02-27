---
title: ClickOnce キャッシュの概要 |Microsoft Docs
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
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 85dbe4917d37c8d39dd8348c32d88933032ede1b
ms.sourcegitcommit: d0425b6b7d4b99e17ca6ac0671282bc718f80910
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 02/21/2019
ms.locfileid: "56603864"
---
# <a name="clickonce-cache-overview"></a>ClickOnce キャッシュの概要
すべて[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]、アプリケーションはオンラインでホストされているまたはローカルにインストールされるかどうか、内のクライアント コンピューターに保存されて、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]アプリケーション*キャッシュ*します。 A[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]キャッシュは現在のユーザーの Documents and Settings フォルダーの設定をローカル ディレクトリの下の隠しディレクトリのファミリです。 このキャッシュは、アセンブリ、構成ファイル、アプリケーションとユーザー設定、およびデータ ディレクトリを含む、アプリケーションのすべてのファイルを保持します。 キャッシュはアプリケーションのデータ ディレクトリを最新バージョンに移行するためも担当します。 データ移行の詳細については、次を参照してください。[ローカルへのアクセスとリモート データには、ClickOnce アプリケーション](../deployment/accessing-local-and-remote-data-in-clickonce-applications.md)します。

 アプリケーションの記憶域用の 1 つの場所を提供することで[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]ユーザーから、アプリケーションの物理的なインストールの管理作業を引き継ぎます。 アセンブリとすべてのアプリケーション データ ファイルを保持することでアプリケーションの分離にも役立ちますをキャッシュし、その個々 のバージョンを互いから分離します。 たとえば、アップグレード、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]アプリケーションでは、バージョンとそのデータ リソースをキャッシュに独自のディレクトリに付属します。

## <a name="cache-storage-quota"></a>キャッシュの記憶域のクォータ
 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] オンラインでホストされているアプリケーションに占有できる領域の量のサイズを制限するクォータによって制限されますが、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]キャッシュします。 キャッシュ サイズはすべてのユーザーのオンライン アプリケーションに適用されます。1 つの部分的に信頼された、オンライン アプリケーションでは、クォータの容量の半分を占有しているに制限されます。 インストールされているアプリケーションでは、キャッシュのサイズによる制限はありませんし、キャッシュ制限としてはカウントされません。 すべての[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]のみ現在のバージョンと以前にインストールされたバージョン、アプリケーション、キャッシュが保持されます。

 既定では、クライアント コンピューターがある 250 MB の記憶域のオンライン[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]アプリケーション。 データ ファイルは、この制限にカウントされません。 システム管理者を拡大またはレジストリ キーを変更することで特定のクライアント コンピューターでは、このクォータを削減できます**HKEY_CURRENT_USER\Software\Classes\Software\Microsoft\Windows\CurrentVersion\Deployment\OnlineAppQuotaInKB**、これは、キャッシュのサイズ (キロバイト単位) を表す DWORD 値です。 たとえば、50 mb のキャッシュ サイズを減らす、この値を 51200 を変更します。

## <a name="see-also"></a>関連項目
- [ClickOnce アプリケーションにおけるローカル データおよびリモート データへのアクセス](../deployment/accessing-local-and-remote-data-in-clickonce-applications.md)