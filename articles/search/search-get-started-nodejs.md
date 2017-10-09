---
title: "aaaGet a trabajar con búsqueda de Azure en Node.js | Documentos de Microsoft"
description: "Siga todos los pasos para realizar una aplicación de búsqueda en un servicio de búsqueda hospedado en la nube en Azure con Node.js como lenguaje de programación."
services: search
documentationcenter: 
author: EvanBoyle
manager: pablocas
editor: v-lincan
ms.assetid: 0625dc1b-9db6-40d5-ba9a-4738b75cbe19
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.date: 04/26/2017
ms.author: evboyle
ms.openlocfilehash: e9c7d756c2ea191ee2a285485c90439b96aa73b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-search-in-nodejs"></a>Introducción a Azure Search en Node.js
> [!div class="op_single_selector"]
> * [Portal](search-get-started-portal.md)
> * [.NET](search-howto-dotnet-sdk.md)
> 
> 

Obtenga información acerca de cómo buscar los toobuild un Node.js personalizado en la aplicación que utiliza la búsqueda de Azure para su experiencia de búsqueda. Este tutorial usa hello [API de REST de servicio de búsqueda de Azure](https://msdn.microsoft.com/library/dn798935.aspx) tooconstruct Hola objetos y operaciones que se usan en este ejercicio.

Utilizamos [Node.js](https://Nodejs.org) y NPM, [fundamentales 3 texto](http://www.sublimetext.com/3)y Windows PowerShell en Windows 8.1 toodevelop y pruebe este código.

toorun en este ejemplo, debe tener un servicio de búsqueda de Azure, que pueden suscribirse a Hola [portal de Azure](https://portal.azure.com). Vea [crear un servicio de búsqueda de Azure en el portal de hello](search-create-service-portal.md) para obtener instrucciones paso a paso.

## <a name="about-hello-data"></a>Acerca de los datos de Hola
Esta aplicación de ejemplo utiliza datos de hello [servicios geológicas de Estados Unidos (USG)](http://geonames.usgs.gov/domestic/download_data.htm)y filtrado en el tamaño de conjunto de datos de hello estado de Rhode Island tooreduce Hola. Usaremos esta toobuild una aplicación de búsqueda que devuelve edificios de punto de referencia como hospitales y varios centros escolares, así como características geológicas como secuencias, lagos y cumbres de datos.

En esta aplicación, Hola **DataIndexer** programa genera y cargas Hola índice usando un [indizador](https://msdn.microsoft.com/library/azure/dn798918.aspx) construcción, recuperar Hola filtra USG conjunto de datos de una base de datos de SQL Azure pública. Las credenciales y conexión de origen de datos en línea de toohello de información se proporciona en el código de programa Hola. No es necesario realizar ninguna otra configuración.

> [!NOTE]
> Se aplica un filtro en este toostay de conjunto de datos en límite del documento 10.000 Hola de hello libre de nivel de precios. Si utiliza el nivel estándar de hello, este límite no se aplica. Para obtener información más detallada sobre las características de cada plan de tarifa, consulte [Límites de servicio en la Búsqueda de Azure](search-limits-quotas-capacity.md).
> 
> 

<a id="sub-2"></a>

## <a name="find-hello-service-name-and-api-key-of-your-azure-search-service"></a>Buscar el nombre del servicio de Hola y clave de api del servicio en la búsqueda de Azure
Después de crear el servicio de hello, devolver toohello tooget portal Hola URL o `api-key`. Conexiones tooyour servicio de búsqueda requieren que tenga las URL de Hola y un `api-key` llamada de hello tooauthenticate.

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. En la barra de salto de hello, haga clic en **servicio de búsqueda** toolist todos los servicios de búsqueda de Azure aprovisionados para su suscripción.
3. Seleccione servicio de Hola que desee toouse.
4. En el panel de servicio de hello, debería ver iconos para obtener información esencial, como icono de llave hello para tener acceso a las claves de administración de Hola.
5. Copiar dirección URL del servicio de hello, una clave de administración y una clave de consulta. Necesita las tres más adelante al agregarlas toohello config.js archivo.

## <a name="download-hello-sample-files"></a>Descargar archivos de ejemplo de Hola
Use uno de hello según enfoques toodownload hello muestra.

1. Vaya demasiado[AzureSearchNodeJSIndexerDemo](https://github.com/AzureSearch/AzureSearchNodejsIndexerDemo).
2. Haga clic en **Download ZIP**, guarde el archivo .zip de hello y, a continuación, extraer todos los archivos de Hola que contiene.

Todas las modificaciones y las instrucciones de ejecución del archivo posteriores se realizan en los archivos de esta carpeta.

## <a name="update-hello-configjs-with-your-search-service-url-and-api-key"></a>Actualizar config.js Hola. con la dirección URL del servicio de búsqueda y la clave de API
Usar Hola dirección URL y la clave de api que copió anteriormente, especifique Hola dirección URL, clave de administración y la clave de consulta en el archivo de configuración.

La clave de administración concede control total sobre las operaciones de servicio, incluidas la creación o eliminación de un índice y la carga de documentos. En cambio, las claves de consulta son para operaciones de solo lectura, que suelen usadas las aplicaciones de cliente que se conectan tooAzure búsqueda.

En este ejemplo, se incluyen consultas de hello toohelp clave reforzar el procedimiento recomendado de hello del uso de clave de consulta de hello en aplicaciones cliente.

Hola siguiente captura de pantalla muestra **config.js** abierto en un editor de texto, con hello las entradas pertinentes delimitadas para que puedan ver donde archivo de hello tooupdate con hello valores que son válidas para el servicio de búsqueda.

![][5]

## <a name="host-a-runtime-environment-for-hello-sample"></a>Hospedar un entorno en tiempo de ejecución de ejemplo de Hola
ejemplo de Hola requiere un servidor HTTP, que se puede instalar mediante global npm.

Utilice una ventana de PowerShell para hello siga los comandos.

1. Desplazarse por las carpetas de toohello que contiene Hola **package.json** archivo.
2. Escriba `npm install`.
3. Escriba `npm install -g http-server`.

## <a name="build-hello-index-and-run-hello-application"></a>Generar índice hello y ejecutar la aplicación hello
1. Escriba `npm run indexDocuments`.
2. Escriba `npm run build`.
3. Escriba `npm run start_server`.
4. Dirija el explorador a `http://localhost:8080/index.html`

## <a name="search-on-usgs-data"></a>Buscar en los datos de USGS
conjunto de datos de Hello USG incluye registros de estado toohello relevante de Rhode Island. Si hace clic en **búsqueda** en un cuadro de búsqueda vacío, obtendrá entradas de 50 primeras hello, que es el valor predeterminado de Hola.

Escriba un término de búsqueda proporciona el motor de búsqueda de hello algo toogo en. Pruebe a escribir un nombre regional. "Roger Williams" era gobernador primera Hola de Rhode Island. Hay numerosos parques, edificios y escuelas que llevan su nombre.

![][9]

También puede probar con alguno de estos términos:

* Pawtucket
* Pembroke
* goose +cape

## <a name="next-steps"></a>Pasos siguientes
Se trata del primer tutorial de búsqueda de Azure hello en función de hello USG dataset y Node.js. Con el tiempo, ampliaremos esta tutorial toodemonstrate características de búsqueda adicional puede toouse en sus soluciones personalizadas.

Si ya tiene conocimientos sobre Búsqueda de Azure, puede usar este ejemplo como punto de partida para probar proveedores de sugerencias (escritura automática o autocompletar consultas), filtros y navegación por facetas. También puede mejorar en la página de resultados de búsqueda de hello agregando los recuentos y procesamiento por lotes de documentos para que los usuarios pueden desplazarse a través de los resultados de Hola.

¿TooAzure nueva búsqueda? Se recomienda intentar otra toodevelop tutoriales una descripción de lo que puede crear. Visite nuestro [página de documentación](https://azure.microsoft.com/documentation/services/search/) toofind más recursos. También puede ver los vínculos de hello en nuestro [lista de vídeo y un Tutorial](search-video-demo-tutorial-list.md) tooaccess obtener más información.

<!--Image references-->
[1]: ./media/search-get-started-Nodejs/create-search-portal-1.PNG
[2]: ./media/search-get-started-Nodejs/create-search-portal-2.PNG
[3]: ./media/search-get-started-Nodejs/create-search-portal-3.PNG
[5]: ./media/search-get-started-Nodejs/AzSearch-Nodejs-configjs.png
[9]: ./media/search-get-started-Nodejs/rogerwilliamsschool.png
