---
title: 再署名を行わずに ClickOnce アプリを配置する
description: ClickOnce マニフェストの再署名や変更を行わずに、複数のネットワークの場所から ClickOnce アプリケーションを配置する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce applications, deploying without resigning
- ClickOnce deployment, without resigning
- application updates, ClickOnce
- update location [ClickOnce]
- deploymentProvider tag
- manifests [ClickOnce]
ms.assetid: 1218a98d-1ad5-4eef-95dd-0e0b3c44168c
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 4d5d7244f70852dee29813834fc427c888df9c1c
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99912155"
---
# <a name="deploy-clickonce-applications-for-testing-and-production-servers-without-resigning"></a>再署名を行わずにテストおよび運用サーバー用の ClickOnce アプリケーションを配置する
この記事では、.NET Framework バージョン 3.5 で導入された ClickOnce の機能について説明します。これを使用すると、ClickOnce マニフェストの再署名や変更を行わずに、複数のネットワークの場所から ClickOnce アプリケーションを配置できます。

> [!NOTE]
> アプリケーションの新しいバージョンを配置する際の推奨される方法は再署名であることに変わりはありません。 可能な限り、再署名の方法を使用してください。 詳細については、「[*Mage.exe* (マニフェストの生成および編集ツール)](/dotnet/framework/tools/mage-exe-manifest-generation-and-editing-tool)」をご覧ください。

 サードパーティの開発者や ISV はこの機能を選択することで、顧客がアプリケーションを簡単に更新できるようにできます。 この機能は次の状況で使用できます。

- アプリケーションを更新する場合 (アプリケーションの最初のインストール時ではありません)。

- コンピューター上にアプリケーションの構成が 1 つしかない場合。 たとえば、アプリケーションが 2 つの異なるデータベースを参照するように構成されている場合、この機能を使用することはできません。

## <a name="exclude-deploymentprovider-from-deployment-manifests"></a>配置マニフェストからの deploymentProvider の除外
 .NET Framework 2.0 および .NET Framework 3.0 では、オフラインで使用できるようにシステムにインストールされる ClickOnce アプリケーションでは、配置マニフェストに `deploymentProvider` を記載する必要があります。 多くの場合、`deploymentProvider` は更新場所として参照されます。つまり、ClickOnce によってアプリケーションの更新プログラムがチェックされる場所です。 アプリケーションの発行元が配置に署名する必要性に加えて、この要件により、企業はベンダーや他のサード パーティの ClickOnce アプリケーションを更新することが困難になっていました。 また、同じネットワーク上の複数の場所から同じアプリケーションを配置することも難しくなります。

 .NET Framework 3.5 で ClickOnce に加えられた変更により、サード パーティが ClickOnce アプリケーションを別の組織に提供することが可能になったので、組織はそのアプリケーションを独自のネットワーク上に配置できます。

 この機能を利用するには、ClickOnce アプリケーションの開発者が配置マニフェストから `deploymentProvider` を除外する必要があります。 この要件は、Mage.exe を使用して配置マニフェストを作成するときに `-providerUrl` 引数を除外する必要があることを意味します。 または、MageUI.exe を使用して配置マニフェストを生成する場合は、 **[アプリケーション マニフェスト]** タブの **[起動場所]** ボックスを必ず空白のままにしておく必要があります。

## <a name="deploymentprovider-and-application-updates"></a>deploymentProvider とアプリケーションの更新プログラム
 .NET Framework 3.5 以降では、オンラインとオフラインの両方で使用する ClickOnce アプリケーションを配置するために配置マニフェストで `deploymentProvider` を指定する必要はなくなりました。 この変更は、配置のパッケージ化と署名を自社で行いながら、他の企業が各社のネットワークを介してアプリケーションを配置できるようにする必要があるシナリオに対応しています。

 注意すべき重要な点は、`deploymentProvider` を除外したアプリケーションは、`deploymentProvider` タグを再度含めた更新プログラムを配布するまで、更新時にインストール場所を変更できないことです。

 この点を明確にするために、2 つの例を示します。 最初の例では、`deploymentProvider` タグのない ClickOnce アプリケーションを発行し、ユーザーに `http://www.adatum.com/MyApplication/` からインストールするよう求めます。 アプリケーションの次の更新プログラムを `http://subdomain.adatum.com/MyApplication/` から発行することにした場合、`http://www.adatum.com/MyApplication/` にある配置マニフェストでこれを示すことはできません。 次の 2 つのいずれかを行うことができます。

- 以前のバージョンをアンインストールし、新しいバージョンを新しい場所からインストールするようユーザーに伝えます。

- `http://www.adatum.com/MyApplication/` を参照する `deploymentProvider` を含む更新プログラムを `http://www.adatum.com/MyApplication/` に含めます。 次に、`http://subdomain.adatum.com/MyApplication/` を参照する `deploymentProvider` を含む別の更新プログラムを後でリリースします。

  2 番目の例では、`deploymentProvider` を指定した ClickOnce アプリケーションを発行し、その後、それを削除することにしました。 `deploymentProvider` のない新しいバージョンがクライアントにダウンロードされると、`deploymentProvider` が復元されたアプリケーションのバージョンをリリースするまで、更新に使用するパスをリダイレクトすることはできません。 最初の例と同様に、`deploymentProvider` は、最初は新しい場所ではなく、現在の更新場所を参照している必要があります。 この場合、`http://subdomain.adatum.com/MyApplication/` を参照する `deploymentProvider` の挿入を試みると、次の更新は失敗します。

## <a name="create-a-deployment"></a>デプロイの作成
 さまざまなネットワークの場所から配置できる配置の作成方法に関する手順付きのガイダンスについては、「[チュートリアル: 再署名が不要で商標を保持する ClickOnce アプリケーションを手動で配置する](../deployment/walkthrough-manually-deploying-a-clickonce-app-no-re-signing-required.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [*Mage.exe* (マニフェスト生成および編集ツール)](/dotnet/framework/tools/mage-exe-manifest-generation-and-editing-tool)
- [*MageUI.exe* (マニフェスト生成および編集ツールのグラフィカル クライアント)](/dotnet/framework/tools/mageui-exe-manifest-generation-and-editing-tool-graphical-client)
