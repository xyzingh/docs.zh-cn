---
title: COR_ARRAY_LAYOUT 结构
ms.date: 03/30/2017
api_name:
- COR_ARRAY_LAYOUT
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- COR_ARRAY_LAYOUT
helpviewer_keywords:
- COR_DEBUG_IL_TO_NATIVE_MAP structure [.NET Framework debugging]
ms.assetid: aa20ac3d-6f60-4aa2-91c5-f3a86f82eba8
topic_type:
- apiref
ms.openlocfilehash: ca2d00611a7530dfb0d1c2a27123947bdf69820d
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/12/2020
ms.locfileid: "79179341"
---
# <a name="cor_array_layout-structure"></a>COR_ARRAY_LAYOUT 结构
提供有关内存中数组对象的布局的信息。  
  
## <a name="syntax"></a>语法  
  
```cpp  
typedef struct COR_ARRAY_LAYOUT {  
    COR_TYPEID componentID;  
    CorElementType componentType;  
    ULONG32 firstElementOffset;  
    ULONG32 elementSize;  
    ULONG32 countOffset;
    ULONG32 rankSize;
    ULONG32 numRanks;
    ULONG32 rankOffset;
} COR_ARRAY_LAYOUT;  
```  
  
## <a name="members"></a>成员  
  
|成员|说明|  
|------------|-----------------|  
|`componentID`|数组包含的对象类型的标识符。|  
|`componentType`|CorElementType 枚举值，用于指示组件是垃圾回收引用、值类还是基元。|  
|`firstElementOffset`|数组中第一个元素的偏移量。|  
|`elementSize`|每个元素的大小。|  
|`countOffset`|数组中元素数的偏移量。|  
|`rankSize`|排名的大小（以字节为单位）。|  
|`numRanks`|数组中的排名数。|  
|`rankOffset`|排名开始的偏移量。|  
  
## <a name="remarks"></a>备注  
 该`rankSize`字段指定多维数组中排名的大小。 对于单维数组来说，它也是准确的。  
  
 对于单维`numRanks`数组和`N`多维`N`维度数组，值为 1。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统要求](../../get-started/system-requirements.md)。  
  
 **标头**：CorDebug.idl、CorDebug.h  
  
 **库：** CorGuids.lib  
  
 **.NET 框架版本：**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>另请参阅

- [调试结构](debugging-structures.md)
- [调试](index.md)
