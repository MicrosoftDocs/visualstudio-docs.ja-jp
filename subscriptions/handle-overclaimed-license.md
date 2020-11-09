---
title: Visual Studio サブスクリプションでライセンスの割り当て超過を処理する | Microsoft Docs
author: evanwindom
ms.author: v-evwin
manager: cabuschl
ms.assetid: a747100c-6f08-41a4-aaad-05099741742b
ms.date: 10/28/2020
ms.topic: conceptual
description: サブスクリプションの割り当て超過を管理者が解決する方法について説明します
ms.openlocfilehash: bf3c23cad87dc88b24bae3e8b31ebf8b7d9e1dfe
ms.sourcegitcommit: f1d47655974a2f08e69704a9a0c46cb007e51589
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/28/2020
ms.locfileid: "92904297"
---
# <a name="over-allocated-subscriptions"></a>サブスクリプションの割り当て超過
サブスクライバーを追加した後に、注文が変更される場合があります。これにより会社が所有するライセンス数よりも割り当てられたサブスクリプションが多くなる場合があります。 これは "割り当て超過" と呼ばれます。  

ご利用のサブスクリプションの割り当てを表示するには、左上にあるアイコンをクリックして、割り当てウィンドウを開きます。  

> [!NOTE]
> Open License プログラムでは割り当て超過は許可されません。  また、他のプログラムでは、ポータルにこの情報を別の方式で表示できます。
>
> [!div class="mx-imgBorder"]
> ![過剰に要求されたサブスクリプションの通知](_img/over-claimed/over-claimed-alert.png "割り当て超過の数は概要に一覧表示され、サブスクリプションの種類ごとに、グラフのハッシュされたバーで表されます。")

表示ではハッシュされたバーを使用して、サブスクリプションの割り当て超過が示されていることに注目してください。  すべてのサブスクリプションの種類全体での割り当て超過の数は、上部の [概要] セクションにあります。また、サブスクリプション レベルごとに、固有の割り当て状態も表示されます。  

## <a name="resolve-over-allocated-subscriptions"></a>サブスクリプションの割り当て超過を解決する
割り当て超過を解決するには、次のようにいくつかの方法があります。
- 再販業者に連絡して追加のサブスクリプションを購入します。
- 年次補正期間まで待って、その時点で割り当て超過のサブスクリプションの支払いを行います。 
- 一部のサブスクリプションの割り当てを削除します  (この場合、補正は年度の任意の時点で割り当てられたサブスクリプション最大数に基づいているため、年次補正の時点で支払いが必要になります)。

## <a name="billing-and-true-up"></a>課金とトゥルーアップ
組織に Enterprise Agreement (EA) がある場合、管理者はサブスクリプションを購入せずに割り当てて、後で "トゥルーアップ" と呼ばれる調整プロセスを通して支払うことができます。  割り当て超過が生じると、組織は、"トゥルーアップ" 中にユーザーに割り当てられているサブスクリプションの最大数に対して課金されます。  トゥルーアップの実行時に割り当てられているサブスクリプションが最大数未満になっている場合でも、このことは当てはまります。  最大使用量の監視の詳細については、[最大使用量](maximum-usage.md)に関するトピックを参照してください。


## <a name="see-also"></a>関連項目
- [Visual Studio ドキュメント](/visualstudio/)
- [Azure DevOps ドキュメント](/azure/devops/)
- [Azure ドキュメント](/azure/)
- [Microsoft 365 ドキュメント](/microsoft-365/)

## <a name="next-steps"></a>次の手順
- [Visual Studio Subscriptions with GitHub Enterprise](assign-github.md) の管理に関する詳細情報をご覧ください。
- Visual Studio サブスクリプションの販売、サブスクリプション、アカウント、課金のサポートについては、Visual Studio [サブスクリプション サポート](https://visualstudio.microsoft.com/subscriptions/support/)にお問い合わせください。