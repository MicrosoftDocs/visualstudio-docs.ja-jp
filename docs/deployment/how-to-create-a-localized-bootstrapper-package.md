---
title: ローカライズ版のブートストラップ パッケージを作成する | Microsoft Docs
description: 各ロケールに対してさらに 2 つのファイルを作成して、ClickOnce でローカライズされたバージョンのブートストラップ パッケージを作成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- localized bootstrapper packages
- dependencies, creating localized bootstrapper packages
- prerequisites, creating localized bootstrapper packages
ms.assetid: 66a1bc7e-6540-4164-963d-557196a69d8a
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 2a9d1fc91dcb385a9250dde3adb47c0d9553147f
ms.sourcegitcommit: 6aa55db5e1fe19d4d17886e0bfe140dbd186f8ba
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/10/2021
ms.locfileid: "111877716"
---
# <a name="how-to-create-a-localized-bootstrapper-package"></a>方法: ローカライズされたブートストラップ パッケージを作成する
ブートストラップ パッケージを作成したら、さらに 2 つのファイルをロケールごとに作成して、ローカライズ版のブートストラップ パッケージを作成できます。2 つのファイルとは、ソフトウェア ライセンス条項ファイル (*eula.rtf* など) とパッケージ マニフェスト (*package.xml*) です。

 既定では、Visual Studio 2010 には .NET Framework 4、.NET Framework 4 Client Profile、F# Runtime 2.0、および F# Runtime 4.0 用のローカライズ版のブートストラップ パッケージのみが用意されています。 3 つのステップを実行することにより、その他のブートストラップのローカライズ版パッケージを作成できます。

1. *\Program Files (x86)\Microsoft SDKs\ClickOnce Bootstrapper\Packages\\\<BootstrapperPackageName>* のロケール名に基づいた名前のフォルダーを作成します。

2. ブートストラップ パッケージのソフトウェア ライセンス条項を示すファイルを作成し、新しいフォルダーに格納します。

3. *package.xml* という名前のパッケージ マニフェストを作成し、文字列とカルチャを更新して、そのファイルを新しいフォルダーに格納します。 Visual Studio のブートストラップを対象言語で既に作成している場合は、Visual Studio の *package.xml* ファイルをコピーして、このステップで変更することができます。

> [!NOTE]
> セットアップ プロジェクトを使用してアプリケーションを配置する場合は、**Localization** プロパティを変更してアプリケーションをローカライズできます。

 [!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

### <a name="to-create-a-localized-bootstrapper-package"></a>ローカライズ版のブートストラップ パッケージを作成するには

1. ロケール名に基づいた名前のフォルダーを作成します。

     32 ビット コンピューターでは、このフォルダーを *\Program Files\Microsoft SDKs\ClickOnce Bootstrapper\Packages\\\<BootstrapperPackageName>\\* フォルダーに作成します。

     64 ビット コンピューターでは、このフォルダーを *\Program Files (x86)\Microsoft SDKs\ClickOnce Bootstrapper\Packages\\\<BootstrapperPackageName>\\* フォルダーに作成します。

     次の表は、ロケールに合わせるために使用できるフォルダー名を示します。

    |Locale|[フォルダー名]|
    |------------|-----------------|
    |簡体中国語|zh-Hans|
    |繁体中国語|zh-Hant|
    |チェコ語|cs|
    |ドイツ語|de|
    |英語|en|
    |スペイン語|es|
    |フランス語|fr|
    |イタリア語|it|
    |韓国語|ko|
    |日本語|ja|
    |ポーランド語|pl|
    |ポルトガル語 (ブラジル)|pt-BR|
    |ロシア語|ru|
    |トルコ語|tr|

2. ブートストラップ パッケージのソフトウェア ライセンス条項を示すファイルを作成し、新しいフォルダーに格納します。

3. *package.xml* という名前のパッケージ マニフェストを作成し、新しいフォルダーに格納します。 詳細については、「[方法: パッケージ マニフェストを作成する](../deployment/how-to-create-a-package-manifest.md)」を参照してください。

4. パッケージ マニフェストの `<Strings>` セクションを更新して、文字列がロケールに対応する正しい言語で表示されるようにします。

5. `<String Name="Culture">` の値をフォルダー名と一致するように変更します。

6. *package.xml* ファイルを保存します。

### <a name="to-create-a-bootstrapper-package-for-net-framework-35-service-pack-1-localized-in-french"></a>フランス語でローカライズした .NET Framework 3.5 Service Pack 1 用のブートストラップ パッケージを作成するには

1. *fr* という名前のフォルダーを作成します。 フォルダー名はロケール名と一致する必要があります。

     32 ビット コンピューターでは、このフォルダーは *\Program Files\Microsoft SDKs\ClickOnce Bootstrapper\Packages\DotNetFX35SP1\\* フォルダーに作成します。

     64 ビット コンピューターでは、このフォルダーは *\Program Files (x86)\Microsoft SDKs\ClickOnce Bootstrapper\Packages\DotNetFX35SP1\\* フォルダーに作成します。

2. ローカライズ版のソフトウェア ライセンス条項を *fr* フォルダーに格納します。

3. *\Program Files (x86)\Microsoft SDKs\ClickOnce Bootstrapper\Packages\DotNetFX35SP1\en\package.xml* ファイルを *fr* フォルダーにコピーし、XML デザイナーでそのファイルを開きます。

4. パッケージ マニフェストの `<Strings>` セクションを更新して、エラー文字列がフランス語で表示されるようにします。

5. `<String Name="Culture">` の値を *fr* に変更します。

6. *package.xml* ファイルを保存します。

>[!NOTE]
> Visual Studio 2019 Update 7 リリース以降、ブートストラッパー パッケージはパス *<VS Install Path>\MSBuild\Microsoft\VisualStudio\BootstrapperPackages* でも見つかります。

## <a name="see-also"></a>関連項目
- [ブートストラップ パッケージの作成](../deployment/creating-bootstrapper-packages.md)
- [アプリケーション配置の必要条件](../deployment/application-deployment-prerequisites.md)
- [方法: パッケージ マニフェストを作成する](../deployment/how-to-create-a-package-manifest.md)