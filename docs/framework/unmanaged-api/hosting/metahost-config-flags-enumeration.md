---
title: METAHOST_CONFIG_FLAGS 枚举
ms.date: 03/30/2017
api_name:
- METAHOST_CONFIG_FLAGS
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- METAHOST_CONFIG_FLAGS
helpviewer_keywords:
- METAHOST_CONFIG_FLAGS enumeration [.NET Framework hosting]
ms.assetid: 6f1e389f-ed99-4d6a-a0ba-72d7d869a01d
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 13a7ad5b59dd318f823645d28f9c3ccbec8a8cb0
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/10/2019
ms.locfileid: "67781091"
---
# <a name="metahostconfigflags-enumeration"></a>METAHOST_CONFIG_FLAGS 枚举
描述中返回的可能标志`pdwConfigFlags`的参数[iclrmetahostpolicy:: Getrequestedruntime](../../../../docs/framework/unmanaged-api/hosting/iclrmetahostpolicy-getrequestedruntime-method.md)方法，指示是否存在并设置`useLegacyV2RuntimeActivationPolicy`属性中[ \<启动 > 元素](../../../../docs/framework/configure-apps/file-schema/startup/startup-element.md)的配置文件。  
  
## <a name="syntax"></a>语法  
  
```cpp  
typedef enum {  
    METAHOST_CONFIG_FLAGS_LEGACY_V2_ACTIVATION_POLICY_UNSET  = 0x00,  
    METAHOST_CONFIG_FLAGS_LEGACY_V2_ACTIVATION_POLICY_TRUE   = 0x01,  
    METAHOST_CONFIG_FLAGS_LEGACY_V2_ACTIVATION_POLICY_FALSE  = 0x02,  
    METAHOST_CONFIG_FLAGS_LEGACY_V2_ACTIVATION_POLICY_MASK   = 0x03  
} METAHOST_CONFIG_FLAGS;  
```  
  
## <a name="members"></a>成员  
  
|成员|描述|  
|------------|-----------------|  
|`METAHOST_CONFIG_FLAGS_LEGACY_V2_ACTIVATION_POLICY_UNSET`|`useLegacyV2RuntimeActivationPolicy`属性未出现在[\<启动 > 元素](../../../../docs/framework/configure-apps/file-schema/startup/startup-element.md)。|  
|`METAHOST_CONFIG_FLAGS_LEGACY_V2_ACTIVATION_POLICY_TRUE`|`useLegacyV2RuntimeActivationPolicy`属性已存在且设置为`true`。|  
|`METAHOST_CONFIG_FLAGS_LEGACY_V2_ACTIVATION_POLICY_FALSE`|`useLegacyV2RuntimeActivationPolicy`属性已存在且设置为`false`。|  
|`METAHOST_CONFIG_FLAGS_LEGACY_V2_ACTIVATION_POLICY_MASK`|将此掩码应用于中返回的值`pdwConfigFlags`若要获取这些值与相关`useLegacyV2RuntimeActivationPolicy`。|  
  
## <a name="remarks"></a>备注  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** Metahost.h  
  
 **库：** 包含为 MSCorEE.dll 中的资源  
  
 **.NET Framework 版本：** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>请参阅

- [承载枚举](../../../../docs/framework/unmanaged-api/hosting/hosting-enumerations.md)
- [GetRequestedRuntime 方法](../../../../docs/framework/unmanaged-api/hosting/iclrmetahostpolicy-getrequestedruntime-method.md)
- [\<startup> 元素](../../../../docs/framework/configure-apps/file-schema/startup/startup-element.md)
