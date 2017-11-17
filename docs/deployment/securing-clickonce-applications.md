---
title: "ClickOnce アプリケーションをセキュリティで保護する |Microsoft ドキュメント"
ms.custom: 
ms.date: 02/17/2017
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-deployment
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- Windows applications, ClickOnce security
- ClickOnce deployment, security
- deploying applications, ClickOnce security
ms.assetid: a05b5f2f-d1f2-471a-8096-8b11f7554265
caps.latest.revision: "45"
author: stevehoag
ms.author: shoag
manager: wpickett
ms.openlocfilehash: 331cdf8ddc449ea8d1d29af346b8f7faea549c00
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/27/2017
---
# <a name="securing-clickonce-applications"></a>ClickOnce アプリケーションのセキュリティ
[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションは、保護されているリソースや操作に対して、コードが持つアクセス権を制限できるようにするための .NET Framework のコード アクセス セキュリティ制約を前提としています。 このため、コード アクセス セキュリティの影響を理解し、それに応じて [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションを作成することが重要です。 アプリケーションでは、完全な信頼ゾーンまたは部分信頼ゾーン (インターネット ゾーンとイントラネット ゾーンなど) を使用して、アクセスを制限できます。  
  
 さらに、ClickOnce では、アプリケーションの発行元の信頼性を検証し、アプリケーションおよび配置マニフェストに署名してファイルが改ざんされていないことを証明するときに証明書を使用します。 署名を行うと、マニフェストの生成後にアプリケーション ファイルをより簡単に変更できるようになりますが、署名は省略可能な手順です。 ただし、署名付きマニフェストがないと、アプリケーション インストーラーが man-in-the-middle セキュリティ攻撃で改ざんされないようにすることが難しくなります。 したがって、アプリケーションをセキュリティで保護するために、アプリケーション マニフェストと配置マニフェストに署名することをお勧めします。  
  
## <a name="zones"></a>ゾーン  
 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] テクノロジを使用して配置されるアプリケーションは、セキュリティ ゾーンで定義されている一連のアクセス許可と操作に制限されます。 セキュリティ ゾーンは Internet Explorer で定義され、アプリケーションの場所に基づいています。 配置場所によって異なる既定のアクセス許可を次の表に示します。  
  
|配置場所|セキュリティ ゾーン|  
|-------------------------|-------------------|  
|Web からの実行|インターネット ゾーン|  
|Web からのインストール|インターネット ゾーン|  
|ネットワーク ファイル共有からのインストール|ローカル イントラネット ゾーン|  
|CD-ROM からのインストール|Full Trust|  
  
 既定のアクセス許可は、アプリケーションの元のバージョンがどこから配置されたかによって異なります。このアプリケーションを更新する際、そのアクセス許可が継承されます。 アプリケーションが Web またはネットワーク上の場所からの更新プログラムをチェックするように構成されていて、新しいバージョンが使用できるようになっている場合には、元のインストールが完全信頼のアクセス許可ではなく、インターネット ゾーンまたはイントラネット ゾーンのアクセス許可を継承する可能性があります。 ユーザーに対する要求が行われないようにするために、システム管理者は、信頼された発行元として特定のアプリケーション発行元を定義する ClickOnce 配置ポリシーを指定できます。 このポリシーが配置されるコンピューター上では、アクセス許可は自動的に付与され、ユーザーへの要求は行われません。 詳細については、「 [Trusted Application Deployment Overview](../deployment/trusted-application-deployment-overview.md)」を参照してください。 信頼されたアプリケーションの配置を構成するには、コンピューター レベルまたはエンタープライズ レベルに証明書をインストールできます。 詳細については、「 [How to: Add a Trusted Publisher to a Client Computer for ClickOnce Applications](../deployment/how-to-add-a-trusted-publisher-to-a-client-computer-for-clickonce-applications.md)」を参照してください。  
  
## <a name="code-access-security-policies"></a>コード アクセス セキュリティ ポリシー  
 アプリケーションのアクセス許可が、設定によって決まりますが、 [ \<trustInfo > 要素](../deployment/trustinfo-element-clickonce-application.md)アプリケーション マニフェストの要素。 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] では、プロジェクトの **"セキュリティ"** プロパティ ページの設定に基づいて、この情報が自動的に生成されます。 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションには、アプリケーションが要求するアクセス許可だけが与えられます。 たとえば、ファイルへのアクセスに完全信頼のアクセス許可が必要な場合、アプリケーションがファイルへのアクセス許可を要求すると、完全信頼ではなくファイルへのアクセス許可だけが与えられます。 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションを開発するときは、アプリケーションに必要な特定のアクセス許可のみを要求する必要があります。 ほとんどの場合は、インターネット ゾーンまたはローカル イントラネット ゾーンを使用して、アプリケーションを部分信頼に制限できます。 詳細については、「 [How to: Set a Security Zone for a ClickOnce Application](../deployment/how-to-set-a-security-zone-for-a-clickonce-application.md)」を参照してください。 アプリケーションにカスタムのアクセス許可が必要な場合、カスタム ゾーンを作成できます。 詳細については、「 [How to: Set Custom Permissions for a ClickOnce Application](../deployment/how-to-set-custom-permissions-for-a-clickonce-application.md)」を参照してください。  
  
 アプリケーションの配置元ゾーンに与えられた既定のアクセス許可セットに含まれないアクセス許可を追加した場合、エンド ユーザーに対して、インストール時または更新時にアクセス許可の付与を求めるプロンプトが表示されます。 ユーザーに対する要求が行われないようにするために、システム管理者は、信頼された発行元として特定のアプリケーション発行元を定義する ClickOnce 配置ポリシーを指定できます。 このポリシーが配置されるコンピューター上では、アクセス許可は自動的に付与され、ユーザーへの要求は行われません。  
  
 開発者は、開発するアプリケーションが適切なアクセス許可で実行されることを確認する必要があります。 実行時にアプリケーションでゾーン以外のアクセス許可が必要な場合、セキュリティの例外が表示されることがあります。 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] によって、対象のセキュリティ ゾーンでアプリケーションをデバッグできます。 また、セキュリティで保護されたアプリケーションの開発に役立ちます。 詳細については、「 [How to: Debug a ClickOnce Application with Restricted Permissions](../deployment/how-to-debug-a-clickonce-application-with-restricted-permissions.md)」を参照してください。  
  
 コード アクセス セキュリティと ClickOnce の詳細については、「 [Code Access Security for ClickOnce Applications](../deployment/code-access-security-for-clickonce-applications.md)」を参照してください。  
  
## <a name="code-signing-certificates"></a>証明書のコード署名  
 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] による配置を使用するアプリケーションを発行するには、アプリケーション マニフェストと配置マニフェストに公開キーと秘密キーのペアを使用して署名できます。 マニフェストに署名するツールは、 **プロジェクト デザイナー** の **[署名]**ページで使用できます。 詳細については、「 [Signing Page, Project Designer](../ide/reference/signing-page-project-designer.md)」を参照してください。 別の方法として、発行ウィザードを使用して、発行プロセスの最中にキー ファイルでマニフェストに署名することもできます。  
  
 マニフェストの署名後、Authenticode 署名に基づいた発行元情報は、インストール時に [アクセス許可] ダイアログ ボックスに表示され、アプリケーションが信頼された発行元から発行されていることをユーザーに示します。  
  
 ClickOnce と証明書の詳細については、「 [ClickOnce and Authenticode](../deployment/clickonce-and-authenticode.md)」を参照してください。  
  
## <a name="aspnet-form-based-authentication"></a>ASP.NET フォーム ベースの認証  
 各ユーザーがアクセスできる配置を制御する場合は、Web サーバーに配置される [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションに対する匿名アクセスを許可しないでください。 代わりに Windows 認証を使用して、インストールした配置に対するユーザーのアクセスをユーザーの ID に基づいて許可します。  
  
 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] は永続的なクッキーを使用するため、ASP.NET フォーム ベースの認証はサポートしません。このクッキーは Internet Explorer のキャッシュに存在し、ハックされる可能性があるため、セキュリティ上のリスクがあります。 このため、 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションを配置する場合、Windows 認証以外の認証シナリオはサポートされません。  
  
## <a name="passing-arguments"></a>引数の受け渡し  
 引数を [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションに渡す必要がある場合、セキュリティ上の考慮事項が増えます。 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] を使用すると、Web に配置されたアプリケーションにクエリ文字列を指定できます。 クエリ文字列は、アプリケーションを起動するための URL の末尾に一連の名前と値のペアが付加された形式になっています。  
  
 `http://servername.adatum.com/WindowsApp1.application?username=joeuser`  
  
 既定では、クエリ文字列の引数が無効になります。 これらを有効にするには、アプリケーションの配置マニフェストで `trustUrlParameters` 属性を設定する必要があります。 この値は、 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] および MageUI.exe から設定できます。 受け渡しを有効にする方法の詳細な手順のクエリ文字列を参照してください[する方法: オンライン ClickOnce アプリケーションを使用したクエリ文字列情報を取得](../deployment/how-to-retrieve-query-string-information-in-an-online-clickonce-application.md)です。  
  
 クエリ文字列を通じて取得された引数は、必ず安全であることを確認してからデータベースまたはコマンド ラインに渡してください。 安全でない引数とは、悪意のあるユーザーがアプリケーションを操作して任意のコマンドを実行できるようにするデータベースまたはコマンド ライン エスケープ文字が含まれた引数のことです。  
  
> [!NOTE]
>  クエリ文字列引数は、起動時に [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションに引数を渡す唯一の手段です。 コマンド ラインから [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションに引数を渡すことはできません。  
  
## <a name="deploying-obfuscated-assemblies"></a>難読化されたアセンブリの配置  
 Visual Studio が含まれていますが、無料[プリエンプティブの保護 - Dotfuscator Community Edition](../ide/dotfuscator/index.md)、コード難読化し、アクティブな保護対策を ClickOnce アプリケーションを保護に使用できます。  詳細については、「 [Dotfuscator Community Edition のユーザー ガイドの ClickOnce セクション](https://www.preemptive.com/dotfuscator/ce/docs/help/5.27/advanced_clickonce.html)です。

## <a name="see-also"></a>関連項目  
 [ClickOnce のセキュリティと配置](../deployment/clickonce-security-and-deployment.md)   
 [ClickOnce 配置ストラテジの選択](../deployment/choosing-a-clickonce-deployment-strategy.md)