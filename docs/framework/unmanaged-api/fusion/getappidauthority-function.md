---
title: GetAppIdAuthority 函数
ms.date: 03/30/2017
api_name:
- GetAppIdAuthority
api_location:
- fusion.dll
- clr.dll
api_type:
- COM
f1_keywords:
- GetAppIdAuthority
helpviewer_keywords:
- GetAppIdAuthority function [.NET Framework fusion]
ms.assetid: 9f968dad-0d09-47fb-bebc-94c39a0d16ad
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 536f3249593333234f7f09921007b483fb80cf79
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/10/2019
ms.locfileid: "67778588"
---
# <a name="getappidauthority-function"></a>GetAppIdAuthority 函数
获取一个指向[IAppIdAuthority](../../../../docs/framework/unmanaged-api/fusion/iappidauthority-interface.md)管理密钥的应用程序标识和引用的实例。  
  
## <a name="syntax"></a>语法  
  
```cpp  
HRESULT GetAppIdAuthority (  
    [out] IAppIdAuthority **ppIAppIdAuthority  
 );  
```  
  
## <a name="parameters"></a>参数  
 `ppIAppIdAuthority`  
 [out]返回`IAppIdAuthority`指针。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** Isolation.h  
  
 **.NET Framework 版本：** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>请参阅

- [IAppIdAuthority 接口](../../../../docs/framework/unmanaged-api/fusion/iappidauthority-interface.md)
- [合成全局静态函数](../../../../docs/framework/unmanaged-api/fusion/fusion-global-static-functions.md)
