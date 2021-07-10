---
title: 多要素認証が必要なアカウントを使用する
ms.date: 05/27/2020
ms.custom: SEO-VS-2020
ms.topic: conceptual
description: 多要素認証が必要なアカウントで Visual Studio を使用する方法を説明します。
author: j-martens
ms.author: jmartens
manager: jmartens
ms.workload:
- multiple
monikerRange: '>=vs-2019'
ms.openlocfilehash: 9ac42ccff8c7bffcc22c453002aad1caf6935d28
ms.sourcegitcommit: e4630a3bb89b4d606fe2cbd709bc773c5b538b78
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/26/2021
ms.locfileid: "112975673"
---
# <a name="how-to-use-visual-studio-with-accounts-that-require-multi-factor-authentication"></a>多要素認証が必要なアカウントで Visual Studio を使用する方法

外部のゲスト ユーザーとコラボレーションするときは、**多要素認証 (MFA)** などの **条件付きアクセス (CA)** ポリシーを使用して貴社のアプリとデータを保護することをお勧めします。  

有効にすると、ゲスト ユーザーはリソースにアクセスするためにユーザー名とパスワードだけでなく、追加のセキュリティ要件を満たす必要があります。 MFA ポリシーは、組織のメンバーに対して有効にするのと同じ方法で、テナント レベル、アプリ レベル、または個々のゲスト ユーザー レベルで適用できます。 

## <a name="how-is-the-visual-studio-experience-affected-by-mfa-policies"></a>MFA ポリシーによって Visual Studio のエクスペリエンスはどのような影響を受けますか。
16.6 より前のバージョンの Visual Studio では、MFA などの CA ポリシーが有効になっていて、2 つ以上のテナントに関連付けられているアカウントで使用した場合、認証エクスペリエンスが低下する可能性があります。

これらの問題により、Visual Studio のインスタンスで再認証が 1 日に複数回要求される可能性があります。 同じ Visual Studio セッション中であっても、以前に認証されたテナントの資格情報の再入力が必要な場合があります。

## <a name="using-visual-studio-with-mfa-policies"></a>MFA ポリシーでの Visual Studio の使用
16.6 リリースでは、Visual Studio 2019 に新しい機能が追加されました。これにより、ユーザーが MFA などの CA ポリシーで保護されたリソースにアクセスする方法が合理化されます。 この強化されたワークフローを使用するには、Visual Studio アカウントを追加および再認証するためのメカニズムとして、システムの既定の Web ブラウザーを使用することを選択する必要があります。  

> [!WARNING]
> このワークフローを使用しないとエクスペリエンスが低下し、Visual Studio アカウントを追加または再認証するときに複数の追加の認証を求められる可能性があります。 

### <a name="enabling-system-web-browser"></a>システム Web ブラウザーを有効にする

> [!NOTE] 
> 最良のエクスペリエンスを実現するために、このワークフローに進む前に、システムの既定の Web ブラウザー データをクリアすることをお勧めします。 また、Windows 10 設定の **[職場または学校にアクセスする]** に職場または学校アカウントがある場合は、それらが適切に認証されていることを確認してください。

このワークフローを有効にするには、Visual Studio の [オプション] ダイアログ **([ツール] > [オプション...])** に移動し、 **[アカウント]** タブを選択し、 **[次を使用してアカウントを追加および再認証する:]** ドロップダウンで **[System web browser] (システム Web ブラウザー)** を選択します。 

:::image type="content" source="media/select-system-web-browser.png" alt-text="メニューからシステム Web ブラウザーを選択します。":::

### <a name="sign-into-additional-accounts-with-mfapolicies"></a>MFA ポリシーを使用して追加アカウントにサインインする 
システム Web ブラウザー ワークフローを有効にしたら、[アカウント設定] ダイアログ **([ファイル] > [アカウントの設定...])** を使用して、通常のように Visual Studio にサインインまたはアカウントを追加できます。   
</br>
:::image type="content" source="media/add-personalization-account.png" alt-text="新しい個人アカウントを Visual Studio に追加します。" border="false":::

この操作により、システムの既定の Web ブラウザーが開き、アカウントへサインインが求められ、必要な MFA ポリシーが検証されます。

サインイン中、サインイン状態を維持するかどうかを問う、追加のプロンプトが表示されることがあります。 このプロンプトは、あるアカウントをサインインに使用することが 2 回目になるときに表示されることがあります。 資格情報を再入力する必要性を最小限に抑えるため、 **[はい]** を選択することをお勧めします。[はい] を選択すると、ブラウザー セッション間で資格情報が保持されます。

:::image type="content" source="media/kmsi.png" alt-text="サインインの状態を維持しますか?":::

開発アクティビティとリソース構成に基づいて、セッション中に資格情報を再入力するように求められる場合があります。 これは、新しいリソースを追加したとき、または以前に CA/MFA の認可要件を満たしていないリソースにアクセスしようとしたときに発生する可能性があります。

## <a name="reauthenticating-an-account"></a>アカウントの再認証  
アカウントに問題がある場合、Visual Studio によってアカウントの資格情報の再入力を求めるメッセージが表示されることがあります。  

:::image type="content" source="media/reauthenticate-account.png" alt-text="Visual Studio アカウントを再認証します。":::

**[資格情報を再入力してください]** をクリックすると、システムの既定の Web ブラウザーが開き、資格情報の自動更新が試みられます。 失敗した場合は、アカウントにサインインし、必要な CA/MFA ポリシーを検証するよう求められます。

> [!NOTE] 
> 最適なエクスペリエンスを実現するために、すべての CA/MFA ポリシーがリソースに対して検証されるまで、ブラウザーを開いたままにしておいてください。 ブラウザーを閉じると、以前に構築した MFA 状態が失われ、追加の認可プロンプトが表示される場合があります。

## <a name="how-to-opt-out-of-using-a-specific-azure-active-directory-tenant-in-visual-studio"></a>Visual Studio で特定の Azure Active Directory テナントの使用をオプトアウトする方法

Visual Studio 2019 バージョン 16.6 には、テナントを個別に、またはグローバルに除外して、Visual Studio で実質的に非表示にする柔軟性があります。 フィルターを適用すると、そのテナントで認証する必要がなくなりますが、関連付けられているリソースにはアクセスできなくなります。

この機能は、複数のテナントがあり、特定のサブセットをターゲットにして開発環境を最適化する場合に便利です。 問題のあるテナントをフィルターで除外できるため、特定の CA/MFA ポリシーを検証できない場合にも役立ちます。 

### <a name="how-to-filter-out-all-tenants"></a>テナントをすべて除外する方法
すべてのテナントをグローバルにフィルターで除外するには、[アカウント設定] ダイアログ **([ファイル] > [アカウント設定])** を開き、 **[Authenticate Across all Azure Active Directories]** \(すべての Azure Active Directories で認証する\) チェックボックスをオフにします。

このオプションをオフにすると、アカウントの既定のテナントでのみで認証されます。 また、お使いのアカウントが、ゲストになっている可能性のある他のテナントに関連付けられているすべてのリソースにアクセスできないことも意味します。

### <a name="how-to-filter-out-individual-tenants"></a>個々のテナントをフィルター処理する方法
Visual Studio アカウントに関連付けられているテナントをフィルター処理するには、[アカウントの設定] ダイアログ **([ファイル] >[アカウントの設定...])** を開き、 **[フィルターの適用]** をクリックします。 
</br>
</br>

:::image type="content" source="media/apply-filter.png" alt-text="フィルターを適用します。" border="false":::

**[Filter account] (アカウントのフィルター処理)** ダイアログが表示され、アカウントで使用するテナントを選択できます。 

:::image type="content" source="media/select-filter-account.png" alt-text="フィルターを適用するアカウントを選択します。":::

## <a name="see-also"></a>関連項目

- [Visual Studio へのサインイン](signing-in-to-visual-studio.md)
- [Visual Studio for Mac にサインインする](/visualstudio/mac/signing-in)
- [複数のユーザー アカウントを使って作業する](work-with-multiple-user-accounts.md)
