---
title: 永続性と実行中のドキュメント テーブル | Microsoft Docs
description: Visual Studio IDE でドキュメントの状態を追跡する実行中のドキュメント テーブルでのドキュメントのオープン、保存、名前変更をプロジェクトで調整する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- persistence, managing
- IVsPersistHierarchyItem interface, implementing
- architecture, persistence
- running document table (RDT), architecture
ms.assetid: 27117eae-6c58-4189-a61a-1397a43b5ecf
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 5244e14498da0f556a71b8d710ccbaa8b9b03e65
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105095122"
---
# <a name="persistence-and-the-running-document-table"></a>ドキュメント テーブルの保存と実行
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE では、プロジェクト項目の永続化の管理はすべてプロジェクトで担っており、プロジェクトでは <xref:Microsoft.VisualStudio.Shell.Interop.SVsRunningDocumentTable> のサービスを使用してこの項目を実行します。 ドキュメントは Visual Studio 環境での永続化の基本単位です。 プロジェクトでは、開いているすべてのドキュメントの状態を追跡するリソースである実行中のドキュメント テーブル (RDT) を使用して、ドキュメントのオープン、保存、名前変更を調整します。

## <a name="managing-persistence"></a>永続化の管理
 プロジェクトでは、<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem> インターフェイスを実装して、環境の永続化サービスを制御します。 環境では、ドキュメントが永続化するように直接要求されることはありませんが、所有しているプロジェクト (または階層) がドキュメントを保存するように要求されます。 これにより、プロジェクトで、プロジェクト項目データをローカル ファイル、リモート ファイル、データベース、リポジトリ、またはその他のメディアに保存できるようになります。

 グローバル環境で RDT が保持されます。 この環境では、すべての開いているウィンドウとドキュメントのエントリが RDT で保持され、これにより、ソリューションが閉じられたときなどに特別な通知を受け取れるようになります。 さらに、RDT により、環境で **ソリューション エクスプローラー** 内の対応するノードを追跡できるようになります。 RDT では、プロジェクト ファイルとプロジェクト項目ドキュメントの両方を含む、開かれた永続化可能なオブジェクトごとに 1 つのレコードが保持されます。

## <a name="see-also"></a>関連項目
- [ドキュメント テーブルの実行](../../extensibility/internals/running-document-table.md)
- [IDE での選択と通貨](../../extensibility/internals/selection-and-currency-in-the-ide.md)
