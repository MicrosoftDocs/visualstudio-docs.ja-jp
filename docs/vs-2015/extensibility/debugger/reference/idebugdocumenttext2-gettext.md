---
title: IDebugDocumentText2::GetText |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugDocumentText2::GetText
helpviewer_keywords:
- IDebugDocumentText2::GetText
ms.assetid: f8c15a58-da77-473e-a721-7a094e306c63
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 066c2c025fe7b1c83fb30cb3a0e1a7b61d8c2c41
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "58974263"
---
# <a name="idebugdocumenttext2gettext"></a>IDebugDocumentText2::GetText
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

ドキュメント内の指定した位置からテキストを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT GetText(   
   TEXT_POSITION pos,  
   ULONG         cMaxChars,  
   WCHAR*        pText,  
   ULONG*        pcNumChars  
);  
```  
  
```csharp  
int GetText(   
   eumn_TEXT_POSITION pos,  
   uint               cMaxChars,  
   IntPtr             pText,  
   out uint           pcNumChars  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pos`  
 [in]A [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md)構造体を取得するテキストの位置を示す。  
  
 `cMaxChars`  
 [in]取得するテキストの文字の最大数。  
  
 `pText`  
 [入力、出力]目的のテキストで格納されるバッファーへのポインター。 このバッファーは、少なくともできる必要があります`cMaxChars`ワイド文字の数。  
  
 `pcNumChars`  
 [out]実際に取得される文字数を返します。  
  
## <a name="return-value"></a>戻り値  
 成功した場合、返します`S_OK`、それ以外のエラー コードを返します。  
  
## <a name="example"></a>例  
 この例では、C# からのこのメソッドの呼び出し方法を示します。  
  
```csharp  
using System.Runtime.Interop.Services;  
using Microsoft.VisualStudio;  
using Microsoft.VisualStudio.Debugger.Interop;  
  
namespace Mynamespace  
{  
    class MyClass  
    {  
         string GetDocumentText(IDebugDocumentText2 pText, TEXT_POSITION pos)  
        {  
             string documentText = string.Empty;  
             if (pText != null)  
             {  
                  uint numLines = 0;  
                  uint numChars = 0;  
                  int hr;  
                  hr = pText.GetSize(ref numLines, ref numChars);  
                  if (ErrorHandler.Succeeded(hr))  
                  {  
                       IntPtr buffer = Marshal.AllocCoTaskMem((int)numChars * sizeof(char));  
                       uint actualChars = 0;  
                       hr = pText.GetText(pos, numChars, buffer, out actualChars);  
                       if (ErrorHandler.Succeeded(hr))  
                       {  
                            documentText = Marshal.PtrToStringUni(buffer, (int)actualChars);  
                       }  
                       Marshal.FreeCoTaskMem(buffer);  
                  }  
              }  
              return documentText;  
         }  
    }  
}  
```  
  
## <a name="see-also"></a>関連項目  
 [IDebugDocumentText2](../../../extensibility/debugger/reference/idebugdocumenttext2.md)   
 [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md)
