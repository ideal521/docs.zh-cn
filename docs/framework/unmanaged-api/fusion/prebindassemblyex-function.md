---
title: PreBindAssemblyEx 函数
ms.date: 03/30/2017
api_name:
- PreBindAssemblyEx
api_location:
- fusion.dll
api_type:
- DLLExport
f1_keywords:
- PreBindAssemblyEx
helpviewer_keywords:
- PreBindAssemblyEx function [.NET Framework fusion]
ms.assetid: bd285233-a4a2-4b52-bbca-0025a60e4864
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: a23d3c4fd8eef2e361abf1602157cb4fbb820b48
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/10/2019
ms.locfileid: "67773859"
---
# <a name="prebindassemblyex-function"></a>PreBindAssemblyEx 函数
获取程序集的策略后的显示名称。  
  
 此函数支持.NET Framework 基础结构，不应在代码中直接使用。  
  
## <a name="syntax"></a>语法  
  
```cpp  
HRESULT PreBindAssemblyEx (  
    [in]  IApplicationContext *pAppCtx,  
    [in]  IAssemblyName       *pName,  
    [in]  IAssembly           *pAsmParent,  
    [in]  LPCWSTR             pwzRuntimeVersion,  
    [out] IAssemblyName       **ppNamePostPolicy,  
    [in]  LPVOID              pvReserved  
 );  
```  
  
## <a name="parameters"></a>参数  
 `pAppCtx`  
 [in]标识应用程序上下文。  
  
 `pName`  
 [in]标识程序集名称。  
  
 `pAsmParent`  
 [in]标识父程序集。 忽略此参数。  
  
 `pwzRuntimeVersion`  
 [in]标识运行时版本。  
  
 `ppNamePostPolicy`  
 [out]包含策略后的显示名称。  
  
 `pvReserved`  
 [in]保留供将来的扩展。 `pvReserved` 必须是 null 引用。  
  
## <a name="remarks"></a>备注  
 `ppNamePostPolicy`仅当该函数将返回 HRESULT FUSION_E_REF_DEF_MISMATCH 设置输出参数。 否则，它为 null。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** Fusion.h  
  
 **库：** 包含为 MsCorEE.dll 中的资源  
  
 **.NET Framework 版本：** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>请参阅

- [合成全局静态函数](../../../../docs/framework/unmanaged-api/fusion/fusion-global-static-functions.md)
