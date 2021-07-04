---
title: デコレーターのプロパティ
description: デコレーターは、図の図形またはコネクタに表示されるアイコン、テキスト、または展開と折りたたみのシェブロンであることについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- Domain-Specific Language, decorators
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 2f3436bb800142e7c85594f4b05cef6fb45c4489
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2021
ms.locfileid: "112390803"
---
# <a name="properties-of-decorators"></a>デコレーターのプロパティ
デコレーターとは、図の図形またはコネクタに表示されるアイコン、テキスト、または展開と折りたたみのシェブロンです。 次の表では、3 種類のデコレーターのプロパティを示します。 一部のプロパティは、図形デコレーターまたはコネクタ デコレーターにのみ表示されます。

 詳細については、「[方法: ドメイン固有言語を定義する](../modeling/how-to-define-a-domain-specific-language.md)」を参照してください。 これらのプロパティの使用方法の詳細については、「[ドメイン固有言語のカスタマイズと拡張](../modeling/customizing-and-extending-a-domain-specific-language.md)」を参照してください。

## <a name="expandcollapse-decorator"></a>展開と折りたたみデコレーター

|プロパティ|説明|Default|
|-|-|-|
|DisplayName|生成されたデザイナーに表示されるデコレーターの名前。|Expand Collapse Decorator|
|名前|デコレーターの名前。|ExpandCollapseDecorator|
|メモ|このデコレーターに関連付けられる私的な覚書。|\<none>|
|HorizontalOffset|デコレーターの既定の位置を基準にした横方向のオフセット (インチ単位)。 (図形のみ)。|0|
|VerticalOffset|デコレーターの既定の位置を基準にした縦方向のオフセット (インチ単位)。 (図形のみ)。|0|
|OffsetFromLine|デコレーターの既定の位置を基準にした線からのデコレーターのオフセット (インチ単位)。 (コネクタのみ)。|0|
|OffsetFromShape|デコレーターの既定の位置を基準にした図形からのデコレーターのオフセット (インチ単位)。 (コネクタのみ)。|0|
|[位置]|デコレーターの既定の位置。|SourceTop|

## <a name="icon-decorator"></a>アイコン デコレーター

|プロパティ|説明|Default|
|-|-|-|
|DefaultIcon|表示されるアイコンまたは画像ファイルのパス。|\<none>|
|DisplayName|生成されたデザイナーに表示されるデコレーターの名前。|アイコン デコレーター|
|名前|デコレーターの名前。|IconDecorator|
|メモ|デコレーターに関連付けられる私的な覚書。|\<none>|
|HorizontalOffset|デコレーターの既定の位置を基準にした横方向のオフセット (インチ単位)。 (図形のみ)。|0|
|VerticalOffset|デコレーターの既定の位置を基準にした縦方向のオフセット (インチ単位)。 (図形のみ)。|0|
|OffsetFromLine|デコレーターの既定の位置を基準にした線からのデコレーターのオフセット (インチ単位)。 (コネクタのみ)。|0|
|OffsetFromShape|デコレーターの既定の位置を基準にした図形からのデコレーターのオフセット (インチ単位)。 (コネクタのみ)。|0|
|[位置]|デコレーターの既定の位置。|SourceTop|

## <a name="textdecorator"></a>TextDecorator

|プロパティ|説明|Default|
|-|-|-|
|DefaultText|既定で表示されるテキスト。|Label|
|DisplayName|生成されたデザイナーに表示されるデコレーターの名前。|Label|
|FontSize|デコレーターに表示されるテキストのフォント サイズ。|8|
|FontStyle|デコレーターに表示されるテキストのフォント スタイル。|通常|
|名前|デコレーターの名前。|Label|
|メモ|デコレーターに関連付けられる私的な覚書。|\<none>|
|HorizontalOffset|デコレーターの既定の位置を基準にした横方向のオフセット (インチ単位)。 (図形のみ)。|0|
|VerticalOffset|デコレーターの既定の位置を基準にした縦方向のオフセット (インチ単位)。 (図形のみ)。|0|
|OffsetFromLine|デコレーターの既定の位置を基準にした線からのデコレーターのオフセット (インチ単位)。 (コネクタのみ)。|0|
|OffsetFromShape|デコレーターの既定の位置を基準にした図形からのデコレーターのオフセット (インチ単位)。 (コネクタのみ)。|0|
|[位置]|デコレーターの既定の位置。|TargetBottom|

## <a name="see-also"></a>こちらもご覧ください

- [ドメイン固有言語ツールの用語集](/previous-versions/bb126564(v=vs.100))