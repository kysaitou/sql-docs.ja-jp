---
title: "allTablesAreSelectable メソッド (SQLServerDatabaseMetaData) |Microsoft ドキュメント"
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
- SQLServerDatabaseMetaData.allTablesAreSelectable
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: eb340450-45a7-49c8-84bc-1b9dd5ee842f
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6d605d9c9725c5819af595115292e1cc3752ec0c
ms.contentlocale: ja-jp
ms.lasthandoff: 09/09/2017

---
# <a name="alltablesareselectable-method-sqlserverdatabasemetadata"></a>allTablesAreSelectable メソッド (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  現在のユーザーがによって返されるすべてのテーブルを使用するアクセス許可を持っているかどうかを取得、 [getTables](../../../connect/jdbc/reference/gettables-method-sqlserverdatabasemetadata.md) SELECT ステートメント内のメソッドです。  
  
## <a name="syntax"></a>構文  
  
```  
  
public boolean allTablesAreSelectable()  
```  
  
## <a name="return-value"></a>戻り値  
 **true**ユーザーを呼び出すアクセス許可を持っている場合は、すべてのテーブルを使用します。 それ以外の場合は、 **false**です。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 この allTablesAreSelectable メソッドは、java.sql.DatabaseMetaData インターフェイスの allTablesAreSelectable メソッドによって指定されます。  
  
## <a name="see-also"></a>参照  
 [SQLServerDatabaseMetaData のメソッド](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData のメンバー](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData クラス](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  