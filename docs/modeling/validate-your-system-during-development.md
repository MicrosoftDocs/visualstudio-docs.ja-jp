---
title: 開発時のシステムの検証
description: Visual Studio を使用して、ソフトウェアがユーザーの要件とシステムのアーキテクチャに合致した状態を維持する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- dependency diagrams
author: JoshuaPartlow
ms.author: joshuapa
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: bac26664a2ef98cffbd60eee0647b39dd1108675
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99924310"
---
# <a name="validate-your-system-during-development"></a>開発時のシステムの検証

Visual Studio を使用すると、ソフトウェアがユーザーの要件とシステムのアーキテクチャに合致した状態を維持できます。

これらの各機能をサポートする Visual Studio のバージョンを確認するには、「 [Version support for architecture and modeling tools](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)」を参照してください。

## <a name="key-tasks"></a>主なタスク

ソフトウェアを検証するには、次のタスクを使用します。

|**タスク**|**関連するトピック**|
|-|-|
|**ソフトウェアがユーザーの要件を満たしているか確認する**:<br /><br />システムとそのコンポーネントのテストを編成する際に、要件モデルとアーキテクチャ モデルを使用します。 こうすることで、ユーザーやその他の利害関係者にとって重要な要求をテストしやすくなり、要求が変更された場合にすばやくテストを更新することができます。|- [モデルからテストを開発する](../modeling/develop-tests-from-a-model.md)|
|**ソフトウェアが、意図されたシステム設計に合致した状態を保っているか確認する:**<br /><br />依存関係図は、アプリケーションのコンポーネント間の、意図された依存関係を表します。 開発中に、コード内の実際の依存関係が、意図された設計に準拠しているか検証できます。|- [コードからの依存関係図の作成](../modeling/create-layer-diagrams-from-your-code.md)<br />- [依存関係図を使用したコードの検証](../modeling/validate-code-with-layer-diagrams.md)|

## <a name="external-resources"></a>外部リソース

|**カテゴリ**|**リンク**|
|-|-|
|**ビデオ**|![ビデオへのリンク](../data-tools/media/playvideo.gif) [チャンネル 9: Doug Seven: Visual Studio 2010 でのコードの理解およびシステム設計](https://channel9.msdn.com/shows/VS2010Launch/Doug-Seven-Code-Understanding-and-Systems-Design-with-Visual-Studio-2010)<br /><br /> ![ビデオへのリンク](../data-tools/media/playvideo.gif) [チャンネル 9: アプリケーションの設計](https://channel9.msdn.com/blogs/clinted/uml-with-vs-2010-part-5-architecting-an-application))|
|**フォーラム**|- [Visual Studio の視覚化ツールとモデリング ツール](https://social.msdn.microsoft.com/Forums/en-US/home?forum=vsarch)<br />- [Visual Studio 機能拡張](https://social.msdn.microsoft.com/Forums/vstudio/home?forum=vsx)|

## <a name="see-also"></a>関連項目

- [ユーザー要件のモデリング](../modeling/model-user-requirements.md)
- [アーキテクチャの分析とモデル化](../modeling/analyze-and-model-your-architecture.md)

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]
