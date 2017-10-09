---
title: aaaInstall Visual Studio como SSDT para almacenamiento de datos SQL | Documentos de Microsoft
description: "Instalación de herramientas de desarrollo de Visual Studio y SQL Server Data Tools (SSDT) para Almacenamiento de datos SQL de Azure"
services: sql-data-warehouse
documentationcenter: NA
author: antvgski
manager: jhubbard
editor: 
ms.assetid: 0ed9b406-9b42-4fe6-b963-fe0a5b48aac1
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: connect
ms.date: 03/30/2017
ms.author: anvang;barbkess
ms.openlocfilehash: cf49c13d5cab598ed127f5702c04168b62ede0dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="install-visual-studio-and-ssdt-for-sql-data-warehouse"></a>Instalación de Visual Studio y SSDT para SQL Data Warehouse
aplicaciones de toodevelop para almacenamiento de datos de SQL, se recomienda usar versión más reciente de Hola de Visual Studio con la versión más reciente de Hola de SQL Server Data Tools (SSDT).  También se admite Visual Studio 2013 Update 5 con SSDT por compatibilidad con versiones anteriores.  

Con Visual Studio con SSDT, podrá toouse Hola Explorador de objetos de SQL Server toovisually explorar las tablas, vistas, procedimientos almacenados y muchos más objetos en el almacenamiento de datos de SQL, así como ejecutar consultas.

> [!NOTE]
> Almacenamiento de datos SQL no es compatible aún con proyectos de base de datos de Visual Studio.  Esta característica se agregará en una versión futura.
> 
> 

## <a name="step-1-install-visual-studio"></a>Paso 1: Instalación de Visual Studio
Siga estos toodownload vínculos e instalar Visual Studio. Si ya tiene Visual Studio 2013 o posterior instalado, puede omitir tooStep 2, instale SSDT.

1. [Descargue Visual Studio][].
2. Siga hello [instalar Visual Studio] [ Installing Visual Studio] guía en MSDN y elija las configuraciones predeterminadas de Hola.

## <a name="step-2-install-ssdt"></a>Paso 2: Instalación de SSDT
tooinstall SSDT para Visual Studio simplemente busque una actualización SSDT desde dentro de Visual Studio, siga estos pasos.

1. En Visual Studio, haga clic en **Herramientas** / **Extensiones y actualizaciones...** / **Actualizaciones**
2. Seleccione **Actualizaciones de productos** y busque la actualización **Microsoft SQL Server Update para herramientas de base de datos**.

Si no se encuentra una actualización, debe tener instalado de versión más reciente de Hola.  tooconfirm SSDT está instalado, haga clic en **ayuda** / **acerca de Microsoft Visual Studio** y buscar las herramientas de datos de SQL Server en la lista de Hola.  versión más reciente de Hola de SSDT es 14.0.60525.0.  Si Hola opción tooinstall no está disponible en Visual Studio, o bien, puede visitar hello [de descarga de SSDT] [ SSDT Download] página toodownload e instale SSDT manualmente.

## <a name="next-steps"></a>Pasos siguientes
Ahora que tiene la versión más reciente de Hola de SSDT, está listo demasiado[conectar] [ connect] tooyour almacenamiento de datos SQL.

<!--Anchors-->

<!--Image references-->

<!--Articles-->
[connect]: ./sql-data-warehouse-query-visual-studio.md

<!--Other-->
[Descargue Visual Studio]: https://www.visualstudio.com/downloads/
[Installing Visual Studio]: https://msdn.microsoft.com/library/e2h7fzkw.aspx
[SSDT Download]: https://msdn.microsoft.com/library/mt204009.aspx
