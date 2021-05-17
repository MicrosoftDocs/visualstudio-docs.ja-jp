---
title: 製品マニフェストを作成する | Microsoft Docs
description: 1 つの製品マニフェストと各ロケールのパッケージ マニフェストを含むパッケージを使用して、ClickOnce アプリケーションの前提条件を配置する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- product files [ClickOnce]
- product files [Windows Installer]
- prerequisites, custom bootstrapper package
- dependencies, custom bootstrapper package
ms.assetid: 2d316aaa-8bc0-4ce5-90ab-23b3eac0b5dd
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 40a620023dad754e3de4fedb9bc4fdbe7b7835a5
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99861232"
---
# <a name="how-to-create-a-product-manifest"></a>方法: 製品マニフェストを作成する
アプリケーションの前提条件を配置するには、ブートストラップ パッケージを作成します。 ブートストラップ パッケージには、ロケールごとのパッケージ マニフェストを除く、単一の製品マニフェスト ファイルが含まれています。 パッケージ マニフェストには、パッケージのローカライズ固有の側面が含まれています。 これには、文字列、エンドユーザー ライセンス契約、および言語パックが含まれます。

 パッケージ マニフェストの詳細については、「[方法: パッケージ マニフェストを作成する](../deployment/how-to-create-a-package-manifest.md)」を参照してください。

## <a name="create-the-product-manifest"></a>製品マニフェストを作成する

#### <a name="to-create-the-product-manifest"></a>製品マニフェストを作成するには

1. ブートストラップ パッケージ用のディレクトリを作成します。 この例では、C:\package を使用します。

2. Visual Studio で、*package.xml* という新しい XML ファイルを作成し、*C:\package* フォルダーに保存します。

3. 次の XML を追加して、パッケージの XML 名前空間と製品コードを記述します。 製品コードをパッケージの一意の識別子に置き換えます。

    ```xml
    <Product
    xmlns="http://schemas.microsoft.com/developer/2004/01/bootstrapper"
    ProductCode="Custom.Bootstrapper.Package">
    ```

4. XML を追加して、パッケージに依存関係があることを指定します。 この例では、Microsoft Windows インストーラー 3.1 の依存関係を使用します。

    ```xml
    <RelatedProducts>
        <DependsOnProduct Code="Microsoft.Windows.Installer.3.1" />
      </RelatedProducts>
    ```

5. ブートストラップ パッケージ内のすべてのファイルを一覧表示する XML を追加します。 この例では、*CorePackage.msi* パッケージのファイル名を使用します。

    ```xml
    <PackageFiles>
        <PackageFile Name="CorePackage.msi"/>
    </PackageFiles>
    ```

6. *CorePackage.msi* ファイルを *C:\package* フォルダーにコピーまたは移動します。

7. ブートストラップ コマンドを使用してパッケージをインストールするには、XML を追加します。 ブートストラップは自動的に **/qn** フラグを *.msi* ファイルに追加します。これはサイレント インストールされます。 ファイルが *.exe* の場合、ブートストラップはシェルを使用して *.exe* ファイルを実行します。 次の XML には *CorePackage.msi* の引数が示されていませんが、コマンドライン引数を `Arguments` 属性に含めることができます。

    ```xml
    <Commands>
        <Command PackageFile="CorePackage.msi" Arguments="">
    ```

8. 次の XML を追加して、このブートストラップ パッケージがインストールされているかどうかを確認します。 製品コードを再頒布可能コンポーネントの GUID に置き換えます。

    ```xml
    <InstallChecks>
        <MsiProductCheck
            Property="IsMsiInstalled"
            Product="{XXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX}"/>
    </InstallChecks>
    ```

9. ブートストラップ コンポーネントが既にインストールされているかどうかによって、ブートストラップの動作を変更するには、XML を追加します。 コンポーネントがインストールされている場合、ブートストラップ パッケージは実行されません。 次の XML は、現在のユーザーが管理者であるかどうかを確認します。このコンポーネントには管理者特権が必要です。

    ```xml
    <InstallConditions>
        <BypassIf
           Property="IsMsiInstalled"
           Compare="ValueGreaterThan" Value="0"/>
        <FailIf Property="AdminUser"
            Compare="ValueNotEqualTo" Value="True"
            String="NotAnAdmin"/>
    </InstallConditions>
    ```

10. インストールが正常に完了したときに再起動が必要な場合は、XML を追加して終了コードを設定します。 次の XML は、ブートストラップがパッケージのインストールを続行しないことを示す、Fail および FailReboot の終了コードを示しています。

    ```xml
    <ExitCodes>
        <ExitCode Value="0" Result="Success"/>
        <ExitCode Value="1641" Result="SuccessReboot"/>
        <ExitCode Value="3010" Result="SuccessReboot"/>
        <DefaultExitCode Result="Fail" String="GeneralFailure"/>
    </ExitCodes>
    ```

11. 次の XML を追加して、ブートストラップ コマンドのセクションを終了します。

    ```xml
        </Command>
    </Commands>
    ```

12. *C:\package* フォルダーを Visual Studio ブートストラップ ディレクトリに移動します。 Visual Studio 2010 の場合、これは *\Program Files\Microsoft SDKs\Windows\v7.0A\Bootstrapper\Packages* ディレクトリです。

## <a name="example"></a>例
 製品マニフェストには、カスタムの必須コンポーネントのインストール手順が含まれています。

```xml
<?xml version="1.0" encoding="utf-8" ?>
<Product
  xmlns="http://schemas.microsoft.com/developer/2004/01/bootstrapper"
  ProductCode="Custom.Bootstrapper.Package">

  <RelatedProducts>
    <DependsOnProduct Code="Microsoft.Windows.Installer.3.1" />
  </RelatedProducts>

  <PackageFiles>
    <PackageFile Name="CorePackage.msi"/>
  </PackageFiles>

  <InstallChecks>
    <MsiProductCheck Product="IsMsiInstalled"
      Property="{XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX}"/>
  </InstallChecks>

  <Commands>
    <Command PackageFile="CorePackage.msi" Arguments="">

      <InstallConditions>
        <BypassIf Property="IsMsiInstalled"
          Compare="ValueGreaterThan" Value="0"/>
        <FailIf Property="AdminUser"
          Compare="ValueNotEqualTo" Value="True"
         String="NotAnAdmin"/>
      </InstallConditions>

      <ExitCodes>
        <ExitCode Value="0" Result="Success"/>
        <ExitCode Value="1641" Result="SuccessReboot"/>
        <ExitCode Value="3010" Result="SuccessReboot"/>
        <DefaultExitCode Result="Fail" String="GeneralFailure"/>
      </ExitCodes>
    </Command>
  </Commands>
</Product>
```

## <a name="see-also"></a>関連項目
- [製品およびパッケージ スキーマ リファレンス](../deployment/product-and-package-schema-reference.md)