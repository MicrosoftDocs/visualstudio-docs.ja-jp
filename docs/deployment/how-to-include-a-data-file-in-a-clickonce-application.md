---
title: ClickOnce アプリにデータ ファイルを含める
description: ClickOnce アプリケーションに任意の種類のデータ ファイルを追加して、インストール先コンピューターのローカル ディスク上のデータ ディレクトリに格納する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, data
- deploying applications [ClickOnce], data files
- data access, ClickOnce applications
ms.assetid: 89ee46ef-bc8c-4ab0-a2ac-1220f9da06fc
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 4f4b5e8fe9d17a6de9abac2681074dcfc162e9b7
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99900599"
---
# <a name="how-to-include-a-data-file-in-a-clickonce-application"></a>方法: ClickOnce アプリケーションにデータ ファイルを含める
インストールした各 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションには、インストール先コンピューターのローカル ディスク上のデータ ディレクトリが割り当てられます。ここでアプリケーションは独自のデータを管理できます。 データ ファイルには、テキスト ファイル、XML ファイル、Microsoft Access データベース ( *.mdb*) ファイルなど、任意の種類のファイルを含めることができます。 以下の手順は、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションに任意の種類のデータ ファイルを追加する方法を示しています。

### <a name="to-include-a-data-file-by-using-mageexe"></a>Mage.exe を使用してデータ ファイルを含めるには

1. アプリケーションの他のファイルと共に、データ ファイルをアプリケーション ディレクトリに追加します。

    通常、アプリケーション ディレクトリは、配置の現在のバージョン (例: v1.0.0.0) でラベル付けされたディレクトリになります。

2. データ ファイルをリストに含めるように、アプリケーション マニフェストを更新します。

    `mage -u v1.0.0.0\Application.manifest -FromDirectory v1.0.0.0`

    このタスクを実行すると、アプリケーション マニフェスト内のファイル リストが再作成され、ハッシュ シグネチャも自動的に生成されます。

3. 任意のテキスト エディターまたは XML エディターでアプリケーション マニフェストを開き、最近追加したファイルの `file` 要素を見つけます。

    `Data.xml` という名前の XML ファイルを追加した場合、ファイルは次のコード例のようになります。

   `<file name="Data.xml" hash="23454C18A2DC1D23E5B391FEE299B1F235067C59" hashalg="SHA1" asmv2:size="39500" />`

4. この要素に `type` 属性を追加し、値として `data` を指定します。

   `<file name="Data.xml" writeableType="applicationData" hash="23454C18A2DC1D23E5B391FEE299B1F235067C59" hashalg="SHA1" asmv2:size="39500" />`

5. キー ペアまたは証明書を使用してアプリケーション マニフェストに再署名してから、配置マニフェストに再署名します。

    アプリケーション マニフェストのハッシュが変更されたため、配置マニフェストに再署名する必要があります。

    `mage -s app manifest -cf cert_file -pwd password`

    `mage -u deployment manifest -appm app manifest`

    `mage -s deployment manifest -cf certfile -pwd password`

### <a name="to-include-a-data-file-by-using-mageuiexe"></a>MageUI.exe を使用してデータ ファイルを含めるには

1. アプリケーションの他のファイルと共に、データ ファイルをアプリケーション ディレクトリに追加します。

2. 通常、アプリケーション ディレクトリは、配置の現在のバージョン (例: v1.0.0.0) でラベル付けされたディレクトリになります。

3. **[ファイル]** メニューの **[開く]** をクリックして、アプリケーション マニフェストを開きます。

4. **[ファイル]** タブを選択します。

5. タブの上部にあるテキスト ボックスに、アプリケーションのファイルが格納されているディレクトリを入力し、 **[作成]** をクリックします。

     データ ファイルがグリッドに表示されます。

6. データ ファイルの **[ファイルの種類]** の値を **[データ]** に設定します。

7. アプリケーション マニフェストを保存し、ファイルに再署名します。

     *MageUI.exe* から、ファイルに再署名するよう求められます。

8. 配置マニフェストに再署名します。

     アプリケーション マニフェストのハッシュが変更されたため、配置マニフェストに再署名する必要があります。

## <a name="see-also"></a>関連項目
- [ClickOnce アプリケーションにおけるローカル データおよびリモート データへのアクセス](../deployment/accessing-local-and-remote-data-in-clickonce-applications.md)