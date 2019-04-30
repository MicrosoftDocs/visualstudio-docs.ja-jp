---
title: 従来の言語サービスで、クイック ヒント |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- Quick Info, supporting in language services [managed package framework]
- IntelliSense, Quick Info
- language services [managed package framework], IntelliSense Quick Info
ms.assetid: 159ccb0b-f5d6-4912-b88b-e9612924ed5e
caps.latest.revision: 17
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 9dc46510aeeaf08279101ff546cde6dbd2593571
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63425675"
---
# <a name="quick-info-in-a-legacy-language-service"></a>従来の言語サービスのクイック ヒント
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

IntelliSense によるクイック ヒントでは、ユーザーが、識別子にキャレットを配置および選択ソースの識別子に関する情報を表示**クイック ヒント**から、 **IntelliSense**メニューまたはマウスを保持識別子の上にカーソル。 これにより、識別子に関する情報を表示するツールヒント。 この情報は通常、識別子の型で構成されます。 デバッグ エンジンがアクティブの場合、この情報には、現在の値が含まれます。 デバッグ エンジンは、言語サービスは、識別子のみを処理中に、式の値を提供します。  
  
 従来の言語サービスは、VSPackage の一部として実装されますが、言語サービスの機能を実装する新しい方法は MEF 拡張機能を使用します。 詳細については、次を参照してください。[チュートリアル。クイック ヒントの表示](../../extensibility/walkthrough-displaying-quickinfo-tooltips.md)します。  
  
> [!NOTE]
> 新しいエディターの API をできるだけ早く使用を開始することをお勧めします。 言語サービスのパフォーマンスを向上させる、エディターの新機能を活用することができます。  
  
 マネージ パッケージ フレームワーク (MPF) 言語のサービス クラスでは、IntelliSense によるクイック ヒントのツールヒントを表示するため完全なサポートを提供します。 行う必要があるすべてが、表示、クイック ヒント機能を有効にするテキストを指定します。  
  
 表示されるテキストは呼び出すことによって取得、<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>メソッド パーサーの解析の理由の値を持つ<xref:Microsoft.VisualStudio.Package.ParseReason>します。 このため、種類の情報 (またはクイック ツールヒントに表示する適切なもの) を取得するパーサーに伝える識別子で指定された位置の<xref:Microsoft.VisualStudio.Package.ParseRequest>オブジェクト。 <xref:Microsoft.VisualStudio.Package.ParseRequest>オブジェクトに渡されたもの、<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>メソッド。  
  
 内の位置まで、パーサーが解析する必要があります、<xref:Microsoft.VisualStudio.Package.ParseRequest>オブジェクトのすべての識別子の種類を決定するためにします。 パーサーは解析要求の場所の識別子を取得する必要があります。 最後に、パーサーには、その id に関連付けられたツール ヒントのデータを渡す必要があります、<xref:Microsoft.VisualStudio.Package.AuthoringScope>オブジェクトのため、そのオブジェクトからテキストを返すことができます、<xref:Microsoft.VisualStudio.Package.AuthoringScope.GetDataTipText%2A>メソッド。  
  
## <a name="enabling-the-quick-info-feature"></a>クイック ヒント機能を有効にします。  
 クイック ヒント機能を有効に設定する必要があります、`CodeSense`と`QuickInfo`名前付きのパラメーター、<xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute>します。これらの属性の設定、<xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableCodeSense%2A>と<xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableQuickInfo%2A>プロパティ。  
  
## <a name="implementing-the-quick-info-feature"></a>クイック ヒント機能を実装します。  
 <xref:Microsoft.VisualStudio.Package.ViewFilter>クラスは、IntelliSense によるクイック ヒントの操作を処理します。 ときに、<xref:Microsoft.VisualStudio.Package.ViewFilter>クラスを受け取る、<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>のコマンドは、クラスの呼び出し、<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>メソッドの解析の理由で<xref:Microsoft.VisualStudio.Package.ParseReason>と時にキャレットの位置、<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>コマンドが送信されました。 <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>メソッド パーサーする必要がありますし、指定した位置までソースを解析してクイック ツールヒントに表示を決定するように指定した位置に識別子を解析しています。  
  
 ほとんどのパーサーでは、全体のソース ファイルの初期の解析を行うし、解析ツリーで、結果を格納します。 場合に、完全な解析が実行される<xref:Microsoft.VisualStudio.Package.ParseReason>に渡される<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>メソッド。 その他の種類の解析は、必要な情報を取得するのに解析ツリーを使用できます。  
  
 たとえば、解析理由の値の<xref:Microsoft.VisualStudio.Package.ParseReason>ソースの場所にある id を見つけるし、型情報を取得して解析ツリーで調べることができます。 この種類の情報に渡されます、<xref:Microsoft.VisualStudio.Package.AuthoringScope>クラスし、によって返される、<xref:Microsoft.VisualStudio.Package.AuthoringScope.GetDataTipText%2A>メソッド。
