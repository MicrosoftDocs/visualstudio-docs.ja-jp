---
title: 従来の言語サービスのモデル | Microsoft Docs
description: 独自の言語サービスを作成するためのガイドとして、この Visual Studio コア エディター用の最小限の言語サービスのモデルを使用してください。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- language services, model
ms.assetid: d8ae1c0c-ee3d-4937-a581-ee78d0499793
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 216bfaf9400847c265820e4bb5967fd3c992caa7
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105063223"
---
# <a name="model-of-a-legacy-language-service"></a>従来の言語サービスのモデル
言語サービスは、特定の言語の要素と機能を定義し、その言語に固有の情報をエディターに提供するために使用されます。 たとえば、エディターで構文の色分けをサポートするには、言語の要素とキーワードを認識している必要があります。

 言語サービスは、エディターによって管理されるテキスト バッファーと、エディターを含むビューと密接に連携しています。 Microsoft IntelliSense の **[クイック ヒント]** オプションは、言語サービスに用意されている機能の一例です。

## <a name="a-minimal-language-service"></a>最小限の言語サービス
 最も基本的な言語サービスには、次の 2 つのオブジェクトが含まれています。

- "*言語サービス*" には <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo> インターフェイスが実装されています。 言語サービスには、名前、ファイル名の拡張子、コード ウィンドウ マネージャー、色分けツールなど、言語に関する情報があります。

- "*色分けツール*" には <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer> インターフェイスが実装されています。

  次の概念図は、基本的な言語サービスのモデルを示しています。

  ![言語サービス モデルの図](../../extensibility/media/vslanguageservicemodel.gif "vsLanguageServiceModel") 基本的な言語サービス モデル

  ドキュメント ウィンドウは、エディター (この場合は [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] コア エディター) の "*ドキュメント ビュー*" をホストします。 ドキュメント ビューとテキスト バッファーはエディターによって所有されます。 これらのオブジェクトは、"*コード ウィンドウ*" と呼ばれる特殊なドキュメント ウィンドウを介して [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] と連携します。 コード ウィンドウは、IDE によって作成および制御される <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame> オブジェクトに含まれています。

  指定された拡張子を持つファイルが読み込まれると、エディターによってその拡張子に関連付けられた言語サービスが検索され、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo.GetCodeWindowManager%2A> メソッドが呼び出され、コード ウィンドウが渡されます。 言語サービスから、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager> インターフェイスを実装する "*コード ウィンドウ マネージャー*" が返されます。

  モデル内のオブジェクトの概要を次の表に示します。

| コンポーネント | Object | 機能 |
|------------------| - | - |
| テキスト バッファー | <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer> | Unicode の読み取りまたは書き込みのテキスト ストリーム。 テキストに他のエンコードを使用することもできます。 |
| [コード ウィンドウ] | <xref:Microsoft.VisualStudio.TextManager.Interop.VsCodeWindow> | 1 つ以上のテキスト ビューを含むドキュメント ウィンドウ。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] がマルチドキュメント インターフェイス (MDI) モードの場合、コード ウィンドウは MDI の子です。 |
| テキスト ビュー | <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextView> | ユーザーがキーボードとマウスを使用してテキストを操作および表示できるウィンドウ。 テキスト ビューは、エディターとしてユーザーに表示されます。 テキスト ビューは、通常のエディター ウィンドウ、出力ウィンドウ、およびイミディエイト ウィンドウで使用できます。 さらに、コード ウィンドウ内で 1 つ以上のテキスト ビューを構成できます。 |
| テキスト マネージャー | <xref:Microsoft.VisualStudio.TextManager.Interop.SVsTextManager> サービスによって管理され、そこから <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextManager> ポインターを取得します | 前述のすべてのコンポーネントによって共有される共通の情報を保持するコンポーネント。 |
| 言語サービス | 実装に依存します。<xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo> を実装します | 構文の強調表示、ステートメント入力候補、かっこの一致など、言語固有の情報をエディターに提供するオブジェクト。 |

## <a name="see-also"></a>こちらもご覧ください
- [カスタム エディターでのドキュメント データとドキュメント ビュー](../../extensibility/document-data-and-document-view-in-custom-editors.md)
