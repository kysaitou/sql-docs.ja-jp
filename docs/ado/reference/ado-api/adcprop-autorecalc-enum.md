---
title: ADCPROP_AUTORECALC_ENUM |Microsoft ドキュメント
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADCPROP_AUTORECALC_ENUM
helpviewer_keywords:
- ADCPROP_AUTORECALC_ENUM [ADO]
ms.assetid: ded4f087-87b9-4efa-8026-bde53d3e9e8a
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e7594e31bc4ffbf20b9c7a9cbd9dc65bfe279a76
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
---
# <a name="adcpropautorecalcenum"></a>ADCPROP_AUTORECALC_ENUM
タイミングを指定します、 [MSDataShape](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)プロバイダーが階層のレコード セットの集計と計算列を再計算します。  
  
 これらの定数のみ使用されます、 **MSDataShape**プロバイダーと**Recordset** "**自動再計算**"動的なプロパティで参照されている、 [ADOプロパティの動的インデックス](../../../ado/reference/ado-api/ado-dynamic-property-index.md)で文書化されていると、 [OLE DB 用の Microsoft カーソル サービス](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md)または[Microsoft Data Shaping Service for OLE DB](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)ドキュメント。  
  
|定数|値|Description|  
|--------------|-----------|-----------------|  
|**adRecalcAlways**|1|既定値です。 たびに再計算されます、 **MSDataShape**プロバイダーでは、計算列が依存する値が変更されたを決定します。|  
|**adRecalcUpFront**|0|最初に、階層を構築した場合にのみ**Recordset**です。|  
  
## <a name="adowfc-equivalent"></a>該当するショートカットは ADO/WFC  
 これらの定数には、対応する ADO/WFC はありません。
