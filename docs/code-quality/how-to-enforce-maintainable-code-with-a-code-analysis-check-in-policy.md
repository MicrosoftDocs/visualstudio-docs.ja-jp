---
title: コード分析のチェックイン ポリシーを使用する
ms.date: 11/04/2016
description: コード分析のチェックイン ポリシーを使用して、コードが継承、クラス結合、保守容易性、複雑さの標準に準拠していることを確認する方法について説明します。
ms.custom: SEO-VS-2020
ms.topic: how-to
helpviewer_keywords:
- code analysis, check-in policies
ms.assetid: d1b3b04f-4dd9-40e6-b2d4-b414d33fb647
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 9f061d9d10d66857a0b2506d13d6d6671f7df401
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99860044"
---
# <a name="how-to-enforce-maintainable-code-with-a-code-analysis-check-in-policy"></a>方法: コード分析のチェックイン ポリシーを使用して保守が容易なコードにする

開発者は、コード メトリックス ツールを使用して、コードの複雑さと保守容易性を測定できますが、チェックイン ポリシーの一部としてコード メトリックスを呼び出すことはできません。 ただし、コード メトリックス標準にコードが準拠していることを確認するコード分析規則を有効にし、チェックイン ポリシーで規則を適用することができます。 コード メトリックスの詳細については、「[コード メトリックスの値](../code-quality/code-metrics-values.md)」を参照してください。

継承の深さ、クラス結合、保守容易性指数、および複雑さの規則を有効にし、コード分析のチェックイン ポリシーを使用して、保守が容易なコードにすることができます。 これらの 4 つのルールはすべて、コード分析ポリシー エディターの [保守容易性の規則] カテゴリにあります。

Team Foundation のバージョン コントロールの管理者は、コード分析の保守容易性の規則をチェックイン ポリシーの要件に追加できます。 これらのチェックイン ポリシーにより、開発者は、チェックインを始める前に、これらの規則の変更に基づいてコード分析を実行することを要求されます。

## <a name="to-open-the-code-analysis-policy-editor"></a>コード分析ポリシー エディターを開くには

1. **チーム エクスプローラー** でプロジェクトを右クリックし、 **[プロジェクトの設定]** をクリックして、 **[ソース管理]** をクリックします。

     **[ソース管理]** ダイアログ ボックスが表示されます。

2. **[チェックイン ポリシー]** タブで、 **[追加]** をクリックします。

     **[チェックイン ポリシーの追加]** ダイアログ ボックスが表示されます。

3. **[チェックイン ポリシー]** の一覧で **[コード分析]** チェック ボックスをオンにして、 **[OK]** をクリックします。

     **[コード分析ポリシー エディター]** ダイアログ ボックスが表示されます。

## <a name="to-enable-code-analysis-maintainability-rules"></a>コード分析の保守容易性規則を有効にするには

1. **[コード分析ポリシー エディター]** ダイアログ ボックスの **[Rule Settings]\(規則の設定\)** で、 **[保守容易性の規則]** ノードを展開します。

2. 以下の規則のチェック ボックスをオンにします。

   - 継承の深さ: **CA1501 AvoidExcessiveInheritance** - しきい値: 5 レベルより深い警告

   - 複雑さ: **CA1502 AvoidExcessiveComplexity** - しきい値: 25 より多い警告

   - 保守容易性指数: **CA1505 AvoidUnmaintainableCode** - しきい値: 20 より少ない警告

   - クラス結合: **CA1506 AvoidExcessiveClassCoupling** - しきい値: クラスの場合は 80 より多い警告、メソッドの場合は 30 より多い警告

     また、規則違反がある場合はビルドが成功しないようにする場合は、規則の説明の横にある **[警告をエラーとして扱う]** チェック ボックスをオンにします。

3. **[OK]** をクリックします。 それ以降のチェックインに、新しいチェックイン ポリシーが適用されるようになります。

## <a name="see-also"></a>こちらもご覧ください

- [コード メトリック値](../code-quality/code-metrics-values.md)
- [コード分析のチェックイン ポリシーの作成と使用](../code-quality/how-to-create-or-update-standard-code-analysis-check-in-policies.md)
