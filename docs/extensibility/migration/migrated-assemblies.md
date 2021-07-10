---
title: VS SDK NuGet パッケージ
description: Visual Studio 拡張機能を Visual Studio 2022 プレビューに移行するとき、場合によっては必要になる VS SDK メタパッケージとその他の NuGet パッケージについて説明します。
ms.date: 06/08/2021
ms.topic: conceptual
author: leslierichardson95
ms.author: lerich
manager: jmartens
monikerRange: vs-2022
ms.workload:
- vssdk
ms.openlocfilehash: dc55bd6abf2d5efabb862419e1bdd218d2ab18e7
ms.sourcegitcommit: 5fb4a67a8208707e79dc09601e8db70b16ba7192
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2021
ms.locfileid: "112309222"
---
# <a name="sdk-reference-packages"></a>SDK 参照パッケージ

[!INCLUDE [preview-note](../includes/preview-note.md)]

Visual Studio 拡張機能を作成する最も簡単な方法は、[`Microsoft.VisualStudio.Sdk` NuGet パッケージ](https://www.nuget.org/packages/microsoft.visualstudio.sdk)を参照することです。
このパッケージは Visual Studio 2017 (15.0)、Visual Studio 2019 (16.0、16.9)、Visual Studio 2022 で利用できます。

拡張機能によっては、上記のメタパッケージに含まれていない VS SDK パッケージを追加する必要があります。
その他の SDK パッケージを参照するとき、これらのパッケージはメジャー VS バージョン間で異なる場合があります。

Visual Studio 2022 より前の場合、さまざまな相互運用機能アセンブリを埋め込むことができます。 Visual Studio 2022 からは、埋め込みは必要ないか、サポートされていません。
リンクせず、相互運用機能アセンブリを *参照* してください。

以下は、Visual Studio 2022 以前と Visual Studio 2022 の対照表です。ご利用の 2022 より前の Visual Studio 拡張機能では、Visual Studio 2022 をターゲットとするときに参照にするため、新しいパッケージ ID を既に参照している可能性があります。 ローカル Visual Studio インストールからのみ以前は利用できた NuGet パッケージでアセンブリが利用できることがあります。

Visual Studio 2022 より前 | Visual Studio 2022
--|--
`envdte` | `Microsoft.VisualStudio.Interop`
`envdte100` | `Microsoft.VisualStudio.Interop`
`envdte80` | `Microsoft.VisualStudio.Interop`
`envdte90` | `Microsoft.VisualStudio.Interop`
`envdte90a` | `Microsoft.VisualStudio.Interop`
`extensibility` | `Microsoft.VisualStudio.Interop`
`Microsoft.MSXML` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.CommandBars` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.Designer.Interfaces` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.OLE.Interop` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.SDK.EmbedInteropTypes` | (非推奨。 参照を削除してください)
`Microsoft.VisualStudio.Shell.Embeddable` | `Microsoft.VisualStudio.Shell.Framework`
`Microsoft.VisualStudio.Shell.Interop.10.0` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.Shell.Interop.11.0` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.Shell.Interop.12.0` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.Shell.Interop.12.1.DesignTime` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.Shell.Interop.14.1.DesignTime` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.Shell.Interop.14.2.DesignTime` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.Shell.Interop.14.3.DesignTime` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.Shell.Interop.15.0.DesignTime` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.Shell.Interop.15.1.DesignTime` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.Shell.Interop.15.3.DesignTime` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.Shell.Interop.15.5.DesignTime` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.Shell.Interop.15.6.DesignTime` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.Shell.Interop.15.7.DesignTime` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.Shell.Interop.15.8.DesignTime` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.Shell.Interop.16.0.DesignTime` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.Shell.Interop.16.1.DesignTime` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.Shell.Interop.16.10.DesignTime` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.Shell.Interop.16.2.DesignTime` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.Shell.Interop.16.3.DesignTime` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.Shell.Interop.16.4.DesignTime` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.Shell.Interop.16.5.DesignTime` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.Shell.Interop.16.6.DesignTime` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.Shell.Interop.16.7.DesignTime` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.Shell.Interop.16.9.DesignTime` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.Shell.Interop.8.0` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.Shell.Interop.9.0` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.Shell.Interop` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.TextManager.Interop.10.0` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.TextManager.Interop.11.0` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.TextManager.Interop.12.0` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.TextManager.Interop.12.1.DesignTime` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.TextManager.Interop.14.2.DesignTime` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.TextManager.Interop.15.0.DesignTime` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.TextManager.Interop.15.1.DesignTime` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.TextManager.Interop.16.0.DesignTime` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.TextManager.Interop.8.0` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.TextManager.Interop.9.0` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.TextManager.Interop` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.UserNotifications.Interop.12.0.DesignTime` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.VSHelp.dll` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.VSHelp80.dll` | `Microsoft.VisualStudio.Interop`
`Microsoft.VisualStudio.WCFReference.Interop` | `Microsoft.VisualStudio.Interop`
`stdole` | `Microsoft.VisualStudio.Interop`
`VSLangProj` | `Microsoft.VisualStudio.Interop`
`VSLangProj100` | `Microsoft.VisualStudio.Interop`
`VSLangProj110` | `Microsoft.VisualStudio.Interop`
`VSLangProj140` | `Microsoft.VisualStudio.Interop`
`VSLangProj150` | `Microsoft.VisualStudio.Interop`
`VSLangProj157` | `Microsoft.VisualStudio.Interop`
`VSLangProj158` | `Microsoft.VisualStudio.Interop`
`VSLangProj165` | `Microsoft.VisualStudio.Interop`
`VSLangProj2` | `Microsoft.VisualStudio.Interop`
`VSLangProj80` | `Microsoft.VisualStudio.Interop`
`VSLangProj90` | `Microsoft.VisualStudio.Interop`

マージされた相互運用機能アセンブリ 1 つからたくさんの相互運用機能アセンブリを利用できるようになっています。
上の表にパッケージがない場合、2 つのバージョンで同じ可能性があります。
