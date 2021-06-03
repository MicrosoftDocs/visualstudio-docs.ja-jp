---
title: DSL 定義のプロパティ
description: DslDefinition プロパティで、バージョン番号付けなどのドメイン固有言語定義のプロパティが定義されることについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- Domain-Specific Language, definition file
author: JoshuaPartlow
ms.author: joshuapa
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: ef8f49e46c554efca89862c787fbfbe97c48c8f4
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99959117"
---
# <a name="properties-of-a-dsl-definition"></a>DSL 定義のプロパティ
DslDefinition プロパティでは、バージョン番号付けなどの "*ドメイン固有言語*" 定義のプロパティを定義します。 DslDefinition プロパティは、"*ドメイン固有言語デザイナー*" の図の空いている領域をクリックすると、 **[プロパティ]** ウィンドウに表示されます。

 詳細については、「[方法: ドメイン固有言語を定義する](../modeling/how-to-define-a-domain-specific-language.md)」を参照してください。 これらのプロパティの使用方法の詳細については、「[ドメイン固有言語のカスタマイズおよび拡張](../modeling/customizing-and-extending-a-domain-specific-language.md)」を参照してください。

 DslDefinition には、次の表のプロパティがあります。

|プロパティ|説明|Default|
|-|-|-|
|アクセス修飾子|ドメイン クラスのアクセス修飾子が public か internal かを決定します。|public|
|カスタム属性|ドメイン クラスのカスタム定義の属性。<br /><br /> **メモ** 属性を追加するには、[参照] ボタンを使用します。|\<none>|
|会社名|システム レジストリ内の現在の会社名の名前。|現在の会社名|
|名前|このドメイン クラスの名前。|現在の名前|
|名前空間|このドメイン クラスに関係する名前空間。|現在の名前空間|
|パッケージ GUID|この DSL 用に生成される Visual Studio パッケージの GUID。|\<none>|
|Package Namespace|この DSL 用に生成された Visual Studio パッケージの名前空間。|\<none>|
|製品名|この DSL 用に生成される Visual Studio パッケージに登録する製品の名前。|\<none>|
|Notes|このドメイン クラスに関連付けられているメモ。|\<none>|
|説明|このドメイン クラスの説明。|\<none>|
|表示名|生成されたデザイナーで、このドメイン クラス向けに表示される名前。|\<none>|
|ヘルプ キーワード|このドメイン クラスに関連付けられているヘルプ キーワード。|\<none>|
|ビルド|このドメイン固有言語定義のインクリメンタル ビルド番号。|0|
|メジャー バージョン|このドメイン固有言語定義のインクリメンタル メジャー ビルド番号。|1|
|マイナー バージョン|このドメイン固有言語定義のインクリメンタル マイナー ビルド番号。|0|
|リビジョン|このドメイン固有言語定義のインクリメンタル リビジョン ビルド番号。|0|

## <a name="see-also"></a>関連項目

- [ドメイン固有言語ツールの用語集](/previous-versions/bb126564(v=vs.100))