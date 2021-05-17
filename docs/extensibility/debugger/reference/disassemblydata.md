---
description: 統合開発環境 (IDE) で表示する 1 つの逆アセンブリ命令を記述します。
title: DisassemblyData | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- DisassemblyData
helpviewer_keywords:
- DisassemblyData structure
ms.assetid: 10e70aa7-9381-40d3-bdd1-d2cad78ef16c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 71d52c4f48f23368d83d81f88fba4bf0ba36f197
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105096123"
---
# <a name="disassemblydata"></a>DisassemblyData
統合開発環境 (IDE) で表示する 1 つの逆アセンブリ命令を記述します。

## <a name="syntax"></a>構文

```cpp
typedef struct tagDisassemblyData {
    DISASSEMBLY_STREAM_FIELDS dwFields;
    BSTR                      bstrAddress;
    BSTR                      bstrAddressOffset;
    BSTR                      bstrCodeBytes;
    BSTR                      bstrOpcode;
    BSTR                      bstrOperands;
    BSTR                      bstrSymbol;
    UINT64                    uCodeLocationId;
    TEXT_POSITION             posBeg;
    TEXT_POSITION             posEnd;
    BSTR                      bstrDocumentUrl;
    DWORD                     dwByteOffset;
    DISASSEMBLY_FLAGS         dwFlags;
} DisassemblyData;
```

```csharp
public struct DisassemblyData { 
    public uint          dwFields;
    public string        bstrAddress;
    public string        bstrAddressOffset;
    public string        bstrCodeBytes;
    public string        bstrOpcode;
    public string        bstrOperands;
    public string        bstrSymbol;
    public ulong         uCodeLocationId;
    public TEXT_POSITION posBeg;
    public TEXT_POSITION posEnd;
    public string        bstrDocumentUrl;
    public uint          dwByteOffset;
    public uint          dwFlags;
};
```

## <a name="members"></a>メンバー
`dwFields`\
入力するフィールドを指定する [DISASSEMBLY_STREAM_FIELDS](../../../extensibility/debugger/reference/disassembly-stream-fields.md) 定数。

`bstrAddress`\
何らかの開始位置 (通常は、関連付けられた関数の先頭) からのオフセットとしてのアドレス。

`bstrCodeBytes`\
この命令のコード バイト。

`bstrOpcode`\
この命令のオペコード。

`bstrOperands`\
この命令のオペランド。

`bstrSymbol`\
アドレスに関連付けられているシンボル名 (存在する場合) (パブリック シンボル、ラベルなど)。

`uCodeLocationId`\
この逆アセンブルされた行のコードの場所識別子。 ある行のコード コンテキスト アドレスが別の行のコード コンテキスト アドレスより大きい場合、最初の行の逆アセンブルされたコードの場所識別子も、2 番目のコードの場所識別子より大きくなります。

`posBeg`\
逆アセンブリ データが開始するドキュメント内の位置に対応する [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md)。

`posEnd`\
逆アセンブリ データが終了するドキュメント内の位置に対応する [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md)。

`bstrDocumentUrl`\
ファイル名として表すことができるテキスト ドキュメントの場合、`bstrDocumentUrl` フィールドには、`file://file name` の形式を使用して、ソースがあるファイル名が入力されます。

ファイル名として表現できないテキスト ドキュメントの場合は、`bstrDocumentUrl` はドキュメントの一意識別子であり、デバッグ エンジンでは [GetDocument](../../../extensibility/debugger/reference/idebugdisassemblystream2-getdocument.md) メソッドを実装する必要があります。

このフィールドには、チェックサムに関する追加情報を含めることもできます。 詳細については、「解説」を参照してください。

`dwByteOffset`\
コード行の先頭からの命令があるバイト数。

`dwFlags`\
アクティブなフラグを指定する [DISASSEMBLY_FLAGS](../../../extensibility/debugger/reference/disassembly-flags.md) 定数。

## <a name="remarks"></a>解説
各 `DisassemblyData` 構造体は、逆アセンブリの 1 つの命令を記述します。 これらの構造体の配列は、[Read](../../../extensibility/debugger/reference/idebugdisassemblystream2-read.md) メソッドから返されます。

[TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md)構造体は、テキストベースのドキュメントでのみ使用されます。 この命令のソース コードの範囲は、`dwByteOffset == 0` の場合など、ステートメントまたは行から生成された最初の命令に対してのみ入力されます。

テキスト以外のドキュメントでは、コードからドキュメント コンテキストを取得でき、`bstrDocumentUrl` フィールドは null 値にする必要があります。 `bstrDocumentUrl` フィールドが前の `DisassemblyData` 配列要素の `bstrDocumentUrl` フィールドと同じ場合は、`bstrDocumentUrl` を null 値に設定します。

`dwFlags` フィールドに `DF_DOCUMENT_CHECKSUM` フラグが設定されている場合は、`bstrDocumentUrl` フィールドが指す文字列の後に追加のチェックサム情報が続きます。 具体的には、null 文字列ターミネータの後に、チェックサム アルゴリズムを識別する GUID が続き、次にその後にチェックサムのバイト数を示す 4 バイトの値が続き、次にその後にチェックサム バイトが続きます。 [!INCLUDE[csprcs](../../../data-tools/includes/csprcs_md.md)] でこのフィールドをエンコードおよびデコードする方法については、このトピックの例を参照してください。

## <a name="example"></a>例
`DF_DOCUMENT_CHECKSUM` フラグが設定されている場合、`bstrDocumentUrl` フィールドには文字列以外の追加情報を含めることができます。 このエンコードされた文字列の作成と読み取りのプロセスは、[!INCLUDE[vcprvc](../../../code-quality/includes/vcprvc_md.md)] では簡単です。 ただし、[!INCLUDE[csprcs](../../../data-tools/includes/csprcs_md.md)] では、別問題です。 興味のあるユーザーは、次の例に、[!INCLUDE[csprcs](../../../data-tools/includes/csprcs_md.md)] からエンコードされた文字列を作成する 1 つの方法と、[!INCLUDE[csprcs](../../../data-tools/includes/csprcs_md.md)] でエンコードされた文字列をデコードする 1 つの方法を示しています。

```csharp
using System;
using System.Runtime.InteropServices;

namespace MyNamespace
{
    class MyClass
    {
        string EncodeData(string documentString,
                          Guid checksumGuid,
                          byte[] checksumData)
        {
            string returnString = documentString;

            if (checksumGuid == null || checksumData == null)
            {
                // Nothing more to do. Just return the string.
                return returnString;
            }

            returnString += '\0'; // separating null value

            // Add checksum GUID to string.
            byte[] guidDataArray  = checksumGuid.ToByteArray();
            int    guidDataLength = guidDataArray.Length;
            IntPtr pBuffer        = Marshal.AllocCoTaskMem(guidDataLength);
            for (int i = 0; i < guidDataLength; i++)
            {
                Marshal.WriteByte(pBuffer, i, guidDataArray[i]);
            }
            // Copy guid data bytes to string as wide characters.
            // Assumption: sizeof(char) == 2.
            for (int i = 0; i < guidDataLength / sizeof(char); i++)
            {
                returnString += (char)Marshal.ReadInt16(pBuffer, i * sizeof(char));
            }

            // Add checksum count (a 32-bit value).
            Int32 checksumCount = checksumData.Length;
            Marshal.StructureToPtr(checksumCount, pBuffer, true);
            for (int i = 0; i < sizeof(Int32) / sizeof(char); i++)
            {
                returnString += (char)Marshal.ReadInt16(pBuffer, i * sizeof(char));
            }

            // Add checksum data.
            pBuffer = Marshal.AllocCoTaskMem(checksumCount);
            for (int i = 0; i < checksumCount; i++)
            {
                Marshal.WriteByte(pBuffer, i, checksumData[i]);
            }
            for (int i = 0; i < checksumCount / sizeof(char); i++)
            {
                returnString += (char)Marshal.ReadInt16(pBuffer, i * sizeof(char));
            }
            Marshal.FreeCoTaskMem(pBuffer);

            return returnString;
        }

        void DecodeData(    string encodedString,
                        out string documentString,
                        out Guid   checksumGuid,
                        out byte[] checksumData)
        {
            documentString = String.Empty;
            checksumGuid = Guid.Empty;
            checksumData = null;

            IntPtr pBuffer = Marshal.StringToBSTR(encodedString);
            if (null != pBuffer)
            {
                int bufferOffset = 0;

                // Parse string out. String is assumed to be Unicode.
                documentString = Marshal.PtrToStringUni(pBuffer);
                bufferOffset += (documentString.Length + 1) * sizeof(char);

                // Parse Guid out.
                // Read guid bytes from buffer and store in temporary
                // buffer that contains only the guid bytes. Then the
                // Marshal.PtrToStructure() can work properly.
                byte[] guidDataArray  = checksumGuid.ToByteArray();
                int    guidDataLength = guidDataArray.Length;
                IntPtr pGuidBuffer    = Marshal.AllocCoTaskMem(guidDataLength);
                for (int i = 0; i < guidDataLength; i++)
                {
                    Marshal.WriteByte(pGuidBuffer, i,
                                      Marshal.ReadByte(pBuffer, bufferOffset + i));
                }
                bufferOffset += guidDataLength;
                checksumGuid = (Guid)Marshal.PtrToStructure(pGuidBuffer, typeof(Guid));
                Marshal.FreeCoTaskMem(pGuidBuffer);

                // Parse out the number of checksum data bytes (always 32-bit value).
                int dataCount = Marshal.ReadInt32(pBuffer, bufferOffset);
                bufferOffset += sizeof(Int32);

                // Parse out the checksum data.
                checksumData = new byte[dataCount];
                for (int i = 0; i < dataCount; i++)
                {
                    checksumData[i] = Marshal.ReadByte(pBuffer, bufferOffset + i);
                }
            }
        }
    }
}
```

## <a name="see-also"></a>関連項目
- [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)
- [読み取り](../../../extensibility/debugger/reference/idebugdisassemblystream2-read.md)
- [DISASSEMBLY_STREAM_FIELDS](../../../extensibility/debugger/reference/disassembly-stream-fields.md)
- [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)
- [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)
- [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md)
- [DISASSEMBLY_FLAGS](../../../extensibility/debugger/reference/disassembly-flags.md)
