---
title: SetPEKind 方法
ms.date: 03/30/2017
api_name:
- IALink2.SetPEKind
api_location:
- alink.dll
api_type:
- COM
f1_keywords:
- SetPEKind
helpviewer_keywords:
- SetPEKind method
ms.assetid: 050e77ee-3014-45c0-9e29-2ebe29347b0d
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 8fc581904351443f4368a68a653fd39b3548999a
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/10/2019
ms.locfileid: "67741425"
---
# <a name="setpekind-method"></a>SetPEKind 方法
确定特定于计算机或计算机不可知的可移植可执行文件类型。  
  
## <a name="syntax"></a>语法  
  
```cpp  
HRESULT SetPEKind(  
    mdAssembly AssemblyID,  
    mdToken FileToken,  
    DWORD dwPEKind,  
    DWORD dwMachine  
) PURE;   
```  
  
## <a name="parameters"></a>参数  
 `AssemblyID`  
 程序集的 ID。  
  
 `FileToken`  
 PE 类型要为其设置的文件的令牌。 可以为 NULL，如果`AssemblyID`并不表示未绑定的 netmodule。  
  
 `dwPEKind`  
 PE 所示的类型[CorPEKind 枚举](../../../../docs/framework/unmanaged-api/metadata/corpekind-enumeration.md)。  
  
 `dwMachine`  
 目标计算机体系结构，如 NT 标头中所示。  
  
## <a name="return-value"></a>返回值  
 如果该方法成功，返回，则为 S_OK。  
  
## <a name="requirements"></a>要求  
 需要 alink.h。  
  
## <a name="see-also"></a>请参阅

- [GetPEKind 方法](../../../../docs/framework/unmanaged-api/metadata/imetadataimport2-getpekind-method.md)
- [IALink2 接口](../../../../docs/framework/unmanaged-api/alink/ialink2-interface.md)
- [IALink 接口](../../../../docs/framework/unmanaged-api/alink/ialink-interface.md)
- [ALink API](../../../../docs/framework/unmanaged-api/alink/index.md)
