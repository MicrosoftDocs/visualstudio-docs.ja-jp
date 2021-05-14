---
title: コード分析を用いたチェックイン ポリシーに関するバージョンの互換性
ms.date: 11/04/2016
description: Team System 2008 Team Foundation Server と Team Foundation Server 2010 での Visual Studio チェックイン ポリシーの評価方法の違いについて説明します。
ms.custom: SEO-VS-2020
ms.topic: conceptual
helpviewer_keywords:
- version compatibility, code analysis check-in policy
- check-in policies, version compatibility for code analysis
ms.assetid: 1af376e3-3be7-4445-803b-76a858567a5b
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 24a97e9175e75d8018aff269066f13a796e1cf64
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99867673"
---
# <a name="version-compatibility-for-code-analysis-check-in-policies"></a>コード分析を用いたチェックイン ポリシーに関するバージョンの互換性

さまざまなバージョンの [!INCLUDE[esprtfc](../code-quality/includes/esprtfc_md.md)] を使用してコード分析チェックイン ポリシーを評価および作成する必要がある場合は、[!INCLUDE[vstsTfsOrcasLong](../code-quality/includes/vststfsorcaslong_md.md)] と [!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)] でのチェックイン ポリシーの評価方法の違いを理解しておく必要があります。

## <a name="version-compatibility-for-evaluating-check-in-policies"></a>チェックイン ポリシーの評価に関するバージョンの互換性

- コード分析チェックイン ポリシーが [!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)] で評価される場合、[!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)] に存在しても、[!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)] には存在しないルールはすべて無視されます。

- コード分析チェックイン ポリシーが [!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)] で評価される場合、[!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)] 専用の新しいルールはすべて無視されます。

- コード分析チェックイン ポリシーでルール アセンブリが指定されている場合、[!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)] では、認識されていないアセンブリによって指定されているすべてのルールが無視されます。

- コード分析チェックイン ポリシーで、[!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)] で認識されていないルール アセンブリが指定されている場合は、メッセージが表示されます。

## <a name="version-compatibility-for-authoring-check-in-policies"></a>チェックイン ポリシーの作成に関するバージョンの互換性

- [!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)] バージョンの [!INCLUDE[esprtfc](../code-quality/includes/esprtfc_md.md)] を使用してコード分析チェックイン ポリシーを作成した場合、[!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)] バージョンの [!INCLUDE[esprtfc](../code-quality/includes/esprtfc_md.md)] を使用して変更することはできません。 また、[!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)] でそのポリシーを評価することはできません。

- [!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)] の [!INCLUDE[esprtfc](../code-quality/includes/esprtfc_md.md)] を使用してコード分析チェックイン ポリシーを作成した場合、[!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)] の [!INCLUDE[esprtfc](../code-quality/includes/esprtfc_md.md)] を使用して変更できます。また、[!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)] でそのポリシーを評価することもできます。 [!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)] の [!INCLUDE[esprtfc](../code-quality/includes/esprtfc_md.md)] を使用してポリシーを変更すると、[!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)] の [!INCLUDE[esprtfc](../code-quality/includes/esprtfc_md.md)] を使用してポリシーを編集することはできなくなります。 [!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)] では、厳密な名前の不一致に関する問題のないポリシーを評価できます。

- [!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)] と [!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)] の両方に適用されるルール設定を使用してコード分析チェックイン ポリシーを作成するには、[!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)] でポリシーを作成し、必要なすべての変更を加えて、ポリシーを保存する必要があります。 ルールの変更が [!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)] にのみ存在する場合は、[!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)] でポリシーを変更して保存します。

   [!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)] でポリシーを保存すると、[!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)] にのみ存在するルールの設定を変更できなくなります。
