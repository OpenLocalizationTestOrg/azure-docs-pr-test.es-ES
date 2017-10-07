---
title: "aaaLearn acerca de las opciones de soporte técnico de tejido de servicio de Azure | Documentos de Microsoft"
description: "Versiones del clúster de Azure Service Fabric compatible y vincula incidencias de soporte técnico de toofile"
services: service-fabric
documentationcenter: .net
author: pkc
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/15/2017
ms.author: pkc
ms.openlocfilehash: 42394e2cd9dad2040d37d3a2ff3600ee040d8720
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-fabric-support-options"></a>Opciones de soporte técnico de Azure Service Fabric

toodeliver Hola adecuado compatibilidad con los clústeres de tejido de servicio que se está ejecutando el trabajo de la aplicación se carga en, hemos configurado varias opciones para usted. Función hello necesario nivel de compatibilidad y gravedad Hola de problema de hello, obtendrá toopick opciones correctas de Hola. 


<a id="getlivesitesupportonazure"></a>

## <a name="report-production-or-live-site-issues-or-request-paid-support-for-azure"></a>Notifique problemas en el entorno de producción o con el sitio activo, o bien solicite soporte técnico de pago para Azure

Si desea informar sobre problemas con el sitio activo en el clúster de Service Fabric que implementó en Azure, abra una incidencia de soporte técnico profesional [en Azure portal](https://ms.portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/overview) o en el [Portal de soporte técnico de Microsoft](http://support.microsoft.com/oas/default.aspx?prid=16146).

Más información sobre:
 
- [Soporte técnico profesional de Microsoft para Azure](https://azure.microsoft.com/en-us/support/plans/?b=16.44).
- [Soporte técnico Premier de Microsoft](https://support.microsoft.com/en-us/premier).

<a id="getlivesitesupportonprem"></a>

## <a name="report-production-or-live-site-issues-or-request-paid-support-for-standalone-service-fabric-clusters"></a>Notifique problemas en el entorno de producción o con el sitio activo, o bien solicite soporte técnico de pago para clústeres independientes de Service Fabric

Si desea informar sobre problemas con el sitio activo en el clúster de Service Fabric que implementó de forma local o en otras nubes, abra una incidencia de soporte técnico profesional en el [Portal de soporte técnico de Microsoft](http://support.microsoft.com/oas/default.aspx?prid=16146).

Más información sobre:

- [Soporte técnico profesional para Microsoft local](https://support.microsoft.com/en-us/gp/offerprophone?wa=wsignin1.0).
- [Soporte técnico Premier de Microsoft](https://support.microsoft.com/en-us/premier).


<a id="getsupportonissues"></a>
## <a name="report-azure-service-fabric-issues"></a>Información de problemas con Azure Service Fabric 
Configuramos un repositorio de GitHub para informar problemas con Service Fabric.  Hola siguientes foros se estamos supervisa también activamente.

### <a name="github-repo"></a>Repositorio de GitHub 
Informe problemas con Azure Service Fabric en el [repositorio de Git Service-Fabric-issues](https://github.com/Azure/service-fabric-issues). Este repositorio está diseñado para informar y rastrear problemas con Azure Service Fabric y para generar solicitudes de funciones pequeñas. **No utilice este sitio live tooreport emite**.

### <a name="stackoverflow-and-msdn-forums"></a>StackOverflow y foros de MSDN

Hola [etiqueta de Service Fabric de StackOverflow] [ stackoverflow] hello y [foro de Service Fabric en MSDN] [ msdn-forum] son mejores utilizado para hacer preguntas acerca de funcionamiento de la plataforma de Hola y cómo puede realizar ciertas tareas con él.

### <a name="azure-feedback-forum"></a>Foro de comentarios de Azure

Hola [foro de comentarios de Azure para Service Fabric] [ uservoice-forum] Hola mejor lugar para el envío de ideas de gran característica tendrá para el producto de hello como revisamos solicitudes más populares de hello forman parte de nuestros términos de toolong intermedio planeación. Le recomendamos que toorally compatibilidad con sus sugerencias dentro de la Comunidad de Hola.


<a id="releasesuport"></a>
## <a name="supported-service-fabric-versions"></a>Versiones admitidas de Service Fabric.

Asegúrese de que el clúster siempre ejecute una versión compatible de Service Fabric. Como y cuando se anunciar el lanzamiento de Hola de una nueva versión de Service Fabric, versión anterior de hello está marcado para finalización del soporte después de un mínimo de 60 días a partir de esa fecha. Hello nuevas versiones se anuncian [en el blog del equipo de Service Fabric hello](https://blogs.msdn.microsoft.com/azureservicefabric/).

Consulte toohello siguiente documentos de obtener detalles sobre cómo tookeep el clúster que ejecuta una versión compatible de Service Fabric.

- [Actualización de la versión de Service Fabric en un clúster de Azure ](service-fabric-cluster-upgrade.md)
- [Actualización de la versión de Service Fabric en un clúster de servidores de Windows independiente ](service-fabric-cluster-upgrade-windows-server.md)
 
Estas son lista Hola de versiones de Service Fabric Hola que son compatibles y sus fechas de finalización de soporte técnico.

| **Clúster de tiempo de ejecución de Service Fabric** | **Versiones del SDK o paquete de NuGet compatibles** | **Fecha de finalización de soporte técnico** |
| --- | --- | --- |
| Todos los clúster too5.3.121 de versiones anteriores |Menor que o igual tooversion 2.3 |20 de enero de 2017 |
| 5.3* |Menor que o igual tooversion 2.3 |24 de febrero de 2017 |
| 5.4.* |Menor que o igual tooversion 2.4 |10 de mayo de 2017     |
| 5.5.* |Menor que o igual tooversion 2.5 |10 de agosto de 2017    |
| 5.6.* |Menor que o igual tooversion 2.6 |13 de octubre de 2017    |
| 5.7.* |Menor que o igual tooversion 2.7 |Versión actual y, por lo tanto, sin fecha de finalización

<a id="previewversion"></a>
## <a name="service-fabric-preview-versions---unsupported-for-production-use"></a>Versiones de vista previa de Service Fabric: no admitidas para su uso en producción.
Desde hora tootime, publicamos versiones que tienen características importantes que deseamos comentarios, que se publican como vistas previas. Estas versiones preliminares solo se deben usar con fines de prueba. El clúster de producción debe estar ejecutando siempre una versión de Service Fabric compatible y estable. Una versión preliminar siempre comienza con un número de versión principal y secundaria de 255. Por ejemplo, si ve una versión 255.255.5703.949 de Service Fabric, esa versión es toobe solo se usa en los clústeres de prueba y está en vista previa. Estas versiones preliminares también se anuncian en hello [blog del equipo de Service Fabric](https://blogs.msdn.microsoft.com/azureservicefabric) y tener detalles sobre características de hello incluidas.

No hay ninguna opción de soporte técnico de pago para estas versiones preliminares. Use una de opciones de hello aparecen en [emite informes Azure Service Fabric](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-support#report-azure-service-fabric-issues) tooask preguntas o proporcionar comentarios.

## <a name="next-steps"></a>Pasos siguientes

- [Actualización de la versión de Service Fabric en un clúster de Azure ](service-fabric-cluster-upgrade.md)
- [Actualización de la versión de Service Fabric en un clúster de servidores de Windows independiente ](service-fabric-cluster-upgrade-windows-server.md)

<!--references-->
[msdn-forum]: https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureServiceFabric
[stackoverflow]: http://stackoverflow.com/questions/tagged/azure-service-fabric
[uservoice-forum]: https://feedback.azure.com/forums/293901-service-fabric
[acom-docs]: http://aka.ms/servicefabricdocs
[sample-repos]: http://aka.ms/servicefabricsamples
