---
title: "aaaLearn sobre Hola últimas versiones de SO invitado de Azure | Documentos de Microsoft"
description: "noticias de versión más recientes de Hola y compatibilidad con el SDK de SO de invitado de servicios de nube de Azure."
services: cloud-services
documentationcenter: na
author: raiye
manager: timlt
editor: 
ms.assetid: 6306cafe-1153-44c7-8554-623b03d59a34
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 8/24/2017
ms.author: raiye
ms.openlocfilehash: 7274f5a68a32ce91bdede77e1443cdb8053c07ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-guest-os-releases-and-sdk-compatibility-matrix"></a>Matriz de compatibilidad del SDK y versiones del SO invitado de Azure
Proporciona información actualizada acerca de hello que versiones del SO de invitado de Azure más reciente para servicios en la nube. Esta información le ayuda a planear la ruta de actualización antes de que se deshabilite un SO invitado. Si configura los roles toouse *automática* actualizaciones del SO invitado como se describe en [configuración de actualización de sistema operativo de invitado de Azure][Azure Guest OS Update Settings], no es fundamental que lea esta página.

> [!IMPORTANT]
> Esta página aplica a roles de web y de trabajo de servicios de tooCloud, que se ejecutan en un sistema operativo invitado. Lo hace **no aplicar** tooIaaS máquinas virtuales.
>
>


> [!NOTE]
> Fuente RSS de Hello recientemente ha quedado obsoleta. Consulte las actualizaciones de una nueva fuente que estará disponible próximamente.
>
>

¿Seguro de qué Hola SO invitado es o cómo Hola el trabajo de versiones de sistema operativo invitado? Lea [esta](#how-it-works) sección.

## <a name="news-updates"></a>Actualizaciones de noticias

###### <a name="august-24-2017"></a>**24 de agosto de 2017**
Se ha publicado el SO invitado de agosto.

###### <a name="august-3-2017"></a>**3 de agosto de 2017**
Se ha publicado el SO invitado de julio.

###### <a name="july-19-2017"></a>**19 de julio de 2017**
La implementación del SO invitado del mes de julio comienza el 19 de julio y está previsto que se lance el 8 de agosto.

###### <a name="july-7-2017"></a>**7 de julio de 2017**
Se ha publicado el SO invitado de junio.

###### <a name="june-16-2017"></a>**16 de junio de 2017**
La implementación del SO invitado del mes de junio comienza el 16 de junio y está previsto que se lance el 11 de julio.

###### <a name="june-5-2017"></a>**5 de junio de 2017**
Se ha publicado el SO invitado de mayo.

###### <a name="may-17-2017"></a>**17 de mayo de 2017**
Debido a los errores de seguridad tooa, nos estamos deshabilitar Hola siguientes de 2016 de diciembre y enero de 2017 versiones de sistema operativo que no tienen hello [corregir] desde el portal de hello: WA-invitado-OS-5.4_201612-01, WA-invitado-OS-4.39_201612-01, WA-invitado-OS-3.46_ 201612-01, WA-GUEST-OS-2.59_201701-01

###### <a name="may-12-2017"></a>**12 de mayo de 2017**
La implementación del SO invitado del mes de mayo comienza el 12 de mayo y está previsto que se lance el 13 de junio.

###### <a name="april-18-2017"></a>**18 de abril de 2017**
La implementación del SO invitado del mes de abril comienza el 18 de abril y está previsto que se lance el 9 de mayo.

###### <a name="april-10-2017"></a>**10 de abril de 2017**
La implementación del SO invitado del mes de marzo comienza el 14 de marzo de 2017 y está previsto que se lance el 10 de abril de 2017.

###### <a name="january-10-2017"></a>**10 de enero de 2017**
Hola SO invitado de enero contiene revisiones que solo afectan al familia del SO 2 (Windows 2008 Server R2). Por lo tanto, hemos publicado solo la imagen de hello 2 de la familia de SO (WA-GUEST-OS-2.59_201701-01) de este mes. Para todas las familias de sistemas operativos, Hola SO diciembre (201612 - 01) sigue siendo Hola más reciente.


## <a name="releases"></a>Lanzamientos
## <a name="family-5-releases"></a>Lanzamientos de la familia 5
**Windows Server, 2016**

Versión de .NET Framework instalada: 4.0, 4.5, 4.5.1, 4.5.2, 4.6, 4.6.1, 4.6.2

> [!NOTE]
> Las fechas con un * son toochange de asunto.
>
> Hola contraseña de RDP para 5 de la familia de SO debe ser como mínimo de 10 caracteres.
>

| Cadena de configuración | Fecha de lanzamiento | Fecha de deshabilitación | Fecha de expiración |
| --- | --- | --- | --- |
| WA-GUEST-OS-5.10_201708-01 |24 de agosto de 2017 |Publicación 5.12 |TBD |
| WA-GUEST-OS-5.9_201707-01 |3 de agosto de 2017 |Post 5.11 |TBD |
| WA-GUEST-OS-5.8_201706-01 |7 de julio de 2017 |Post 5.10 |TBD |
|~~WA-GUEST-OS-5.7_201705-01~~ |5 de junio de 2017 |24 de agosto de 2017 |TBD |
|~~WA-GUEST-OS-5.6_201704-01~~ |9 de mayo de 2017 |3 de agosto de 2017 |TBD |
|~~WA-GUEST-OS-5.5_201703-01~~ |10 de abril de 2017 |7 de julio de 2017 |TBD |
|~~WA-GUEST-OS-5.4_201612-01~~ |10 de enero de 2017 |5 de junio de 2017|TBD |
|~~WA-GUEST-OS-5.3_201611-01~~ |14 de diciembre de 2016 |9 de mayo de 2017 |TBD |
|~~WA-GUEST-OS-5.2_201610-02~~ |1 de noviembre de 2016 |10 de abril de 2017 |TBD |

## <a name="family-4-releases"></a>Lanzamientos de la familia 4
**Windows Server 2012 R2**

Admite .NET 4.0, 4.5, 4.5.1 y 4.5.2

> [!NOTE]
> Las fechas con un * son toochange de asunto
>
>

| Cadena de configuración | Fecha de lanzamiento | Fecha de deshabilitación | Fecha de expiración |
| --- | --- | --- | --- |
| WA-GUEST-OS-4.45_201708-01 |24 de agosto de 2017 |Publicación 4.47 |TBD |
| WA-GUEST-OS-4.44_201707-01 |3 de agosto de 2017 |Post 4.46 |TBD |
| WA-GUEST-OS-4.43_201706-01 |7 de julio de 2017 |Post 4.45 |TBD |
|~~WA-GUEST-OS-4.42_201705-01~~ |5 de junio de 2017 |24 de agosto de 2017 |TBD |
|~~WA-GUEST-OS-4.41_201704-01~~ |9 de mayo de 2017 |3 de agosto de 2017 |TBD |
|~~WA-GUEST-OS-4.40_201703-01~~ |10 de abril de 2017 |7 de julio de 2017 |TBD |
|~~WA-GUEST-OS-4.39_201612-01~~ |10 de enero de 2017 |5 de junio de 2017 |TBD |
|~~WA-GUEST-OS-4.38_201611-01~~ |14 de diciembre de 2016 |9 de mayo de 2017 |TBD |
|~~WA-GUEST-OS-4.37_201610-02~~ |16 de noviembre de 2016 |10 de abril de 2017 |TBD |
|~~WA-GUEST-OS-4.36_201609-01~~ |13 de octubre de 2016 |14 de enero de 2017 |TBD |
|~~WA-GUEST-OS-4.35_201608-01~~ |13 de septiembre de 2016 |16 de diciembre de 2016 |TBD |
|~~WA-GUEST-OS-4.34_201607-01~~ |8 de agosto de 2016 |13 de noviembre de 2016 |TBD |


## <a name="family-3-releases"></a>Lanzamientos de la familia 3
**Windows Server 2012**

Admite .NET 4.0, 4.5, 4.5.1 y 4.5.2

> [!NOTE]
> Las fechas con un * son toochange de asunto
>
>

| Cadena de configuración | Fecha de lanzamiento | Fecha de deshabilitación | Fecha de expiración |
| --- | --- | --- | --- |
| WA-GUEST-OS-3.52_201708-01 |24 de agosto de 2017 |Publicación 3.54 |TBD |
| WA-GUEST-OS-3.51_201707-01 |3 de agosto de 2017 |Post 3.53 |TBD |
| WA-GUEST-OS-3.50_201706-01 |7 de julio de 2017 |Post 3.52 |TBD |
|~~WA-GUEST-OS-3.49_201705-01~~ |5 de junio de 2017 |24 de agosto de 2017 |TBD |
|~~WA-GUEST-OS-3.48_201704-01~~ |9 de mayo de 2017 |3 de agosto de 2017 |TBD |
|~~WA-GUEST-OS-3.47_201703-01~~ |10 de abril de 2017 |7 de julio de 2017 |TBD |
|~~WA-GUEST-OS-3.46_201612-01~~ |10 de enero de 2017 |5 de junio de 2017 |TBD |
|~~WA-GUEST-OS-3.45_201611-01~~ |14 de diciembre de 2016 |9 de mayo de 2017 |TBD |
|~~WA-GUEST-OS-3.44_201610-02~~ |16 de noviembre de 2016 |1 de mayo de 2017 |TBD |
|~~WA-GUEST-OS-3.43_201609-01~~ |13 de octubre de 2016 |14 de enero de 2017 |TBD |
|~~WA-GUEST-OS-3.42_201608-01~~ |13 de septiembre de 2016 |16 de diciembre de 2016 |TBD |
|~~WA-GUEST-OS-3.41_201607-01~~ |8 de agosto de 2016 |13 de noviembre de 2016 |TBD |


## <a name="family-2-releases"></a>Lanzamientos de la familia 2
**Windows Server 2008 R2 SP1**

Admite .NET 3.5, 4.0, 4.5, 4.5.1, 4.5.2

> [!NOTE]
> Las fechas con un * son toochange de asunto
>
>

| Cadena de configuración | Fecha de lanzamiento | Fecha de deshabilitación | Fecha de expiración |
| --- | --- | --- | --- |
| WA-GUEST-OS-2.65_201708-01 |24 de agosto de 2017 |Publicación 2.67 |TBD |
| WA-GUEST-OS-2.64_201707-01 |3 de agosto de 2017 |Post 2.66 |TBD |
| WA-GUEST-OS-2.63_201706-01 |7 de julio de 2017 |Post 2.65 |TBD |
|~~WA-GUEST-OS-2.62_201705-01~~ |5 de junio de 2017 |24 de agosto de 2017 |TBD |
|~~WA-GUEST-OS-2.61_201704-01~~ |9 de mayo de 2017 |3 de agosto de 2017 |TBD |
|~~WA-GUEST-OS-2.60_201703-01~~ |10 de abril de 2017 |7 de julio de 2017 |TBD |
|~~WA-GUEST-OS-2.59_201701-01~~ |10 de enero de 2017 |5 de junio de 2017 |TBD |
|~~WA-GUEST-OS-2.58_201612-01~~ |10 de enero de 2017 |9 de mayo de 2017|TBD |
|~~WA-GUEST-OS-2.57_201611-01~~ |14 de diciembre de 2016 |10 de abril de 2017 |TBD |
|~~WA-GUEST-OS-2.56_201610-02~~ |16 de noviembre de 2016 |10 de febrero de 2017 |TBD |
|~~WA-GUEST-OS-2.55_201609-01~~ |13 de octubre de 2016 |14 de enero de 2017 |TBD |
|~~WA-GUEST-OS-2.54_201608-01~~ |13 de septiembre de 2016 |16 de diciembre de 2016 |TBD |
|~~WA-GUEST-OS-2.53_201607-01~~ |8 de agosto de 2016 |13 de noviembre de 2016 |TBD |



## <a name="msrc-patch-updates"></a>Actualizaciones de revisiones de MSRC
Hello lista de revisiones que se incluyen con cada versión de SO invitado mensual está disponible [aquí][patches].

## <a name="sdk-support"></a>Compatibilidad con SDK
Aunque Hola [directiva de retirada para hello Azure SDK] [ retire policy sdk] indica que solo versiones anteriormente 2.2 son compatibles, específico familias del SO invitado permiten toouse versiones anteriores. Debe utilizar siempre Hola SDK admite la versión más reciente.

| Familia del SO invitado | Versiones del SDK compatibles |
| --- | --- |
| 5 |Versión 2.9.5.1+ |
| 4 |Versión 2.1 o superior |
| 3 |Versión 1.8 o superior |
| 2 |Versión 1.3 o superior |
| 1 |Versión 1.0 o superior |

## <a name="guest-os-release-information"></a>Información de los lanzamientos del SO invitado
Hay tres fechas importantes libera tooGuest OS: **versión** fecha, **deshabilitado** fecha, y **caducidad** fecha. Un SO invitado se considera disponible cuando está en hello Portal y se pueden seleccionar como destino de hello SO invitado. Cuando llegue a un sistema operativo invitado hello **deshabilitado** fecha, se quita de Azure. aunque todos los servicios en la nube que usen dicho SO invitado seguirán funcionando con normalidad.

ventana de Hello entre hello **deshabilitado** hello y fecha **caducidad** fecha proporciona una transición de tooeasily de búfer de una tooone de SO invitado más reciente. Si usas *automática* como el SO invitado, siempre estará en la versión más reciente de hello y no tiene tooworry respecto a expirar.

Cuando Hola **caducidad** fecha pasadas, cualquier servicio en la nube se detendrá sigue usando ese sistema operativo invitado, tooupgrade eliminado o forzada. Puede leer más acerca de la directiva de retirada de hello [aquí][retirepolicy].

## <a name="guest-os-family-version-explanation"></a>Diferencias entre la versión y la familia de los SO invitados
familias del SO invitado Hola se basan en las versiones publicadas de Microsoft Windows Server. Hola SO invitado es el sistema operativo subyacente Hola servicios en la nube se ejecuta en. Cada SO invitado tiene un número de familia, versión y lanzamiento.

* **Guest OS family**  
  Versión del sistema operativo Windows Server en la que se basa un SO invitado. Por ejemplo, la *familia 3* se basa en Windows Server 2012.
* **Versión del SO invitado**  
  Tooa específico familia del SO invitado de la imagen más relevante [Microsoft Security Response Center (MSRC)] [ msrc] revisiones que están disponibles en la versión del SO invitado nuevo Hola fecha Hola se genera. Es posible que no se incluyan todas las revisiones.

    Los números empiezan por 0 y se incrementan en 1 cada vez que se agrega un nuevo conjunto de actualizaciones. Solo se muestran los ceros finales si es importante. Es decir, la versión 2.10 es una versión mucho más posterior y diferente que la versión 2.1.
* **Lanzamiento del SO invitado**  
  Relanzamiento de una versión de SO invitado. Un relanzamiento se produce si Microsoft encuentra, durante las pruebas, problemas que requieran cambios. Hello más reciente lanzamiento reemplaza siempre a las anteriores versiones, público o no. Hola portal de Azure solo permitirá a los usuarios la versión más reciente de hello toopick para una versión concreta. Las implementaciones que se ejecuta en una versión anterior no suelen ser force actualizado, según la gravedad de Hola de los errores de Hola.

En el ejemplo de Hola siguiente, 2 es la familia de hello, 12 es la versión de Hola y "rel2" es una versión Hola.

**Lanzamiento del SO invitado** : 2.12 rel2

**Cadena de configuración para este lanzamiento** - WA-GUEST-OS-2.12_201208-02

cadena de configuración de Hola para un SO invitado incluye esta misma información incrustada en él, junto con una fecha que muestra qué revisiones de MSRC se tuvieron en cuenta para esa versión. En este ejemplo, revisiones de MSRC generadas para Windows Server 2008 R2 seguridad tooand incluidos agosto de 2012 se tuvieron en cuenta para su inclusión. Se incluyen solo las revisiones se aplican específicamente toothat versión de Windows Server. Por ejemplo, si una revisión de MSRC aplica tooMicrosoft Office, no se incluirá porque ese producto no forma parte de la imagen base del servidor de Windows hello.

## <a name="guest-os-system-update-process"></a>Proceso de actualización del SO invitado
Esta página incluye información sobre los próximos lanzamientos del SO invitado. Los clientes han indicado que desean tooknow cuando se produce un lanzamiento porque sus roles de servicio de nube se reiniciarán si se establecen demasiado "actualización"Automática". Versiones del SO invitado suelen producen al menos cinco (5) días después de hello MSRC actualizaciones de versión que se produce en hello segundo martes de cada mes. Los nuevos lanzamientos incluyen todas las revisiones de MSRC relevantes Hola para cada familia del SO invitado.

Microsoft Azure publica actualizaciones constantemente. Hola SO invitado es solo una de estas actualizaciones en la canalización de Hola. Un lanzamiento puede verse afectado por diversos factores demasiado numerosos toolist aquí. Además, Azure se ejecuta literalmente en cientos de miles de máquinas. Esto significa que resulta imposible toogive una fecha y hora exacta cuando se reiniciarán los roles. Se está trabajando en un plan toolimit o acotar los reinicios.

Cuando una nueva versión de SO invitado se publica de hello, puede tardar tiempo toofully propagarse a través de Azure. Como los servicios están actualizado toohello nuevo SO invitado, son reiniciada respetando los dominios de actualización. Conjunto toouse actualizaciones "Automáticas" obtendrá una versión primero. Después de la actualización de hello, verá la nueva versión de SO invitado Hola enumerados para el servicio en hello portal de Azure. Durante ese período se pueden producir relanzamientos. Algunas versiones se pueden implementar durante largos períodos de tiempo y es podrán que los reinicios de actualización automática no se produzcan hasta muchas semanas después de la fecha de lanzamiento oficial de Hola. Una vez que un SO invitado está disponible, puede, a continuación, explícitamente elegir esa versión del portal de Hola o en el archivo de configuración.

Para una gran cantidad de información valiosa sobre los reinicios y punteros toomore detalles técnicos de las actualizaciones de sistemas operativos Host e invitado, vea el blog de MSDN de hello titulado [actualizaciones de instancia de rol se reinicia debido tooOS] [ restarts].

Si actualiza manualmente el SO invitado, consulte hello [directiva de retirada de SO invitado] [ retirepolicy] para obtener información adicional.

## <a name="guest-os-supportability-and-retirement-policy"></a>Directiva de compatibilidad y retirada del SO invitado
se explica la directiva de compatibilidad y retirada de SO invitado de Hello [aquí][retirepolicy].

[Install .NET on a Cloud Service Role]: https://azure.microsoft.com/en-us/documentation/articles/cloud-services-dotnet-install-dotnet/?WT.mc_id=azurebg_email_Trans_963_RevisedNET_Update
[Azure Guest OS Update Settings]: cloud-services-how-to-configure.md
[ssl3 announcement]: http://azure.microsoft.com/blog/2014/12/09/azure-security-ssl-3-0-update/
[Microsoft Security Advisory 3009008]: https://technet.microsoft.com/library/security/3009008.aspx
[ssl3-fixit]: http://go.microsoft.com/?linkid=9863266
[MS14-066]: https://technet.microsoft.com/library/security/ms14-066.aspx
[MS14-046]: https://technet.microsoft.com/library/security/ms14-046.aspx
[retire policy sdk]: https://msdn.microsoft.com/library/dn479282.aspx
[server and gos]: https://msdn.microsoft.com/library/dn775043.aspx
[azuresupport]: http://azure.microsoft.com/support/options/
[net install pkg]: http://www.microsoft.com/download/details.aspx?id=42643
[msrc]: http://www.microsoft.com/security/msrc/default.aspx
[update guest os portal]: https://msdn.microsoft.com/library/gg433101.aspx
[update guest os svc]: https://msdn.microsoft.com/library/gg456324.aspx
[restarts]: http://blogs.msdn.com/b/kwill/archive/2012/09/19/role-instance-restarts-due-to-os-upgrades.aspx
[patches]: cloud-services-guestos-msrc-releases.md
[retirepolicy]: cloud-services-guestos-retirement-policy.md
[fam1retire]: cloud-services-guestos-family1-retirement.md
[corregir]: https://technet.microsoft.com/en-us/library/security/ms17-010.aspx
