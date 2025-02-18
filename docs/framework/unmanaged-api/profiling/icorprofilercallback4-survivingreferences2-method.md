---
title: ICorProfilerCallback4::SurvivingReferences2 方法
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback4.SurvivingReferences2
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback4::SurvivingReferences2
helpviewer_keywords:
- ICorProfilerCallback4::SurvivingReferences2 method [.NET Framework profiling]
- SurvivingReferences2 method, ICorProfilerCallback4 interface [.NET Framework profiling]
ms.assetid: 02b51888-5d89-4e50-a915-45b7e329aad9
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: beb260030914de211d227342e497daa3db287c9e
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/10/2019
ms.locfileid: "67758077"
---
# <a name="icorprofilercallback4survivingreferences2-method"></a>ICorProfilerCallback4::SurvivingReferences2 方法
将堆中对象的布局报告为非压缩垃圾回收的结果。 如果探查器实现会调用此方法[ICorProfilerCallback4](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback4-interface.md)接口。 此回调可替换[ICorProfilerCallback2::SurvivingReferences](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback2-survivingreferences-method.md)方法，因为它能报告更大范围的长度超过 ULONG 中可表达的对象。  
  
## <a name="syntax"></a>语法  
  
```cpp  
HRESULT SurvivingReferences2(  
    [in] ULONG  cSurvivingObjectIDRanges,  
    [in, size_is(cSurvivingObjectIDRanges)] ObjectID  
                objectIDRangeStart[] ,  
    [in, size_is(cSurvivingObjectIDRanges)] SIZE_T  
                cObjectIDRangeLength[] );  
```  
  
## <a name="parameters"></a>参数  
 `cSurvivingObjectIDRanges`  
 [in] 作为非压缩垃圾回收的结果而仍存在的连续对象块的数量。 即，`cSurvivingObjectIDRanges` 的值是 `objectIDRangeStart` 和 `cObjectIDRangeLength` 数组的大小，分别存储每个对象块的 `ObjectID` 和长度。  
  
 `SurvivingReferences2` 接来下的两个参数为并行数组。 即，`objectIDRangeStart` 和 `cObjectIDRangeLength` 涉及同一连续对象块。  
  
 `objectIDRangeStart`  
 [in] `ObjectID` 值的数组，其中每个值均为内存中连续活动对象块的起始地址。  
  
 `cObjectIDRangeLength`  
 [in] 整数数组，其中每个整数均为内存中保留下来的连续对象块的大小。  
  
           `objectIDRangeStart` 数组中引用的每个块均指定了大小。  
  
## <a name="remarks"></a>备注  
 应按以下方式解释 `objectIDRangeStart` 和 `cObjectIDRangeLength` 数组的元素，以确定垃圾回收后对象是否仍存在。 假定 `ObjectID` 值 (`ObjectID`) 在以下范围内：  
  
 `ObjectIDRangeStart[i]` <= `ObjectID` < `ObjectIDRangeStart[i]` + `cObjectIDRangeLength[i]`  
  
 对于以下范围内 `i` 的任何值，此对象在垃圾回收后仍存在：  
  
 0 <= `i` < `cSurvivingObjectIDRanges`  
  
 非压缩垃圾回收将回收“死”对象占用的内存，但不会压缩释放的空间。 由此，内存返回到堆中，但“活”对象不会移动。  
  
 公共语言运行时 (CLR) 调用 `SurvivingReferences2` 进行非压缩垃圾回收。 对于压缩垃圾回收， [MovedReferences2](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback4-movedreferences2-method.md)改为调用。 单个垃圾回收可针对一个生成进行压缩，而针对另一个生成不进行压缩。 对于任何特定代的垃圾回收，探查器会收到任何`SurvivingReferences2`回调或[MovedReferences2](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback4-movedreferences2-method.md)回调，但不可同时使用两者。  
  
 由于内部缓冲有限、服务器垃圾回收期间的多个回调以及其他原因，在特定的垃圾回收过程中，可能收到多个 `SurvivingReferences2` 回调。 如果在垃圾回收期间收到多个回调，则信息是累积的；所有 `SurvivingReferences2` 回调中报告的任何引用都将在垃圾回收后仍然存在。  
  
 如果探查器同时实现[ICorProfilerCallback](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-interface.md)并[ICorProfilerCallback4](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback4-interface.md)接口，`SurvivingReferences2`方法之前调用[ICorProfilerCallback2::SurvivingReferences](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback2-survivingreferences-method.md)方法，但仅当`SurvivingReferences2`成功返回。 探查器可以返回一个 HRESULT，指示由 `SurvivingReferences2` 方法引发的故障，以避免调用第二种方法。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** CorProf.idl, CorProf.h  
  
 **库：** CorGuids.lib  
  
 **.NET Framework 版本：** [!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>请参阅

- [ICorProfilerCallback 接口](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-interface.md)
- [ICorProfilerCallback2 接口](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback2-interface.md)
- [ICorProfilerCallback4 接口](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback4-interface.md)
