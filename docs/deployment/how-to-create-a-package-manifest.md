---
title: '方法: パッケージ マニフェストを作成する |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
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
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d8083ca9a8d3025b1760edde96279a0cd557f722
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62899741"
---
# <a name="how-to-create-a-package-manifest"></a>方法: パッケージ マニフェストを作成する
アプリケーションの必須コンポーネントを展開するには、ブートス トラップ パッケージを使用できます。 ブートス トラップ パッケージには、ロケールごとに、パッケージ マニフェストが 1 つの製品マニフェスト ファイルが含まれています。 別のローカライズされたバージョン間で共有機能は、製品マニフェストに移動してください。

 マニフェストの製品の詳細については、次を参照してください。[方法。製品マニフェストを作成する](../deployment/how-to-create-a-product-manifest.md)します。

## <a name="create-the-package-manifest"></a>パッケージ マニフェストを作成します。

#### <a name="to-create-the-package-manifest"></a>パッケージ マニフェストを作成するには

1. ブートス トラップ パッケージ用のディレクトリを作成します。 この例では*C:\package*します。

2. など、ロケールの名前を持つサブディレクトリを作成*en*英語の場合。

3. Visual Studio では、という XML ファイルを作成*package.xml*、保存して、 *C:\package\en*フォルダー。

4. このローカライズされたパッケージ マニフェストと省略可能なライセンス契約のカルチャにブートス トラップ パッケージの名前を一覧表示する XML を追加します。 次の XML は、変数を使用して`DisplayName`と`Culture`、以降の要素で定義されています。

    ```xml
    <Package
        xmlns="http://schemas.microsoft.com/developer/2004/01/bootstrapper"
        Name="DisplayName"
        Culture="Culture"
        LicenseAgreement="eula.txt">
    ```

5. ロケール固有のディレクトリ内にあるすべてのファイルを一覧表示の XML を追加します。 次の XML という名前のファイルを使用して*eula.txt*に適用される、 **en**ロケール。

    ```xml
    <PackageFiles>
      <PackageFile Name="eula.txt"/>
    </PackageFiles>
    ```

6. ブートス トラップ パッケージのローカライズ可能な文字列を定義する XML を追加します。 次の XML に追加のエラー文字列、 **en**ロケール。

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

7. コピー、 *C:\package*を Visual Studio ブートス トラップ ディレクトリのフォルダー。 これは Visual Studio 2010 の場合、 *\Program Files\Microsoft SDKs\Windows\v7.0A\Bootstrapper\Packages*ディレクトリ。

## <a name="example"></a>例
 パッケージ マニフェストには、エラー メッセージ、ソフトウェア ライセンス条項、および言語パックなど、ロケールに固有の情報が含まれています。

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