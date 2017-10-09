---
title: "aaaPorts más allá de 1433 para la base de datos SQL | Documentos de Microsoft"
description: "Conexiones de cliente de ADO.NET tooAzure base de datos SQL a veces omiten el proxy de Hola e interactúan directamente con la base de datos de Hola. Los puertos que no sean 1433 se convierten en puertos importantes."
services: sql-database
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: 
ms.assetid: 3f17106a-92fd-4aa4-b6a9-1daa29421f64
ms.service: sql-database
ms.custom: develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2016
ms.author: sstein
ms.openlocfilehash: a35ff2d827ae3fa29b3ea855dbb7ed78583c82eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="ports-beyond-1433-for-adonet-45"></a>Puertos más allá de 1433 para ADO.NET 4.5
Este tema describe el comportamiento de conexión de base de datos de SQL Azure de Hola para los clientes que utilizan ADO.NET 4.5 o una versión posterior. 

> [!IMPORTANT]
> Para obtener información acerca de la arquitectura de conectividad, consulte [Arquitectura de conectividad de Azure SQL Database](sql-database-connectivity-architecture.md).
>

## <a name="outside-vs-inside"></a>Fuera o dentro
Para las conexiones tooAzure base de datos SQL, debemos primero pedimos si se ejecuta el programa cliente *fuera* o *dentro de* límite de nube de Azure Hola. subsecciones de Hola describen dos escenarios comunes.

#### <a name="outside-client-runs-on-your-desktop-computer"></a>*Fuera:* el cliente se ejecuta en el equipo de escritorio
Puerto 1433 es Hola solo que deben estar abiertos en el equipo de escritorio que hospeda la aplicación de cliente de base de datos SQL.

#### <a name="inside-client-runs-on-azure"></a>*Dentro:* el cliente se ejecuta en Azure
Cuando el cliente se ejecuta dentro del límite de la nube de Azure de hello, usa lo que podemos llamar un *ruta directa* toointeract con el servidor de base de datos SQL de Hola. Una vez establecida una conexión, las interacciones entre el cliente de Hola y de base de datos no implican a ningún proxy de middleware.

secuencia de Hello es como sigue:

1. ADO.NET 4.5 (o posterior) inicia una interacción breve con hello nube de Azure y recibe un número de puerto identificada de forma dinámica.
   
   * número de puerto de Hello identificada de manera dinámica esté entre Hola 11000 a 11999 o 14000 a 14999.
2. ADO.NET, a continuación, se conecta toohello servidor de base de datos SQL directamente, con ningún middleware en medio.
3. Las consultas se envían directamente toohello base de datos y los resultados se devuelven directamente toohello cliente.

Asegúrese de que el puerto Hola intervalos de 11000 a 11999 y 14000 a 14999 en el equipo cliente de Azure quedan disponibles para las interacciones de cliente de ADO.NET 4.5 con base de datos de SQL.

* En concreto, los puertos Hola intervalo deben permanecer sin bloqueadores de otros elementos de salida.
* En la VM de Azure, Hola **Firewall de Windows con seguridad avanzada** controles Hola configuración del puerto.
  
  * Puede usar hello [interfaz de usuario del servidor de seguridad](http://msdn.microsoft.com/library/cc646023.aspx) tooadd una regla para la que se especifique hello **TCP** como protocolo junto con un intervalo de puertos con la sintaxis de hello **11000 a 11999**.

## <a name="version-clarifications"></a>Aclaraciones de versiones
En esta sección se aclara los monikers de Hola que hacen referencia a las versiones de tooproduct. También se muestran algunos emparejamientos de versiones entre productos.

#### <a name="adonet"></a>ADO.NET
* ADO.NET 4.0 es compatible con el protocolo de hello TDS 7.3, pero no 7.4.
* ADO.NET 4.5 y posterior admite protocolo de hello TDS 7.4.

## <a name="related-links"></a>Vínculos relacionados
* ADO.NET 4.6 se publicó el 20 de julio de 2015. Hay un anuncio del blog del equipo de .NET de hello [aquí](http://blogs.msdn.com/b/dotnet/archive/2015/07/20/announcing-net-framework-4-6.aspx).
* ADO.NET 4.5 se publicó el 15 de julio de 2012. Hay un anuncio del blog del equipo de .NET de hello [aquí](http://blogs.msdn.com/b/dotnet/archive/2012/08/15/announcing-the-release-of-net-framework-4-5-rtm-product-and-source-code.aspx).
  
  * Hay una entrada de blog sobre ADO.NET 4.5.1 disponible [aquí](http://blogs.msdn.com/b/dotnet/archive/2013/06/26/announcing-the-net-framework-4-5-1-preview.aspx).
* [Lista de versiones del protocolo TDS](http://www.freetds.org/userguide/tdshistory.htm)
* [Información general de desarrollo de Base de datos SQL](sql-database-develop-overview.md)
* [Firewall de Base de datos SQL de Azure](sql-database-firewall-configure.md)
* [Configuración del firewall en Base de datos SQL](sql-database-configure-firewall-settings.md)

