---
title: "FIELD_MODIFIERS | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "vs-ide-sdk"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "FIELD_MODIFIERS"
helpviewer_keywords: 
  - "FIELD_MODIFIERS 列挙型"
ms.assetid: 1e44681c-1f03-41a9-9c04-b79f231b0822
caps.latest.revision: 15
caps.handback.revision: 15
ms.author: "gregvanl"
manager: "ghogen"
---
# FIELD_MODIFIERS
[!INCLUDE[vs2017banner](../../../code-quality/includes/vs2017banner.md)]

フィールドの種類の修飾子を指定します。  
  
## 構文  
  
```cpp#  
enum enum_FIELD_MODIFIERS {   
   FIELD_MOD_NONE             = 0x00000000,  
  
   // Modifier of the field  
   FIELD_MOD_ACCESS_NONE      = 0x00000001,  
   FIELD_MOD_ACCESS_PUBLIC    = 0x00000002,  
   FIELD_MOD_ACCESS_PROTECTED = 0x00000004,  
   FIELD_MOD_ACCESS_PRIVATE   = 0x00000008,  
  
   // Storage modifier of the field  
   FIELD_MOD_NOMODIFIERS      = 0x00000010,  
   FIELD_MOD_STATIC           = 0x00000020,  
   FIELD_MOD_CONSTANT         = 0x00000040,  
   FIELD_MOD_TRANSIENT        = 0x00000080,  
   FIELD_MOD_VOLATILE         = 0x00000100,  
   FIELD_MOD_ABSTRACT         = 0x00000200,  
   FIELD_MOD_NATIVE           = 0x00000400,  
   FIELD_MOD_SYNCHRONIZED     = 0x00000800,  
   FIELD_MOD_VIRTUAL          = 0x00001000,  
   FIELD_MOD_INTERFACE        = 0x00002000,  
   FIELD_MOD_FINAL            = 0x00004000,  
   FIELD_MOD_SENTINEL         = 0x00008000,  
   FIELD_MOD_INNERCLASS       = 0x00010000,  
   FIELD_TYPE_OPTIONAL        = 0x00020000,  
   FIELD_MOD_BYREF            = 0x00040000,  
   FIELD_MOD_HIDDEN           = 0x00080000,  
   FIELD_MOD_MARSHALASOBJECT  = 0x00100000,  
   FIELD_MOD_SPECIAL_NAME     = 0x00200000,  
   FIELD_MOD_HIDEBYSIG        = 0x00400000,  
  
   FIELD_MOD_WRITEONLY        = 0x80000000,  
   FIELD_MOD_ACCESS_MASK      = 0x000000ff,  
   FIELD_MOD_MASK             = 0xffffff00,  
   FIELD_MOD_ALL              = 0x7fffffff  
};  
typedef DWORD FIELD_MODIFIERS;  
```  
  
```c#  
public enum enum_FIELD_MODIFIERS {  
   FIELD_MOD_NONE             = 0x00000000,  
  
   // Modifier of the field  
   FIELD_MOD_ACCESS_NONE      = 0x00000001,  
   FIELD_MOD_ACCESS_PUBLIC    = 0x00000002,  
   FIELD_MOD_ACCESS_PROTECTED = 0x00000004,  
   FIELD_MOD_ACCESS_PRIVATE   = 0x00000008,  
  
   // Storage modifier of the field  
   FIELD_MOD_NOMODIFIERS      = 0x00000010,  
   FIELD_MOD_STATIC           = 0x00000020,  
   FIELD_MOD_CONSTANT         = 0x00000040,  
   FIELD_MOD_TRANSIENT        = 0x00000080,  
   FIELD_MOD_VOLATILE         = 0x00000100,  
   FIELD_MOD_ABSTRACT         = 0x00000200,  
   FIELD_MOD_NATIVE           = 0x00000400,  
   FIELD_MOD_SYNCHRONIZED     = 0x00000800,  
   FIELD_MOD_VIRTUAL          = 0x00001000,  
   FIELD_MOD_INTERFACE        = 0x00002000,  
   FIELD_MOD_FINAL            = 0x00004000,  
   FIELD_MOD_SENTINEL         = 0x00008000,  
   FIELD_MOD_INNERCLASS       = 0x00010000,  
   FIELD_TYPE_OPTIONAL        = 0x00020000,  
   FIELD_MOD_BYREF            = 0x00040000,  
   FIELD_MOD_HIDDEN           = 0x00080000,  
   FIELD_MOD_MARSHALASOBJECT  = 0x00100000,  
   FIELD_MOD_SPECIAL_NAME     = 0x00200000,  
   FIELD_MOD_HIDEBYSIG        = 0x00400000,  
  
   FIELD_MOD_WRITEONLY        = 0x80000000,  
   FIELD_MOD_ACCESS_MASK      = 0x000000ff,  
   FIELD_MOD_MASK             = 0xffffff00,  
   FIELD_MOD_ALL              = 0x7fffffff  
};  
```  
  
## メンバー  
 FIELD\_MOD\_ACCESS\_TYPE  
 フィールドにアクセスできないことを示します。  
  
 FIELD\_MOD\_ACCESS\_PUBLIC  
 パブリック フィールドにアクセスできることを示します。  
  
 FIELD\_MOD\_ACCESS\_PROTECTED  
 フィールドにアクセスを保護することを示します。  
  
 FIELD\_MOD\_ACCESS\_PRIVATE  
 プライベート フィールドにアクセスできることを示します。  
  
 FIELD\_MOD\_NOMODIFIERS  
 フィールドに修飾子がないことを示します。  
  
 FIELD\_MOD\_STATIC  
 フィールドが静的であることを示します。  
  
 FIELD\_MOD\_CONSTANT  
 フィールドが定数であることを示します。  
  
 FIELD\_MOD\_TRANSIENT  
 フィールドが一時的であることを示します。  
  
 FIELD\_MOD\_VOLATILE  
 フィールドは揮発性であることを示します。  
  
 FIELD\_MOD\_ABSTRACT  
 フィールドが抽象クラスであることを示します。  
  
 FIELD\_MOD\_NATIVE  
 フィールドがネイティブであることを示します。  
  
 FIELD\_MOD\_SYNCHRONIZED  
 フィールドが同期されていることを示します。  
  
 FIELD\_MOD\_VIRTUAL  
 フィールドが仮想であることを示します。  
  
 FIELD\_MOD\_INTERFACE  
 フィールドがインターフェイスであることを示します。  
  
 FIELD\_MOD\_FINAL  
 フィールドが最終的であることを示します。  
  
 FIELD\_MOD\_SENTINEL  
 フィールドが sentinel であることを示します。  
  
 FIELD\_MOD\_INNERCLASS  
 フィールドがの内部クラスであることを示します。  
  
 FIELD\_TYPE\_OPTIONAL  
 フィールドが省略可能であることを示します。  
  
 FIELD\_MOD\_BYREF  
 フィールドは参照引数であることを示します。  これはメソッド引数の用です。  
  
 FIELD\_MOD\_HIDDEN  
 フィールドに別のコンテキストで非表示になるかがあることを示しています ; たとえば[!INCLUDE[vbprvb](../../../code-quality/includes/vbprvb_md.md)] のローカル。  
  
 FIELD\_MOD\_MARSHALASOBJECT  
 フィールドが `IUnknown` インターフェイスとオブジェクトを表すことを示します。  
  
 FIELD\_MOD\_SPECIAL\_NAME  
 フィールドに特別な名前のみ\)コンストラクター \([!INCLUDE[vbprvb](../../../code-quality/includes/vbprvb_md.md)] のたとえば`.ctor` があることを示します。  
  
 FIELD\_MOD\_HIDEBYSIG  
 フィールドに適用される `Overloads` のキーワードがあることを示します \([!INCLUDE[vbprvb](../../../code-quality/includes/vbprvb_md.md)] のみ\)。  
  
 FIELD\_MOD\_WRITEONLY  
 フィールドに書き込み専用であることを示します。  この値は `FIELD_MOD_ALL` にこのような書き込み専用フィールドの使用は関数の評価は異なり含まれません。  ユーザーは `FIELD_MOD_WRITEONLY` のフィールドを明示的に頼まなければ必要があります。  
  
 FIELD\_MOD\_ACCESS\_MASK  
 フィールドのアクセスのマスクを示します。  
  
 FIELD\_MOD\_MASK  
 フィールド修飾子のマスクを示します。  
  
## 解説  
 [FIELD\_INFO](../../../extensibility/debugger/reference/field-info.md) の構造体のメンバー `dwModifiers` に使用されます。  
  
 これらの値は特定のフィールドにフィルターに [EnumFields](../Topic/IDebugContainerField::EnumFields.md) のメソッドに渡されます。  
  
## 必要条件  
 ヘッダー : sh.h  
  
 名前空間 : Microsoft.VisualStudio.Debugger.Interop  
  
 アセンブリ : Microsoft.VisualStudio.Debugger.Interop.dll  
  
## 参照  
 [列挙](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)   
 [FIELD\_INFO](../../../extensibility/debugger/reference/field-info.md)   
 [EnumFields](../Topic/IDebugContainerField::EnumFields.md)