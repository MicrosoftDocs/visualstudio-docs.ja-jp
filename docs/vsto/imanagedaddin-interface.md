---
title: IManagedAddin インターフェイス
description: マネージド VSTO アドインを読み込むコンポーネントを作成するには、IManagedAddin インターフェイスを実装します。
ms.date: 02/02/2017
ms.topic: interface
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- IManagedAddin interface
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 614cf7e8d0e682d894328fb764c6d64b855d2834
ms.sourcegitcommit: 8590cf6b3351e82827fd21159beefef0c02bf162
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/08/2021
ms.locfileid: "102469789"
---
# <a name="imanagedaddin-interface"></a>IManagedAddin インターフェイス
  マネージド VSTO アドインを読み込むコンポーネントを作成するには、IManagedAddin インターフェイスを実装します。このインターフェイスは、Microsoft Office 2007 システムに追加されました。

## <a name="syntax"></a>構文

```csharp
[
    object,
    uuid(B9CEAB65-331C-4713-8410-DDDAF8EC191A),
    pointer_default(unique),
    oleautomation
]
interface IManagedAddin : IUnknown
{
    HRESULT Load(
        [in] BSTR bstrManifestURL,
        [in] IDispatch *pdispApplication);
    HRESULT Unload();
};
```

## <a name="methods"></a>メソッド
 IManagedAddin インターフェイスで定義されているメソッドを次の表に示します。

|名前|説明|
|----------|-----------------|
|[IManagedAddin::Load](../vsto/imanagedaddin-load.md)|Microsoft Office アプリケーションがマネージド VSTO アドインを読み込むときに呼び出されます。|
|[IManagedAddin::Unload](../vsto/imanagedaddin-unload.md)|Microsoft Office アプリケーションがマネージド VSTO アドインをアンロードする直前に呼び出されます。|

## <a name="remarks"></a>解説
 Microsoft Office 2007 システム以降の Microsoft Office アプリケーションでは、IManagedAddin インターフェイスを使用して Office VSTO アドインを読み込むことができます。VSTO アドイン ローダー (*VSTOLoader.dll*) および [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] を使用する代わりに、IManagedAddin インターフェイスを実装して、マネージド VSTO アドイン用の独自の VSTO アドイン ローダーとランタイムを作成できます。 詳細については、「 [Architecture of VSTO Add-ins](../vsto/architecture-of-vsto-add-ins.md)」を参照してください。

## <a name="how-managed-add-ins-are-loaded"></a>マネージド アドインの読み込みのしくみ
 アプリケーションが起動すると、次の処理が行われます。

1. アプリケーションによって、次のレジストリ キーにあるエントリが検索され、VSTO アドインが検出されます。

    **HKEY_CURRENT_USER\Software\Microsoft\Office\\ *\<application name>* \Addins\\**

    このレジストリ キーにある各エントリは、VSTO アドインの一意な ID です。 通常、これは VSTO アドイン アセンブリの名前です。

2. アプリケーションによって、各 VSTO アドイン エントリにある `Manifest` エントリが検索されます。

    マネージド VSTO アドインでは、**HKEY_CURRENT_USER\Software\Microsoft\Office\\ _\<application name>_ \Addins\\ _\<add-in ID>_** にある `Manifest` エントリに、マニフェストの完全なパスを格納できます。 マニフェストは、VSTO アドインの読み込みに使用される情報を提供するファイル (通常は XML ファイル) です。

3. アプリケーションによって `Manifest` エントリが検出されると、そのアプリケーションはマネージド VSTO アドイン ローダー コンポーネントの読み込みを試みます。 アプリケーションでは、IManagedAddin インターフェイスを実装する COM オブジェクトを作成することでこれが試みられます。

    [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] には、VSTO アドイン ローダー コンポーネント (*VSTOLoader.dll*) が含まれていますが、IManagedAddin インターフェイスを実装して独自のアドイン ローダーを作成することもできます。

4. アプリケーションによって [IManagedAddin::Load](../vsto/imanagedaddin-load.md) メソッドが呼び出され、 `Manifest` エントリの値に渡されます。

5. [IManagedAddin::Load](../vsto/imanagedaddin-load.md) メソッドによって、読み込む VSTO アドイン用のアプリケーション ドメインやセキュリティ ポリシーの構成など、VSTO アドイン読み込みに必要なタスクが実行されます。

   Microsoft Office アプリケーションでマネージド VSTO アドインの検出と読み込みに使用するレジストリ キーの詳細については、「[VSTO アドインのレジストリ エントリ](../vsto/registry-entries-for-vsto-add-ins.md)」を参照してください。

## <a name="guidance-to-implement-imanagedaddin"></a>IManagedAddin を実装するためのガイダンス
 IManagedAddin を実装する場合には、次の CLSID を使用して実装が含まれている DLL を登録する必要があります。

 99D651D7-5F7C-470E-8A3B-774D5D9536AC

 Microsoft Office アプリケーションでは、この CLSID を使用して IManagedAddin を実装する COM オブジェクトを作成します。

> [!CAUTION]
> この CLSID は、[!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] で *VSTOLoader.dll* によっても使用されます。 したがって、IManagedAddin を使用して独自の VSTO アドイン ローダーおよびランタイム コンポーネントを作成する場合は、[!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] に依存して VSTO アドインを実行しているコンピューターにはコンポーネントをデプロイできません。

## <a name="see-also"></a>関連項目
- [アンマネージド API リファレンス &#40;Visual Studio での Office 開発&#41;](../vsto/unmanaged-api-reference-office-development-in-visual-studio.md)
