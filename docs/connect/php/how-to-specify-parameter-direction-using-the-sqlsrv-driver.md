---
title: '方法: SQLSRV ドライバーを使用してパラメーターの方向を指定 |Microsoft ドキュメント'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- stored procedure support
ms.assetid: 1209eeca-df75-4283-96dc-714f39956b95
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 048b2961d933787cbdd35a95f676e602c37ee9f9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
---
# <a name="how-to-specify-parameter-direction-using-the-sqlsrv-driver"></a>方法: SQLSRV ドライバーを使用してパラメーターの方向を指定する
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

このトピックでは、ストアド プロシージャを呼び出す際に、SQLSRV ドライバーを使用して、パラメーターの方向を指定する方法について説明します。 パラメーターの方向に渡されるパラメーター配列 (手順 3) を構築する場合は、指定された[sqlsrv_query](../../connect/php/sqlsrv-query.md)または[sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md)です。  
  
### <a name="to-specify-parameter-direction"></a>パラメーターの方向を指定するには  
  
1.  ストアド プロシージャを呼び出す TRANSACT-SQL クエリを定義します。 ストアド プロシージャに渡されるパラメーターの代わりに疑問符 (?) を使用します。 たとえば、この文字列は、2 つのパラメーターを受け付けるストアド プロシージャ (UpdateVacationHours) を呼び出します。  
  
    ```  
    $tsql = "{call UpdateVacationHours(?, ?)}";  
    ```  
  
    > [!NOTE]  
    > 正規の構文を使用してストアド プロシージャを呼び出すことをお勧めします。 正規の構文の詳細については、次を参照してください。[ストアド プロシージャの呼び出し](../../relational-databases/native-client-odbc-stored-procedures/calling-a-stored-procedure.md)です。  
  
2.  Transact-SQL クエリ内のプレースホルダーに対応する PHP 変数を初期化または更新します。 たとえば、次のコードは、UpdateVacationHours ストアド プロシージャの 2 つのパラメーターを初期化します。  
  
    ```  
    $employeeId = 101;  
    $usedVacationHours = 8;  
    ```  
  
    > [!NOTE]  
    > **null**、 **DateTime**、またはストリーム型に初期化または更新される変数は出力パラメーターとして使用できません。  
  
3.  手順 2 からの PHP 変数を使用して、Transact-SQL 文字列内のパラメーター プレースホルダーに順番に対応するパラメーター値の配列を作成または更新します。 配列に各パラメーターの方向を指定します。 2 つの方法のいずれかで各パラメーターの方向が決定されます: 入力パラメーターの) (既定でまたはを使用して**sqlsrv_param _\*** 定数です。 出力および双方向のパラメーター)。 たとえば、次のコードは、入力パラメーターとして *$employeeId* パラメーターおよび双方向パラメーターとして *$usedVacationHours* パラメーターを指定しています。  
  
    ```  
    $params = array(  
                     array($employeeId, SQLSRV_PARAM_IN),  
                     array($usedVacationHours, SQLSRV_PARAM_INOUT)  
                    );  
    ```  
  
    一般に、パラメーターの方向を指定する構文を理解するため、 *$var1*、 *$var2*、および *$var3* はそれぞれ入力、出力、および双方向のパラメーターに対応するものとします。 パラメーターの方向は、次の方法のいずれかで指定できます。  
  
    -   暗黙的にパラメーターを指定、入力、出力パラメーターを明示的に指定して双方向のパラメーターを明示的に指定します。  
  
        ```  
        array(   
               array($var1),  
               array($var2, SQLSRV_PARAM_OUT),  
               array($var3, SQLSRV_PARAM_INOUT)  
               );  
        ```  
  
    -   入力パラメーターを明示的に指定、出力パラメーターを明示的に指定および双方向のパラメーターを明示的に指定します。  
  
        ```  
        array(   
               array($var1, SQLSRV_PARAM_IN),  
               array($var2, SQLSRV_PARAM_OUT),  
               array($var3, SQLSRV_PARAM_INOUT)  
               );  
        ```  
  
4.  クエリを実行[sqlsrv_query](../../connect/php/sqlsrv-query.md)または[sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md)と[sqlsrv_execute](../../connect/php/sqlsrv-execute.md)です。 たとえば、次のコードは接続 *$conn* を使用して、 *$params* に指定されたパラメーター値でクエリ *$tsql*を実行します。  
  
    ```  
    sqlsrv_query($conn, $tsql, $params);  
    ```  
  
## <a name="see-also"></a>参照  
[方法: SQLSRV ドライバーを使用して出力パラメーターを取得する](../../connect/php/how-to-retrieve-output-parameters-using-the-sqlsrv-driver.md)

[How to: Retrieve Input and Output Parameters Using the SQLSRV Driver](../../connect/php/how-to-retrieve-input-and-output-parameters-using-the-sqlsrv-driver.md)  
  
