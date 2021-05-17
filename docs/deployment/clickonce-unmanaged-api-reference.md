---
title: ClickOnce アンマネージド API リファレンス |Microsoft Docs
description: dfshim.dll の ClickOnce アンマネージド パブリック Api について説明します。これには、CleanOnlineAppcache、GetDeploymentDataFromManifest、LaunchApplication が含まれます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
api_name:
- CleanOnlineAppCache
- GetDeploymentDataFromManifest
- LaunchApplication
api_location:
- dfshim.dll
api_type:
- COM
topic_type:
- apiref
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- LaunchApplication [ClickOnce unmanaged]
- ClickOnce, unmanaged APIs
- CleanOnlineAppCache [ClickOnce unmanaged]
- CleanOnlineAppCacheW interface [ClickOnce unmanaged]
- GetDeploymentDataFromManifest [ClickOnce unmanaged]
ms.assetid: ec002138-4054-456d-bcc1-79ac2f4a4fd7
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- cplusplus
ms.openlocfilehash: 88d8147dded05c6bec54682e76c6a8c1826b43e0
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99900797"
---
# <a name="clickonce-unmanaged-api-reference"></a>ClickOnce アンマネージド API リファレンス
dfshim.dll の [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アンマネージド パブリック API。

## <a name="cleanonlineappcache"></a>CleanOnlineAppCache
 すべてのオンライン アプリケーションを [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーション キャッシュからクリーンまたはアンインストールします。

### <a name="return-value"></a>戻り値
 成功した場合は S_OK を返します。それ以外の場合は、エラーを表す HRESULT を返します。 マネージド例外が発生した場合は、0x80020009 (DISP_E_EXCEPTION) を返します。

### <a name="remarks"></a>解説
 CleanOnlineAppCache を呼び出すと、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] サービスがまだ実行されていない場合は起動されます。

## <a name="getdeploymentdatafrommanifest"></a>GetDeploymentDataFromManifest
 マニフェストおよびライセンス認証 URL から配置情報を取得します。

### <a name="parameters"></a>パラメーター

|パラメーター|説明|Type|
|---------------|-----------------|----------|
|`pcwzActivationUrl`|`ActivationURL` へのポインター。|LPCWSTR|
|`pcwzPathToDeploymentManifest`|`PathToDeploymentManifest` へのポインター。|LPCWSTR|
|`pwzApplicationIdentity`|返される完全なアプリケーション ID を指定する NULL 終端文字列を受け取るバッファーへのポインター。|LPWSTR|
|`pdwIdentityBufferLength`|`pwzApplicationIdentity` バッファーの長さ (WCHAR 単位) である DWORD へのポインター。 これには、NULL 終端文字用の空白が含まれます。|LPDWORD|
|`pwzProcessorArchitecture`|アプリケーション配置のプロセッサ アーキテクチャを指定する NULL 終端文字列をマニフェストから受け取るためのバッファーへのポインター。|LPWSTR|
|`pdwArchitectureBufferLength`|`pwzProcessorArchitecture` バッファーの長さ (WCHAR 単位) である DWORD へのポインター。|LPDWORD|
|`pwzApplicationManifestCodebase`|アプリケーション マニフェストのコードベースを指定する NULL 終端文字列をマニフェストから受け取るためのバッファーへのポインター。|LPWSTR|
|`pdwCodebaseBufferLength`|`pwzApplicationManifestCodebase` バッファーの長さ (WCHAR 単位) である DWORD へのポインター。|LPDWORD|
|`pwzDeploymentProvider`|存在する場合、配置プロバイダーを指定する NULL 終端文字列をマニフェストから受け取るためのバッファーへのポインター。 それ以外の場合は、空の文字列が返されます。|LPWSTR|
|`pdwProviderBufferLength`|`pwzProviderBufferLength` の長さである DWORD へのポインター。|LPDWORD|

### <a name="return-value"></a>戻り値
 成功した場合は S_OK を返します。それ以外の場合は、エラーを表す HRESULT を返します。 バッファーが小さすぎる場合は、HRESULTFROMWIN32(ERROR_INSUFFICIENT_BUFFER) を返します。

### <a name="remarks"></a>解説
 ポインターで null 値を指定することはできません。 `pcwzActivationUrl` および `pcwzPathToDeploymentManifest` を空にすることはできません。

 ライセンス認証 URL をクリーンアップするのは、呼び出し元が行います。 たとえば、必要に応じてエスケープ文字を追加したり、クエリ文字列を削除したりします。

 入力の長さを制限するのは、呼び出し元が行います。 たとえば、URL の最大長は 2 KB です。

## <a name="launchapplication"></a>LaunchApplication
 配置 URL を使用してアプリケーションを起動またはインストールします。

### <a name="parameters"></a>パラメーター

|パラメーター|説明|Type|
|---------------|-----------------|----------|
|`deploymentUrl`|配置マニフェストの URL を格納している NULL 終端文字列へのポインター。|LPCWSTR|
|`data`|将来使用するために予約されています。 NULL にする必要があります|LPVOID|
|`flags`|将来使用するために予約されています。 0 を指定する必要があります。|DWORD|

### <a name="return-value"></a>戻り値
 成功した場合は S_OK を返します。それ以外の場合は、エラーを表す HRESULT を返します。 マネージド例外が発生した場合は、0x80020009 (DISP_E_EXCEPTION) を返します。

## <a name="see-also"></a>関連項目
- <xref:System.Deployment.Application.DeploymentServiceCom.CleanOnlineAppCache%2A>