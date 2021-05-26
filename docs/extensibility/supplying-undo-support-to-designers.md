---
title: デザイナー向けの元に戻す操作のサポート提供 | Microsoft Docs
description: デザイナー向けに、自動的に、または Visual Studio SDK の機能を使用して、元に戻す操作のサポートを提供する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- designers [Visual Studio SDK], undo support
ms.assetid: 43eb1f14-b129-404a-8806-5bf9b099b67b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 6b56eb762cf4a2746af04ed69c7c4c49afc15dec
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105056312"
---
# <a name="supply-undo-support-to-designers"></a>デザイナー向けの元に戻す操作のサポートを提供する

通常、エディターと同様に、デザイナーではコード要素を変更するときにユーザーが最新の変更を元に戻すことができるように、元に戻す操作をサポートする必要があります。

Visual Studio で実装されているほとんどのデザイナーには、環境によって自動的に提供される "元に戻す" 操作のサポートがあります。

元に戻す機能のサポートを提供する必要があるデザイナーの実装は次のとおりです。

- 抽象基本クラス <xref:System.ComponentModel.Design.UndoEngine> を実装して、元に戻す操作の管理を提供します

- <xref:System.ComponentModel.Design.Serialization.IDesignerSerializationService> と <xref:System.ComponentModel.Design.IComponentChangeService> クラスを実装して、永続化および CodeDOM サポートを提供します。

.NET Framework を使用したデザイナーの作成の詳細については、「[デザイン時のサポートの拡張](/previous-versions/37899azc(v=vs.140))」を参照してください。

[!INCLUDE[vsipsdk](../extensibility/includes/vsipsdk_md.md)] から、次のように既定の元に戻す操作のインフラストラクチャが提供されます。

- <xref:Microsoft.VisualStudio.Shell.Design.OleUndoEngine> と <xref:Microsoft.VisualStudio.Shell.Design.OleUndoEngine.UndoUnit> クラスを使用して、元に戻す操作の管理の実装を提供します。

- 既定の <xref:System.ComponentModel.Design.Serialization.CodeDomComponentSerializationService> と <xref:System.ComponentModel.Design.IComponentChangeService> 実装を使用して、永続化および CodeDOM サポートを提供します。

## <a name="obtain-undo-support-automatically"></a>元に戻す操作のサポートを自動的に取得する

Visual Studio で作成されたすべてのデザイナーでは、デザイナーが次の場合に自動および完全な復元がサポートされます。

- ユーザー インターフェイスに <xref:System.Windows.Forms.Control> に基づいたクラスを使用しています。

- コードの生成と永続化のために、CodeDOM ベースの標準的なコード生成および解析システムを使用しています。

   Visual Studio CodeDOM サポートの使用方法の詳細については、[動的ソースコードの生成とコンパイル](/dotnet/framework/reflection-and-codedom/dynamic-source-code-generation-and-compilation)に関するページを参照してください。

## <a name="when-to-use-explicit-designer-undo-support"></a>明示的なデザイナーの元に戻す操作のサポートを使用する場合
 デザイナーでは、<xref:System.Windows.Forms.Control> により提供されるもの以外のグラフィカル ユーザー インターフェイス (ビュー アダプター) を使用する場合、独自の元に戻す操作の管理を提供する必要があります。

 この例としては、.NET Framework ベースのグラフィカル インターフェイスではなく、Web ベースのグラフィカル デザイン インターフェイスを使用して製品を作成することが考えられます。

 このような場合は、<xref:Microsoft.VisualStudio.Shell.Design.ProvideViewAdapterAttribute> を使用してこのビュー アダプターを Visual Studio に登録し、明示的な元に戻す操作の管理を提供する必要があります。

 <xref:System.CodeDom> 名前空間に用意されている Visual Studio コード生成モデルを使用しない場合、デザイナーでは CodeDOM および永続化サポートを提供する必要があります。

## <a name="undo-support-features-of-the-designer"></a>デザイナーの元に戻す操作のサポート機能
 環境 SDK には、ユーザー インターフェイスまたは標準の CodeDOM および永続化モデルに対して <xref:System.Windows.Forms.Control> ベースのクラスを使用しないデザイナーで使用できる、元に戻す機能を提供するために必要なインターフェイスの既定の実装が用意されています。

 <xref:Microsoft.VisualStudio.Shell.Design.OleUndoEngine> クラスは、元に戻す操作を管理する <xref:Microsoft.VisualStudio.OLE.Interop.IOleUndoManager> クラスの実装を使用する .NET Framework <xref:System.ComponentModel.Design.UndoEngine> クラスから派生します。

 Visual Studio では、デザイナーの元に戻す操作のための次の機能が用意されています。

- 複数のデザイナー間でリンクされた元に戻す機能。

- デザイナー内の子ユニットは、<xref:Microsoft.VisualStudio.Shell.Design.OleUndoEngine.UndoUnit> に <xref:Microsoft.VisualStudio.OLE.Interop.IOleUndoUnit> と <xref:Microsoft.VisualStudio.OLE.Interop.IOleParentUndoUnit> を実装することによって、親と対話できます。

環境 SDK では、次のように指定することで、CodeDOM および永続化をサポートしています。

- <xref:System.ComponentModel.Design.Serialization.IDesignerSerializationService> の実装としての <xref:System.ComponentModel.Design.Serialization.CodeDomComponentSerializationService>

- Visual Studio デザイン ホストによって提供される <xref:System.ComponentModel.Design.IComponentChangeService>。

## <a name="use-the-environment-sdk-features-to-supply-undo-support"></a>環境 SDK 機能を使用して元に戻す操作のサポートを提供する

元に戻す操作のサポートを取得するには、デザイナーを実装するオブジェクトで、有効な <xref:System.IServiceProvider> の実装を使用して <xref:Microsoft.VisualStudio.Shell.Design.OleUndoEngine> クラスのインスタンスをインスタンス化し、初期化する必要があります。 この <xref:System.IServiceProvider> クラスは、次のサービスを提供する必要があります。

- <xref:System.ComponentModel.Design.IDesignerHost>.

- <xref:System.ComponentModel.Design.Serialization.IDesignerSerializationService>

   Visual Studio CodeDOM シリアル化を使用するデザイナーは、<xref:System.ComponentModel.Design.Serialization.IDesignerSerializationService> の実装として、[!INCLUDE[vsipsdk](../extensibility/includes/vsipsdk_md.md)] で提供される <xref:System.ComponentModel.Design.Serialization.CodeDomComponentSerializationService> を使用することができます。

   この場合、<xref:Microsoft.VisualStudio.Shell.Design.OleUndoEngine> コンストラクターに提供される <xref:System.IServiceProvider> クラスでは、このオブジェクトを <xref:System.ComponentModel.Design.Serialization.IDesignerSerializationService> クラスの実装として返す必要があります。

- <xref:System.ComponentModel.Design.IComponentChangeService>

   Visual Studio デザイン ホストによって提供される既定の <xref:System.ComponentModel.Design.DesignSurface> を使用するデザイナーには、<xref:System.ComponentModel.Design.IComponentChangeService> クラスの既定の実装があることが保証されます。

<xref:Microsoft.VisualStudio.Shell.Design.OleUndoEngine> ベースの元に戻すメカニズムを実装するデザイナーでは、次の場合に変更が自動的に追跡されます。

- プロパティの変更が、<xref:System.ComponentModel.TypeDescriptor> オブジェクトを使用して行われた場合。

- <xref:System.ComponentModel.Design.IComponentChangeService> イベントが、元に戻すことが可能な変更がコミットされると、手動で生成された場合。

- デザイナーでの変更が、<xref:System.ComponentModel.Design.DesignerTransaction> のコンテキスト内で作成された場合。

- デザイナーで、<xref:System.ComponentModel.Design.UndoEngine.UndoUnit> の実装によって提供される標準の元に戻す操作ユニット、または <xref:System.ComponentModel.Design.UndoEngine.UndoUnit> から派生した Visual Studio 固有の実装 <xref:Microsoft.VisualStudio.Shell.Design.OleUndoEngine.UndoUnit> のいずれかを使用して、元に戻す単位を明示的に作成することを選択し、また、<xref:Microsoft.VisualStudio.OLE.Interop.IOleUndoUnit> と <xref:Microsoft.VisualStudio.OLE.Interop.IOleParentUndoUnit> の両方の実装も提供した場合。

## <a name="see-also"></a>関連項目

- <xref:System.ComponentModel.Design.UndoEngine>
- <xref:Microsoft.VisualStudio.Shell.Design.OleUndoEngine>
- [デザイン時サポートの拡張](/previous-versions/37899azc(v=vs.140))
