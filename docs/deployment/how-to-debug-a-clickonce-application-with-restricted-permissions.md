---
title: '方法: ClickOnce アプリケーションをデバッグ アクセス許可の制限 |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- debugging [Visual Studio], ClickOnce applications
- ClickOnce deployment, debugging
- ClickOnce applications, debugging
ms.assetid: 6991ea91-5253-451b-923d-22273a3d38b1
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2f913a5981e16f067dd10836c78485d635a35052
ms.sourcegitcommit: d0425b6b7d4b99e17ca6ac0671282bc718f80910
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 02/21/2019
ms.locfileid: "56636932"
---
# <a name="how-to-debug-a-clickonce-application-with-restricted-permissions"></a>方法: アクセス許可が制限された ClickOnce アプリケーションをデバッグする
通常、開発用コンピューターは完全信頼アクセス許可で実行するので、ClickOnce アプリケーションのデバッグ時には、エンド ユーザーが制限されたアクセス許可でアプリケーションを実行したときと同じセキュリティ例外は発生しません。

 これらの例外をキャッチするには、開発者はエンドユーザーと同じアクセス許可を使用してアプリケーションをデバッグする必要があります。 制限されたアクセス許可でのデバッグは、 **プロジェクト デザイナー** の **セキュリティ**ページで有効にすることができます。

 さらに、Web サービスを呼び出すアプリケーションを開発するときは、通常、これらの Web サービスは開発用コンピューターに存在します。 配置後には、エンド ユーザーはこれらの Web サービスに異なる URL からアクセスします。 デバッグ中にエンド ユーザー エクスペリエンスをエミュレートするには、URL を指定すると、デバッガーはその URL から呼び出されているかのように Web サービスを扱います。

### <a name="to-enable-debugging-with-restricted-permissions"></a>制限されたアクセス許可でのデバッグを有効にするには

1.  **ソリューション エクスプ ローラー**でプロジェクトを選択し、 **[プロジェクト]** メニューの **[プロパティ]** をクリックします。

2.  **プロジェクト デザイナー**で、 **[セキュリティ]** タブをクリックします。

3.  **[ClickOnce セキュリティ設定を有効にする]** チェック ボックスをオンにし、 **[これは部分的に信頼するアプリケーションです]** オプション ボタンをクリックします。

4.  **[詳細設定]** ボタンをクリックします。

5.  **[選択されたアクセス許可セットでこのアプリケーションをデバッグする]** チェック ボックスをオンにし、 **[OK]** をクリックします。

     アプリケーションのデバッグ時に、アクセス許可セットに含まれないアクセス許可にアクセスしようとすると、セキュリティ例外が発生します。

### <a name="to-specify-a-url-for-debugging"></a>デバッグ用の URL を指定するには

1.  **ソリューション エクスプローラー**でプロジェクトを選択し、 **[プロジェクト]** メニューの **[プロパティ]** をクリックします。

2.  **プロジェクト デザイナー**で、 **[セキュリティ]** タブをクリックします。

3.  **[ClickOnce セキュリティ設定を有効にする]** チェック ボックスをオンにし、 **[これは部分的に信頼するアプリケーションです]** オプション ボタンをクリックします。

4.  **[詳細設定]** ボタンをクリックします。

5.  **[選択されたアクセス許可セットでこのアプリケーションをデバッグする]** チェック ボックスをオンにし、 **[OK]** をクリックします。

6.  **[このアプリケーションが次の URL からダウンロードされたと仮定してデバッグする]** テキスト ボックスに、URL またはネットワーク パスを入力します。

## <a name="see-also"></a>関連項目
- [方法: ClickOnce アプリケーションのカスタム アクセス許可を設定する](../deployment/how-to-set-custom-permissions-for-a-clickonce-application.md)
- [ClickOnce アプリケーションのセキュリティ保護](../deployment/securing-clickonce-applications.md)
- [ClickOnce アプリケーションのコード アクセス セキュリティ](../deployment/code-access-security-for-clickonce-applications.md)
- [ClickOnce アプリケーションのセキュリティ保護](../deployment/securing-clickonce-applications.md)