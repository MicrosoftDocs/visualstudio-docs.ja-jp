---
title: ClickOnce アプリと共に必須コンポーネントをインストールする
description: インストールされる ClickOnce アプリケーションと共にパッケージ化する必須コンポーネントを選択する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- deploying applications [ClickOnce], prerequisites
- prerequisites, ClickOnce
- components, bootstrapping
ms.assetid: e964fca5-fdfd-47cf-a1c9-7fb96b1c88b5
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 09337ee164c8b740e9aa8a044c4a9df385f01016
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99900565"
---
# <a name="how-to-install-prerequisites-with-a-clickonce-application"></a>方法: ClickOnce アプリケーションと共に必須コンポーネントをインストールする
すべての [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションは、実行する前に適切なバージョンの .NET Framework がコンピューターにインストールされている必要があります。多くのアプリケーションには、他の必須コンポーネントもあります。 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションを発行するときに、アプリケーションと共にパッケージ化する一連の必須コンポーネントを選択できます。 インストール時に、必須コンポーネントごとにチェックが実行され、既に存在するかどうかが確認されます。存在しない場合は、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションをインストールする前にインストールされます。

 必須コンポーネントをパッケージ化して発行する代わりに、コンポーネントのダウンロード場所を指定することもできます。 たとえば、発行するすべてのアプリケーションに必須コンポーネントを含めるのではなく、すべての必須コンポーネントのインストーラーが含まれた、一元化されたファイル共有または Web 上の場所を使用できます。インストール時には、コンポーネントがその場所からダウンロードされ、インストールされます。

> [!IMPORTANT]
> 最初の [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションを発行する前に、開発用コンピューターに必須コンポーネントのインストーラー パッケージを追加する必要があります。 詳細については、「[方法: ClickOnce アプリケーションと共に必須コンポーネントを含める](../deployment/how-to-include-prerequisites-with-a-clickonce-application.md)」を参照してください。

 必須コンポーネントは、**プロジェクト デザイナー** の **[発行]** ペインからアクセスできる **[必須コンポーネント]** ダイアログ ボックスで管理されます。

> [!NOTE]
> あらかじめ指定された必須コンポーネントの一覧に加えて、独自のコンポーネントを一覧に追加できます。 詳細については、「[ブートストラップ パッケージの作成](../deployment/creating-bootstrapper-packages.md)」を参照してください。

### <a name="to-specify-prerequisites-to-install-with-a-clickonce-application"></a>ClickOnce アプリケーションと共にインストールする必須コンポーネントを指定するには

1. **ソリューション エクスプ ローラー** でプロジェクトを選択し、 **[プロジェクト]** メニューの **[プロパティ]** をクリックします。

2. **[発行]** ペインを選択します。

3. **[必須コンポーネント]** ボタンをクリックして、 **[必須コンポーネント]** ダイアログ ボックスを開きます。

4. **[必須コンポーネント]** ダイアログ ボックスの **[必須コンポーネントをインストールするセットアップ プログラムを作成する]** チェック ボックスをオンにします。

5. **[必須コンポーネント]** の一覧で、インストールするコンポーネントをオンにし、 **[OK]** をクリックします。

     選択したコンポーネントがアプリケーションと共にパッケージ化され、発行されます。

### <a name="to-specify-a-different-download-location-for-prerequisites"></a>必須コンポーネントの別のダウンロード場所を指定するには

1. **ソリューション エクスプ ローラー** でプロジェクトを選択し、 **[プロジェクト]** メニューの **[プロパティ]** をクリックします。

2. **[発行]** ペインを選択します。

3. **[必須コンポーネント]** ボタンをクリックして、 **[必須コンポーネント]** ダイアログ ボックスを開きます。

4. **[必須コンポーネント]** ダイアログ ボックスの **[必須コンポーネントをインストールするセットアップ プログラムを作成する]** チェック ボックスをオンにします。

5. **[必須コンポーネントのインストール場所を指定してください]** セクションで、 **[次の場所から必須コンポーネントをダウンロードする]** を選択します。

6. ドロップダウン リストから場所を選択するか、URL、ファイル パス、または FTP の場所を入力して、 **[OK]** をクリックします。

    > [!NOTE]
    > 指定したコンポーネントのインストーラーが指定した場所に存在することを確認する必要があります。

## <a name="see-also"></a>関連項目
- [ClickOnce アプリケーションの発行](../deployment/publishing-clickonce-applications.md)
- [方法: 発行ウィザードを使用して ClickOnce アプリケーションを発行する](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)