---
description: 特定のモジュール (DLL、EXE、またはアセンブリ) を記述します。
title: MODULE_INFO | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- MODULE_INFO
helpviewer_keywords:
- MODULE_INFO structure
ms.assetid: f2e06180-1ab3-4eb5-a428-7994cceb61b6
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 0b432e0373e81124d18e3bf9cc5f8ed3a4707ab6
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105079723"
---
# <a name="module_info"></a>MODULE_INFO
特定のモジュール (DLL、EXE、またはアセンブリ) を記述します。

## <a name="syntax"></a>構文

```cpp
typedef struct tagMODULE_INFO { 
   MODULE_INFO_FIELDS dwValidFields;
   BSTR               m_bstrName;
   BSTR               m_bstrUrl;
   BSTR               m_bstrVersion;
   BSTR               m_bstrDebugMessage;
   UINT64             m_addrLoadAddress;
   UINT64             m_addrPreferredLoadAddress;
   DWORD              m_dwSize;
   DWORD              m_dwLoadOrder;
   FILETIME           m_TimeStamp;
   BSTR               m_bstrUrlSymbolLocation;
   MODULE_FLAGS       m_dwModuleFlags;
} MODULE_INFO;
```

```csharp
public struct MODULE_INFO { 
   public uint     dwValidFields;
   public string   m_bstrName;
   public string   m_bstrUrl;
   public string   m_bstrVersion;
   public string   m_bstrDebugMessage;
   public ulong    m_addrLoadAddress;
   public ulong    m_addrPreferredLoadAddress;
   public uint     m_dwSize;
   public uint     m_dwLoadOrder;
   public FILETIME m_TimeStamp;
   public string   m_bstrUrlSymbolLocation;
   public uint     m_dwModuleFlags;
};
```

## <a name="members"></a>メンバー
 `dwValidFields`\
 入力するフィールドを指定する [MODULE_INFO_FIELDS](../../../extensibility/debugger/reference/module-info-fields.md) 列挙体からのフラグの組み合わせ。

 `m_bstrName`\
 モジュール名。

 `m_bstrUrl`\
 モジュールの URL。

 `m_bstrVersion`\
 モジュールのバージョン。

 `m_bstrDebugMessage`\
 "シンボルを読み込むことができません" など、モジュールに関するオプションのメッセージ。

 `m_addrLoadAddress`\
 モジュールの読み込みアドレス。

 `m_addrPreferredLoadAddress`\
 モジュールの優先読み込みアドレス。

 `m_dwSize`\
 モジュールのサイズ。

 `m_dwLoadOrder`\
 モジュールの読み込み順序。

 `m_TimeStamp`\
 シンボル ファイルが最後に変更された時刻。

 `m_bstrUrlSymbolLocation`\
 モジュールで指定されたシンボル ファイル (".\\" など) の場所。 モジュールのシンボルを検索するための開始位置として使用されます。

 `m_dwModuleFlags`\
 モジュールを記述する [MODULE_FLAGS](../../../extensibility/debugger/reference/module-flags.md) 列挙体からのフラグの組み合わせ。

## <a name="remarks"></a>解説
 この構造体は、入力する [GetInfo](../../../extensibility/debugger/reference/idebugmodule2-getinfo.md) メソッドに渡されます。

 この構造体は、 **[モジュール]** ウィンドウに一覧表示される各モジュールに対応します。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)
- [MODULE_INFO_FIELDS](../../../extensibility/debugger/reference/module-info-fields.md)
- [MODULE_FLAGS](../../../extensibility/debugger/reference/module-flags.md)
- [GetInfo](../../../extensibility/debugger/reference/idebugmodule2-getinfo.md)
