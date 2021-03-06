---
title: 記述子フィールドの設定 |Microsoft ドキュメント
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], retrieving or setting field values
ms.assetid: d735dc64-370f-48ab-a59f-6cef9bc4e1e8
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c67bb653f1dd87aea52d613b427f5bcb6e66f821
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
ms.locfileid: "32912007"
---
# <a name="setting-descriptor-fields"></a>記述子フィールドの設定
記述子のフィールドを変更するには、アプリケーションが呼び出すことができます**SQLSetDescField**です。 いくつかのフィールドは読み取り専用と、設定することはできません。 (を参照してください、 [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)関数の説明です)。  
  
 レコード番号を持つ記述子レコードのフィールドが設定されます (*RecNumber*) 1 以上の while の記述子のヘッダー フィールドが 0 のレコード数が設定されます。 0 のレコード数は、列 0 にブックマークが含まれている規則に従って、ブックマークのフィールドを設定にも使用されます。 記述子のヘッダー内のブックマークのフィールドが含まれているが、そうではない印象のままにこの可能性があります。 ブックマークのフィールドは、ヘッダー フィールドとは異なります。  
  
 アプリケーションで定義されている順序に従う必要がありますフィールドを個別に設定するときに[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)です。 一部のフィールドを設定すると、その他のフィールドを設定するドライバーとします。 これにより記述子が常に、アプリケーションのデータ型が指定した後で使用する準備がされます。 SQL_DESC_TYPE フィールドの設定、アプリケーション、ドライバーはその他の種類を指定するフィールドが有効で一貫性のあることを確認します。  
  
 記述子フィールドを設定する関数呼び出しが失敗した場合、記述子フィールドの内容が、失敗した関数を呼び出した後定義できません。
