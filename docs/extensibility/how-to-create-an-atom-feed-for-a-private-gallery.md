---
title: '方法: プライベート ギャラリーの Atom フィードの作成 | Microsoft Docs'
description: 拡張機能を含むイントラネットの場所に Atom (RSS) フィードを作成し、そのフィードをプライベート ギャラリーとして拡張機能と更新プログラムに追加することができます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- Atom feed, VSIX private galleries
- VSIX private galleries, Atom feed
ms.assetid: 5897f538-9c41-486f-97d9-a1976d20d9fd
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 2a83d5aa68f6f631243fbbfcad7cf28b25e7bc70
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105057378"
---
# <a name="how-to-create-an-atom-feed-for-a-private-gallery"></a>方法: プライベート ギャラリーの Atom フィードの作成
拡張機能を含むイントラネットの場所に Atom (RSS) フィードを作成し、そのフィードをプライベート ギャラリーとして **拡張機能と更新プログラム** に追加することができます。 詳細については、「[プライベート ギャラリー](../extensibility/private-galleries.md)」を参照してください。

## <a name="create-an-atom-feed"></a>Atom フィードを作成する
 Atom フィードをプライベート ギャラリーとして作成するには、まず、拡張機能 ( *.vsix* ファイル) をフォルダーに集めます。 必要に応じて、サブフォルダーに整理することができます。 また、以下のリソースも必要です。

- 拡張機能をプライベート ギャラリーとして使用できるようにする *atom.xml* ファイル。 *atom.xml* ファイルを **拡張機能と更新プログラム** に接続する方法の詳細については、「[プライベート ギャラリー](../extensibility/private-galleries.md)」を参照してください。

- 拡張機能から抽出されたイメージ ファイル (スクリーンショットなど) を含むフォルダー。 *atom.xml* ファイルには、**拡張機能と更新プログラム** で使用できるように、これらのイメージへの相対リンクが含まれています。

  たとえば、フォルダーに次の 2 つの拡張機能を収集したとします。

- 空の VSIX プロジェクトテンプレートである *Template_Wizard_239.vsix*。

- 選択した単語のすべてのインスタンスを強調表示するツールである *SelectionHighlight.vsix*。

  *atom.xml* ファイルの内容は、次の例のようになります。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<feed xmlns="http://www.w3.org/2005/Atom">
  <title type="text" />
  <id>uuid:bcecded5-97c8-4d24-96f1-7d9e16652433;id=1</id>
  <updated>2011-04-14T21:25:48Z</updated>
  <entry>
    <id>SelectionHighlight..a14874d2-8199-4a60-af8a-11d6447813aa</id>
    <title type="text">Highlight all occurrences of selected word</title>
    <summary type="text">This extends the editor to highlight ....</summary>
    <published>2011-04-14T14:24:51-07:00</published>
    <updated>2011-04-14T14:24:22-07:00</updated>
    <author>
      <name>Microsoft</name>
    </author>
    <link rel="icon" href="VSIXImages/SelectionHighlight..a14874d2-8199-4a60-af8a-11d6447813aa_Icon_SelectionHighlightIcon.jpg" />
    <link rel="previewimage" href="VSIXImages/SelectionHighlight..a14874d2-8199-4a60-af8a-11d6447813aa_PreviewImage_SelectionHighlight.jpg" />
    <content type="application/octet-stream" src="SelectionHighlight.vsix" />
    <Vsix xmlns="http://schemas.microsoft.com/developer/vsx-syndication-schema/2010" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
      <Id>SelectionHighlight..a14874d2-8199-4a60-af8a-11d6447813aa</Id>
      <Version>1.31</Version>
      <References />
      <Rating xsi:nil="true" />
      <RatingCount xsi:nil="true" />
      <DownloadCount xsi:nil="true" />
    </Vsix>
  </entry>
  <entry>
    <id>Template_Wizard_239.Microsoft.3b38a7e3-5cbc-4389-a92a-d82tyc2ed592</id>
    ...
  </entry>
</feed>
```

 2 つのリンク タグにより、生成されるイメージのフォルダー内のスクリーンショットが参照されていることに注意してください。

## <a name="see-also"></a>関連項目
- [プライベート ギャラリー](../extensibility/private-galleries.md)
