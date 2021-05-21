---
title: '&lt;PackageFiles&gt; 要素 (ブートストラップ) | Microsoft Docs'
description: PackageFiles 要素について説明します。この要素には、Command 要素の結果として実行されるインストール パッケージを定義する PackageFile 要素が含まれています。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- <PackageFiles> element [bootstrapper]
ms.assetid: 3ea252d7-18a3-47d8-af83-47feebcfe82b
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 0fbf76fec604819d7944a7b54fa4b2421e37c111
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99925364"
---
# <a name="ltpackagefilesgt-element-bootstrapper"></a>&lt;PackageFiles&gt; 要素 (ブートストラップ)
`PackageFiles` 要素には、`Command` 要素の結果として実行されるインストール パッケージを定義する `PackageFile` 要素が含まれます。

## <a name="syntax"></a>構文

```xml
<PackageFiles
    CopyAllPackageFiles
>
    <PackageFile
        Name
        HomeSite
        CopyOnBuild
        PublicKey
        Hash
    />
</PackageFiles>
```

## <a name="elements-and-attributes"></a>要素と属性
 `PackageFiles` 要素には、次の属性があります。

|属性|説明|
|---------------|-----------------|
|`CopyAllPackageFiles`|省略可能。 `false` に設定すると、インストーラーでは `Command` 要素から参照されるファイルのみがダウンロードされます。 `true` に設定すると、すべてのファイルがダウンロードされます。<br /><br /> `IfNotHomesite` に設定したときに、`ComponentsLocation` が `HomeSite` に設定されている場合、インストーラーの動作は `False` に設定されている場合と同じになります。それ以外の場合は、`True` と同じように動作します。 この設定は、ブートストラップ自体のパッケージが HomeSite シナリオで独自の動作を実行できるようにするのに役立ちます。<br /><br /> 既定では、 `true`です。|

## <a name="packagefile"></a>PackageFile
 `PackageFile` 要素は、`PackageFiles` 要素の子です。 `PackageFiles` 要素には `PackageFile` 要素が少なくとも 1 つ必要です。

 `PackageFile` には以下の属性があります。

| 属性 | 説明 |
|---------------| - |
| `Name` | 必須。 パッケージ ファイルの名前。 これは、パッケージがインストールされる条件を定義するときに `Command` 要素によって参照される名前です。 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] などのツールでパッケージを記述するために使用されるローカライズされた名前を取得する `Strings` テーブルのキーとしても使用されます。 |
| `HomeSite` | 省略可能。 リモート サーバー上のパッケージの場所 (インストーラーに含まれていない場合)。 |
| `CopyOnBuild` | 省略可能。 ビルド時にブートストラップによるパッケージ ファイルのディスクへのコピーが必要かどうかを指定します。 既定値は true です。 |
| `PublicKey` | パッケージの証明書署名者の暗号化された公開キー。 `HomeSite` を使用する場合は必須。それ以外の場合は省略可能。 |
| `Hash` | 省略可能。 パッケージ ファイルの SHA1 ハッシュ。 これは、インストール時にファイルの整合性を確認するために使用されます。 パッケージ ファイルから同じハッシュを計算できない場合、パッケージはインストールされません。 |

## <a name="example"></a>例
 次のコード例では、.NET Framework 再頒布可能パッケージとその依存関係 (Windows インストーラーなど) のパッケージを定義します。

```xml
<PackageFiles>
    <PackageFile Name="instmsia.exe" HomeSite="InstMsiAExe" PublicKey="3082010A0282010100AA99BD39A81827F42B3D0B4C3F7C772EA7CBB5D18C0DC23A74D793B5E0A04B3F595ECE454F9A7929F149CC1A47EE55C2083E1220F855F2EE5FD3E0CA96BC30DEFE58C82732D08554E8F09110BBF32BBE19E5039B0B861DF3B0398CB8FD0B1D3C7326AC572BCA29A215908215E277A34052038B9DC270BA1FE934F6F335924E5583F8DA30B620DE5706B55A4206DE59CBF2DFA6BD154771192523D2CB6F9B1979DF6A5BF176057929FCC356CA8F440885558ACBC80F464B55CB8C96774A87E8A94106C7FF0DE968576372C36957B443CF323A30DC1BE9D543262A79FE95DB226724C92FD034E3E6FB514986B83CD0255FD6EC9E036187A96840C7F8E203E6CF050203010001"/>
    <PackageFile Name="WindowsInstaller-KB884016-v2-x86.exe" HomeSite="Msi30Exe" PublicKey="3082010A0282010100B22D8709B55CDF5599EB5262E7D3F4E34571A932BF94F20EE90DADFE9DC7046A584E9CA4D1D84441FB647E0F65EEC817DA4DDBD9D650B40C565B6C16884BBF03EE504883EC4F88939A51E394197FFAB397A5CE606D9FDD4C9338BDCD345971E686CEE98399A096B8EAE0445B1342B93A484E5472F70896E400C482017643AF61C2DBFAE5C5F00213DDF835B40F0D5236467443B1A2CA9CDD7E99F1351177FB1526018ECFE0B804782A15FD72C66076910CE74FB218181B6989B4F12F211B66EACA91C7460DB91758715856866523D10232AE64A06FDA5295FDFBDD8D34F5C10C35A347D7E91B6AFA0F45B4E8321D7019BDD1F9E5641FEB8737EA6FD40D838FFD0203010001"/>
    <PackageFile Name="dotnetfx.exe" HomeSite="DotNetFXExe" PublicKey="3082010A0282010100B22D8709B55CDF5599EB5262E7D3F4E34571A932BF94F20EE90DADFE9DC7046A584E9CA4D1D84441FB647E0F65EEC817DA4DDBD9D650B40C565B6C16884BBF03EE504883EC4F88939A51E394197FFAB397A5CE606D9FDD4C9338BDCD345971E686CEE98399A096B8EAE0445B1342B93A484E5472F70896E400C482017643AF61C2DBFAE5C5F00213DDF835B40F0D5236467443B1A2CA9CDD7E99F1351177FB1526018ECFE0B804782A15FD72C66076910CE74FB218181B6989B4F12F211B66EACA91C7460DB91758715856866523D10232AE64A06FDA5295FDFBDD8D34F5C10C35A347D7E91B6AFA0F45B4E8321D7019BDD1F9E5641FEB8737EA6FD40D838FFD0203010001"/>
    <PackageFile Name="dotnetchk.exe"/>
</PackageFiles>
```

## <a name="see-also"></a>関連項目
- [\<Product> 要素](../deployment/product-element-bootstrapper.md)
- [\<Package> 要素](../deployment/package-element-bootstrapper.md)
- [製品およびパッケージ スキーマ リファレンス](../deployment/product-and-package-schema-reference.md)