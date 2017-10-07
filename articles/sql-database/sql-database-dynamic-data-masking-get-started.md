---
title: "enmascaramiento dinámico de datos de base de datos SQL de aaaAzure | Documentos de Microsoft"
description: "Enmascaramiento de datos dinámicos de la base de datos SQL limita la exposición de información confidencial ocultándola a los usuarios privilegios toonon"
services: sql-database
documentationcenter: 
author: ronitr
manager: jhubbard
editor: 
ms.assetid: 4b36d78e-7749-4f26-9774-eed1120a9182
ms.service: sql-database
ms.custom: security
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 03/09/2017
ms.author: ronitr; ronmat
ms.openlocfilehash: 68b55128dc096f7e3dd0e5ed1427b39da5d64736
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="sql-database-dynamic-data-masking"></a>Enmascaramiento dinámico de datos de SQL Database

Enmascaramiento de datos dinámicos de la base de datos SQL limita la exposición de información confidencial ocultándola a los usuarios privilegios toonon. 

Enmascaramiento dinámico de datos ayuda a evitar datos toosensitive de acceso no autorizado al habilitar clientes toodesignate cuánto Hola confidencial tooreveal con un impacto mínimo en el nivel de aplicación Hola. Es una característica de seguridad basada en directivas que oculta los datos confidenciales Hola Hola conjunto de resultados de una consulta de campos de la base de datos designada, Hola datos en la base de datos de hello no cambian.

Por ejemplo, un representante del servicio en un centro de llamadas puede identificar a los llamadores mediante varios dígitos de su número de tarjeta de crédito, pero esos elementos no deben estar completamente los datos expuestos a toohello representante del servicio. Puede definir una regla de enmascaramiento que enmascare todos excepto Hola los últimos cuatro dígitos de cualquier número de tarjeta de crédito en el conjunto de resultados de Hola de cualquier consulta. Como otro ejemplo, una máscara de datos apropiados puede ser datos de información personal identificable (PII) de tooprotect definido, por lo que un desarrollador puede realizar consultas en entornos de producción para resolver problemas sin infringir las normativas de cumplimiento.

## <a name="sql-database-dynamic-data-masking-basics"></a>Conceptos básicos del enmascaramiento dinámico de datos de SQL Database
Configurar una directiva de Hola de enmascaramiento de datos dinámicos portal de Azure mediante la selección de la operación en la hoja de configuración de base de datos SQL o una hoja de configuración de enmascaramiento de datos dinámicos de Hola.

### <a name="dynamic-data-masking-permissions"></a>Permisos de enmascaramiento de datos dinámicos
Enmascaramiento dinámico de datos puede configurarse Hola, Administrador de base de datos de Azure, el Administrador de servidor o roles de seguridad responsable de seguridad.

### <a name="dynamic-data-masking-policy"></a>Directiva de enmascaramiento de datos dinámicos
* **Los usuarios SQL excluidos del enmascaramiento** : conjunto de usuarios SQL o resultados de la consulta de las identidades AAD que obtienen datos sin enmascarar Hola SQL. Los usuarios con privilegios de administrador siempre quedan excluidos del enmascaramiento y vean Hola de datos original sin ninguna máscara.
* **Reglas de enmascaramiento** -un conjunto de reglas que definen Hola designado toobe campos enmascarada y Hola función que se usa de enmascaramiento. Hola designado campos puede definirse mediante un nombre de esquema de base de datos, el nombre de la tabla y el nombre de columna.
* **Funciones de enmascaramiento** -un conjunto de métodos que controlan la exposición de Hola de datos para diferentes escenarios.

| Función de enmascaramiento | Lógica de enmascaramiento |
| --- | --- |
| **Valor predeterminado** |**Completa el enmascaramiento de datos correspondiente de toohello tipos de hello describen campos**<br/><br/>• Use XXXX o número menor de x si el tamaño de Hola de campo de hello es inferior a 4 caracteres para los tipos de datos de cadena (nchar, ntext, nvarchar).<br/>• Use un valor de cero para los tipos de datos numéricos (bigint, bit, decimal, int, money, numeric, smallint, smallmoney, tinyint, float, real).<br/>• Use 01-01-1900 para los tipos de datos de fecha y hora (date, datetime2, datetime, datetimeoffset, smalldatetime, time).<br/>• Para SQL variant, Hola valor del tipo actual Hola se utiliza.<br/>• Para de documento XML hello <masked/> se utiliza.<br/>• Use un valor vacío para los tipos de datos especiales (tipos timestamp table, hierarchyid, GUID, binary, image, varbinary spatial). |
| **Tarjeta de crédito** |**Método de enmascaramiento, que expone Hola los últimos cuatro dígitos de hello designado campos** y agrega una cadena constante como un prefijo en forma de Hola de una tarjeta de crédito.<br/><br/>XXXX-XXXX-XXXX-1234 |
| **Correo electrónico** |**Método de enmascaramiento, que expone la primera letra de Hola y reemplaza el dominio Hola con XXX.com** utilizando un prefijo de cadena constante en forma de Hola de una dirección de correo electrónico.<br/><br/>aXX@XXXX.com |
| **Número aleatorio** |**Método de enmascaramiento, que genera un número aleatorio** según toohello seleccionado los límites y los tipos de datos reales. Si Hola designado límites es igual, función de enmascaramiento de hello es un número constante.<br/><br/>![Panel de navegación](./media/sql-database-dynamic-data-masking-get-started/1_DDM_Random_number.png) |
| **Texto personalizado** |**Método, que expone Hola primeros y últimos caracteres de enmascaramiento** y agrega una cadena de relleno personalizada en medio de Hola. Si cadena original hello es menor que sufijo y prefijo de hello expuesto, se usa solo Hola cadena de relleno. <br/>prefijo[relleno]sufijo<br/><br/>![Panel de navegación](./media/sql-database-dynamic-data-masking-get-started/2_DDM_Custom_text.png) |

<a name="Anchor1"></a>

### <a name="recommended-fields-toomask"></a>Campos recomendados toomask
Hello motor de recomendaciones de DDM, marcas de algunos de los campos de la base de datos como campos potencialmente confidenciales, que pueden ser buenas candidatas para la máscara. En la hoja de enmascaramiento de datos dinámicos de hello en el portal de hello, verá Hola recomienda las columnas de la base de datos. Todo lo que necesita toodo es hacer clic en **agregar máscara** para una o varias columnas y, a continuación, **guardar** tooapply una máscara para estos campos.

## <a name="set-up-dynamic-data-masking-for-your-database-using-powershell-cmdlets"></a>Configuración del enmascaramiento de datos dinámicos para la base de datos mediante cmdlets de PowerShell
Consulte [Cmdlets de Base de datos SQL de Azure](https://msdn.microsoft.com/library/azure/mt574084.aspx).

## <a name="set-up-dynamic-data-masking-for-your-database-using-rest-api"></a>Configuración del enmascaramiento de datos dinámicos para la base de datos mediante la API de REST
Consulte [Operaciones para Bases de datos SQL de Azure](https://msdn.microsoft.com/library/dn505719.aspx).

