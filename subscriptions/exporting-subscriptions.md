---
title: サブスクリプション情報のエクスポート | Microsoft Docs
author: evanwindom
ms.author: jaunger
manager: evelynp
ms.date: 03/14/2018
ms.topic: conceptual
description: サブスクライバーの一覧とサブスクリプションの割り当ての詳細をエクスポートする方法について説明します。
ms.openlocfilehash: 02081a0b36b2baf769396c13a2ae69f9af5be58b
ms.sourcegitcommit: 208395bc122f8d3dae3f5e5960c42981cc368310
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/10/2019
ms.locfileid: "67783503"
---
# <a name="exporting-subscription-information"></a>サブスクリプション情報のエクスポート

Visual Studio サブスクリプションの[管理ポータル](https://manage.visualstudio.com)では、ユーザーの一覧とその割り当てに関する詳細情報をエクスポートできます。 この情報には、名前、メール アドレス、連絡用メール アドレス、サブスクリプション レベル、割り当て日、ライセンス認証の状態、有効期限、参照フィールド、有効なダウンロード、国、言語、サブスクリプションの状態、サブスクリプション GUID が含まれます。

この機能は、割り当てや有効期限の追跡をはじめ、いくつかのシナリオで役立ちます。 たとえば、BAN から GUID の使用に切り替えてサブスクリプションの割り当てを追跡する場合、このレポートと Microsoft Excel の VLOOKUP 式を使用して、サブスクライバーを適切に照合することができます。

**[エクスポート]** タブを選択するだけでエクスポートが実行され、ファイルはローカル コンピューターにダウンロードされます。 このファイルには、ユーザー サブスクリプションを含む割り当ての名前と、エクスポートの日付が含まれます。
> [!div class="mx-imgBorder"]
> ![サブスクライバーのエクスポート](_img/exporting-subscriptions/exporting-subscriptions.png)
