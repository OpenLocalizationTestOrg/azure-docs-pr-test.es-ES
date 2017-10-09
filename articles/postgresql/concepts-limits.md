---
title: aaaLimitations en la base de datos de Azure para PostgreSQL | Documentos de Microsoft
description: Describe las limitaciones en Azure Database for PostgreSQL.
services: postgresql
author: kamathsun
ms.author: sukamat
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.topic: article
ms.date: 06/01/2017
ms.openlocfilehash: f53dd240e55e0633bc1dfb8ad25e1818fa8ae18c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="limitations-in-azure-database-for-postgresql"></a>Limitaciones en Azure Database for PostgreSQL
Hola base de datos de Azure para servicio PostgreSQL está en vista previa pública. Hello siguientes secciones describen los límites funcionales en el servicio de base de datos de Hola y capacidad.

## <a name="service-tier-maximums"></a>Máximos de nivel de servicio
Azure Database for PostgreSQL tiene varios niveles de servicio entre los que puede elegir al crear un servidor. Para obtener más información, consulte la [descripción sobre los elementos disponibles en cada nivel de servicio](concepts-service-tiers.md).  

Hay un número máximo de conexiones, unidades de proceso y almacenamiento en cada nivel de servicio durante la vista previa del servicio de hello, como se indica a continuación: 

|                            |                   |
| :------------------------- | :---------------- |
| **Conexiones máximas**        |                   |
| 50 unidades de proceso básicas     | 50 conexiones    |
| 100 unidades de proceso básicas    | 100 conexiones   |
| 100 unidades de proceso estándar | 200 conexiones   |
| 200 unidades de proceso estándar | 300 conexiones   |
| 400 unidades de proceso estándar | 400 conexiones   |
| 800 unidades de proceso estándar | 500 conexiones   |
| **Unidades de proceso máximas**      |                   |
| Nivel de servicio Básico         | 100 unidades de proceso |
| Nivel de servicio Estándar      | 800 unidades de proceso |
| **Almacenamiento máximo**            |                   |
| Nivel de servicio Básico         | 1 TB              |
| Nivel de servicio Estándar      | 1 TB              |

Cuando se alcanzan demasiadas conexiones, recibirá Hola siguiente error:
> FATAL:  sorry, too many clients already

## <a name="preview-functional-limitations"></a>Limitaciones funcionales de la versión preliminar
### <a name="scale-operations"></a>Operaciones de escalado
1.  El escalado dinámico de servidores entre niveles de servicio no se admite en este momento. Es decir, el cambio entre los niveles de servicio Básico y Estándar.
2.  El aumento dinámico bajo demanda del almacenamiento en un servidor creado previamente no se admite en este momento.
3.  La reducción del tamaño de almacenamiento del servidor no se admite.

### <a name="server-version-upgrades"></a>Actualizaciones de la versión de servidor
- La migración automatizada entre las principales versiones del motor de base de datos no se admite en este momento.

### <a name="subscription-management"></a>Administración de suscripciones
- El movimiento dinámico de servidores creados previamente entre grupo de suscripciones y recursos no se admite en este momento.

### <a name="point-in-time-restore"></a>Restauración a un momento dado
1.  No se admite la restauración de nivel de servicio de toodifferent o tamaño de unidades de proceso y almacenamiento.
2.  La restauración a un servidor que se ha quitado no se admite en este momento.

## <a name="next-steps"></a>Pasos siguientes
- Comprenda lo que [hay disponible en cada plan de tarifa](concepts-service-tiers.md).
- Conozca las [versiones de base de datos de PostgreSQL admitidas](concepts-supported-versions.md).
- Revisión [cómo tooBack seguridad y restauración de un servidor de base de datos de Azure para usar PostgreSQL Hola portal de Azure](howto-restore-server-portal.md)
