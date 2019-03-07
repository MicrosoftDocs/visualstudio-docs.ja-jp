---
title: XML スキーマ
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.xmleditor.schemasdialog
ms.assetid: 0271fa26-2205-49bd-96e0-ae1441571808
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f5323582bfe945bc031b9fd02fcf96bb615bcceb
ms.sourcegitcommit: 3ca33862c1cfc3ccb83de3e95f1e69e860ab143a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2019
ms.locfileid: "57524924"
---
# <a name="xml-schemas-dialog-box"></a>XML スキーマ ダイアログ ボックス

**XML スキーマ**どの XML スキーマ定義言語 (XSD) スキーマ、XML ドキュメントに関連付けるを選択するダイアログ ボックスを使用します。 スキーマ キャッシュにあるスキーマを選択することも、キャッシュ内に置かれていないスキーマを指定することもできます。 選択したスキーマは、スキーマ セットの一部と見なされます。 そのスキーマ セットは、IntelliSense と XML ドキュメントの検証に使用されます。

アクセスできる、 **XML スキーマ** ダイアログ ボックスをクリックするか、**スキーマ**ドキュメントのプロパティ ウィンドウで、または選択してボタン**スキーマ**から**XML**メニュー。

## <a name="uielement-list"></a>UIElement の一覧

**使用**

XML スキーマの使用方法を選択します。

- **自動**します。 このスキーマは現在のドキュメントで使用されていませんが、自動的な関連付けには使用できます。 XML ドキュメントでこのスキーマの `targetNamespace` に一致する名前空間を宣言すると、スキーマが自動的に関連付けられ、スキーマ セットに含まれます。

- **このスキーマを使用して、** します。 このスキーマは、現在のドキュメントで使用されています。 ユーザーがこの列をクリックしてこのスキーマが使用されることを明示的に要求したか、一致する `targetNamespace` に基づいてスキーマが自動的に関連付けられたかのいずれかです。

- **選択したスキーマを使用しないでください**します。 スキーマに一致する `targetNamespace` がある場合でも、このスキーマは現在のドキュメントで使用されません。 この設定は、スキーマ キャッシュまたはソリューションに同じスキーマのバージョンが複数存在する場合の競合を解決する際に役立ちます。

**Target Namespace**

XML スキーマに関連付けられているターゲット名前空間が表示されます。

**ファイル名**

XML スキーマ ファイル名が表示されます。

**[追加]**

開く、 **XSD スキーマを開く**ダイアログ ボックスで、スキーマ セットに追加するその他のスキーマを選択することができます。 設定のスキーマにスキーマを追加すると、**使用**列の値に設定されて**このスキーマを使用して、** します。

**削除**

現在選択されているスキーマをスキーマ セットから削除します。 この操作では、メモリ内のスキーマ キャッシュからスキーマが削除されますが、ファイル システムからは削除されません。

## <a name="see-also"></a>関連項目

- [方法: 使用する XML スキーマを選択します。](../xml-tools/how-to-select-the-xml-schemas-to-use.md)
- [スキーマ キャッシュ](../xml-tools/schema-cache.md)