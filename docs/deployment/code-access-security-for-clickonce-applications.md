---
title: ClickOnce アプリケーションのコード アクセス セキュリティ | Microsoft Docs
description: ClickOnce アプリケーションのコード アクセス セキュリティと、コード アクセス セキュリティのアクセス許可を構成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vb.XBAPProjectPropertiesSecurity.HowTo
- vb.XBAProjectPropertiesSecurity.HowTo
- vb.ProjectPropertiesSecurity.HowTo
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- deploying applications [ClickOnce], security
- ClickOnce applications, caspol
- security [ClickOnce], WPF browser-hosted applications
- security [ClickOnce], ClickOnce applications
- ClickOnce applications, code access security policies
- security, ClickOnce
ms.assetid: 04b104d0-0bd3-4ccb-b164-1de92d234487
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 4bf2977b3b6875a7dc38711b235f5848aa78559e
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99889162"
---
# <a name="code-access-security-for-clickonce-applications"></a>ClickOnce アプリケーションのコード アクセス セキュリティ
ClickOnce アプリケーションは、.NET Framework に基づいており、コード アクセス セキュリティ制約の対象です。 このため、コード アクセス セキュリティの影響を理解し、それに応じて ClickOnce アプリケーションを作成することが重要です。

 コード アクセス セキュリティとは、保護されているリソースや操作に対して、コードが持つアクセス権を制限できるようにするための .NET Framework の機構です。 アプリケーションのインストーラーの場所に適切なゾーンを使用するには、ClickOnce アプリケーションのコード アクセス セキュリティのアクセス許可を構成する必要があります。 ほとんどの場合、一連のアクセス許可を制限する **インターネット** ゾーンまたは一連のより多くのアクセス許可を与える **ローカル イントラネット** ゾーンを選択できます。

## <a name="default-clickonce-code-access-security"></a>既定の ClickOnce コード アクセス セキュリティ
 既定では、ClickOnce アプリケーションは、クライアント コンピュータへインストールされる際、またはクライアント コンピュータで実行される際に、完全な信頼アクセス許可を受けます。

- 完全信頼アクセス許可のあるアプリケーションは、ファイル システムやレジストリなどのリソースに無制限にアクセスします。 このためご使用のアプリケーション (およびエンド ユーザーのシステム) が悪意のあるコードによって不当に利用される可能性があります。

- アプリケーションに完全な信頼アクセス許可が必要な場合、エンド ユーザーにアプリケーションにアクセス許可を付与するよう求めるプロンプトが表示されることがあります。 これはアプリケーションが実際には ClickOnce エクスペリエンスを提供していないことを示しており、このプロンプトによって経験の少ないユーザーが混乱してしまう可能性があります。

  > [!NOTE]
  > CD-ROM などのリムーバブル メディアからアプリケーションをインストールする場合、これらのプロンプトが表示されることはありません。 さらに、ユーザーが信頼できるソースからアプリケーションをインストールする場合、ネットワーク管理者はこれらのプロンプトが表示がされないようにネットワーク ポリシーを構成できます。 詳細については、「[信頼されたアプリケーションの配置の概要](../deployment/trusted-application-deployment-overview.md)」を参照してください。

  ClickOnce アプリケーションのアクセス許可を制限するためには、アプリケーションのコード アクセス セキュリティのアクセス許可を変更して、アプリケーションに必要な最適なアクセス許可ゾーンを要求できます。 ほとんどの場合、アプリケーションの配置元のゾーンを選択できます。 たとえば、アプリケーションが企業アプリケーションである場合、 **ローカル イントラネット** が使用できます。 アプリケーションがインターネット アプリケーションである場合は、 **インターネット** ゾーンが使用できます。

## <a name="configure-security-permissions"></a>セキュリティのアクセス許可を構成する
 必ずコード アクセス セキュリティのアクセス許可を制限する適切なゾーンを要求するよう ClickOnce アプリケーションを構成する必要があります。 セキュリティのアクセス許可は、 **プロジェクト デザイナー** の **セキュリティ** ページで構成できます。

 **プロジェクト デザイナー** の **セキュリティ** ページには、 **[ClickOnce セキュリティ設定を有効にする]** チェック ボックスがあります。 このチェック ボッスクを選択すると、アプリケーションの配置マニフェストにセキュリティのアクセス許可要求が追加されます。 インストール時に、要求されたアクセス許可がアプリケーションの配置元ゾーンの既定のアクセス許可を超えると、ユーザーにはアクセス許可を付与するよう求るプロンプトが表示されます。 詳しくは、「[方法: ClickOnce のセキュリティ設定を有効にする](../deployment/how-to-enable-clickonce-security-settings.md)」をご覧ください。

 異なる場所から配置されたアプリケーションには、プロンプトが表示されることなく異なるレベルのアクセス許可が付与されます。 たとえば、アプリケーションがインターネットから配置される場合は、一連のアクセス許可が高度に厳しく制限されます。 ローカル イントラネットからインストールされる場合には、より多くのアクセス許可が付与され、CD-ROM からインストールされる場合は、完全な信頼アクセス許可が与えられます。

 まず最初にアクセス許可を構成する手順として、 **セキュリティ** ページの **ゾーン** リストからセキュリティ ゾーンを選択します。 アプリケーションが複数のゾーンから配置される可能性がある場合には、最もアクセス許可の少ないゾーンを選択します。 詳しくは、「[方法: ClickOnce アプリケーションのセキュリティ ゾーンを設定する](../deployment/how-to-set-a-security-zone-for-a-clickonce-application.md)」をご覧ください。

 設定できるプロパティはアクセス許可設定によって異なります。すべてのアクセス許可設定に構成可能なプロパティがあるわけではありません。 アプリケーションが要求できるアクセス許可の全リストについては、 <xref:System.Security.Permissions>を参照してください。 カスタムのゾーンのアクセス許可を設定する方法の詳細については、「[方法: ClickOnce アプリケーションのカスタムアクセス許可を設定する](../deployment/how-to-set-custom-permissions-for-a-clickonce-application.md)」を参照してください。

## <a name="debug-an-application-that-has-restricted-permissions"></a>アクセス許可が制限されているアプリケーションをデバッグする
 開発者の場合、完全な信頼アクセス許可で開発コンピュータを実行しがちです。 そのため、開発者がアプリケーションのデバッグを行う際には、ユーザーが制限されたアクセス許可でアプリケーションを実行する際に表示されるセキュリティ例外と同じものは表示されません。

 これらの例外をキャッチするには、開発者はエンドユーザーと同じアクセス許可を使用してアプリケーションをデバッグする必要があります。 制限されたアクセス許可でのデバッグは、 **プロジェクト デザイナー** の **セキュリティ** ページで有効にすることができます。

 制限されたアクセス許可でアプリケーションをデバッグする場合、 **セキュリティ** ページで有効にされていないコード セキュリティ要求に対して例外が発生します。 例外ヘルパーが表示され、例外を防止するためのコードの変更方法に関するヒントが利用できます。

 さらに、コードを記述する場合、コード エディターの IntelliSense 機能を使用すると、構成したセキュリティ アクセス許可に含まれないすべてのメンバーが無効になります。

 詳細については、「 [How to: Debug a ClickOnce Application with Restricted Permissions](securing-clickonce-applications.md)」を参照してください。

## <a name="security-permissions-for-browser-hosted-applications"></a>ブラウザーでホストされるアプリケーションのセキュリティ アクセス許可
 Visual Studio は、Windows Presentation Foundation (WPF) アプリケーションの以下のプロジェクト タイプを提供します。

- WPF Windows アプリケーション

- WPF Web ブラウザー アプリケーション

- WPF カスタム コントロール ライブラリ

- WPF サービス ライブラリ

  これらのプロジェクト タイプのうち、WPF Web ブラウザー アプリケーションのみ Web ブラウザーでホストされており、そのため特別な配置とセキュリティ設定が必要です。 これらのアプリケーションの既定のセキュリティ設定は、次のとおりです。

- **[ClickOnce セキュリティ設定を有効にする]**

- **部分的に信頼するアプリケーション**

- **インターネット ゾーン** (選択された WPF Web ブラウザー アプリケーションに対し既定のアクセス許可が設定されているゾーン)

  **[セキュリティの詳細設定]** ダイアログ ボックスでは、 **[選択したアクセス許可でこのアプリケーションをデバッグする]** チェック ボックスが選択され、無効になっています。 これはブラウザーによってホストされるアプリケーションでは、[ゾーン内でデバッグする] をオフにできないためです。

## <a name="see-also"></a>関連項目
- [ClickOnce アプリケーションのセキュリティ保護](../deployment/securing-clickonce-applications.md)
- [方法: ClickOnce のセキュリティ設定を有効にする](../deployment/how-to-enable-clickonce-security-settings.md)
- [方法: ClickOnce アプリケーションのセキュリティ ゾーンを設定する](../deployment/how-to-set-a-security-zone-for-a-clickonce-application.md)
- [方法: ClickOnce アプリケーションのカスタム アクセス許可を設定する](../deployment/how-to-set-custom-permissions-for-a-clickonce-application.md)
- [方法: アクセス許可が制限された ClickOnce アプリケーションをデバッグする](securing-clickonce-applications.md)
- [信頼されたアプリケーションの配置の概要](../deployment/trusted-application-deployment-overview.md)
- [[セキュリティ] ページ (プロジェクト デザイナー)](../ide/reference/security-page-project-designer.md)