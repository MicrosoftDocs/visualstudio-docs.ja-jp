﻿---
title: '[セキュリティ] ページ (プロジェクト デザイナー) | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- vb.ProjectPropertiesSecurity
- vb.XBAPProjectPropertiesSecurity
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- Project Designer, Security page
- Security page in Project Designer
ms.assetid: 641d9cd3-fa07-498a-8568-3c169bb4d3d5
caps.latest.revision: 40
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: cc6c7af3732f2f96ad53651b146898b655b68fdd
ms.sourcegitcommit: 53aa5a413717a1b62ca56a5983b6a50f7f0663b3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59647928"
---
# <a name="security-page-project-designer"></a>[セキュリティ] ページ (プロジェクト デザイナー)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

**プロジェクト デザイナー**の **[セキュリティ]** ページを使用して、[!INCLUDE[ndptecclick](../../includes/ndptecclick-md.md)] 配置によって配置されたアプリケーションのコード アクセス セキュリティの設定を構成できます。 詳細については、「[ClickOnce アプリケーションのコード アクセス セキュリティ](../../deployment/code-access-security-for-clickonce-applications.md)」を参照してください。  
  
 この **[セキュリティ]** ページにアクセスするには、**ソリューション エクスプローラー**でプロジェクト ノードを選択し、**[プロジェクト]** メニューの **[プロパティ]** をクリックします。 **プロジェクト デザイナー**が表示されたら、**[セキュリティ]** タブをクリックします。  
  
## <a name="security-settings"></a>セキュリティ設定  
 **[ClickOnce セキュリティ設定を有効にする]**  
 セキュリティ設定をデザイン時に有効にするかどうかを指定します。 このオプションがオフの場合は、**[セキュリティ]** ページの他のオプションもすべて無効になります。  
  
> [!NOTE]
>  **発行**ウィザードを使用してアプリケーションを発行するときは、このオプションが自動的に有効になります。  
  
 このオプションをオンにすると、2 つのオプション ボタン **[これは完全に信頼するアプリケーションです]** と **[これは部分的に信頼するアプリケーションです]** のいずれかを選択できるようになります。  
  
 WPF Web ブラウザー アプリケーション プロジェクトでは、このオプションは既定でオンになります。  
  
 それ以外のすべての種類のプロジェクトでは、このオプションは既定でオフになります。  
  
 **[これは完全に信頼するアプリケーションです]**  
 このオプションをオンにすると、アプリケーションをクライアント コンピューターにインストールしたり実行したりするときに、完全信頼のアクセス許可が要求されます。 ファイル システムやレジストリなどのリソースへの無制限のアクセス許可がアプリケーションに与えられるため、完全信頼の使用はできるだけ避けてください。  
  
 WPF Web ブラウザー アプリケーション プロジェクトでは、このオプションは既定で部分信頼に設定されます。  
  
 それ以外のすべての種類のプロジェクトでは、このオプションは既定で完全信頼に設定されます。  
  
 **部分的に信頼するアプリケーション**  
 このオプションをオンにすると、アプリケーションをクライアント コンピューターにインストールしたり実行したりするときに、部分信頼アクセス許可が要求されます。 *部分信頼*とは、要求したコード アクセス セキュリティ許可で許可されたアクションのみが実行されることを意味します。 セキュリティ アクセス許可の構成方法の詳細については、「[ClickOnce アプリケーションのコード アクセス セキュリティ](../../deployment/code-access-security-for-clickonce-applications.md)」を参照してください。  
  
 部分信頼セキュリティの設定は、**[ClickOnce セキュリティのアクセス許可]** 領域のオプションを構成することで指定できます。  
  
## <a name="clickonce-security-permissions"></a>ClickOnce セキュリティのアクセス許可  
 **[アプリケーションがインストールされるゾーン]**  
 コード アクセス セキュリティのアクセス許可の既定のセットを指定します。 制限されたアクセス許可セットを使用するには **[インターネット]** または **[ローカル イントラネット]** を選択し、カスタムのアクセス許可セットを設定するには **[(カスタム)]** を選択します。 ゾーンで付与されているよりも多くのアクセス許可がアプリケーションで要求された場合、エンド ユーザーのアクセス許可を追加するために、ClickOnce 信頼プロンプトが表示されます。 セキュリティ アクセス許可の構成方法の詳細については、「[ClickOnce アプリケーションのコード アクセス セキュリティ](../../deployment/code-access-security-for-clickonce-applications.md)」を参照してください。  
  
 WPF Web ブラウザー アプリケーション プロジェクトでは、このオプションは既定で **[インターネット]** に設定されます。  
  
 **アクセス許可 XML の編集**  
 **[(カスタム)]** アクセス許可セットのアクセス許可を構成するには、アプリケーション マニフェスト テンプレート (app.manifest) を開きます。  
  
 **詳細設定**  
 [[セキュリティの詳細設定]](../../ide/reference/advanced-security-settings-dialog-box.md) ダイアログ ボックスが開きます。このダイアログ ボックスでは、制限されたアクセス許可でのアプリケーションのデバッグ用の設定を構成できます。 これらの設定はデバッグ中にチェックされます。アクセス許可例外は、ゾーンで定義されているよりも多くのアクセス許可をアプリケーションが必要としている可能性があることを示します。  
  
## <a name="see-also"></a>関連項目
 <xref:System.Security.Permissions.WebBrowserPermission>   
 <xref:System.Security.Permissions.MediaPermission>   
 [ClickOnce アプリケーションのコード アクセス セキュリティ](../../deployment/code-access-security-for-clickonce-applications.md)   
 [方法: ClickOnce のセキュリティ設定を有効にします。](../../deployment/how-to-enable-clickonce-security-settings.md)   
 [方法: ClickOnce アプリケーションのセキュリティ ゾーンを設定します。](../../deployment/how-to-set-a-security-zone-for-a-clickonce-application.md)   
 [方法: ClickOnce アプリケーションのカスタム アクセス許可の設定](../../deployment/how-to-set-custom-permissions-for-a-clickonce-application.md)   
 [方法: 制限されたアクセス許可を使用して ClickOnce アプリケーションをデバッグします。](../../deployment/how-to-debug-a-clickonce-application-with-restricted-permissions.md)   
 [ClickOnce のセキュリティと配置](../../deployment/clickonce-security-and-deployment.md)   
 [プロジェクトのプロパティのリファレンス](../../ide/reference/project-properties-reference.md)   
 [[セキュリティの詳細設定] ダイアログ ボックス](../../ide/reference/advanced-security-settings-dialog-box.md)
