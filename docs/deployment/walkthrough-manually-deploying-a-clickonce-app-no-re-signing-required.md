---
title: ClickOnce アプリケーションを手動で配置し、商標を保持する
description: 新しい配置マニフェストを生成せずに顧客が配置し、顧客の商標を使用できる ClickOnce アプリケーションを作成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- branding
- preserved branding information
- ClickOnce deployment, manually
- multiple ClickOnce deployment and branding
- ClickOnce deployment, SDK tools
- customer deployments
- manual ClickOnce deployments
- manifests [ClickOnce]
- ClickOnce applications, deployed by others
ms.assetid: c21822fb-d4ee-42e4-b72d-41ee9786efe5
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: c0e8895f45524526fc8007ff909a9c541e9899b3
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99917259"
---
# <a name="walkthrough-manually-deploy-a-clickonce-application-that-does-not-require-re-signing-and-that-preserves-branding-information"></a>チュートリアル: 再署名が不要で商標を保持する ClickOnce アプリケーションを手動で配置する
[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションを作成し、発行して配置するために顧客に提供する場合、従来、顧客は配置マニフェストを更新し、再署名する必要がありました。 今でもほとんどの場合この方法が推奨されますが、.NET Framework 3.5 では、新しい配置マニフェストを再生成する必要なく顧客が配置できる [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 配置を作成することができます。 詳細については、「[再署名を行わない ClickOnce アプリケーションの配置 (テスト サーバーおよび運用サーバー)](../deployment/deploying-clickonce-applications-for-testing-and-production-without-resigning.md)」を参照してください。

 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションを作成し、発行して配置するために顧客に提供する場合、アプリケーションで顧客の商標を使用したり、開発者の商標を保持したりすることができます。 たとえば、アプリケーションが単一の専用アプリケーションである場合は、開発者の商標を保持することができます。 アプリケーションが顧客ごとに大幅にカスタマイズされている場合は、顧客の商標を使用することができます。 .NET Framework 3.5 では、配置のために組織にアプリケーションを提供するときに、開発者の商標、パブリッシャー情報、およびセキュリティ署名を保持できます。 詳細については、「[開発者以外が配置する ClickOnce アプリケーションを作成する](../deployment/creating-clickonce-applications-for-others-to-deploy.md)」を参照してください。

> [!NOTE]
> このチュートリアルでは、コマンドライン ツール *Mage.exe* またはグラフィカル ツール *MageUI.exe* を使用して、手動で配置を作成します。 手動での配置の詳細については、「[チュートリアル: ClickOnce アプリケーションを手動で配置する](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)」を参照してください。

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルの手順を実行するための要件は次のとおりです。

- 配置する準備ができている Windows フォーム アプリケーション。 このアプリケーションを *WindowsFormsApp1* と呼びます。

- Visual Studio または Windows SDK。

### <a name="to-deploy-a-clickonce-application-with-multiple-deployment-and-branding-support-using-mageexe"></a>Mage.exe を使用して複数の配置および商標をサポートする ClickOnce アプリケーションを配置するには

1. Visual Studio のコマンド プロンプトまたは [!INCLUDE[winsdkshort](../debugger/debug-interface-access/includes/winsdkshort_md.md)] コマンド プロンプトを開き、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] ファイルを保存するディレクトリに移動します。

2. 配置の現在のバージョンにちなんだ名前のディレクトリを作成します。 アプリケーションを初めて配置する場合は、**1.0.0.0** を選択する可能性が高くなります。

   > [!NOTE]
   > 配置のバージョンは、アプリケーション ファイルのバージョンとは異なる場合があります。

3. **bin** という名前のサブディレクトリを作成し、実行可能ファイル、アセンブリ、リソース、およびデータ ファイルを含むすべてのアプリケーション ファイルをここにコピーします。

4. Mage.exe を呼び出して、アプリケーション マニフェストを生成します。

   ```cmd
   mage -New Application -ToFile 1.0.0.0\WindowsFormsApp1.exe.manifest -Name "Windows Forms App 1" -Version 1.0.0.0 -FromDirectory 1.0.0.0\bin -UseManifestForTrust true -Publisher "A. Datum Corporation"
   ```

5. デジタル証明書でアプリケーション マニフェストに署名します。

   ```cmd
   mage -Sign WindowsFormsApp1.exe.manifest -CertFile mycert.pfx
   ```

6. *Mage.exe* を呼び出して、配置マニフェストを生成します。 既定では、*Mage.exe* によって [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 配置がインストール済みのアプリケーションとしてマークされ、オンラインとオフラインの両方で実行できるようになります。 ユーザーがオンラインの場合のみアプリケーションを使用できるようにするには、`-i` 引数を値 `f` で使用します。 このアプリケーションでは複数の配置機能を利用するため、*Mage.exe* への `-providerUrl` 引数を除外します。 (バージョン 3.5 よりも前の .NET Framework のバージョンでは、オフライン アプリケーションに対して `-providerUrl` を除外するとエラーが発生します。)

   ```cmd
   mage -New Deployment -ToFile WindowsFormsApp1.application -Name "Windows Forms App 1" -Version 1.0.0.0 -AppManifest 1.0.0.0\WindowsFormsApp1.manifest
   ```

7. 配置マニフェストに署名しないでください。

8. すべてのファイルを顧客に提供し、顧客がアプリケーションをネットワークに配置します。

9. この時点で、顧客は自己生成した証明書を使用して配置マニフェストに署名する必要があります。 たとえば、Adventure Works という名前の会社に対で顧客が働いている場合、*MakeCert.exe* ツールを使用して自己署名証明書を生成できます。 次に、*Pvk2pfx.exe* ツールを使用して、*MakeCert.exe* によって作成されたファイルを *Mage.exe* に渡すことができる PFX ファイルに結合します。

    ```cmd
    makecert -r -pe -n "CN=Adventure Works" -sv MyCert.pvk MyCert.cer
    pvk2pfx.exe -pvk MyCert.pvk -spc MyCert.cer -pfx MyCert.pfx
    ```

10. 次に、顧客はこの証明書を使用して配置マニフェストに署名します。

    ```cmd
    mage -Sign WindowsFormsApp1.application -CertFile MyCert.pfx
    ```

11. 顧客がアプリケーションをユーザーに配置します。

### <a name="to-deploy-a-clickonce-application-with-multiple-deployment-and-branding-support-using-mageuiexe"></a>MageUI.exe を使用して複数の配置および商標をサポートする ClickOnce アプリケーションを配置するには

1. Visual Studio のコマンド プロンプトまたは [!INCLUDE[winsdkshort](../debugger/debug-interface-access/includes/winsdkshort_md.md)] コマンド プロンプトを開き、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] ファイルを保存するディレクトリに移動します。

2. **bin** という名前のサブディレクトリを作成し、実行可能ファイル、アセンブリ、リソース、およびデータ ファイルを含むすべてのアプリケーション ファイルをここにコピーします。

3. 配置の現在のバージョンにちなんだ名前のサブディレクトリを作成します。 アプリケーションを初めて配置する場合は、**1.0.0.0** を選択する可能性が高くなります。

   > [!NOTE]
   > 配置のバージョンは、アプリケーション ファイルのバージョンとは異なる場合があります。

4. \\**bin** ディレクトリを手順 2. で作成したディレクトリに移動します。

5. グラフィカル ツール *MageUI.exe* を起動します。

   ```cmd
   MageUI.exe
   ```

6. メニューから **[ファイル]** 、 **[新規作成]** 、 **[アプリケーション マニフェスト]** の順に選択して、新しいアプリケーション マニフェストを作成します。

7. 既定の **[名前]** タブで、この配置の名前とバージョン番号を入力します。 また、 **[発行元]** に値を指定します。この値は、アプリケーションの配置時に [スタート] メニュー内のアプリケーションのショートカット リンクのフォルダー名として使用されます。

8. **[アプリケーション オプション]** タブを選択し、 **[信頼情報のアプリケーション マニフェストを使用する]** をクリックします。 これにより、この [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションのサードパーティ商標が有効になります。

9. **[ファイル]** タブを選択し、 **[アプリケーション ディレクトリ]** テキスト ボックスの横にある **[参照]** ボタンをクリックします。

10. 手順 2. で作成したアプリケーション ファイルが格納されているディレクトリを選択し、フォルダーの選択ダイアログ ボックスで **[OK]** をクリックします。

11. **[設定]** ボタンをクリックして、すべてのアプリケーション ファイルをファイル一覧に追加します。 アプリケーションに複数の実行可能ファイルが含まれる場合は、 **[ファイルの種類]** ドロップダウン リストから **[エントリ ポイント]** を選択して、この配置のメインの実行可能ファイルをスタートアップ アプリケーションとしてマークします。 (アプリケーションに実行可能ファイルが 1 つだけ含まれている場合は、*MageUI.exe* によってマークされます。)

12. **[必要なアクセス許可]** タブを選択し、アプリケーションでアサートする必要がある信頼レベルを選択します。 既定値は **[完全な信頼]** で、ほとんどのアプリケーションに適しています。

13. メニューから **[ファイル]** 、 **[保存]** の順にクリックし、アプリケーション マニフェストを保存します。 アプリケーション マニフェストの保存時に、署名を求めるメッセージが表示されます。

14. ファイル システムにファイルとして保存されている証明書がある場合は、 **[証明書ファイルで署名する]** オプションを使用し、省略記号 ( **...** ) ボタンを使用してファイル システムから証明書を選択します。

     または

     お使いのコンピューターからアクセスできる証明書ストアに証明書が保持されている場合は、 **[保存された証明書で署名する]** オプションを選択し、提供された一覧から証明書を選択します。

15. メニューから **[ファイル]** 、 **[新規作成]** 、 **[配置マニフェスト]** を選択して配置マニフェストを作成し、 **[名前]** タブで、名前とバージョン番号 (この例では **1.0.0.0**) を指定します。

16. **[更新]** タブに切り替え、このアプリケーションが更新される頻度を指定します。 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] Deployment API を使用して更新プログラムをアプリケーション自体で確認する場合は、 **[このアプリケーションの更新プログラムを確認する]** をオフにします。

17. **[アプリケーション参照]** タブに切り替えます。 **[マニフェストの選択]** ボタンをクリックし、前の手順で作成したアプリケーション マニフェストを選択して、このタブのすべての値を事前設定できます。

18. **[保存]** を選択し、配置マニフェストをディスクに保存します。 アプリケーション マニフェストの保存時に、署名を求めるメッセージが表示されます。 **[キャンセル]** をクリックしして、署名せずにマニフェストを保存します。

19. すべてのアプリケーション ファイルを顧客に提供します。

20. この時点で、顧客は自己生成した証明書を使用して配置マニフェストに署名する必要があります。 たとえば、Adventure Works という名前の会社に対で顧客が働いている場合、*MakeCert.exe* ツールを使用して自己署名証明書を生成できます。 次に、*Pvk2pfx.exe* ツールを使用して、*MakeCert.exe* によって作成されたファイルを *MageUI.exe* に渡すことができる PFX ファイルに結合します。

    ```cmd
    makecert -r -pe -n "CN=Adventure Works" -sv MyCert.pvk MyCert.cer
    pvk2pfx.exe -pvk MyCert.pvk -spc MyCert.cer -pfx MyCert.pfx
    ```

21. 証明書が生成されたので、顧客は *MageUI.exe* で配置マニフェストを開き、保存することによって、配置マニフェストに署名します。 署名ダイアログ ボックスが表示されると、顧客は **[証明書ファイルで署名する]** オプションを選択し、ディスクに保存した PFX ファイルを選択します。

22. 顧客がアプリケーションをユーザーに配置します。

## <a name="see-also"></a>関連項目
- [Mage.exe (マニフェストの生成および編集ツール)](/dotnet/framework/tools/mage-exe-manifest-generation-and-editing-tool)
- [MageUI.exe (マニフェスト生成および編集ツールのグラフィカル クライアント)](/dotnet/framework/tools/mageui-exe-manifest-generation-and-editing-tool-graphical-client)
- [MakeCert](/windows/desktop/SecCrypto/makecert)
