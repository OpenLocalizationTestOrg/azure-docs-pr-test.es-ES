---
title: bibliotecas de aaaClient necesarias para conectar tooAzure Analysis Services | Documentos de Microsoft
description: Describe las bibliotecas de cliente necesarias para las aplicaciones y herramientas de cliente, tooconnect Azure Analysis Services
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 74ba5c05ba76c6587c5aed38f200a1ba469aa4f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="client-libraries-for-connecting-tooazure-analysis-services"></a>Bibliotecas de cliente para conectar tooAzure Analysis Services

Bibliotecas de cliente son necesarias para las aplicaciones cliente y servidores de servicios de herramientas tooconnect tooAnalysis. 

Analysis Services usa tres bibliotecas de cliente. ADOMD.NET y los objetos de administración de Analysis Services (AMO), son bibliotecas de cliente administradas. proveedor de OLE DB de Analysis Services de Hello (MSOLAP DLL) es una biblioteca de cliente nativo. Normalmente, las tres se instalan en hello mismo tiempo. Azure Analysis Services requiere que las versiones más recientes de Hola. 

Las aplicaciones cliente de Microsoft, como Power BI Desktop y Excel, instalan las tres bibliotecas de cliente. Sin embargo, dependiendo de la versión de Hola o la frecuencia de las actualizaciones, las bibliotecas de cliente no pueden ser versiones más recientes de hello requeridas por los servicios de análisis de Azure. Hello mismo aplica toocustom aplicaciones u otras interfaces, como AsCmd, TOM, ADOMD.NET. Estas aplicaciones requieren la instalación manual de las bibliotecas de Hola. bibliotecas de cliente de Hello para la instalación manual se incluyen en los paquetes de características de SQL Server como paquetes de distribución. Sin embargo, estas bibliotecas de cliente son de la versión de SQL Server toohello relacionados y no pueden ser hello más reciente.  

Bibliotecas de cliente para conexiones de cliente son diferentes de tooconnect necesaria de proveedores de datos de un origen de datos de Azure Analysis Services server tooa. toolearn más información acerca de las conexiones de origen de datos, vea [las conexiones de origen de datos](analysis-services-datasource.md).

## <a name="download-hello-latest-client-libraries"></a>Descargar las bibliotecas de cliente más recientes de Hola  
Usar hello siguiendo las bibliotecas de cliente si se encuentra en un entorno de producción y necesita las versiones de lanzamiento y soporte completos.

[MSOLAP (amd64)](https://go.microsoft.com/fwlink/?linkid=829576)</br>
[MSOLAP (x86)](https://go.microsoft.com/fwlink/?linkid=829575)</br>
[AMO](https://go.microsoft.com/fwlink/?linkid=829578)</br>
[ADOMD](https://go.microsoft.com/fwlink/?linkid=829577)</br>

## <a name="next-steps"></a>Pasos siguientes
[Connect with Excel](analysis-services-connect-excel.md)   (Conexión con Excel)  
[Conexión con Power BI](analysis-services-connect-pbi.md)
