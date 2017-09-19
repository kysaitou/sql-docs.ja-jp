---
title: "sqlsrv_get_config |Microsoft ドキュメント"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- sqlsrv_get_config
apitype: NA
helpviewer_keywords:
- API Reference, sqlsrv_get_config
- sqlsrv_get_config
ms.assetid: ce2befc2-af98-45bb-8d41-60f1674dccfc
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a5712c6f98da82b422e76a7cb6c8d07adac86b5e
ms.contentlocale: ja-jp
ms.lasthandoff: 09/09/2017

---
# <a name="sqlsrvgetconfig"></a>sqlsrv_get_config
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

指定された構成設定の現在の値を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
sqlsrv_get_config( string $setting )  
```  
  
#### <a name="parameters"></a>パラメーター  
*$setting*: 値を返す構成設定。 構成可能な設定の一覧については、「 [sqlsrv_configure](../../connect/php/sqlsrv-configure.md)」を参照してください。  
  
## <a name="return-value"></a>戻り値  
*$setting* パラメーターで指定された設定の値。 無効な設定を指定した場合は、 **false** が返されて、エラーがエラー コレクションに追加されます。  
  
## <a name="remarks"></a>解説  
場合**false**によって返される**sqlsrv_get_config**、呼び出す必要があります[sqlsrv_errors](../../connect/php/sqlsrv-errors.md)エラーが発生した場合、または場合を決定する**false**は、指定された設定の値、 *$setting*パラメーター。  
  
## <a name="see-also"></a>参照  
[SQLSRV ドライバー API リファレンス](../../connect/php/sqlsrv-driver-api-reference.md)  
[sqlsrv_configure](../../connect/php/sqlsrv-configure.md)  
[sqlsrv_errors](../../connect/php/sqlsrv-errors.md)  
  
