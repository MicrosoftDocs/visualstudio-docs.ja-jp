---
title: "方法: バックグラウンド スレッド (C++) からサービスを取得する | Microsoft Docs"
ms.custom: ""
ms.date: "11/16/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "マルチスレッド、サービス"
ms.assetid: 97a56709-66d4-431a-ae63-392ee5898511
caps.latest.revision: 8
caps.handback.revision: 8
manager: "douge"
---
# 方法: バックグラウンド スレッド (C++) からサービスを取得する
サービスはバックグラウンド スレッドから `IServiceProvider.QueryService` によって取得できません。  メイン スレッドでサービスを取得するために `QueryService` を使用しバックグラウンド スレッドでサービスを使用すると失敗します。  
  
 バックグラウンド スレッドからサービスを取得するにはメイン スレッドのストリームにサービス プロバイダーをマーシャリングするために `IVsPackage.SetSite` のメソッドで `CoMarshalInterThreadInterfaceInStream` を使用します。  バックグラウンド スレッドを unmarshal サービス プロバイダー サービスを取得するために使用することもできます。  一度だけ unmarshal できます。そのため返されたインターフェイスをキャッシュします。  
  
> [!NOTE]
>  マネージ コードが自動的にスレッド間のインターフェイスをマーシャリングするためバックグラウンド スレッドからサービスを取得するには特別なコードは不要です。  
  
## 使用例  
 次のコードはメイン スレッドのサービス プロバイダーを unmarshal にマーシャリングしバックグラウンド スレッドからサービスを取得するに `QueryServiceFromBackgroundThread` サービス プロバイダーのメソッドを提供します。  
  
```  
class CMyPackage : public IVsPackage  
{  
private:  
    // Used to marshal IServiceProvider between threads  
    CComPtr< IStream > m_pSPStream;  
    // IServiceProvider proxy for the background thread  
    CComPtr< IServiceProvider > m_pBackgroundSP;  
  
public:  
    HRESULT SetSite( IServiceProvider* pSP )  
    {  
        // Marshal the service provider into a stream so that  
        // the background thread can retrieve it later  
        CoMarshalInterThreadInterfaceInStream(  
            IID_IServiceProvider, pSP, &m_pSPStream);  
  
        //... do the rest of your initialization  
    }  
  
    // Call this when your background thread needs to call QueryService  
    // The first time through, it unmarshals the interface stored   
    HRESULT QueryServiceFromBackgroundThread(  
        REFGUID rsid,        // [in] Service ID  
        REFIID riid,         // [in] Interface ID  
        // [out] Interface pointer of requested service (NULL on error)  
        void **ppvObj  
    {  
        if( !m_pBackgroundSP )  
        {  
            if( !m_pSPStream )  
            {  
                return E_UNEXPECTED;  
            }  
  
            HRESULT hr = CoGetInterfaceAndReleaseStream(   
                m_pSPStream, IID_IServiceProvider,   
                (void **)&m_pBackgroundSP );  
            if( FAILED(hr) )  
            {  
                return hr;  
            }  
  
            // The CoGetInterfaceAndReleaseStream has already   
            // destroyed the stream.  To avoid double-freeing,   
            // the smart wrapper needs to be detached.  
            m_pSPStream.Detach();  
        }  
  
        return m_pBackgroundSP->QueryService( rsid, riid, ppvObj );  
    }  
};  
```  
  
## 参照  
 [使用して、サービスを提供します。](../extensibility/using-and-providing-services.md)   
 [サービスの基礎](../extensibility/internals/service-essentials.md)