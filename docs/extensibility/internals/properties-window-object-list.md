---
title: プロパティ ウィンドウのオブジェクト一覧 | Microsoft Docs
description: Visual Studio IDE で プロパティ ウィンドウ内のオブジェクト一覧を操作するために使用されるインターフェイスについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- Properties window, object list
ms.assetid: 6c159c9d-345d-4b23-8ddd-9839d338b62f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 908acf3f8ecad390266c3d085778dc13077a6fa8
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112903438"
---
# <a name="properties-window-object-list"></a>プロパティ ウィンドウのオブジェクト一覧
**[プロパティ]** ウィンドウ内のオブジェクト一覧は、選択項目を、選択されている 1 つ以上のウィンドウ内で使用可能な他のオブジェクトに変更できるドロップダウン リストです。 この一覧内から別のオブジェクトを選択すると、新しいオブジェクトが選択されたことを環境に通知するための <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer.SelectObjects%2A> の呼び出しがトリガーされます。 その後、 **[プロパティ]** ウィンドウに表示される情報が変更され、新しく選択されたオブジェクトに関連付けられているプロパティが表示されます。

## <a name="the-object-list"></a>オブジェクト一覧
 オブジェクト一覧は、オブジェクト名 (太字で表示されます) とオブジェクトの種類の 2 つのフィールドで構成されています。

 オブジェクトの種類の左側に太字で表示されているオブジェクト名は、<xref:Microsoft.VisualStudio.OLE.Interop.IProvideClassInfo> インターフェイスによって提供される `Name` プロパティを使用して、そのオブジェクト自体から取得されます。 <xref:Microsoft.VisualStudio.OLE.Interop.IProvideClassInfo> での唯一のメソッドである <xref:Microsoft.VisualStudio.OLE.Interop.IProvideClassInfo.GetClassInfo%2A> は、そのインターフェイスのコクラスの <xref:Microsoft.VisualStudio.OLE.Interop.ITypeInfo> を返します。 **[プロパティ]** ウィンドウでは、<xref:Microsoft.VisualStudio.OLE.Interop.IProvideClassInfo> を使用してコクラスの名前を取得します。これは、ドロップダウン リストにオブジェクト名として表示されます。

 そのオブジェクトに `Name` プロパティがない場合は、オブジェクト一覧の [名前] 領域に名前が表示されません。 オブジェクト一覧に名前が表示されるようにしたい場合は、そのオブジェクトに Name プロパティを追加できます。

 COM オブジェクトで <xref:Microsoft.VisualStudio.OLE.Interop.IProvideClassInfo> を実装していない場合、 **[プロパティ]** ウィンドウの一覧の左側には、オブジェクト名の代わりにインターフェイス名が表示されます。

## <a name="see-also"></a>関連項目
- [プロパティの拡張](../../extensibility/internals/extending-properties.md)
