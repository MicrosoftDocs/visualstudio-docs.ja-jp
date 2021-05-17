---
title: アプリケーション マニフェストおよび配置マニフェストに再署名する | Microsoft Docs
description: 配置プロパティを変更した後、証明書を使用してアプリケーション マニフェストと配置マニフェストの両方に再署名する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- Office applications, signing manifests
- deploying applications [ClickOnce], signing manifests
- deploying applications, signing manifests
- ClickOnce deployment, signing manifests
- Office development in Visual Studio, signing manifests
ms.assetid: d53bceb9-4d3b-4c22-b909-8f370e7231fb
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 0b4e4efee02ca1571f40ae33f9d69d8fbec0a1d1
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99900430"
---
# <a name="how-to-re-sign-application-and-deployment-manifests"></a>方法: アプリケーション マニフェストおよび配置マニフェストに再署名する
Windows フォーム アプリケーション、Windows Presentation Foundation アプリケーション (xbap)、または Office ソリューションのアプリケーション マニフェストの配置プロパティを変更した後、アプリケーション マニフェストと配置マニフェストの両方に証明書を使用して再署名する必要があります。 このプロセスによって、改ざんされたファイルがエンド ユーザーのコンピューターにインストールされないようにすることができます。

 マニフェストに再署名する可能性があるもう 1 つのシナリオは、顧客が独自の証明書を使用してアプリケーション マニフェストと配置マニフェストに署名することを希望する場合です。

## <a name="re-sign-the-application-and-deployment-manifests"></a>アプリケーション マニフェストと配置マニフェストへの再署名
 この手順では、既にアプリケーション マニフェスト ファイル ( *.manifest*) に変更を加えていることを前提としています。 詳細については、「[方法: 配置プロパティを変更する](/previous-versions/cc442869(v=vs.110))」を参照してください。

#### <a name="to-re-sign-the-application-and-deployment-manifests-with-mageexe"></a>Mage.exe を使用してアプリケーション マニフェストと配置マニフェストへ再署名するには

1. **Visual Studio のコマンド プロンプト** ウィンドウを開きます。

2. 署名するマニフェスト ファイルが格納されているフォルダーにディレクトリを変更します。

3. 次のコマンドを入力してアプリケーション マニフェスト ファイルに署名します。 *ManifestFileName* は、マニフェスト ファイルの名前に拡張子を加えたものに置き換えます。 *Certificate* は、証明書ファイルの相対パスまたは完全修飾パスに置き換え、*Password* は、証明書のパスワードに置き換えます。

    ```cmd
    mage -sign ManifestFileName.manifest -CertFile Certificate -Password Password
    ```

     たとえば、アドイン、Windows フォーム アプリケーション、または Windows Presentation Foundation ブラウザー アプリケーション用のアプリケーション マニフェストに署名するには、次のコマンドを実行できます。 運用環境への配置では、Visual Studio によって作成された一時的な証明書は推奨されません。

    ```cmd
    mage -sign WindowsFormsApplication1.exe.manifest -CertFile ..\WindowsFormsApplication1_TemporaryKey.pfx
    mage -sign ExcelAddin1.dll.manifest -CertFile ..\ExcelAddIn1_TemporaryKey.pfx
    mage -sign WpfBrowserApplication1.exe.manifest -CertFile ..\WpfBrowserApplication1_TemporaryKey.pfx
    ```

4. 次のコマンドを入力して、配置マニフェスト ファイルを更新して署名します。前の手順と同様にプレースホルダー名を置き換えます。

    ```cmd
    mage -update DeploymentManifest -appmanifest ApplicationManifest -CertFile Certificate -Password Password
    ```

     たとえば、Excel アドイン、Windows フォーム アプリケーション、または Windows Presentation Foundation ブラウザー アプリケーション用の配置マニフェストを更新して署名するには、次のコマンドを実行できます。

    ```cmd
    mage -update WindowsFormsApplication1.application -appmanifest WindowsFormsApplication1.exe.manifest -CertFile ..\WindowsFormsApplication1_TemporaryKey.pfx
    mage -update ExcelAddin1.vsto -appmanifest ExcelAddin1.dll.manifest -CertFile ..\ExcelAddIn1_TemporaryKey.pfx
    mage -update WpfBrowserApplication1.xbap -appmanifest WpfBrowserApplication1.exe.manifest -CertFile ..\WpfBrowserApplication1_TemporaryKey.pfx
    ```

5. 必要に応じて、マスター配置マニフェスト (*publish\\\<appname>.application*) をバージョン配置ディレクトリ (*publish\Application Files \\\<appname>_\<version>* ) にコピーします。

## <a name="update-and-re-sign-the-application-and-deployment-manifests"></a>アプリケーション マニフェストと配置マニフェストを更新して再署名する
 この手順では、既にアプリケーション マニフェスト ファイル ( *.manifest*) を変更したが、更新された他のファイルがあることを前提としています。 ファイルが更新された場合は、ファイルを表すハッシュも更新する必要があります。

#### <a name="to-update-and-re-sign-the-application-and-deployment-manifests-with-mageexe"></a>Mage.exe を使用してアプリケーション マニフェストと配置マニフェストを更新して再署名するには

1. **Visual Studio のコマンド プロンプト** ウィンドウを開きます。

2. 署名するマニフェスト ファイルが格納されているフォルダーにディレクトリを変更します。

3. 発行出力フォルダー内のファイルから *.deploy* ファイル拡張子を削除します。

4. 次のコマンドを入力して、更新されたファイルの新しいハッシュでアプリケーション マニフェストを更新し、アプリケーション マニフェスト ファイルに署名します。 *ManifestFileName* は、マニフェスト ファイルの名前に拡張子を加えたものに置き換えます。 *Certificate* は、証明書ファイルの相対パスまたは完全修飾パスに置き換え、*Password* は、証明書のパスワードに置き換えます。

    ```cmd
    mage -update ManifestFileName.manifest -CertFile Certificate -Password Password
    ```

     たとえば、アドイン、Windows フォーム アプリケーション、または Windows Presentation Foundation ブラウザー アプリケーション用のアプリケーション マニフェストに署名するには、次のコマンドを実行できます。 運用環境への配置では、Visual Studio によって作成された一時的な証明書は推奨されません。

    ```cmd
    mage -update WindowsFormsApplication1.exe.manifest -CertFile ..\WindowsFormsApplication1_TemporaryKey.pfx
    mage -update ExcelAddin1.dll.manifest -CertFile ..\ExcelAddIn1_TemporaryKey.pfx
    mage -update WpfBrowserApplication1.exe.manifest -CertFile ..\WpfBrowserApplication1_TemporaryKey.pfx
    ```

5. 次のコマンドを入力して、配置マニフェスト ファイルを更新して署名します。前の手順と同様にプレースホルダー名を置き換えます。

    ```cmd
    mage -update DeploymentManifest -appmanifest ApplicationManifest -CertFile Certificate -Password Password
    ```

     たとえば、Excel アドイン、Windows フォーム アプリケーション、または Windows Presentation Foundation ブラウザー アプリケーション用の配置マニフェストを更新して署名するには、次のコマンドを実行できます。

    ```cmd
    mage -update WindowsFormsApplication1.application -appmanifest WindowsFormsApplication1.exe.manifest -CertFile ..\WindowsFormsApplication1_TemporaryKey.pfx
    mage -update ExcelAddin1.vsto -appmanifest ExcelAddin1.dll.manifest -CertFile ..\ExcelAddIn1_TemporaryKey.pfx
    mage -update WpfBrowserApplication1.xbap -appmanifest WpfBrowserApplication1.exe.manifest -CertFile ..\WpfBrowserApplication1_TemporaryKey.pfx
    ```

6. アプリケーション マニフェスト ファイルと配置マニフェストファイルを除くファイルに *.deploy* ファイル拡張子を追加して戻します。

7. 必要に応じて、マスター配置マニフェスト (*publish\\\<appname>.application*) をバージョン配置ディレクトリ (*publish\Application Files \\\<appname>_\<version>* ) にコピーします。

## <a name="see-also"></a>関連項目
- [ClickOnce アプリケーションのセキュリティ保護](../deployment/securing-clickonce-applications.md)
- [ClickOnce アプリケーションのコード アクセス セキュリティ](../deployment/code-access-security-for-clickonce-applications.md)
- [ClickOnce と Authenticode](../deployment/clickonce-and-authenticode.md)
- [信頼されたアプリケーションの配置の概要](../deployment/trusted-application-deployment-overview.md)
- [方法: ClickOnce のセキュリティ設定を有効にする](../deployment/how-to-enable-clickonce-security-settings.md)
- [方法: ClickOnce アプリケーションのセキュリティ ゾーンを設定する](../deployment/how-to-set-a-security-zone-for-a-clickonce-application.md)
- [方法: ClickOnce アプリケーションのカスタム アクセス許可を設定する](../deployment/how-to-set-custom-permissions-for-a-clickonce-application.md)
- [方法: アクセス許可が制限された ClickOnce アプリケーションをデバッグする](securing-clickonce-applications.md)
- [方法: ClickOnce アプリケーション用の信頼された発行者をクライアント コンピューターに追加する](../deployment/how-to-add-a-trusted-publisher-to-a-client-computer-for-clickonce-applications.md)
- [方法: ClickOnce 信頼プロンプトの動作を構成する](../deployment/how-to-configure-the-clickonce-trust-prompt-behavior.md)