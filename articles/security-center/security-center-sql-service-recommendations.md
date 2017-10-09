---
title: aaaProtecting SQL Azure servicio y los datos en el centro de seguridad de Azure | Documentos de Microsoft
description: "En este documento se explica cómo las recomendaciones de Azure Security Center ayudan a proteger el servicio SQL de Azure y los datos y a cumplir las directivas de seguridad."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: bcae6987-05d0-4208-bca8-6a6ce7c9a1e3
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/03/2017
ms.author: terrylan
ms.openlocfilehash: 75d782d3c2418f9645139e4cd6ecb7765c488f91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="protecting-azure-sql-service-and-data-in-azure-security-center"></a>Protección del servicio SQL de Azure en Azure Security Center
Centro de seguridad de Azure analiza el estado de seguridad de Hola de los recursos de Azure. Cuando el centro de seguridad identifica posibles vulnerabilidades de seguridad, crea las recomendaciones que le guiarán a lo largo de proceso de Hola de configuración de controles de Hola que sea necesitado.  Las recomendaciones aplican tipos de recursos de tooAzure: máquinas virtuales (VM), redes, aplicaciones y datos y SQL.

Este artículo tratan las recomendaciones que se aplican los datos y el servicio SQL de tooAzure. Las recomendaciones se centran en la habilitación de la auditoría de servidores y bases de datos de SQL de Azure, el cifrado de bases de datos SQL Database y la habilitación del cifrado de su cuenta de Azure Storage.  Uso de tabla de Hola a continuación como un toohelp de referencia comprende recomendaciones de SQL disponibles servicio y los datos de Hola y lo que hace cada uno de ellos si se aplica.

## <a name="available-sql-service-and-data-recommendations"></a>Recomendaciones de datos y servicio SQL disponibles
| Recomendación | Descripción |
| --- | --- |
| [Habilitar la auditoría y la detección de amenazas en los servidores SQL Server](security-center-enable-auditing-on-sql-servers.md) |Recomienda activar la auditoría y la detección de amenazas para los servidores de Azure SQL (solo en el servicio Azure SQL; no incluye la instancia SQL que se ejecuta en sus máquinas virtuales). |
| [Habilitación de la auditoría y la detección de amenazas en bases de datos SQL](security-center-enable-auditing-on-sql-databases.md) |Recomienda activar la auditoría y la detección de amenazas para las bases de datos de Azure SQL (solo en el servicio Azure SQL; no incluye la instancia SQL que se ejecuta en sus máquinas virtuales). |
| [Habilitar Cifrado de datos transparente en bases de datos SQL](security-center-enable-transparent-data-encryption.md) |Recomienda habilitar el cifrado de bases de datos SQL (solo el servicio SQL de Azure). |

## <a name="see-also"></a>Otras referencias
toolearn más información acerca de las recomendaciones que se aplican tooother tipos de recursos de Azure, vea Hola recursos siguientes:

* [Protección de las máquinas virtuales en Azure Security Center](security-center-virtual-machine-recommendations.md)
* [Protección de las aplicaciones en Azure Security Center](security-center-application-recommendations.md)
* [Protección de las redes en Azure Security Center](security-center-network-recommendations.md)

toolearn más información acerca del centro de seguridad, vea Hola recursos siguientes:

* [Configuración de directivas de seguridad de Azure Security Center](security-center-policies.md) : Obtenga información acerca de cómo tooconfigure las directivas de seguridad para los grupos de recursos y las suscripciones de Azure.
* [Toosecurity de administración y de que responda las alertas en el centro de seguridad de Azure](security-center-managing-and-responding-alerts.md) : Obtenga información acerca de cómo las alertas de toosecurity toomanage y que responden.
* [Preguntas más frecuentes de Azure Security Center](security-center-faq.md) --buscar preguntas más frecuentes sobre el uso de servicio de Hola.
