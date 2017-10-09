---
title: aaaHow tooupdate un servicio en la nube | Documentos de Microsoft
description: "Obtenga información acerca de cómo servicios en la nube tooupdate en Azure. Obtenga información acerca de cómo realiza una actualización en un servicio de nube tooensure disponibilidad."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: c6a8b5e6-5c99-454c-9911-5c7ae8d1af63
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: adegeo
ms.openlocfilehash: 7e4c8bd46e51a555b4309ea8927d120e8efcf0ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooupdate-a-cloud-service"></a>¿Cómo tooupdate un servicio de nube

La actualización de un servicio en la nube, incluidos sus roles y el sistema operativo invitado, es un proceso de tres pasos. En primer lugar, los archivos binarios de Hola y archivos de configuración de hello nuevo servicio en la nube o se debe cargar la versión del sistema operativo. A continuación, Azure reserva los recursos y de red para el servicio de nube de hello en función de los requisitos de hello de la nueva versión del servicio de nube para Hola. Por último, Azure realiza una gradual tooincrementally actualización Hola inquilino toohello nueva versión de actualización o el sistema operativo invitado conservando su disponibilidad. En este artículo se trata detalles de Hola de este último paso: Hola actualización gradual.

## <a name="update-an-azure-service"></a>Actualización de un servicio de Azure
Azure organiza las instancias de rol en agrupaciones lógicas denominadas dominios de actualización (UD). Los dominios de actualización (UD) son conjuntos lógicos de instancias de rol que se actualizan como un grupo.  Azure actualiza una nube de servicio uno UD a la vez, lo que permite a instancias de otro toocontinue ud que sirve al tráfico.

número predeterminado de Hola de dominios de actualización es 5. Puede especificar un número diferente de dominios de actualización mediante la inclusión de atributo de upgradeDomainCount hello en el archivo de definición del servicio de hello (.csdef). Para obtener más información sobre el atributo de upgradeDomainCount hello, consulte [esquema WebRole](https://msdn.microsoft.com/library/azure/gg557553.aspx) o [esquema WorkerRole](https://msdn.microsoft.com/library/azure/gg557552.aspx).

Cuando se realiza una actualización en contexto de uno o varios roles en el servicio, Azure actualiza los conjuntos de instancias de rol según toohello toowhich de dominio de actualización al que pertenecen. Las actualizaciones de Azure todos de instancias de hello en un dominio de actualización determinado: deteniéndolas, actualizándolas, poniéndolas de nuevo en línea, a continuación, se desplaza al siguiente dominio de Hola. Deteniendo solo Hola instancias que se ejecutan en hello actual dominio de actualización, Azure se asegura de que se produce una actualización con hello menos posible impacto toohello ejecuta el servicio. Para obtener más información, consulte [cómo tiene lugar la actualización de hello](#howanupgradeproceeds) más adelante en este artículo.

> [!NOTE]
> Mientras que los términos de hello **actualizar** y **actualizar** tienen un significado ligeramente diferente en el contexto de hello Azure, pueden usarse indistintamente para procesos de Hola y descripciones de características de hello en este documento.
>
>

El servicio debe definir al menos dos instancias de un rol para ese rol toobe actualizar en contexto sin tiempo de inactividad. Si el servicio Hola consta de una única instancia de un rol, el servicio dejará de estar disponible hasta que hello actualización en contexto haya finalizado.

En este tema se trata Hola después de obtener información acerca de las actualizaciones de Azure:

* [Cambios de servicio permitidos durante una actualización](#AllowedChanges)
* [Cómo se realiza una actualización](#howanupgradeproceeds)
* [Reversión de una actualización](#RollbackofanUpdate)
* [Iniciación de varias operaciones mutantes en una implementación en curso](#multiplemutatingoperations)
* [Distribución de roles entre dominios de actualización](#distributiondfroles)

<a name="AllowedChanges"></a>

## <a name="allowed-service-changes-during-an-update"></a>Cambios de servicio permitidos durante una actualización
Hello tabla siguiente se muestran Hola permite cambios tooa servicio durante una actualización:

| Cambios permitidos toohosting, servicios y roles | Actualización local | Por etapas (intercambio de VIP) | Eliminar y volver a implementar |
| --- | --- | --- | --- |
| Versión del sistema operativo |Sí |Sí |Sí |
| Nivel de confianza de .NET |Sí |Sí |Sí |
| Tamaño de la máquina virtual<sup>1</sup> |Sí<sup>2</sup> |Sí |Sí |
| Configuración de almacenamiento local |Solo aumentar<sup>2</sup> |Sí |Sí |
| Agregar o quitar roles en un servicio |Sí |Sí |Sí |
| Número de instancias de un rol concreto |Sí |Sí |Sí |
| Número o tipo de puntos de conexión de un servicio |Sí<sup>2</sup> |No |Sí |
| Nombres y valores de configuración |Sí |Sí |Sí |
| Valores (pero no nombres) de configuración |Sí |Sí |Sí |
| Incorporación de nuevos certificados |Sí |Sí |Sí |
| Cambio de certificados existentes |Sí |Sí |Sí |
| Implementación de nuevo código |Sí |Sí |Sí |

<sup>1</sup> cambio de tamaño limitado toohello subconjunto de los tamaños disponibles para el servicio de nube de Hola.

<sup>2</sup> Requiere Azure SDK 1.5 o versiones posteriores.

> [!WARNING]
> Cambiar el tamaño de la máquina virtual de hello destruirá datos locales.
>
>

Hola siguientes elementos no se admite durante una actualización:

* Cambiar nombre de Hola de un rol. Quitar y, a continuación, agregar rol de hello con hello nuevo nombre.
* Cambio de hello recuento de actualización del dominio.
* Reducir el tamaño de Hola de recursos locales de Hola.

Si va a realizar otras actualizaciones de definición del servicio de tooyour, como reducir el tamaño de hello del recurso local, debe realizar una actualización de intercambio de VIP en su lugar. Para obtener más información, consulte [Intercambiar implementaciones](https://msdn.microsoft.com/library/azure/ee460814.aspx).

<a name="howanupgradeproceeds"></a>

## <a name="how-an-upgrade-proceeds"></a>Cómo se realiza una actualización
Puede decidir si desea que tooupdate todos los roles de hello en el servicio o un único rol en el servicio de Hola. En cualquier caso, todas las instancias de cada rol que se está actualizando y deben pertenecer toohello primer dominio de actualización se detiene, se actualizará y se vuelve a poner en línea. Una vez que se vuelve a estar conectados, hello instancias en el segundo dominio de actualización de Hola se detiene, actualizar y poner en línea. Un servicio en la nube puede tener como mucho una actualización activa a la vez. actualización de Hola se realiza siempre en la versión más reciente de hello del servicio de nube de Hola.

Hello siguiente diagrama muestra cómo se realiza Hola actualización si va a actualizar todos los roles de hello en el servicio de Hola de:

![Actualizar servicio](media/cloud-services-update-azure-service/IC345879.png "Actualizar servicio")

En el diagrama siguiente muestra cómo se realiza la actualización de hello si va a actualizar un único rol:

![Actualizar rol](media/cloud-services-update-azure-service/IC345880.png "Actualizar rol")  

Durante una actualización automática, hello Azure Fabric Controller evalúa periódicamente mantenimiento Hola de toodetermine de servicio de nube de hello cuando su toowalk seguro Hola UD siguiente. Esta evaluación de mantenimiento se realiza en una base por rol y considera que solo las instancias en la versión más reciente de hello (es decir, instancias de ud que ya se ha visto). Comprueba que un número mínimo de instancias de rol, para cada rol, hayan alcanzado un estado terminal satisfactorio.

### <a name="role-instance-start-timeout"></a>Tiempo de espera de inicio de la instancia de rol
Controlador de tejido de Hello esperará 30 minutos para cada tooreach de instancia de rol un estado iniciado. Si transcurre la duración del tiempo de espera de hello, controlador de tejido de Hola continuará recorrer toohello siguiente instancia de rol.

### <a name="impact-toodrive-data-during-cloud-service-upgrades"></a>Datos de impacto de toodrive durante las actualizaciones de servicio en la nube

Al actualizar un servicio desde una instancia de toomultiple de instancia única se desactivará su servicio mientras se realiza la actualización de hello debido forma toohello que Azure actualiza los servicios. disponibilidad de servicio garantiza de contrato de nivel de servicio de Hello solo aplica tooservices que se implementan con más de una instancia. Hello lista siguiente describe cómo afectan los datos de hello en cada unidad de distintos escenarios de actualización de servicio de Azure:

|Escenario|Unidad C|Unidad D|Unidad E|
|--------|-------|-------|-------|
|Reinicio de máquina virtual|Conservado|Conservado|Conservado|
|Reinicio del Portal|Conservado|Conservado|Destruido|
|Restablecimiento de la imagen inicial del portal|Conservado|Destruido|Destruido|
|Actualización local|Conservado|Conservado|Destruido|
|Migración de nodos|Destruido|Destruido|Destruido|

Tenga en cuenta que, en Hola por encima de la lista representa la unidad raíz del rol de Hola Hola unidad E: y no debe estar codificado de forma rígida. En su lugar, use hello **% RoleRoot %** unidad de hello toorepresent variables de entorno.

toominimize Hola el tiempo de inactividad al actualizar un servicio de instancia única, implemente un servidor provisional de varias instancias servicio toohello nuevo y realice un intercambio de VIP.

<a name="RollbackofanUpdate"></a>

## <a name="rollback-of-an-update"></a>Reversión de una actualización
Azure proporciona flexibilidad en la administración de servicios durante una actualización que le permite iniciar operaciones adicionales en un servicio, una vez se acepta la solicitud de actualización inicial de Hola por hello controlador de tejido de Azure. Solo se puede realizar una reversión cuando una actualización (cambio de configuración) o la actualización está en hello **en curso** estado de implementación de Hola. Una actualización o una actualización se considera toobe en curso, siempre que hay al menos una instancia del servicio de Hola que aún no ha sido actualizada toohello nueva versión. tootest si se permite una reversión, compruebe valor Hola de marca de RollbackAllowed hello, devuelto por [Get Deployment](https://msdn.microsoft.com/library/azure/ee460804.aspx) y [obtener propiedades del servicio de nube](https://msdn.microsoft.com/library/azure/ee460806.aspx) operaciones, se establece tootrue.

> [!NOTE]
> Sólo tiene sentido toocall Rollback en un **in situ** actualizar o actualizar debido a las actualizaciones del intercambio de VIP implican reemplazar una instancia en ejecución completa de su servicio con otro.
>
>

Reversión de una actualización en curso tiene Hola siguientes efectos en la implementación de hello:

* Las instancias de rol que no se hubiera aún toohello actualizadas nueva versión no se actualizan o actualizar, porque dichas instancias ya están ejecutando la versión de destino de hello del servicio de Hola.
* Cualquier rol instancias ya que hubiera actualizado o actualizado toohello nueva versión del paquete de servicio de hello (\*.cspkg) Hola o archivo de configuración del servicio (\*.cscfg) archivo (o ambos archivos) están toohello revertida versión previa a la actualización de estos archivos.

Esta funcionalidad la proporcionan Hola siguientes características:

* Hola [reversión actualizar o actualizar](https://msdn.microsoft.com/library/azure/hh403977.aspx) operación, que se puede llamar en una actualización de la configuración (desencadenada al llamar a [cambiar la configuración de implementación](https://msdn.microsoft.com/library/azure/ee460809.aspx)) o una actualización (desencadenada al llamar a [ Actualizar implementación](https://msdn.microsoft.com/library/azure/ee460793.aspx)) siempre que hay al menos una instancia de servicio de Hola que no se ha recibido actualizado a la versión nueva de toohello.
* Hola bloqueada y hello RollbackAllowed elemento, que se devuelven como parte del cuerpo de respuesta de Hola de hello [Get Deployment](https://msdn.microsoft.com/library/azure/ee460804.aspx) y [obtener propiedades del servicio de nube](https://msdn.microsoft.com/library/azure/ee460806.aspx) operaciones:

  1. Hola bloqueado elemento le permite toodetect, cuando una operación de mutación se puede invocar en una implementación determinada.
  2. Hello RollbackAllowed elemento le permite toodetect cuando hello [revertir actualización o actualizar](https://msdn.microsoft.com/library/azure/hh403977.aspx) operación puede llamarse en una implementación determinada.

  En orden tooperform una reversión, no tiene toocheck Hola bloqueada tanto Hola RollbackAllowed elementos. Es suficiente con tooconfirm que RollbackAllowed se establece tootrue. Estos elementos solo se devuelven si estos métodos se invocan utilizando el encabezado de solicitud de hello establecido demasiado "x-ms-version: 2011-10-01" o una versión posterior. Para obtener más información acerca de los encabezados de control de versiones, consulte [Control de versiones de la administración del servicio](https://msdn.microsoft.com/library/azure/gg592580.aspx).

Hay algunas situaciones en las que no se admite la reversión de una actualización, estas son las siguientes:

* Reducción de recursos locales: si Hola actualización aumenta Hola recursos locales para un rol Hola plataforma Windows Azure no permite la reversión.
* Limitaciones de cuota: si actualización Hola estaba una escala hacia abajo de la operación, puede que no tenga suficientes proceso cuota toocomplete Hola de reversión. Cada suscripción de Azure tiene una cuota asociada que especifica el número máximo de Hola de núcleos que puede ser utilizado por todos los servicios hospedados que pertenecen toothat suscripción. Si la reversión de una determinada actualización hace que su suscripción supere la cuota asignada, no se habilitará dicha reversión.
* Condición de carrera: si ha completado la actualización inicial de hello, no es posible una operación de deshacer.

Un ejemplo de cuando la reversión Hola de una actualización puede resultar útil es si usas hello [actualizar implementación](https://msdn.microsoft.com/library/azure/ee460793.aspx) se implanta operación en velocidad de hello toocontrol de modo manual en el que un tooyour de actualización en contexto principal Azure servicio hospedado.

Durante la implementación de Hola de actualización de Hola llaman a [actualizar implementación](https://msdn.microsoft.com/library/azure/ee460793.aspx) en modo manual y empezar a dominios de actualización de toowalk. Si en algún momento, como supervisar actualización hello, tenga en cuenta algunas instancias de rol en los primeros dominios de actualización Hola que examinar han dejado de responder, puede llamar a hello [revertir actualización o actualizar](https://msdn.microsoft.com/library/azure/hh403977.aspx) operación de implementación de hello, que sale de instancias de hello intactos que aún no se han actualizado y actualizar las instancias de reversión que habría sido toohello paquete de servicio anterior y la configuración.

<a name="multiplemutatingoperations"></a>

## <a name="initiating-multiple-mutating-operations-on-an-ongoing-deployment"></a>Iniciación de varias operaciones mutantes en una implementación en curso
En algunos casos puede que desee tooinitiate varias operaciones simultáneas de mutación en una implementación en curso. Por ejemplo, puede realizar una actualización de servicio y, mientras que la actualización se está implantando a través de su servicio, desea toomake algún cambio, por ejemplo, tooroll Hola actualización, aplicar otra actualización o incluso eliminar la implementación de Hola. Un caso en el que esto podría ser necesario es si una actualización de servicio contiene código con errores que causa un bloqueo de toorepeatedly de instancia de rol actualizada. En este caso, Hola controlador de tejido de Azure no será toomake capaz de progreso en la aplicación de actualización, ya que un número insuficiente de instancias en el dominio de actualización de hello está en buen estado. Este estado es tooas que se hace referencia una *implementación bloqueada*. Implementación de Hola para desbloquear revertir la actualización de Hola o aplicando una nueva actualización encima de hello producen errores en uno.

Una vez que ha recibido el servicio de Hola de tooupdate o actualización de solicitud inicial de Hola Hola controlador de tejido de Azure, puede iniciar las operaciones de mutación posteriores. Es decir, no es necesario toowait para saludo inicial operación toocomplete antes de empezar otra operación de mutación.

Iniciar una segunda operación de actualización mientras se está realizando la primera actualización de hello llevará a cabo una operación de reversión toohello similar. Si Hola segunda actualización está en modo automático, Hola primer dominio de actualización se actualizará inmediatamente, lo que probablemente ocasionará tooinstances desde varios dominios de actualización estén sin conexión en hello mismo momento dado.

Hello operaciones de mutación son las siguientes: [cambiar la configuración de implementación](https://msdn.microsoft.com/library/azure/ee460809.aspx), [actualizar implementación](https://msdn.microsoft.com/library/azure/ee460793.aspx), [estado de implementación de actualización](https://msdn.microsoft.com/library/azure/ee460808.aspx), [eliminar Implementación](https://msdn.microsoft.com/library/azure/ee460815.aspx), y [revertir actualización o actualizar](https://msdn.microsoft.com/library/azure/hh403977.aspx).

Las dos operaciones, [Get Deployment](https://msdn.microsoft.com/library/azure/ee460804.aspx) y [obtener propiedades del servicio de nube](https://msdn.microsoft.com/library/azure/ee460806.aspx), devuelve una marca de bloqueado Hola que puede ser examinado toodetermine si una operación de mutación se puede invocar en una implementación determinada.

En orden toocall Hola versión de estos métodos que devuelve la marca de hello bloqueada, debe establecer el encabezado de solicitud demasiado "x-ms-version: 2011-10-01" o una posterior. Para obtener más información acerca de los encabezados de control de versiones, consulte [Control de versiones de la administración del servicio](https://msdn.microsoft.com/library/azure/gg592580.aspx).

<a name="distributiondfroles"></a>

## <a name="distribution-of-roles-across-upgrade-domains"></a>Distribución de roles entre dominios de actualización
Azure distribuye las instancias de un rol uniformemente entre un número determinado de dominios de actualización, que se pueden configurar como parte del archivo de definición (.csdef) del servicio de Hola. Hola número máximo de dominios de actualización es 20 y Hola predeterminado es 5. Para obtener más información acerca de cómo toomodify Hola archivo de definición de servicio, consulte [esquema de definición de servicio de Azure (archivo de .csdef)](cloud-services-model-and-package.md#csdef).

Por ejemplo, si su rol tiene diez instancias, de forma predeterminada cada dominio de actualización contiene dos instancias. Si su rol tiene 14 instancias, cuatro Hola dominios de actualización contienen tres instancias y quinto dominio contiene dos.

Dominios de actualización se identifican mediante un índice basado en cero: Hola primer dominio de actualización tiene un identificador de 0 y el segundo dominio de actualización de hello tiene un Id. de 1 y así sucesivamente.

Hello diagrama siguiente ilustra cómo se distribuyen un servicio que contiene dos funciones al servicio de hello define dos dominios de actualización. servicio de Hello está ejecutando ocho instancias del rol web de Hola y nueve instancias de rol de trabajo de Hola.

![Distribución de dominios de actualización](media/cloud-services-update-azure-service/IC345533.png "Distribución de dominios de actualización")

> [!NOTE]
> Tenga en cuenta que Azure controla cómo se asignan las instancias en los dominios de actualización. No es posible toospecify las instancias que se asignan toowhich dominio.
>
>

## <a name="next-steps"></a>Pasos siguientes
[Cómo tooManage los servicios de nube](cloud-services-how-to-manage.md)  
[Cómo tooMonitor los servicios de nube](cloud-services-how-to-monitor.md)  
[Cómo tooConfigure los servicios de nube](cloud-services-how-to-configure.md)  
