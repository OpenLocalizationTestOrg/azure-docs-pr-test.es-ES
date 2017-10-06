---
title: aaaCreate y restaurar una copia de seguridad en servicios de BizTalk | Documentos de Microsoft
description: "Entre los Servicios de BizTalk se incluye Copias de seguridad y restauración. Obtenga información acerca de cómo toocreate y restaurar una copia de seguridad y determinar qué obtiene la copia de seguridad. MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 59f91173-4683-48df-abd5-41262bfce6df
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 32356ad870678fa5fd5bbbbf13d9377188f770a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="biztalk-services-backup-and-restore"></a>Servicios de BizTalk: copias de seguridad y restauración

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

Azure BizTalk Services incluye las capacidades de copia de seguridad y restauración. Este tema describe cómo toobackup y restauración de los servicios de BizTalk mediante Hola portal de Azure clásico.

También puede hacer una servicios de BizTalk mediante hello [API de REST de servicios de BizTalk](http://go.microsoft.com/fwlink/p/?LinkID=325584). 

> [!NOTE]
> Las conexiones híbridas no se copian de seguridad, independientemente de hello Edition. Debe volver a crear las conexiones híbridas.


## <a name="before-you-begin"></a>Introducción
* Puede que las copias de seguridad y restauración no estén disponible para todas las ediciones. Consulte [Servicios de BizTalk: gráfico de ediciones](biztalk-editions-feature-chart.md).
* Hola portal de Azure clásico puede crear una copia de seguridad a petición o crear una copia de seguridad programada. 
* Contenido de copia de seguridad puede ser restaurada toohello mismo BizTalk Service u tooa nueva BizTalk Service. toorestore Hola BizTalk Service mediante Hola debe eliminarse el mismo nombre, existentes BizTalk Service de Hola y Hola nombre debe estar disponible. Después de eliminar un BizTalk Service, puede tardar más tiempo del que deseaba Hola igual nombre toobe disponible. Si no puede esperar Hola igual nombre toobe disponible, a continuación, restaurar tooa nueva BizTalk Service.
* Servicios de BizTalk puede ser restaurada toohello misma edición o una edición superior. No se admite la restauración de servicios de BizTalk tooa edición anterior de cuando se realizó la copia de seguridad de hello.
  
    Por ejemplo, una copia de seguridad mediante Hola que edición básica se puede restaura toohello Premium Edition. Una copia de seguridad mediante Hola que Premium Edition no se puede restaura toohello Standard Edition.
* números de Control de EDI de Hola se copian la continuidad de toomaintain Hola de números de control. Si los mensajes se procesan después de la última copia de seguridad de hello, restaurar el contenido de esta copia de seguridad puede producir números de control duplicados.
* Si un lote tiene mensajes activos, procesar por lotes de hello **antes de** ejecuta una copia de seguridad. Al crear una copia de seguridad (según sea necesario o según se programe), no se almacenan nunca los mensajes en lotes. 
  
    **Si se realiza una copia de seguridad con mensajes activos en un lote, estos mensajes no se incluyen en la copia de seguridad y, por lo tanto, se pierden.**
* Opcional: Hola Portal de servicios de BizTalk, detenga las operaciones de administración.

## <a name="create-a-backup"></a>Creación de una copia de seguridad
Puede realizar una copia de seguridad en cualquier momento y controlarla por completo. Esta sección enumeran Hola pasos toocreate copias de seguridad con hello Azure clásico portal, incluidos:

[Copia de seguridad bajo demanda](#backupnow)

[Programación de una copia de seguridad](#backupschedule)

#### <a name="backupnow"></a>Copia de seguridad bajo demanda
1. Hola portal de Azure clásico, seleccione **servicios de BizTalk**, y, a continuación, seleccione Hola BizTalk Service desea toobackup.
2. Hola **panel** ficha, seleccione **copia de seguridad** final Hola de página Hola.
3. Escriba un nombre para la copia de seguridad. Por ejemplo, escriba *myBizTalkService*BU*Fecha*.
4. Elija una cuenta de almacenamiento blob y copia de seguridad de hello seleccione marca de verificación toostart Hola.

Una vez completada la copia de seguridad de hello, se crea un contenedor con nombre de copia de seguridad de Hola que especifique en la cuenta de almacenamiento de Hola. Este contenedor contiene la configuración de la copia de seguridad del servicio de BizTalk.

#### <a name="backupschedule"></a>Programación de una copia de seguridad
1. Hola portal de Azure clásico, seleccione **servicios de BizTalk**, seleccione Hola nombre de BizTalk Service que desee copia de seguridad de tooschedule hello y, a continuación, seleccione hello **configurar** ficha.
2. Conjunto hello **estado de copia de seguridad** demasiado**automática**. 
3. Seleccione hello **cuenta de almacenamiento** toostore Hola copia de seguridad, escriba Hola **frecuencia** toocreate Hola copias de seguridad y cuánto tiempo tookeep Hola (**días de retención**):
   
    ![][AutomaticBU]
   
    **Notas**     
   
   * En **días de retención**, período de retención de hello debe ser mayor que la frecuencia de copia de seguridad de Hola.
   * Seleccione **mantenga siempre al menos una copia de seguridad**, incluso si ya ha transcurrido el período de retención de Hola.
4. Seleccione **Guardar**.

Cuando se ejecuta un trabajo de copia de seguridad programado, crea un contenedor (datos de copia de seguridad de toostore) en la cuenta de almacenamiento de Hola que especificó. Hola nombre del contenedor de Hola se denomina *BizTalk Service Name-date-time*. 

Si muestra un panel de BizTalk Service Hola un **error** estado:

![Estado de la última copia de seguridad programada][BackupStatus] 

vínculo de Hello abre Hola registros de operaciones de administración de servicios toohelp solucionar problemas. Consulte [Servicios de BizTalk: solución de problemas mediante registros de operaciones](http://go.microsoft.com/fwlink/p/?LinkId=391211).

## <a name="restore"></a>Restauración
Puede restaurar las copias de seguridad de portal de Azure clásico de Hola o de hello [API de REST de servicios de BizTalk restaurar](http://go.microsoft.com/fwlink/p/?LinkID=325582). Esta sección enumeran Hola pasos toorestore mediante el portal clásico de Hola.

#### <a name="before-restoring-a-backup"></a>Antes de restaurar una copia de seguridad
* Se pueden especificar los nuevos almacenes de seguimiento, archivado y supervisión al restaurar un servicio de BizTalk.
* Hola se restauran los mismos datos en tiempo de ejecución de EDI. copia de seguridad de Hello en tiempo de ejecución de EDI almacena números de control de Hola. números de control de Hello restaurar están en orden desde el momento de Hola de copia de seguridad de Hola. Si los mensajes se procesan después de la última copia de seguridad de hello, restaurar el contenido de esta copia de seguridad puede producir números de control duplicados.

#### <a name="restore-a-backup"></a>Restauración de una copia de seguridad
1. Hola portal de Azure clásico, seleccione **New** > **servicios de aplicaciones** > **BizTalk Service** > **restaurar** :
   
    ![Restauración de una copia de seguridad][Restore]
2. En **dirección URL de la copia de seguridad**, seleccione el icono de carpeta de Hola y expanda la cuenta de almacenamiento de Azure de Hola que almacenes Hola copia de seguridad de configuración de BizTalk Service. Expanda el contenedor de Hola y en el panel derecho de hello, seleccione Hola correspondiente archivo .txt de copia de seguridad. 
   <br/><br/>
   seleccione **Open**(Abrir).
3. En hello **restaurar el servicio de BizTalk** página, escriba un **el nombre del servicio de BizTalk** y compruebe hello **dirección URL del dominio**, **edición**y **Región** para hello restaura BizTalk Service. **Crear una nueva instancia de base de datos SQL** para hello base de datos de seguimiento:
   
    ![][RestoreBizTalkService]
   
    Seleccione la flecha siguiente Hola.
4. Comprobar nombre de Hola de base de datos SQL de hello, escriba Hola servidor físico donde se creará la base de datos SQL de Hola y un nombre de usuario y una contraseña para ese servidor.

    Si desea edición de base de datos SQL tooconfigure hello, tamaño y otras propiedades, seleccione **configurar opciones de base de datos avanzada**. 

    Seleccione la flecha siguiente Hola.

1. Crear una nueva cuenta de almacenamiento o escriba una cuenta de almacenamiento existente Hola BizTalk Service.
2. Seleccione Hola marca de verificación toostart Hola restaurar.

Una vez que se complete correctamente la restauración de hello, aparece un nuevo BizTalk Service en un estado suspendido en la página de servicios de BizTalk de Hola Hola portal de Azure clásico.

### <a name="postrestore"></a>Después de restaurar una copia de seguridad
Hello BizTalk Service se restaura siempre en un **Suspended** estado. En este estado, puede realizar los cambios de configuración antes de hello nuevo entorno es funcional, incluyendo:

* Si ha creado aplicaciones de BizTalk Service mediante Hola SDK de servicios de BizTalk de Azure, deberá credenciales de Control de acceso (ACS) de tootooupdate hello en esos toowork de aplicaciones con el entorno de hello restaurar.
* Restaurar un tooreplicate un entorno de BizTalk Service existente de BizTalk Service. En esta situación, si hay contratos configurados en el portal de servicios de BizTalk original de Hola que use una carpeta de origen FTP, deberá tooupdate contratos de hello en hello recién restaurado entorno toouse una carpeta FTP de origen diferente. En caso contrario, puede haber dos contratos diferentes intentar toopull Hola mismo mensaje.
* Si ha restaurado toohave varios entornos de BizTalk Service, asegúrese de que el destino correcto del entorno hello en aplicaciones de Visual Studio de hello, cmdlets de PowerShell, las API de REST o API de OM de administración de socios comerciales.
* Es una copias de seguridad de buena práctica tooconfigure automatizada en el entorno del servicio de BizTalk de hello recién restaurado.

Hola toostart BizTalk Service Hola portal de Azure clásico, seleccione Hola restaura BizTalk Service y seleccione **reanudar** en la barra de tareas de Hola. 

## <a name="what-gets-backed-up"></a>¿Qué se incluye en la copia de seguridad?
Cuando se crea una copia de seguridad, hello siguientes elementos se copian:

<table border="1"> 
<tr bgcolor="FAF9F9">
<th> </th>
<TH>Elementos incluidos en la copia de seguridad</TH> 
</tr> 
<tr>
<td colspan="2">
 <strong>Portal de Azure BizTalk Services</strong></td>
</tr> 
<tr>
<td>Configuración y tiempo de ejecución</td> 
<td>
<ul>
<li>Detalles del asociado y perfil</li>
<li>Acuerdos de socios</li>
<li>Ensamblados personalizados implementados</li>
<li>Puentes implementados</li>
<li>Certificados</li>
<li>Transformaciones implementadas</li>
<li>Procesos</li>
<li>Plantillas creado y guardado en hello Portal de servicios de BizTalk</li>
<li>Asignaciones X12 ST01 y GS01</li>
<li>Números de control (EDI)</li>
<li>Valores MIC de mensaje AS2</li>
</ul>
</td>
</tr> 

<tr>
<td colspan="2">
 <strong>Servicio Azure BizTalk</strong></td>
</tr> 
<tr>
<td>Certificado SSL</td> 
<td>
<ul>
<li>Datos del certificado SSL</li>
<li>Contraseña del certificado SSL</li>
</ul>
</td>
</tr> 
<tr>
<td>Configuración del servicio de BizTalk</td> 
<td>
<ul>
<li>Recuento de unidades de escalado</li>
<li>Edition</li>
<li>Versión del producto</li>
<li>Región/Centro de datos</li>
<li>Clave y espacio de nombres del servicio de control de acceso (ACS)</li>
<li>Cadena de conexión de la base de datos de seguimiento</li>
<li>Cadena de conexión de la cuenta de almacenamiento de archivado</li>
<li>Cadena de conexión de la cuenta de almacenamiento de supervisión</li>
</ul>
</td>
</tr> 
<tr>
<td colspan="2">
 <strong>Elementos adicionales</strong></td>
</tr> 
<tr>
<td>Tracking Database</td> 
<td>Cuando se crea Hola BizTalk Service, se especifican detalles de la base de datos de seguimiento de hello, incluidos el nombre de base de datos de seguimiento de Hola y Hola servidor de base de datos de SQL Azure. Hola base de datos de seguimiento no se copia automáticamente.
<br/><br/>
<strong>Importante</strong><br/>
Si Hola base de datos de seguimiento se elimina y Hola necesidades de base de datos recuperadas, debe existir una copia de seguridad anterior. Si no existe una copia de seguridad, base de datos de seguimiento de Hola y sus datos no son recuperables. En esta situación, cree una nueva base de datos de seguimiento con hello mismo nombre de base de datos. Además, se recomienda la replicación geográfica.</td>
</tr> 
</table>

## <a name="next"></a>Pasos siguientes
Servicios de BizTalk de Azure toocreate en hello Azure clásico, vaya demasiado[servicios de BizTalk: portal clásico de aprovisionamiento con Azure](http://go.microsoft.com/fwlink/p/?LinkID=302280). toostart crear aplicaciones, vaya demasiado[Azure BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=235197).

## <a name="see-also"></a>Otras referencias
* [Copia de seguridad del servicio de BizTalk](http://go.microsoft.com/fwlink/p/?LinkID=325584)
* [Restauración del servicio de BizTalk a partir de una copia de seguridad](http://go.microsoft.com/fwlink/p/?LinkID=325582)
* [Servicios de BizTalk: gráfico de las ediciones Developer, Basic, Standard y Premium](http://go.microsoft.com/fwlink/p/?LinkID=302279)
* [Servicios de BizTalk: aprovisionamiento con el Portal de Azure clásico](http://go.microsoft.com/fwlink/p/?LinkID=302280)
* [Servicios de BizTalk: gráfico del estado de aprovisionamiento](http://go.microsoft.com/fwlink/p/?LinkID=329870)
* [Servicios de BizTalk: pestañas Panel, Monitor y Escala](http://go.microsoft.com/fwlink/p/?LinkID=302281)
* [Servicios de BizTalk: limitaciones](http://go.microsoft.com/fwlink/p/?LinkID=302282)
* [Servicios de BizTalk: nombre del emisor y clave del emisor](http://go.microsoft.com/fwlink/p/?LinkID=303941)
* [¿Cómo puedo comenzar a utilizar Hola SDK de servicios de BizTalk de Azure](http://go.microsoft.com/fwlink/p/?LinkID=302335)

[BackupStatus]: ./media/biztalk-backup-restore/status-last-backup.png
[Restore]: ./media/biztalk-backup-restore/restore-ui.png
[AutomaticBU]: ./media/biztalk-backup-restore/AutomaticBU.png
[RestoreBizTalkService]: ./media/biztalk-backup-restore/RestoreBizTalkServiceWindow.png

