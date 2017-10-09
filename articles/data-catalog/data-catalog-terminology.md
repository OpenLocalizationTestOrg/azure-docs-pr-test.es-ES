---
title: "terminología de catálogo de datos aaaAzure | Documentos de Microsoft"
description: "Este artículo proporciona una introducción tooconcepts y términos usados en la documentación del catálogo de datos de Azure."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 6fec74d9-4a3c-4b4b-88ba-cad5ad143331
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: b5f071db4f62c914d2c1cdef9aa686b18d5297d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-catalog-terminology"></a>Terminología del Catálogo de datos de Azure
## <a name="catalog"></a>Catálogo
Hola el catálogo de datos es un repositorio de metadatos basados en la nube de los datos que se pueden registrar orígenes y activos de datos. catálogo de Hello actúa como una ubicación de almacenamiento central para los metadatos estructurales extraídos de orígenes de datos y metadatos descriptivos agregadas por usuarios.

## <a name="data-source"></a>Origen de datos
Un origen de datos es un sistema o un contenedor que administra los recursos de datos. Como ejemplos se incluyen las bases de datos de SQL Server, de Oracle, de SQL Server Analysis Services (tabulares o multidimensionales) y servidores de SQL Server Reporting Services.

## <a name="data-asset"></a>Recurso de datos
Los activos de datos son objetos contenidos en orígenes de datos que se pueden registrar con el catálogo de Hola. Entre algunos ejemplos se incluyen tablas y vistas de SQL Server, tablas y vistas de Oracle, medidas de SQL Server Analysis Services, dimensiones y KPI e informes de SQL Server Reporting Services.

## <a name="data-asset-location"></a>Ubicación del recurso de datos
Hello catálogo almacena Hola ubicación de un origen de datos o recurso de datos, que puede ser usado tooconnect toohello mediante una aplicación cliente de origen. formato de Hola y detalles de ubicación de hello varían en función de tipo de origen de datos de Hola. Por ejemplo, una tabla de SQL Server puede identificarse mediante su nombre de cuatro partes (nombre del servidor, nombre de la base de datos, nombre del esquema y nombre de objeto), mientras que un informe de SQL Server Reporting Services se puede identificar mediante su dirección URL.

## <a name="structural-metadata"></a>Metadatos estructurales
Metadatos estructurales son metadatos de hello extraídos de un origen de datos que describe la estructura de Hola de un recurso de datos. Esto incluye la ubicación de activos de hello, su nombre de objeto y el tipo y las características específicas del tipo. Por ejemplo, hello metadatos estructurales de tablas y vistas incluyen nombres de Hola y tipos de datos para las columnas del objeto de Hola.

## <a name="descriptive-metadata"></a>Metadatos descriptivos
Metadatos descriptivos son metadatos que describe el propósito de Hola o el propósito de un recurso de datos. Normalmente se agregan metadatos descriptivos y los usuarios de catálogo con el portal del catálogo de datos de Azure de hello, pero también se puede extraer del origen de datos de Hola durante el registro. Por ejemplo, herramienta de registro de catálogo de datos de Azure de hello extraerá las descripciones de hello propiedad Description en SQL Server Analysis Services y SQL Server Reporting Services y de hello [ms_descriptionpropiedadextendida](https://technet.microsoft.com/library/ms190243.aspx)en bases de datos de SQL Server, si estas propiedades se han llenado con valores.

## <a name="request-access"></a>Solicitar acceso
Metadatos descriptivos del recurso de datos pueden incluir información sobre cómo acceder toorequest a toohello datos activos u origen de datos. Esta información se presenta con la ubicación de activos de datos de Hola y puede incluir una o varias de las siguientes opciones de hello:

* dirección de correo electrónico de saludo del usuario de Hola o equipo responsable de dar el origen de datos de access toohello.
* dirección URL de Hola de hello documenta proceso que los usuarios deben seguir el origen de datos de toogain access toohello.
* Hola dirección URL de una identidad y acceso herramienta de administración (por ejemplo, Microsoft Identity Manager) que puede ser el origen de datos de uso toogain access toohello.
* Una entrada de texto sin formato que describe cómo los usuarios pueden obtener el origen de datos de access toohello.

## <a name="preview"></a>Vista previa
Una vista previa en el catálogo de datos es una instantánea de too20 registros que se pueden extraer del origen de datos de Hola durante el registro y almacenan en el catálogo de hello con metadatos del activo de datos de Hola. vista previa de Hello puede ayudar a los usuarios que detección un recurso de datos entiendan mejor su función y el propósito. En otras palabras, ver datos de ejemplo puede ser más valioso que vean solo los nombres de columna de Hola y los tipos de datos.
Las vistas previas solo se admiten para tablas y vistas y deben seleccionarse explícitamente por el usuario de Hola durante el registro.

## <a name="data-profile"></a>Perfil de datos
Un perfil de datos en el catálogo de datos es una instantánea de nivel de tabla y columna de metadatos sobre un recurso de datos registrado que se pueden extraer del origen de datos de Hola durante el registro y almacenan en el catálogo de hello con metadatos del activo de datos de Hola. perfil de datos de Hello puede ayudar a los usuarios que detección un recurso de datos entiendan mejor su función y el propósito. Toopreviews similar, perfiles de datos debe seleccionarse explícitamente por el usuario de Hola durante el registro.

> [!NOTE]
> Extraer un perfil de datos puede ser una operación costosa para grandes tablas y vistas, y puede significativamente aumento Hola tooregister tiempo necesario un origen de datos.
>
>

## <a name="user-perspective"></a>Perspectiva del usuario
En el Catálogo de datos de Azure, cualquier usuario puede proporcionar metadatos descriptivos para un recurso de datos registrados. Cada usuario tiene una perspectiva distinta de los datos de Hola y su uso. Por ejemplo, los administradores de hello responsables de un servidor pueden proporcionar los detalles de Hola de su contrato de nivel de servicio (SLA) o de copia de seguridad windows; un administrador de datos puede proporcionar vínculos toodocumentation para la empresa de hello procesa Hola datos admite; y un analista que puede proporcionar una descripción en términos de Hola que son más relevantes tooother los analistas y que puede ser especialmente útil toothose quienes necesitan toodiscover y comprensión los datos de Hola.

Cada una de estas perspectivas son inherentemente valiosa y con el catálogo de datos de Azure, cada usuario puede proporcionar información de Hola que es significativo toothem, aunque todos los usuarios pueden utilizar esos datos de hello toounderstand de información y su finalidad.

## <a name="expert"></a>Experto
Un experto es un usuario que se ha identificado como poseedor de una perspectiva informada "experta" para un recurso de datos. Cualquier usuario puede agregarse a sí mismo o a otro usuario como experto para un recurso. Se muestra como un experto no transmite ningún privilegio adicional en el catálogo de datos; permite que los usuarios tooeasily localizar las perspectivas que están toobe probablemente útil para consultar los metadatos descriptivos de un recurso.

## <a name="owner"></a>Propietario
Un propietario es un usuario que tiene privilegios adicionales para administrar un recurso de datos en el Catálogo de datos de Azure. Los usuarios pueden tomar posesión de los recursos de datos registrados y los propietarios pueden agregar a otros usuarios como copropietarios. Para obtener más información, vea [cómo toomanage activos de datos](data-catalog-how-to-manage.md)  

> [!NOTE]
> Propiedad y administración solo están disponibles en hello edición estándar de catálogo de datos de Azure.
>
>

## <a name="registration"></a>Registro
Registro es Hola de extraer metadatos del activo de datos de un origen de datos y copiar toohello servicio de catálogo de datos de Azure. Es posible anotar y descubrir los recursos de datos que se han registrado.

## <a name="see-also"></a>Otras referencias
* [¿Qué es el Catálogo de datos de Azure?](data-catalog-what-is-data-catalog.md) -Este artículo proporciona una visión general de servicio del catálogo de datos de Azure hello, proporciona el valor de Hola y escenarios de hello admite.
* [Empezar a trabajar con el catálogo de datos de Azure](data-catalog-get-started.md) -este artículo proporciona un tutorial de extremo a extremo que muestra cómo toouse catálogo de datos de Azure para la detección de origen de datos.  
