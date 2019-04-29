---
title: コンテキスト メニュー |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - context menus
ms.assetid: 44fd9e6a-6d42-4aba-80ba-f37fa0070f1d
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 19838bbc1dfeeb0a0df9e1e1ce409557b6a28f1e
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62926666"
---
# <a name="context-menus"></a>コンテキスト メニュー
コンテキスト メニューでは、クライアント領域のアクティブなリージョンでユーザーを右クリックしたときに表示され、マウスの右ボタンが離されたときをオフにします。

## <a name="editor-context-menus"></a>エディター コンテキスト メニュー
 インターセプトすることで`ECMD_SHOWCONTEXTMENU`、言語サービスは、エディターに表示されるコンテキスト メニューを制御できます。 独自のコンテキスト メニューを表示するには、次のコマンド処理に渡されると、<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>呼び出して<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.ShowContextMenu%2A>します。 このコマンドを処理しない場合は、エディターの提供される標準のコンテキスト メニューが表示されます。 マーカーあたりごとに、コンテキスト メニューの内容を制御することもできます。 詳細については、次を参照してください。[テキスト マーカーを使用して、従来の API を使用した](../extensibility/using-text-markers-with-the-legacy-api.md)と[従来の言語サービスのコマンドをインターセプト](../extensibility/internals/intercepting-legacy-language-service-commands.md)します。

## <a name="see-also"></a>関連項目
- [従来の言語サービスを開発します。](../extensibility/internals/developing-a-legacy-language-service.md)
- [メニューとコマンドを拡張します。](../extensibility/extending-menus-and-commands.md)