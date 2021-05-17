---
title: VSPackage のリソース | Microsoft Docs
description: VSPackage に埋め込むことができるローカライズされたリソースの種類について説明します。 また、ネイティブ サテライト UI DLL またはマネージド サテライト DLL にリソースを埋め込むこともできます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- managed VSPackages, resources in
- resources, managed VSPackages
- VSPackages, managed resources
ms.assetid: cc8c17a6-b190-4856-b001-0c1104f104b2
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: a80fc4fbfaf9a308492345ba897363d31d4669ca
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106216541"
---
# <a name="resources-in-vspackages"></a>VSPackage のリソース
ローカライズされたリソースは、ネイティブ サテライト UI DLL、マネージド サテライト DLL、またはマネージド VSPackage 自体に埋め込むことができます。

 一部のリソースは VSPackage に埋め込むことができません。 次のマネージド型を埋め込むことができます。

- 文字列

- パッケージ ロード キー (文字列でもあります)

- ツール ウィンドウのアイコン

- コンパイルされたコマンド テーブル出力 (CTO) ファイル

- CTO ビットマップ

- コマンド ライン ヘルプ

- [バージョン情報] ダイアログ ボックスのデータ

  マネージド パッケージ内のリソースは、リソース ID によって選択されます。 例外は CTO ファイルです。このファイルには、CTMENU という名前を付ける必要があります。 CTO ファイルは、リソース テーブルに `byte[]` として表示される必要があります。 他のすべてのリソース項目は、型によって識別されます。

  <xref:Microsoft.VisualStudio.Shell.PackageRegistrationAttribute> 属性を使用して、管理対象リソースが使用可能であることを [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] に示すことができます。

  :::code language="csharp" source="../../snippets/csharp/VS_Snippets_VSSDK/vssdkresources/cs/vssdkresourcespackage.cs" id="Snippet1":::
  :::code language="vb" source="../../snippets/visualbasic/VS_Snippets_VSSDK/vssdkresources/vb/vssdkresourcespackage.vb" id="Snippet1":::

  この方法で <xref:Microsoft.VisualStudio.Shell.PackageRegistrationAttribute> を設定すると、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] で <xref:Microsoft.VisualStudio.Shell.Interop.IVsShell.LoadPackageString%2A> などを使用してリソースを検索するときに、アンマネージド サテライト DLL が無視されるように指定されます。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] で同じリソース ID を持つ 2 つ以上のリソースが検出された場合は、最初に検出されたリソースが使用されます。

## <a name="example"></a>例
 次の例は、ツール ウィンドウのアイコンのマネージド表現です。

```
<data name="1001"
type="System.Resources.ResXFileRef,System.Windows.Forms">
     <value>
     MyToolWinIcon.bmp;
     System.Drawing.Bitmap,
     System.Drawing,
     Version=1.0.0.0,
     Culture=neutral,
     PublicKeyToken=b03f5f7f11d50a3a
     </value>
</data>
```

 次の例では、CTO のバイト配列を埋め込む方法を示します。この配列には、CTMENU という名前を付ける必要があります。

```
<data name="CTMENU"
type="System.Resources.ResXFileRef,System.Windows.Forms">
     <value>
     MyPackage.cto;
     System.Byte[],
     mscorlib,
     Version=1.0.0.0,
     Culture=neutral,
     PublicKeyToken=b03f5f7f11d50a3a
     </value>
</data>
```

## <a name="implementation-notes"></a>実装に関するメモ
 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] では、可能な限り VSPackage の読み込みを遅延します。 VSPackage に CTO ファイルを埋め込むと、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] では、セットアップ中 (マージされたコマンド テーブルを構築するとき) に、このような VSPackage をすべてメモリに読み込む必要があります。 リソースを VSPackage から抽出するには、VSPackage でコードを実行せずにメタデータを調べます。 VSPackage は現時点で初期化されていないため、パフォーマンスが低下することはほとんどありません。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] でセットアップ後に VSPackage からリソースが要求された場合、そのパッケージは既に読み込まれて初期化されている可能性が高いため、パフォーマンスが低下することはほとんどありません。

## <a name="see-also"></a>関連項目
- [VSPackage の管理](../../extensibility/managing-vspackages.md)
- [MFC アプリケーションのローカライズされたリソース: サテライト DLL](/cpp/build/localized-resources-in-mfc-applications-satellite-dlls)
