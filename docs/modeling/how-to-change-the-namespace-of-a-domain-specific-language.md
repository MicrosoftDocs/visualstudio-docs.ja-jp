---
title: '方法: ドメイン固有言語の名前空間を変更する'
description: ドメイン固有言語の名前空間を変更する方法について説明します。
ms.date: 10/31/2018
ms.topic: how-to
titleSuffix: ''
helpviewer_keywords:
- Domain-Specific Language, namespace
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.custom: SEO-VS-2020
ms.workload:
- multiple
ms.openlocfilehash: db9043c2a4c5abd19c839d2586709412d7607019
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2021
ms.locfileid: "112387308"
---
# <a name="how-to-change-the-namespace-of-a-domain-specific-language"></a>方法: ドメイン固有言語の名前空間を変更する

ドメイン固有言語の名前空間を変更することができます。 **DSL エクスプローラー**、Dsl パッケージ プロジェクトのプロパティ、およびアセンブリ情報に変更を加えます。

## <a name="to-change-the-namespace-of-a-domain-specific-language"></a>ドメイン固有言語の名前空間を変更するには

1. **DSL エクスプローラー** で、**Dsl** ノードを選択します。

2. **[プロパティ]** ウィンドウで、 **[名前空間]** プロパティを変更します。

3. ソリューションを保存し、テンプレートを変換します。

4. **[プロジェクト]** メニューで **[Dsl プロパティ]** を選択します。

   プロジェクトのプロパティが表示されます。

5. **[アプリケーション]** タブを選択します。

6. **[既定の名前空間]** プロパティを新しい名前空間の名前に変更します。

7. アセンブリの名前も変更する場合は、 **[アセンブリ名プロパティ]** を変更します。

8. アセンブリ名を変更した場合は、DslPackage\Package.tt を開き、次の行を更新します。

   `string dslAssembly = "YourDSLassembly.Dsl.dll";`

9. カスタム コードを記述した場合は、コード ファイル内の名前空間とクラス参照を必ず変更してください。

10. Visual Studio の実験用インスタンスをリセットします。

    1. **\Users\\** _{your name}_ **\AppData\Local\Microsoft\VisualStudio\\\*Exp** を削除します。

    2. Windows の **[スタート]** メニューで、 **[すべてのプログラム]**  >  **[Microsoft Visual Studio 2010 SDK]**  >  **[ツール]**  >  **[実験用インスタンスのリセット]** を選択します。

11. **[ビルド]** メニューの **[ソリューションのリビルド]** をクリックします。

## <a name="see-also"></a>関連項目

[ドメイン固有言語ツールの用語集](/previous-versions/bb126564(v=vs.100))