---
title: raceOnRCWCleanup MDA
ms.date: 03/30/2017
helpviewer_keywords:
- RCW
- managed debugging assistants (MDAs), RCWs
- race on RCW cleanup
- MDAs (managed debugging assistants), RCWs
- RaceOnRCWCleanup MDA
- runtime callable wrappers
ms.assetid: bee1e9b1-50a8-4c89-9cd9-7dd6b2458187
author: mairaw
ms.author: mairaw
ms.openlocfilehash: e6400986d58fcb5f11d06e371a1b58f5256f4c62
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/30/2019
ms.locfileid: "68629367"
---
# <a name="raceonrcwcleanup-mda"></a>raceOnRCWCleanup MDA
当使用命令（如 <xref:System.Runtime.InteropServices.Marshal.ReleaseComObject%2A?displayProperty=nameWithType> 方法）发出一个调用来发布[运行时可调用包装](../../../docs/standard/native-interop/runtime-callable-wrapper.md) (RCW) 时，如果公共语言运行时 (CLR) 检测到该包装正在使用中，则激活 `raceOnRCWCleanup` 托管调试助手 (MDA)。  
  
## <a name="symptoms"></a>症状  
 使用 <xref:System.Runtime.InteropServices.Marshal.ReleaseComObject%2A> 或类似方法释放 RCW 期间或之后发生访问冲突或内存损坏。  
  
## <a name="cause"></a>原因  
 正在另一个线程中或释放线程堆栈中使用 RCW。  无法释放使用中的 RCW。  
  
## <a name="resolution"></a>解决方法  
 不要释放在当前或在其他线程中可能使用的 RCW。  
  
## <a name="effect-on-the-runtime"></a>对运行时的影响  
 此 MDA 对 CLR 无任何影响。  
  
## <a name="output"></a>Output  
 描述错误的消息。  
  
## <a name="configuration"></a>配置  
  
```xml  
<mdaConfig>  
  <assistants>  
    <raceOnRCWCleanup/>  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="see-also"></a>请参阅

- <xref:System.Runtime.InteropServices.MarshalAsAttribute>
- [使用托管调试助手诊断错误](../../../docs/framework/debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants.md)
- [互操作封送处理](../../../docs/framework/interop/interop-marshaling.md)
