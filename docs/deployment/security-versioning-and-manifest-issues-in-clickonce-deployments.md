---
title: セキュリティ/バージョン管理/マニフェストに関する問題 (ClickOnce)
description: ClickOnce 配置が成功しなくなる可能性がある、ClickOnce のセキュリティ、アプリケーションのバージョン管理、マニフェストの構文とセマンティクスに関する問題について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- versioning, ClickOnce applications
- ClickOnce applications, Windows Vista User Account Control
- ClickOnce applications, versioning issues
- security, ClickOnce applications
- Windows 7, ClickOnce deployments
- ClickOnce applications, manifest issues
- User Account Control, ClickOnce applications
- Windows Vista, ClickOnce deployments
- manifests [ClickOnce]
- ClickOnce applications, security issues
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 55758f67c845cbf753d51ebfb94b87af6cf55cde
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99877630"
---
# <a name="security-versioning-and-manifest-issues-in-clickonce-deployments"></a>ClickOnce 配置でのセキュリティ、バージョン管理、およびマニフェストの問題

[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 配置が成功しなくなる可能性がある、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] のセキュリティ、アプリケーションのバージョン管理、マニフェストの構文とセマンティクスに関する問題は、さまざまなものが存在します。

## <a name="clickonce-and-windows-vista-user-account-control"></a>ClickOnce と Windows Vista のユーザー アカウント制御

[!INCLUDE[windowsver](../deployment/includes/windowsver_md.md)] では、現在のユーザーが管理者アクセス許可を持つアカウントでログインしている場合でも、アプリケーションは既定で、標準ユーザーとして実行されます。 アプリケーションで管理者アクセス許可が必要なアクションを実行する必要がある場合は、アプリケーションからオペレーティング システムに伝えられ、その後ユーザーに、管理者の資格情報の入力を求めるメッセージが表示されます。 ユーザー アカウント制御 (UAC) という名前のこの機能では、ユーザーの明示的承認なしにアプリケーションがオペレーティング システム全体に影響を与える可能性がある変更を加えることが防止されます。 Windows アプリケーションは、アプリケーション マニフェストの `trustInfo` セクションで `requestedExecutionLevel` 属性を指定することによって、このアクセス許可の昇格が必要であることを宣言します。

アプリケーションがセキュリティ昇格攻撃にさらされるリスクのため、クライアントで UAC が有効になっていると、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションはアクセス許可の昇格を要求できません。 `requestedExecutionLevel` 属性を `requireAdministrator` または `highestAvailable` に設定しようとする [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションはすべて、[!INCLUDE[windowsver](../deployment/includes/windowsver_md.md)] にインストールされません。

場合によっては、[!INCLUDE[windowsver](../deployment/includes/windowsver_md.md)] でのインストーラー検出ロジックが原因で、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションが管理者アクセス許可を使用して実行を試みることがあり ます。 この場合は、アプリケーション マニフェストで `requestedExecutionLevel` 属性を `asInvoker` に設定できます。 これにより、アプリケーション自体が昇格なしで実行されるようになります。 [!INCLUDE[vs_orcas_long](../debugger/includes/vs_orcas_long_md.md)] により、すべてのアプリケーション マニフェストにこの属性が自動的に追加されます。

アプリケーションの有効期間全体で管理者アクセス許可を必要とするアプリケーションを開発している場合は、代わりに Windows インストーラー (MSI) テクノロジを使用してアプリケーションを配置することを検討してください。 詳細については、「[Windows インストーラーの基本事項](../extensibility/internals/windows-installer-basics.md)」を参照してください。

## <a name="online-application-quotas-and-partial-trust-applications"></a>オンライン アプリケーション クォータと部分信頼アプリケーション

[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションがインストールを通してではなく、オンラインで実行される場合は、オンライン アプリケーション用に確保されているクォータに収まる必要があります。 また、部分信頼で実行されるネットワーク アプリケーション (セキュリティ アクセス許可の制限付きセットを使用するなど) は、クォータ サイズの半分より大きくできません。

オンライン アプリケーションのクォータを変更する方法の詳細と手順については、「[ClickOnce キャッシュの概要](../deployment/clickonce-cache-overview.md)」を参照してください。

## <a name="versioning-issues"></a>バージョン管理に関する問題

アセンブリに厳密な名前を割り当てて、アプリケーションの更新を反映するようにアセンブリのバージョン番号を増やすと、問題が発生することがあります。 厳密な名前が付けられたアセンブリへの参照を使用してコンパイルされたすべてのアセンブリは、それ自体の再コンパイルが必要です。そうしないと、アセンブリは古いバージョンを参照しようとします。 アセンブリでこれが試みられるのは、アセンブリではバインド要求内で古いバージョンの値が使用されているためです。

たとえば、独自のプロジェクト内に、バージョン 1.0.0.0 の厳密な名前が付けられたアセンブリがあるとします。 アセンブリのコンパイル後に、メイン アプリケーションを含むプロジェクトへの参照としてそれを追加します。 アセンブリを更新してバージョンを 1.0.0.1 に増やし、アプリケーションを再コンパイルせずに配置しようとすると、実行時にアプリケーションでアセンブリを読み込めなくなくなります。

このエラーは、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] マニフェストを手動で編集している場合にのみ発生する可能性があります。Visual Studio を使用して配置を生成した場合、このエラーは発生しないはずです。

## <a name="specify-individual-net-framework-assemblies-in-the-manifest"></a>マニフェストで個々の .NET Framework アセンブリを指定する

古いバージョンの .NET Framework アセンブリを参照するように[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 配置を手動で編集した場合、アプリケーションの読み込みは失敗します。 たとえば、マニフェストで指定されているバージョンより前のバージョンの .NET Framework に向けた System.Net アセンブリへの参照を追加した場合は、エラーが発生します。 一般に、アプリケーションの実行対象となる .NET Framework のバージョンは、アプリケーション マニフェストで依存関係として指定されているため、個々の .NET Framework アセンブリへの参照を指定しようとしないでください。

## <a name="manifest-parsing-issues"></a>マニフェストの解析に関する問題

[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] によって使用されるマニフェスト ファイルは、XML ファイルであり、適切な形式かつ有効である必要があります。これらは、XML 構文規則に従っていて、関連する XML スキーマで定義されている要素と属性のみを使用する必要があります。

マニフェスト ファイルで問題を発生させる可能性があるのは、アプリケーションの名前として、単一引用符や二重引用符などの特殊文字が含まれる名前を選択することです。 アプリケーションの名前は、その [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] ID の一部です。 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] では、現在のところ、特殊文字が含まれる ID は解析されません。 アプリケーションをアクティブにできない場合は、名前でアルファベットと数字の文字だけが使用されていることを確認し、もう一度配置を試みてください。

配置またはアプリケーションのマニフェストを手動で編集した場合は、それらを意図せず破損している可能性があります。 マニフェストが破損していると、正しい [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] のインストールが妨げられます。 **[ClickOnce エラー]** ダイアログ ボックスの **[詳細]** をクリックし、ログのエラー メッセージを読むことで、実行時のそのようなエラーをデバッグできます。 ログには、以下のメッセージのいずれかが示されます。

- 構文エラーの説明と、エラーが発生した行番号および文字位置。

- マニフェストのスキーマの違反で使用された要素または属性の名前。 マニフェストに手動で XML を追加した場合は、マニフェスト スキーマへの追加の内容と比較する必要があります。 詳細については、「[ClickOnce 配置マニフェスト](../deployment/clickonce-deployment-manifest.md)」と「[ClickOnce アプリケーション マニフェスト](../deployment/clickonce-application-manifest.md)」を参照してください。

- ID が競合しています。 配置マニフェストとアプリケーション マニフェストの依存関係の参照は、`name` 属性と `publicKeyToken` 属性の両方で一意である必要があります。 1 つのマニフェスト内のいずれか 2 つの要素間で両方の属性が一致する場合、マニフェストの解析は成功しません。

## <a name="precautions-when-manually-changing-manifests-or-applications"></a>マニフェストまたはアプリケーションを手動で変更する際の注意事項

アプリケーション マニフェストを更新するときは、アプリケーション マニフェストと配置マニフェストの両方に再署名する必要があります。 配置マニフェストには、そのファイルのハッシュと、そのデジタル署名を含むアプリケーション マニフェストへの参照が含まれています。

### <a name="precautions-with-deployment-provider-usage"></a>配置プロバイダーの使用に関する注意事項

[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 配置マニフェストには、アプリケーションをインストールしてサービスを提供する場所の完全パスを指し示す `deploymentProvider` プロパティが含まれています。

```xml
<deploymentProvider codebase="http://myserver/myapp.application" />
```

このパスは、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] によってアプリケーションが作成されるときに設定され、インストールされたアプリケーションには必須です。 パスは、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] インストーラーによってアプリケーションがインストールされ、更新プログラムが検索される標準の場所を指し示します。 **xcopy** コマンドを使用して [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションを別の場所にコピーしても、`deploymentProvider` プロパティを変更しないと、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] では、アプリケーションのダウンロードを試みるときに引き続き元の場所が参照されます。

アプリケーションを移動またはコピーする場合は、`deploymentProvider` のパスも更新して、クライアントが実際に新しい場所からインストールされるようにする必要があります。 インストール済みのアプリケーションがある場合は、このパスを更新するとたいていは問題が生じます。 常に元の URL を使用して起動されるオンライン アプリケーションの場合、`deploymentProvider` の設定は省略可能です。 `deploymentProvider` が設定されている場合は、それが尊重されます。それ以外の場合は、アプリケーションの起動に使用される URL が、アプリケーション ファイルをダウンロードするためのベース URL として使用されます。

> [!NOTE]
> マニフェストを更新するたびに、それに再度署名する必要もあります。

## <a name="see-also"></a>関連項目

[ClickOnce 配置のトラブルシューティング](../deployment/troubleshooting-clickonce-deployments.md)
[ClickOnce アプリケーションのセキュリティ保護](../deployment/securing-clickonce-applications.md)
[ClickOnce 配置ストラテジの選択](../deployment/choosing-a-clickonce-deployment-strategy.md)
