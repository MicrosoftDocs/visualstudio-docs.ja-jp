---
title: ClickOnce アプリケーションのカスタム インストーラーの作成
description: カスタム インストーラーを使用して、.exe ファイルに基づく ClickOnce アプリケーションをサイレント インストールおよび更新する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, custom installer
- installer [ClickOnce], custom
- deploying applications [ClickOnce], custom installer
- InPlaceHostingManager [ClickOnce], custom installer
- custom installer [ClickOnce]
ms.assetid: fb222cc5-8aeb-4b94-8c49-b93e342f5f69
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: e7ae131026a94fa368d55bad1d8cd2164b6f960b
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106216931"
---
# <a name="walkthrough-create-a-custom-installer-for-a-clickonce-application"></a>チュートリアル: ClickOnce アプリケーションのカスタム インストーラーの作成
*.exe* ファイルに基づく ClickOnce アプリケーションは、カスタム インストーラーによってサイレント インストールおよび更新できます。 カスタム インストーラーでは、セキュリティ操作とメンテナンス操作のためのカスタム ダイアログ ボックスなど、インストール時のカスタムのユーザー エクスペリエンスを実装できます。 インストール操作を実行するために、カスタム インストーラーでは <xref:System.Deployment.Application.InPlaceHostingManager> クラスを使用します。 このチュートリアルでは、ClickOnce アプリケーションをサイレント インストールするカスタム インストーラーを作成する方法について説明します。

## <a name="prerequisites"></a>必須コンポーネント

### <a name="to-create-a-custom-clickonce-application-installer"></a>カスタム ClickOnce アプリケーション インストーラーを作成するには

1. ClickOnce アプリケーションで、System.Deployment と System.Windows.Forms への参照を追加します。

2. アプリケーションに新しいクラスを追加し、任意の名前を指定します。 このチュートリアルでは、名前 `MyInstaller` を使用します。

3. 次の `Imports` ディレクティブまたは `using` ディレクティブを新しいクラスの先頭に追加します。

    ```vb
    Imports System.Deployment.Application
    Imports System.Windows.Forms
    ```

    ```csharp
    using System.Deployment.Application;
    using System.Windows.Forms;
    ```

4. 次のメソッドをクラスに追加します。

     これらのメソッドでは、<xref:System.Deployment.Application.InPlaceHostingManager> メソッドを呼び出して配置マニフェストをダウンロードし、適切なアクセス許可をアサートし、インストールのアクセス許可をユーザーに要求してから、アプリケーションを ClickOnce キャッシュにダウンロードしてインストールします。 カスタム インストーラーでは、ClickOnce アプリケーションが事前に信頼されていることを指定できます。また、<xref:System.Deployment.Application.InPlaceHostingManager.AssertApplicationRequirements%2A> メソッド呼び出しに対して信頼の決定を保留することもできます。 このコードによって、アプリケーションが事前に信頼されます。

    > [!NOTE]
    > 事前信頼によって割り当てられるアクセス許可は、カスタム インストーラー コードのアクセス許可を超えることはできません。

    :::code language="vb" source="../snippets/visualbasic/VS_Snippets_Winforms/System.Deployment.Application.InPlaceHostingManager/VB/Form1.vb" id="Snippet1":::
    :::code language="csharp" source="../snippets/csharp/VS_Snippets_Winforms/System.Deployment.Application.InPlaceHostingManager/CS/Form1.cs" id="Snippet1":::

5. コードからインストールを試みるには、`InstallApplication` メソッドを呼び出します。 たとえば、クラスに `MyInstaller` という名前を付けた場合は、次のように `InstallApplication` を呼び出すことができます。

    ```vb
    Dim installer As New MyInstaller()
    installer.InstallApplication("\\myServer\myShare\myApp.application")
    MessageBox.Show("Installer object created.")
    ```

    ```csharp
    MyInstaller installer = new MyInstaller();
    installer.InstallApplication(@"\\myServer\myShare\myApp.application");
    MessageBox.Show("Installer object created.");
    ```

## <a name="next-steps"></a>次のステップ
 ClickOnce アプリケーションでは、更新プロセス中に表示するカスタム ユーザー インターフェイスを含む、カスタムの更新ロジックを追加することもできます。 詳細については、「<xref:System.Deployment.Application.UpdateCheckInfo>」を参照してください。 ClickOnce アプリケーションでは、`<customUX>` 要素を使用して、[スタート] メニューの標準エントリ、ショートカット、および [プログラムの追加と削除] エントリを抑制することもできます。 詳細については、[\<entryPoint> 要素](../deployment/entrypoint-element-clickonce-application.md)と <xref:System.Deployment.Application.DownloadApplicationCompletedEventArgs.ShortcutAppId%2A> に関するページを参照してください。

## <a name="see-also"></a>関連項目
- [ClickOnce アプリケーション マニフェスト](../deployment/clickonce-application-manifest.md)
- [\<entryPoint> 要素](../deployment/entrypoint-element-clickonce-application.md)
