---
title: IDebugDocumentChecksum2::GetChecksumAndAlgorithmId | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- IDebugDocumentChecksum2::GetChecksumAndAlgorithmI
- GetChecksumAndAlgorithmI
ms.assetid: 25efef99-0ef3-4332-a752-607605fc6e67
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 0f1a00b34aa640f9198649552ad7f1620d9b026d
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62875740"
---
# <a name="idebugdocumentchecksum2getchecksumandalgorithmid"></a>IDebugDocumentChecksum2::GetChecksumAndAlgorithmId
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

使用するバイトの最大数を指定されたドキュメントのチェックサムとアルゴリズム識別子を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT GetChecksumAndAlgorithmId(   
   GUID  *pRetVal,  
   ULONG cMaxBytes,  
   BYTE  *pChecksum,  
   ULONG *pcNumBytes  
);  
```  
  
```csharp  
public int GetChecksumAndAlgorithmId(   
   out Guid pRetVal,  
   uint     cMaxBytes,  
   out byte pChecksum,  
   out uint pcNumBytes  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pRetVal`  
 [out]チェックサム アルゴリズムの一意の識別子。  
  
 `cMaxBytes`  
 [in]チェックサムを使用するバイトの最大数。  
  
 `pChecksum`  
 [out]チェックサムの値。  
  
 `pcNumBytes`  
 [out]実際のチェックサムの使用バイト数。  
  
## <a name="return-value"></a>戻り値  
 成功した場合、返します`S_OK`、それ以外のエラー コードを返します。  
  
## <a name="example"></a>例  
 次の例では、このメソッドを使用して、チェックサムとドキュメントのアルゴリズムを取得します。  
  
```cpp#  
HRESULT CDebugCodeContext::GetDocumentChecksumAndAlgorithmId(GUID *pguidAlgorithm, BYTE **ppChecksum, ULONG *pcNumBytes)  
{  
    HRESULT hRes = E_FAIL;  
  
    *ppChecksum = NULL;  
    *pcNumBytes = 0;  
  
    CComPtr<IDebugDocumentContext2> pDocContext;  
  
    hRes = this->GetDocumentContext(&pDocContext);  
  
    if ( HREVAL(S_OK, hRes) )  
    {  
        CComQIPtr<IDebugDocumentChecksum2> pDocChecksum(pDocContext);  
  
        if ( pDocChecksum != NULL )  
        {  
            // Figure out the size of the checksum buffer required  
            ULONG cNumBytes = 0;  
  
            hRes = pDocChecksum->GetChecksumAndAlgorithmId(pguidAlgorithm, 0, NULL, &cNumBytes);  
  
            if ( S_OK == hRes )  
            {  
                // check to see if we got back valid values  
                if ( cNumBytes && GUID_NULL != (*pguidAlgorithm) )  
                {  
                    // Alloc space for the checksum data  
                    BYTE *pChecksum = (BYTE*) CoTaskMemAlloc(cNumBytes);  
  
                    if ( pChecksum )  
                    {  
                        // Get the buffer containing the checksum info  
                        hRes = pDocChecksum->GetChecksumAndAlgorithmId(pguidAlgorithm, cNumBytes, pChecksum, &cNumBytes);  
  
                        if ( HREVAL(S_OK, hRes) )  
                        {  
                            *ppChecksum = pChecksum;  
                            *pcNumBytes = cNumBytes;  
                        }  
                        else  
                        {  
                            CoTaskMemFree(pChecksum);  
                        }  
                    }  
                    else  
                        hRes = E_OUTOFMEMORY;  
                }  
                else  
                    hRes = S_FALSE; // lang doesn't support checksums  
            }  
            else  
                hRes = S_FALSE; // failed to work out checksum info  
        }  
        else  
            hRes = S_FALSE; // SH doesn't support checksums  
    }  
  
    return ( hRes );  
}  
```  
  
## <a name="see-also"></a>関連項目  
 [IDebugDocumentChecksum2](../../../extensibility/debugger/reference/idebugdocumentchecksum2.md)
