---
title: 関連サービスとインターフェイス (ソース管理 VSPackage)
titleSuffix: ''
description: Visual Studio SDK でのソース管理 VSPackage 関連のインターフェイスについて説明します。 パッケージでは、一部のインターフェイスを実装し、別のインターフェイスをソース管理に使用します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- source control packages, interfaces
- interfaces, source control packages
ms.assetid: 3e96e838-5675-46bb-99cf-40d420086038
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 6385307c91541204d58228b489160888f79dec85
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112903334"
---
# <a name="related-services-and-interfaces-source-control-vspackage"></a>関連サービスとインターフェイス (ソース管理 VSPackage)

このセクションでは、[!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] でのソース管理 VSPackage 関連のインターフェイスがすべて一覧表示されます。 ソース管理 VSPackage では、これらのインターフェイスの一部を実装し、別のインターフェイスを使用してソース管理タスクを実行します。

## <a name="interfaces-implemented-by-and-for-source-control-vspackages"></a>ソース管理 VSPackage によりソース管理 VSPackage 用に実装されるインターフェイス

 次のインターフェイスが [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] に記述されており、ソース管理 VSPackage では、目的の機能セットに応じて、それらのサブセットを実装します。 一部のインターフェイスには、必要に応じてマークが付けられ、すべてのソース管理 VSPackage で実装される必要があります。

 パッケージで実装されないインターフェイスについては、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] により既定の実装が行われます。 既定の実装は、VSPackage が登録されておらず、プロジェクトが制御されない場合に対して設計されていることに注意してください。 適切に作成されたソース管理 VSPackage では、必要なインターフェイスをすべて実装しており、これらのインターフェイスの既定の実装に委ねることはありません。

 ソース管理 VSPackage では、次のインターフェイスの一部またはすべてをカプセル化するプライベート サービスを実装する必要があります。

 インターフェイスは次のとおりです。

- 必須: このインターフェイスは、適切なエンティティ (ソース管理 VSPackage、ソース管理スタブ、プロジェクト) で実装する必要があります。

- 推奨: このインターフェイスは、エンティティで実装することが望ましく、実装しない場合は、ソース管理機能が制限される可能性があります。

- 省略可能: このインターフェイスは、より豊富な機能セットを得るためにエンティティで実装できます。

| インターフェイス | 目的 | 実装先 | 実装 |
| - | - |--------------------------|-------------|
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2> | このインターフェイスは、ファイルを変更または保存する前に、エディターによって呼び出されます。 ソース管理 VSPackage では、ファイルをチェックアウトしたり、チェックアウトが失敗した場合には操作を拒否したりできます。 | ソース管理 VSPackage | 推奨 |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2> | このインターフェイスは、プロジェクトの基本的なソース管理機能を提供します。たとえば、ソース管理を使用したプロジェクトの登録と登録解除や、基本的なソース管理のグリフのサポートなどを行うことができます。 | ソース管理 VSPackage | 必須 |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProject2> | このインターフェイスは、<xref:System.Runtime.InteropServices.Marshal.QueryInterface%2A> 関数を使用して、または単に `IVsHierarchy` を実装するオブジェクトを `IVsSccProject2` にキャストして、<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> から取得されます。 プロジェクトでファイルをソース管理下に置くため、または現在のソース管理のステータスまたは位置についてプロジェクトに伝えるために使用されます。 | Project | 必須 |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProvider> | 統合モジュールでは、このインターフェイスを使用して、現在アクティブな VSPackage を設定します。 | ソース管理 VSPackage | 必須 |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2> | このインターフェイスは、サブスクリプション モデルに基づきます。 どの VSPackage でも、ドキュメント イベントを受信する必要があるという信号を発して、行われるところのイベントに関する通知をシェルから受けることができます。 これは、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] によって実装および処理され、今度はここから、`IVsTrackProjectDocumentsEvents2` を実装するイベントが VSPackage に渡されます。 | ソース管理スタブ | 必須 |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments3> | このインターフェイスには、バッチ処理、同期された読み取り/書き込み操作、高度な `OnQueryAddFiles` メソッドが用意されています。 | ソース管理スタブ | 必須 |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocumentsEvents2> | 新しいファイルがプロジェクトに追加されたときや、プロジェクトからファイルとフォルダーの名前変更や削除が行われたときに、**ソリューション エクスプローラー** とプロジェクトによりこのインターフェイスが呼び出されます。 ソース管理 VSPackage では、プロジェクト ファイルをチェックアウトしたり、操作を取り消したりできます。 | ソース管理 VSPackage | 推奨 |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocumentsEvents3> | IVstrackProjectDocuments3 インターフェイスのメソッドに対して行われた呼び出しに応答して、**ソリューション エクスプローラー** とプロジェクトによってこのインターフェイスが呼び出されます。 ソース管理 VSPackage では、バッチ操作、同期された読み書き操作を追跡でき、より高度な `OnQueryAddFiles` メソッドを操作できます。 | ソース管理 VSPackage | 推奨 |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccEnlistmentPathTranslation> | このインターフェイスには、Web プロジェクトの参加管理サポートが用意されています。 | ソース管理 VSPackage | 推奨 |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManagerTooltip> | このインターフェイスは、プロジェクトのソース管理されたファイルのツールヒントを取得するために使用されます。 | ソース管理 VSPackage | オプション |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccOpenFromSourceControl> | このインターフェイスでは、名前空間拡張をサポートします。 | ソース管理 VSPackage | オプション |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccControlNewSolution> | VSPackage では、このインターフェイスを使用して、名前空間拡張を **[新規]** 、 **[開く]** 、または **[保存]** のダイアログ ボックスに統合します。 その結果、プロジェクトを、作成時にソース管理に自動的に追加したり、保存操作が有効なときにソース管理に追加したりできます。 | ソース管理 VSPackage | オプション |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccGlyphs> | VSPackage では、このインターフェイスを使用して、**ソリューション エクスプローラー** で追加のグリフをノードのソース管理グリフとして定義します。 | ソース管理 VSPackage | オプション |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccAddWebProjectFromSourceControl> | Web プロジェクトの **[追加]** ダイアログ ボックスではこのインターフェイスを使用します。 ソース管理場所を参照する方法と、その場所のソース管理リポジトリに以前に追加した Web プロジェクトを開く方法を提供します。 | ソース管理 VSPackage | 推奨 |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsAsynchOpenFromScc> | このインターフェイスでは、ソース管理からのプロジェクトの非同期 (バックグラウンド) 読み込みをサポートします。 | ソース管理 VSPackage | オプション |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsAsynchOpenFromSccProjectEvents> | このインターフェイスでは、<xref:Microsoft.VisualStudio.Shell.Interop.IVsAsynchOpenFromScc> で開始された非同期読み込みの進行状況をプロジェクトで監視できるようにします。 | Project | オプション |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccToolsOptions> | このインターフェイスでは、IDE で、アクティブなソース管理 VSPackage を照会できるようにします。 IDE では、登録されたアクティブなソース管理 VSPackage がない場合でも意味のあるソース管理設定の値を照会します。 このインターフェイスは、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] で実装および処理されます。 | ソース管理スタブ | 必須 |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterScciProvider> | このインターフェイスは、ソース管理 VSPackage の登録で使用されます。 | ソース管理スタブ | 必須 |
| <xref:EnvDTE.SourceControl> | このインターフェイスはオートメーションで使用されます。 したがって、実行できる関数だけが公開され、どの UI も表示されません。 | ソース管理 VSPackage | オプション |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps> | このインターフェイスは、ソリューション (.sln) ファイルでのソース管理設定の保存に使用されます。 設定には、ソース管理の場所とソース管理ステータス フラグが含まれます。 | ソース管理 VSPackage | 推奨 |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionOpts> | このインターフェイスは、ソリューション オプション (.suo) ファイルでのソース管理設定の保存に使用されます。 これには、現在のユーザーの参加場所など、ユーザー固有のソース管理設定を含められます。 | ソース管理 VSPackage | 推奨 |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3> | このインターフェイスは、ソリューションを閉じる前にプロジェクトファイルをチェックインしたり、プロジェクトを開くときにソース管理から新しいファイルを取得したりするなどの操作を実行するために、イベントの監視に使用されます。 | ソース管理 VSPackage | 推奨 |

## <a name="see-also"></a>関連項目
- [デザイン要素](../../extensibility/internals/source-control-vspackage-design-elements.md)
