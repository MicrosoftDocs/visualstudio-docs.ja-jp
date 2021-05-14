---
title: ClickOnce アプリケーションの保護 | Microsoft Docs
description: ClickOnce アプリケーションのコードへのアクセスを制限できる、.NET Framework のコード アクセス セキュリティ制約の意味について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/17/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- Windows applications, ClickOnce security
- ClickOnce deployment, security
- deploying applications, ClickOnce security
ms.assetid: a05b5f2f-d1f2-471a-8096-8b11f7554265
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: aa698fc0ac0e46fa645ede54d6608b79dd031655
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99949663"
---
# <a name="secure-clickonce-applications"></a>ClickOnce アプリケーションのセキュリティ保護
[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションは、保護されているリソースや操作に対して、コードが持つアクセス権を制限できるようにするための .NET Framework のコード アクセス セキュリティ制約を前提としています。 このため、コード アクセス セキュリティの影響を理解し、それに応じて [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションを作成することが重要です。 アプリケーションでは、完全な信頼ゾーンまたは部分信頼ゾーン (インターネット ゾーンとイントラネット ゾーンなど) を使用して、アクセスを制限できます。

 さらに、ClickOnce では、アプリケーションの発行元の信頼性を検証し、アプリケーションおよび配置マニフェストに署名してファイルが改ざんされていないことを証明するときに証明書を使用します。 署名を行うと、マニフェストの生成後にアプリケーション ファイルをより簡単に変更できるようになりますが、署名は省略可能な手順です。 ただし、署名付きマニフェストがないと、アプリケーション インストーラーが man-in-the-middle セキュリティ攻撃で改ざんされないようにすることが難しくなります。 したがって、アプリケーションをセキュリティで保護するために、アプリケーション マニフェストと配置マニフェストに署名することをお勧めします。

## <a name="zones"></a>ゾーン
 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] テクノロジを使用して配置されるアプリケーションは、セキュリティ ゾーンで定義されている一連のアクセス許可と操作に制限されます。 セキュリティ ゾーンは Internet Explorer で定義され、アプリケーションの場所に基づいています。 配置場所によって異なる既定のアクセス許可を次の表に示します。

|デプロイの場所|セキュリティ ゾーン|
|-------------------------|-------------------|
|Web からの実行|インターネット ゾーン|
|Web からのインストール|インターネット ゾーン|
|ネットワーク ファイル共有からのインストール|ローカル イントラネット ゾーン|
|CD-ROM からのインストール|Full Trust|

 既定のアクセス許可は、アプリケーションの元のバージョンがどこから配置されたかによって異なります。このアプリケーションを更新する際、そのアクセス許可が継承されます。 アプリケーションが Web またはネットワーク上の場所からの更新プログラムをチェックするように構成されていて、新しいバージョンが使用できるようになっている場合には、元のインストールが完全信頼のアクセス許可ではなく、インターネット ゾーンまたはイントラネット ゾーンのアクセス許可を継承する可能性があります。 ユーザーに対する要求が行われないようにするために、システム管理者は、信頼された発行元として特定のアプリケーション発行元を定義する ClickOnce 配置ポリシーを指定できます。 このポリシーが配置されるコンピューター上では、アクセス許可は自動的に付与され、ユーザーへの要求は行われません。 詳細については、「 [Trusted Application Deployment Overview](../deployment/trusted-application-deployment-overview.md)」を参照してください。 信頼されたアプリケーションの配置を構成するには、コンピューター レベルまたはエンタープライズ レベルに証明書をインストールできます。 詳細については、「 [How to: Add a Trusted Publisher to a Client Computer for ClickOnce Applications](../deployment/how-to-add-a-trusted-publisher-to-a-client-computer-for-clickonce-applications.md)」を参照してください。

## <a name="code-access-security-policies"></a>コード アクセス セキュリティ ポリシー
 アプリケーションのアクセス許可は、アプリケーション マニフェストの [\<trustInfo> Element](../deployment/trustinfo-element-clickonce-application.md) 要素の設定によって決まります。 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] では、プロジェクトの **"セキュリティ"** プロパティ ページの設定に基づいて、この情報が自動的に生成されます。 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションには、アプリケーションが要求するアクセス許可だけが与えられます。 たとえば、ファイルへのアクセスに完全信頼のアクセス許可が必要な場合、アプリケーションがファイルへのアクセス許可を要求すると、完全信頼ではなくファイルへのアクセス許可だけが与えられます。 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションを開発するときは、アプリケーションに必要な特定のアクセス許可のみを要求する必要があります。 ほとんどの場合は、インターネット ゾーンまたはローカル イントラネット ゾーンを使用して、アプリケーションを部分信頼に制限できます。 詳しくは、「[方法: ClickOnce アプリケーションのセキュリティ ゾーンを設定する](../deployment/how-to-set-a-security-zone-for-a-clickonce-application.md)」をご覧ください。 アプリケーションにカスタムのアクセス許可が必要な場合、カスタム ゾーンを作成できます。 詳しくは、「[方法 : ClickOnce アプリケーションのカスタム アクセス許可を設定する](../deployment/how-to-set-custom-permissions-for-a-clickonce-application.md)」をご覧ください。

 アプリケーションの配置元ゾーンに与えられた既定のアクセス許可セットに含まれないアクセス許可を追加した場合、エンド ユーザーに対して、インストール時または更新時にアクセス許可の付与を求めるプロンプトが表示されます。 ユーザーに対する要求が行われないようにするために、システム管理者は、信頼された発行元として特定のアプリケーション発行元を定義する ClickOnce 配置ポリシーを指定できます。 このポリシーが配置されるコンピューター上では、アクセス許可は自動的に付与され、ユーザーへの要求は行われません。

 開発者は、開発するアプリケーションが適切なアクセス許可で実行されることを確認する必要があります。 実行時にアプリケーションでゾーン以外のアクセス許可が必要な場合、セキュリティの例外が表示されることがあります。 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] を使用すると、対象のセキュリティ ゾーン内部でアプリケーションをデバッグして、セキュリティで保護されたアプリケーションを開発できます。 詳細については、「[System.Deployment.Application を使用する ClickOnce アプリケーションのデバッグ](../deployment/debugging-clickonce-applications-that-use-system-deployment-application.md)」を参照してください。

 コード アクセス セキュリティと ClickOnce の詳細については、「[ClickOnce アプリケーションのコード アクセス セキュリティ](../deployment/code-access-security-for-clickonce-applications.md)」を参照してください。

## <a name="code-signing-certificates"></a>証明書のコード署名
 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] による配置を使用するアプリケーションを発行するには、アプリケーション マニフェストと配置マニフェストに公開キーと秘密キーのペアを使用して署名できます。 マニフェストに署名するツールは、 **プロジェクト デザイナー** の **[署名]** ページで使用できます。 詳細については、「 [Signing Page, Project Designer](../ide/reference/signing-page-project-designer.md)」を参照してください。

 マニフェストの署名後、Authenticode 署名に基づいた発行元情報は、インストール時に [アクセス許可] ダイアログ ボックスに表示され、アプリケーションが信頼された発行元から発行されていることをユーザーに示します。

 ClickOnce と証明書の詳細については、「 [ClickOnce and Authenticode](../deployment/clickonce-and-authenticode.md)」を参照してください。

## <a name="aspnet-form-based-authentication"></a>ASP.NET フォーム ベースの認証
 各ユーザーがアクセスできる配置を制御する場合は、Web サーバーに配置される [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションに対する匿名アクセスを許可しないでください。 代わりに Windows 認証を使用して、インストールした配置に対するユーザーのアクセスをユーザーの ID に基づいて許可します。

 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] は永続的なクッキーを使用するため、ASP.NET フォーム ベースの認証はサポートしません。このクッキーは Internet Explorer のキャッシュに存在し、ハックされる可能性があるため、セキュリティ上のリスクがあります。 このため、 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションを配置する場合、Windows 認証以外の認証シナリオはサポートされません。

## <a name="pass-arguments"></a>引数を渡す
 引数を [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションに渡す必要がある場合、セキュリティ上の考慮事項が増えます。 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] を使用すると、Web に配置されたアプリケーションにクエリ文字列を指定できます。 クエリ文字列は、アプリケーションを起動するための URL の末尾に一連の名前と値のペアが付加された形式になっています。

 `http://servername.adatum.com/WindowsApp1.application?username=joeuser`

 既定では、クエリ文字列の引数が無効になります。 これらを有効にするには、アプリケーションの配置マニフェストで `trustUrlParameters` 属性を設定する必要があります。 この値は、 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] および MageUI.exe から設定できます。 クエリ文字列の受け渡しを有効にする詳細な手順については、「[方法: オンライン ClickOnce アプリケーションでクエリ文字列の情報を取得する](../deployment/how-to-retrieve-query-string-information-in-an-online-clickonce-application.md)」を参照してください。

 クエリ文字列を通じて取得された引数は、必ず安全であることを確認してからデータベースまたはコマンド ラインに渡してください。 安全でない引数とは、悪意のあるユーザーがアプリケーションを操作して任意のコマンドを実行できるようにするデータベースまたはコマンド ライン エスケープ文字が含まれた引数のことです。

> [!NOTE]
> クエリ文字列引数は、起動時に [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションに引数を渡す唯一の手段です。 コマンド ラインから [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションに引数を渡すことはできません。

## <a name="deploying-obfuscated-assemblies"></a>難読化されたアセンブリの配置
 Visual Studio には、無料の [PreEmptive Protection - Dotfuscator Community](../ide/dotfuscator/index.md) が含まれています。これを使うと、コードの難読化とアクティブな保護手段を使って ClickOnce アプリケーションを保護できます。  詳細については、[Dotfuscator Community ユーザー ガイドの ClickOnce セクション](https://www.preemptive.com/dotfuscator/ce/docs/help/5.27/advanced_clickonce.html)を参照してください。

## <a name="see-also"></a>関連項目
- [ClickOnce のセキュリティと配置](../deployment/clickonce-security-and-deployment.md)
- [ClickOnce 配置ストラテジの選択](../deployment/choosing-a-clickonce-deployment-strategy.md)
