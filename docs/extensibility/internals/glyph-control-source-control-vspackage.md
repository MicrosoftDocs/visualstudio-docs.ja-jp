---
title: グリフ管理 (ソース管理 VSPackage) | Microsoft Docs
description: 独自のアイコンを使用してソース管理下にある項目の状態を示すことができるように、ソース管理 VSPackage でカスタム グリフを表示する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- glyphs, source control packages
- source control packages, glyphs
ms.assetid: b9413b08-b3c3-4fc3-a6e0-3dc0db3652d7
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: cb0175f3e74bf979bcbabaa5785ed9e015c5e7a1
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105061213"
---
# <a name="glyph-control-source-control-vspackage"></a>グリフ管理 (ソース管理 VSPackage)
ソース管理 VSPackage から使用できる緊密な統合の一部として、独自のグリフを表示してソース管理下にある項目の状態を示す機能があります。

## <a name="levels-of-glyph-control"></a>グリフ管理のレベル
 状態グリフは、**ソリューション エクスプローラー** や **クラス ビュー** などで、表示されたときの項目の現在の状態を示すアイコンです。 ソース管理 VSPackage では、2 つのレベルのグリフ管理を実行できます。 つまり、グリフの選択肢を [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE によって提供されるグリフの定義済みのセットに制限するか、または表示されるグリフのカスタム セットを定義することができます。

### <a name="default-set-of-glyphs"></a>グリフの既定のセット
 **ソリューション エクスプローラー** で項目に関連付けられている状態グリフを確認するために、プロジェクトでは、<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2.GetSccGlyph%2A> を使用してソース管理に状態グリフを要求します。 ソース管理 VSPackage では、グリフの選択肢を、IDE によって提供される定義済みのグリフに制限されたままにすることを決定できます。 この場合、VSPackage では、*vsshell.idl* で定義されているグリフ列挙型を表す値の配列を戻します。 詳細については、「<xref:Microsoft.VisualStudio.Shell.Interop.VsStateIcon>」を参照してください。 これは、チェックインされたグリフの南京錠や、チェックアウトされたグリフのチェック マークなどの、IDE によって設定されたグリフの定義済みのセットです。

### <a name="custom-set-of-glyphs"></a>グリフのカスタム セット
 ソース管理 VSPackage では、インストールされているときの固有の外観のために独自のグリフを使用できます。 新しいソース管理 VSPackage がアクティブになると、以前のソース管理 VSPackage がまだ読み込まれた状態であっても、非アクティブであれば、独自のグリフを使い始めることができます。 このモードでは、ソース管理 VSPackage では引き続き、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] と一貫した外観を維持するために既存のアイコンを使用できます (それが選択された場合)。

 <xref:Microsoft.VisualStudio.Shell.Interop.SVsSccManager> サービスは、VSPackage が必要に応じて実装でき、IDE によって要求されるインターフェイス <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccGlyphs> をサポートしています。 IDE が要求を行うと、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] は次に、現在登録されているソース管理 VSPackage からこのインターフェイスを取得しようとします。 このインターフェイスが登録済みの VSPackage に存在する場合、カスタム グリフに対する IDE の要求は成功します。そうでない場合、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE では、グリフのその既定のセットを使用します。

 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccGlyphs.GetCustomGlyphList%2A> メソッドは、さまざまなソース管理状態を示す画像の一覧を取得するために [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] によって使用されます。 ソース管理 VSPackage は、IDE に、そのカスタム グリフの画像の一覧へのハンドルを返します。 IDE では、この時点で画像の一覧のコピーを作成し、後で表示するグリフを選択するためにそれを使用します。 この新しいインターフェイスがサポートされていないか、または `IVsSccGlyphs::GetCustomGlyphList` メソッドが `E_NOTIMPL` を返した場合、IDE では、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] によって提供されるグリフの既定の一覧からそのグリフを取得します。

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccGlyphs>
- <xref:Microsoft.VisualStudio.Shell.Interop.VsStateIcon>
- <xref:Microsoft.VisualStudio.Shell.Interop.SVsSccManager>
