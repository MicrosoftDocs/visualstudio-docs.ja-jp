---
title: ブレークポイントのバインド | Microsoft Docs
description: ユーザーがブレークポイントを設定している場合に、IDE でどのようにブレークポイントの要求を作成し、デバッグ セッションにブレークポイントの作成を促すかについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- breakpoints, binding
ms.assetid: 70737387-c52f-4dae-8865-77d4b203bf25
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 622d61c6083288f7293258feb3743ef7cfdd0b8b
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105055285"
---
# <a name="bind-breakpoints"></a>ブレークポイントのバインド
ユーザーがブレークポイントを設定している場合、たとえば **F9** キーを押すと、IDE によって要求が作成され、デバッグ セッションにブレークポイントの作成が促されます。

## <a name="set-a-breakpoint"></a>ブレークポイントの設定
 ブレークポイントの設定は 2 段階のプロセスです。ブレークポイントの影響を受けるコードまたはデータがまだ使用できないことがあるためです。 まず、ブレークポイントを記述する必要があります。次に、コードまたはデータが使用可能になったら、そのコードまたはデータに次のようにバインドする必要があります。

1. ブレークポイントは関連するデバッグ エンジン (DE) から要求されます。その後、コードまたはデータが使用可能になった時点でブレークポイントがバインドされます。

2. ブレークポイント要求はデバッグ セッションに送信され、そこから関連するすべての DE に送信されます。 ブレークポイントの処理を選択した DE によって、対応する保留中ブレークポイントが作成されます。

3. デバッグ セッションによって、保留中ブレークポイントが収集され、それらがデバッグ パッケージ (Visual Studio のデバッグ コンポーネント) に送り返されます。

4. デバッグ パッケージにより、保留中ブレークポイントをコードまたはデータにバインドするようにデバッグ セッションが促されます。 デバッグ セッションによって、関連するすべての DE にこの要求が送信されます。

5. DE でブレークポイントをバインドできる場合は、ブレークポイントにバインドされたイベントがデバッグ セッションに送り返されます。 そうでない場合は、ブレークポイント エラー イベントが代わりに送信されます。

## <a name="pending-breakpoints"></a>保留中ブレークポイント
 保留中ブレークポイントは、コードの複数の場所にバインドできます。 たとえば、C++ テンプレート用のソース コード行は、そのテンプレートから生成されるすべてのコード シーケンスにバインドできます。 デバッグ セッションでは、ブレークポイントがバインドされたイベントを使用して、そのイベントの送信時にブレークポイントにバインドされるコード コンテキストを列挙できます。 さらに多くのコード コンテキストを後でバインドできるため、DE は各バインド要求でブレークポイントがバインドされたイベントを複数送信できます。 ただし、DE によって、ブレークポイント エラー イベントはバインド要求ごとに 1 つしか送信できません。

## <a name="implementation"></a>実装
 デバッグ パッケージはプログラムによって、セッション デバッグ マネージャー (SDM) を呼び出して、[BP_REQUEST_INFO](../../extensibility/debugger/reference/bp-request-info.md) 構造体 (設定対象のブレークポイントが記述されている) をラップする [IDebugBreakpointRequest2](../../extensibility/debugger/reference/idebugbreakpointrequest2.md) インターフェイスを提供できます。 ブレークポイントはさまざまな形式にすることができますが、最終的にはコードまたはデータ コンテキストに解決されます。

 SDM は、[CreatePendingBreakpoint](../../extensibility/debugger/reference/idebugengine2-creatependingbreakpoint.md) メソッドを呼び出すことで、関連する各 DE にこの呼び出しを渡します。 DE によってブレークポイントの処理が選択される場合、[IDebugPendingBreakpoint2](../../extensibility/debugger/reference/idebugpendingbreakpoint2.md) インターフェイスが作成されて返されます。 SDM によって、これらのインターフェイスが収集され、1 つの `IDebugPendingBreakpoint2` インターフェイスとしてデバッグ パッケージに送り返されます。

 ここまで、イベントは生成されていません。

 次に、デバッグ パッケージによって、[Bind](../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md) (DE によって実装される) が呼び出され、コードまたはデータへの保留中ブレークポイントのバインドが試行されます。

 ブレークポイントがバインドされると、DE によって [IDebugBreakpointBoundEvent2](../../extensibility/debugger/reference/idebugbreakpointboundevent2.md) イベント インターフェイスがデバッグ パッケージに送信されます。 デバッグ パッケージで、1 つ以上の [IDebugBoundBreakpoint2](../../extensibility/debugger/reference/idebugboundbreakpoint2.md) インターフェイスを返す [EnumBoundBreakpoints](../../extensibility/debugger/reference/idebugbreakpointboundevent2-enumboundbreakpoints.md) を呼び出すことで、このインターフェイスが使用され、ブレークポイントにバインドされたすべてのコード コンテキスト (または 1 つのデータ コンテキスト) が列挙されます。 [GetBreakpointResolution](../../extensibility/debugger/reference/idebugboundbreakpoint2-getbreakpointresolution.md) インターフェイスは [IDebugBreakpointResolution2](../../extensibility/debugger/reference/idebugbreakpointresolution2.md) インターフェイスを返し、[GetResolutionInfo](../../extensibility/debugger/reference/idebugbreakpointresolution2-getresolutioninfo.md) はコードまたはデータ コンテキストを含む [BP_RESOLUTION_INFO](../../extensibility/debugger/reference/bp-resolution-info.md) 共用体を返します。

 DE によってブレークポイントがバインドできない場合、1 つの [IDebugBreakpointErrorEvent2](../../extensibility/debugger/reference/idebugbreakpointerrorevent2.md) イベント インターフェイスがデバッグ パッケージに送信されます。 デバッグ パッケージによって、[GetErrorBreakpoint](../../extensibility/debugger/reference/idebugbreakpointerrorevent2-geterrorbreakpoint.md)、[GetBreakpointResolution](../../extensibility/debugger/reference/idebugerrorbreakpoint2-getbreakpointresolution.md) および [GetResolutionInfo](../../extensibility/debugger/reference/idebugerrorbreakpointresolution2-getresolutioninfo.md) を続けて呼び出すことで、エラーの種類 (エラーまたは警告) と情報メッセージが取得されます。 これによって、エラーの種類とメッセージを含む [BP_ERROR_RESOLUTION_INFO](../../extensibility/debugger/reference/bp-error-resolution-info.md) 構造体が返されます。

 DE によってブレークポイントが処理されるがバインドできなかった場合、種類が `BPET_TYPE_ERROR` のエラーが返されます。 デバッグ パッケージではエラー ダイアログ ボックスを表示してこれに応答し、IDE ではソース コード行の左側のブレークポイント グリフ内に感嘆符のグリフが表示されます。

 ある DE によってブレークポイントが処理されてバインドできなかったが、別の DE でバインドされる可能性がある場合は、警告が返されます。 IDE によって、ソース コード行の左側のブレークポイント グリフ内に疑問符のグリフが表示されます。

## <a name="see-also"></a>こちらもご覧ください
- [タスクのデバッグ](../../extensibility/debugger/debugging-tasks.md)
