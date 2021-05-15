---
title: カスタムのアクセス許可を設定する (ClickOnce アプリ)
description: 既定のアクセス許可を使用する ClickOnce アプリケーションを配置する方法と、アプリケーションで必要とされる特定のアクセス許可向けにカスタム ゾーンを作成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce applications, permissions
- permissions, ClickOnce applications
ms.assetid: 660459ca-ef73-44a8-b323-610001f63b93
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 2050f3534caba8aba12fa8550eb6e573a3d0db08
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99885041"
---
# <a name="how-to-set-custom-permissions-for-a-clickonce-application"></a>方法: ClickOnce アプリケーションのカスタム アクセス許可を設定する
インターネット ゾーンまたはローカル イントラネット ゾーンの既定のアクセス許可を使用する [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションを配置できます。 または、アプリケーションに必要な特定のアクセス許可用にカスタム ゾーンを作成することもできます。 そのためには、 **プロジェクト デザイナー** の **[セキュリティ]** ページでセキュリティのアクセス許可をカスタマイズします。

### <a name="to-customize-a-permission"></a>アクセス許可をカスタマイズするには

1. **ソリューション エクスプローラー** でプロジェクトを選択し、 **[プロジェクト]** メニューの **[プロパティ]** をクリックします。

2. **[セキュリティ]** タブをクリックします。

3. **[ClickOnce セキュリティ設定を有効にする]** チェック ボックスをオンにします。

4. **[これは部分的に信頼するアプリケーションです]** オプション ボタンを選択します。

     **[ClickOnce セキュリティのアクセス許可]** セクション内のコントロールが有効になります。

5. **[アプリケーションのインストール元のゾーン]** ドロップダウン リストの **[(カスタム)]** を選択します。

6. **[アクセス許可 XML の編集]** をクリックします。

     XML エディターで *app.manifest* ファイルが開きます。

7. `</applicationRequestMinimum>` 要素の前に、アプリケーションに必要なアクセス許可の XML コードを追加します。

    > [!NOTE]
    > アクセス許可セットの `ToXml` メソッドを使用して、アプリケーション マニフェスト用の XML コードを生成できます。 たとえば、 <xref:System.Security.Permissions.EnvironmentPermission> アクセス許可セットの XML を生成するには、 <xref:System.Security.Permissions.EnvironmentPermission.ToXml%2A> メソッドを呼び出します。

## <a name="see-also"></a>関連項目
- [ClickOnce アプリケーションのセキュリティ保護](../deployment/securing-clickonce-applications.md)
- [ClickOnce アプリケーションのコード アクセス セキュリティ](../deployment/code-access-security-for-clickonce-applications.md)
