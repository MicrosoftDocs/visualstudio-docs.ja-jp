---
title: IDebugProgramNode2::GetHostName |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- IDebugProgramNode2::GetHostName
helpviewer_keywords:
- IDebugProgramNode2::GetHostName
ms.assetid: 16aad1ff-ad34-4394-a2e4-5621374a7729
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: b7c6642d088da304b0a2d2e48292e8dcbcec1e38
ms.sourcegitcommit: 845442e2b515c3ca1e4e47b46cc1cef4df4f08d8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/20/2019
ms.locfileid: "56450036"
---
# <a name="idebugprogramnode2gethostname"></a>IDebugProgramNode2::GetHostName
プログラムをホストするプロセスの名前を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetHostName (
    GETHOSTNAME_TYPE dwHostNameType,
    BSTR*            pbstrHostName
);
```

```csharp
int GetHostName (
    enum_GETHOSTNAME_TYPE dwHostNameType,
    out string            pbstrHostName
);
```

#### <a name="parameters"></a>パラメーター
`dwHostNameType`  
[in]値、 [GETHOSTNAME_TYPE](../../../extensibility/debugger/reference/gethostname-type.md)列挙型を返す名前の型を指定します。

`pbstrHostName`  
[out]ホスト プロセスの名前を返します。

## <a name="return-value"></a>戻り値
成功した場合、返します`S_OK`、それ以外のエラー コードを返します。

## <a name="example"></a>例
次の例は、単純なは、このメソッドを実装する方法を示しています。`CProgram`を公開するオブジェクト、 [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)インターフェイス。 この例では無視、`dwHostNameType`パラメーターをモジュールのファイル パスのベース名から取得したように、プログラムの名前のみを返します。

```cpp
HRESULT CProgram::GetHostName(DWORD dwHostNameType, BSTR* pbstrHostName) {
    // Check for valid argument.
    if (pbstrHostName)
    {
        char szModule[_MAX_PATH];

        // Attempt to assign to szModule the path for the file used
        // to create the calling process.
        if (GetModuleFileName(NULL, szModule, sizeof (szModule)))
        {
            // If successful then declare several char arrays
            char  szDrive[_MAX_DRIVE];
            char  szDir[_MAX_DIR];
            char  szName[_MAX_FNAME];
            char  szExt[_MAX_EXT];
            char  szFilename[_MAX_FNAME + _MAX_EXT];
            WCHAR wszFilename[_MAX_FNAME + _MAX_EXT];

            // Break the szModule path name into components.
            _splitpath(szModule, szDrive, szDir, szName, szExt);

            // Copy the base file name szName into szFilename.
            lstrcpy(szFilename, szName);
            // Append the field extension szExt into szFilename.
            lstrcat(szFilename, szExt);

            // Convert the szFilename sequence of multibyte characters
            // to the wszFilename sequence of wide characters.
            mbstowcs(wszFilename, szFilename, sizeof (wszFilename) / 2);

            // Assign the wszFilename to the value at *pbstrHostName.
            *pbstrHostName = SysAllocString(wszFilename);

            return S_OK;
        }
    }

    return E_INVALIDARG;
}
```

## <a name="see-also"></a>関連項目
[IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)  
[GETHOSTNAME_TYPE](../../../extensibility/debugger/reference/gethostname-type.md)  
[IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)
