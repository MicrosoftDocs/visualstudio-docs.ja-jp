---
title: パッケージ マニフェストを作成する |Microsoft Docs
description: ブートストラップ パッケージを使用して ClickOnce アプリケーションの前提条件を配置する方法について説明します。これには、各ロケールのパッケージ マニフェストが含まれます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- package files [Windows Installer]
- package files [ClickOnce]
- prerequisites, custom bootstrapper package
- dependencies, custom bootstrapper packages
ms.assetid: 5aecc507-2764-42f2-ae6f-c227971cf0af
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: cef6cd23a1e5ff1e00e2d4d93313ee1e9355ece2
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99927562"
---
# <a name="how-to-create-a-package-manifest"></a>方法: パッケージ マニフェストを作成する
アプリケーションの前提条件を配置するには、ブートストラップ パッケージを使用します。 ブートストラップ パッケージには、ロケールごとのパッケージ マニフェストを除く、単一の製品マニフェスト ファイルが含まれています。 ローカライズされたさまざまなバージョンで共有される機能は、製品マニフェストに入れる必要があります。

 製品マニフェストの詳細については、「[方法: 製品マニフェストを作成する](../deployment/how-to-create-a-product-manifest.md)」を参照してください。

## <a name="create-the-package-manifest"></a>パッケージ マニフェストを作成する

#### <a name="to-create-the-package-manifest"></a>パッケージ マニフェストを作成するには

1. ブートストラップ パッケージ用のディレクトリを作成します。 この例では、*C:\package* を使用します。

2. ロケールの名前 (英語の場合は *en* など) を使用してサブディレクトリを作成します。

3. Visual Studio で、*package.xml* という名前の XML ファイルを作成し、*C:\package\en* フォルダーに保存します。

4. ブートストラップ パッケージの名前、このローカライズされたパッケージマニフェストのカルチャ、およびオプションの使用許諾契約を列挙するための XML を追加します。 次の XML では、後の要素で定義される変数 `DisplayName` と `Culture` を使用します。

    ```xml
    <Package
        xmlns="http://schemas.microsoft.com/developer/2004/01/bootstrapper"
        Name="DisplayName"
        Culture="Culture"
        LicenseAgreement="eula.txt">
    ```

5. ロケール固有のディレクトリにあるすべてのファイルを列挙するための XML を追加します。 次の XML では、**en** ロケールに適用される *eula.txt* という名前のファイルを使用します。

    ```xml
    <PackageFiles>
      <PackageFile Name="eula.txt"/>
    </PackageFiles>
    ```

6. ブートストラップ パッケージ用のローカライズ可能な文字列を定義するための XML を追加します。 次の XML では、**en** ロケール用のエラー文字列を追加します。

    ```xml
      <Strings>
        <String Name="DisplayName">Custom Bootstrapper Package</String>
        <String Name="CultureName">en</String>
        <String Name="NotAnAdmin">You must be an administrator to install
    this package.</String>
        <String Name="GeneralFailure">A general error has occurred while
    installing this package.</String>
    </Strings>
    ```

7. *C:\package* フォルダーを Visual Studio ブートストラップ ディレクトリにコピーします。 Visual Studio 2010 の場合、これは *\Program Files\Microsoft SDKs\Windows\v7.0A\Bootstrapper\Packages* ディレクトリです。

## <a name="example"></a>例
 パッケージ マニフェストには、エラー メッセージ、ソフトウェア ライセンス条項、言語パックなど、ロケール固有の情報が含まれます。

```xml
<?xml version="1.0" encoding="utf-8" ?>
<Package
  xmlns="http://schemas.microsoft.com/developer/2004/01/bootstrapper"
  Name="DisplayName"
  Culture="Culture"
  LicenseAgreement="eula.txt">

  <PackageFiles>
    <PackageFile Name="eula.txt"/>
  </PackageFiles>

  <Strings>
    <String Name="DisplayName">Custom Bootstrapper Package</String>
    <String Name="Culture">en</String>
    <String Name="NotAnAdmin">You must be an administrator to install this package.</String>
    <String Name="GeneralFailure">A general error has occurred while
installing this package.</String>
  </Strings>
</Package>
```

## <a name="see-also"></a>関連項目
- [製品およびパッケージ スキーマ リファレンス](../deployment/product-and-package-schema-reference.md)