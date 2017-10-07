---
title: aaaCreate servicios de BizTalk de Azure en hello portal de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooprovision o crear servicios de BizTalk de Azure en hello portal de Azure; MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 3ad18876-a649-40d6-9aa0-1509c1d62c43
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 6781cadada8ac9c84e1fe045d2b0f995811f75b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-biztalk-services-using-hello-azure-portal"></a>Crear servicios de BizTalk mediante Hola portal de Azure

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]


> [!TIP]
> toosign en toohello portal de Azure, necesitará una cuenta de Azure y suscripción de Azure. En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos. Consulte [Evaluación gratuita de Azure](http://go.microsoft.com/fwlink/p/?LinkID=239738).


## <a name="CreateService"></a>Creación de un servicio de BizTalk
Función hello la edición que elija, no todas las configuraciones de BizTalk Service pueden estar disponibles.

1. Inicie sesión en toohello [portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=213885).
2. En el panel de navegación de la parte inferior de hello, seleccione **NEW**:  
   ![Seleccione el botón nuevo Hola][NEWButton]
3. Seleccione **APP SERVICES** > **SERVICIO DE BIZTALK** > **CREACIÓN PERSONALIZADA**:  
   ![Seleccione Servicio de BizTalk y seleccione Custom Create][NewBizTalkService]
4. Escriba la configuración de servicio de BizTalk de hello:
   
    <table border="1">
    <tr>
    <td><strong>Nombre del servicio de BizTalk</strong></td>
    <td>Puede escribir cualquier nombre pero sea específico. Estos son algunos ejemplos:<br/><br/>
    <em>mycompany</em>.biztalk.windows.net<br/>
    <em>mycompanymyapplication</em>.biztalk.windows.net<br/>
    <em>myapplication</em>.biztalk.windows.net<br/><br/>". biztalk.windows.net" es nombre toohello agregadas automáticamente que especifique. Esto crea una dirección URL que es usado tooaccess su BizTalk del servicio, como <strong>https://<em>myapplication</em>. biztalk.windows.net</strong>.
    </td>
    </tr>
    <tr>
    <td><strong>Edición</strong></td>
    <td>Si se encuentra en fase de pruebas y desarrollo de hello, elija <strong>Developer</strong>. Si se encuentra en fase de producción de hello, use hello <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302279">servicios de BizTalk: gráfico de ediciones</a> toodetermine si <strong>Premium</strong>, <strong>estándar</strong>, o <strong>Basic</strong>es Hola opción correcta para su escenario de negocio.
    </td>
    </tr>
    <tr>
    <td><strong>Región</strong></td>
    <td>Seleccione Hola región geográfica toohost su BizTalk Service.</td>
    </tr>
    <tr>
    <td><strong>URL de dominio</strong></td>
    <td><strong>Opcional</strong>. De forma predeterminada, es la dirección URL del dominio de Hola <em>YourBizTalkServiceName</em>. biztalk.windows.net. También se puede escribir un dominio personalizado. Por ejemplo, si el dominio es <em>contoso</em>, puede escribir: <br/><br/>
    <em>MyCompany</em>.contoso.com<br/>
    <em>MyCompanyMyApplication</em>.contoso.com<br/>
    <em>MyApplication</em>.contoso.com<br/>
    <em>YourBizTalkServiceName</em>.contoso.com<br/>
    </td>
    </tr>
    </table>
Seleccione la flecha siguiente Hola.
5. Escriba Hola almacenamiento y la configuración de la base de datos:  <table border="1">
    <tr>
    <td><strong>Cuenta de almacenamiento de supervisión y archivado</strong></td>
    <td>Seleccione una cuenta de almacenamiento existente o cree una nueva cuenta de almacenamiento. <br/><br/>Si crea una nueva cuenta de almacenamiento, escriba Hola <strong>nombre de la cuenta de almacenamiento</strong>.</td>
    </tr>
    <tr>
    <td><strong>Base de datos de seguimiento</strong></td>
    <td>Si usa una Base de datos SQL de Azure existente, no puede usarla otro Servicio de BizTalk. Necesita el nombre de inicio de sesión de Hola y la contraseña que especificó cuando se creó ese servidor de base de datos de SQL Azure.<br/><br/><strong>Sugerencia</strong> crear base de datos de seguimiento de Hola y cuenta de almacenamiento de supervisión y archivado en Hola la misma región como Hola BizTalk Service.</td>
    </tr>
    </table>
Seleccione la flecha siguiente Hola.
6. Escriba la configuración de la base de datos de hello:  <table border="1">
    <tr>
    <td><strong>Name</strong></td>
    <td>Disponible cuando <strong>crear una nueva instancia de base de datos SQL</strong> está seleccionado en la pantalla de bienvenida anterior.
    <br/><br/>
Escriba un toobe de nombre de base de datos SQL utilizado por su BizTalk Service.</td>
    </tr>
    <tr>
    <td><strong>Servidor</strong></td>
    <td>Disponible cuando <strong>crear una nueva instancia de base de datos SQL</strong> está seleccionado en la pantalla de bienvenida anterior.
    <br/><br/>
Seleccione un servidor de SQL Database existente o cree uno nuevo.</td>
    </tr>
    <tr>
    <td><strong>Nombre de inicio de sesión del servidor</strong></td>
    <td>Escriba el nombre de usuario de inicio de sesión de Hola.</td>
    </tr>
    <tr>
    <td><strong>Contraseña de inicio de sesión del servidor</strong></td>
    <td>Escriba la contraseña de inicio de sesión de Hola.</td>
    </tr>
    <tr>
    <td><strong>Región</strong></td>
    <td>Disponible cuando se selecciona <strong>Crear una nueva instancia de SQL Database</strong>. Seleccione toohost de región geográfica de hello en la base de datos de SQL.</td>
    </tr>
    </table>

Seleccione a Hola marca de verificación toocomplete Hola asistente. aparece el icono de progreso de Hello:  
![El icono de progreso aparece cuando se completa][ProgressComplete]

Cuando haya finalizado, Hola servicio de BizTalk de Azure se haya creado y listo para las aplicaciones. configuración predeterminada de Hello es suficientes. Si desea que la configuración predeterminada de toochange hello, seleccione **servicios de BIZTALK** en Hola panel de navegación izquierdo y, a continuación, seleccione su BizTalk Service. Opciones de configuración adicionales se muestran en hello [pestañas panel, Monitor y escala](biztalk-dashboard-monitor-scale-tabs.md) en la parte superior de Hola.

Según el estado de Hola de hello BizTalk Service, hay algunas operaciones que no se puede completar. Para obtener una lista de estas operaciones, vaya demasiado[gráfico de estado de servicios de BizTalk](biztalk-service-state-chart.md).

## <a name="post-provisioning-steps"></a>Pasos posteriores al aprovisionamiento
* [Instalar certificado de hello en un equipo local](#InstallCert)
* [Incorporación de un certificado listo para producción](#AddCert)
* [Obtener el espacio de nombres de Control de acceso de Hola](#ACS)

#### <a name="InstallCert"></a>Instalar certificado de hello en un equipo local
Como parte del aprovisionamiento del Servicio de BizTalk, se crea un certificado autofirmado y se asocia a su suscripción del Servicio de BizTalk. Debe descargar este certificado e instalarlo en los equipos desde donde se implemente aplicaciones de BizTalk Service o enviar mensajes tooa punto de conexión de BizTalk Service.

1. Inicie sesión en toohello [portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=213885).
2. Seleccione **servicios de BIZTALK** en Hola panel de navegación izquierdo y, a continuación, seleccione la suscripción de BizTalk Services.
3. Seleccione hello **panel** ficha.
4. Seleccione **Descargar certificado SSL**:  
   ![Modificar certificado SSL][QuickGlance]
5. Haga doble clic en el certificado de Hola y ejecutar mediante Hola Asistente tooinstall Hola de certificado. Asegúrese de instalar el certificado de hello en hello **entidades emisoras de certificados raíz de confianza** almacenar.

#### <a name="AddCert"></a>Incorporación de un certificado listo para producción
Hola certificado de firma automática que se crea automáticamente al crear servicios de BizTalk está diseñado para su uso en entornos de desarrollo únicamente. Para escenarios de producción, reemplácelo por un certificado listo para producción.

1. En hello **panel** ficha, seleccione **certificado SSL de actualización**.
2. Examinar el certificado SSL de privado tooyour (*CertificateName*.pfx) que incluya el nombre de BizTalk Service, escriba la contraseña de hello y, a continuación, haga clic en la casilla de verificación Hola.

#### <a name="ACS"></a>Obtener el espacio de nombres de Control de acceso de Hola
1. Inicie sesión en toohello [portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=213885).
2. Seleccione **servicios de BIZTALK** en Hola panel de navegación izquierdo y, a continuación, seleccione su BizTalk Service.
3. En la barra de tareas de hello, seleccione **información de conexión**:  
   ![Seleccione Connection Information][ACSConnectInfo]
4. Copiar valores de Control de acceso de Hola.

Cuando implementa un proyecto de servicio de BizTalk desde Visual Studio, debe escribir este espacio de nombres del servicio de control de acceso. espacio de nombres de Control de acceso de Hola se crea automáticamente para su BizTalk Service.

valores de Control de acceso de Hola se pueden usar con cualquier aplicación. Cuando se crea el servicios de BizTalk de Azure, este espacio de nombres de Control de acceso controla la autenticación de hello con la implementación de BizTalk Service. Si desea toochange Hola suscripción o administrar el espacio de nombres de hello, seleccione **ACTIVE DIRECTORY** en Hola panel de navegación izquierdo y, a continuación, seleccione el espacio de nombres. barra de tareas de Hola enumera las opciones.

Haga clic en **administrar** abre Hola Portal de administración de Control de acceso. En el Portal de administración de Control de acceso de hello, Hola usa BizTalk Service **identidades de servicio**:  
![Identidades de servicio de ACS en hello Portal de administración de Control de acceso][ACSServiceIdentities]

Hola identidad de servicio de Control de acceso es un conjunto de credenciales que permite que las aplicaciones o los clientes tooauthenticate directamente con el Control de acceso y recibir un token.

> [!IMPORTANT]
> usa Hello BizTalk Service **propietario** para la identidad del servicio predeterminado Hola y Hola **contraseña** valor. Si se usa el valor de clave simétrica de hello en lugar de hello valor de contraseña, hello siguiente error puede producirse.<br/><br/>*No se pudo conectar la cuenta de servicio de administración de Control de acceso de toohello con hello especificada las credenciales*
> 
> 

[Administración del espacio de nombres ACS](https://msdn.microsoft.com/library/azure/hh674478.aspx) muestra algunas directrices y recomendaciones.

## <a name="requirements-explained"></a>Requisitos explicados
Estos requisitos no aplican toohello edición gratuita.

<table border="1">
<tr bgcolor="FAF9F9">
        <td><strong>Lo que necesita</strong></td>
        <td><strong>Por qué es necesario</strong></td>
</tr>
<tr>
<td>Suscripción de Azure</td>
<td>suscripción de Hello determina quién puede iniciar sesión en toohello portal de Azure. titular de la cuenta de Hello crea la suscripción de hello en <a HREF="https://account.windowsazure.com/Subscriptions"> suscripciones de Azure</a>.
<br/><br/>
Hola cuenta de Azure puede tener varias suscripciones y puede administrarse por alguien que se permite. Por ejemplo, el titular de la cuenta de Azure crea una suscripción denominada <em>BizTalkServiceSubscription</em> y proporciona Hola administradores de BizTalk dentro de su empresa (por ejemplo, ContosoBTSAdmins@live.com) tener acceso a toothis suscripción. En este escenario, administradores de BizTalk Server Hola inicia sesión en toohello portal de Azure y tiene los servicios de hello hospedado tooall completos de administrador derechos en la suscripción de hello, incluidos los servicios de BizTalk de Azure. Administradores de BizTalk Server Hello no son titulares de la cuenta de Azure de hello y, por tanto, no tiene acceso a información de facturación de tooany.
<br/><br/>
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=267577">Administrar suscripciones y cuentas de almacenamiento en el portal de Azure hello</a> proporciona más información.
</td>
</tr>
<tr>
<td>Azure SQL Database</td>
<td>Almacena Hola tablas, vistas y procedimientos almacenados utilizados por BizTalk Service, incluidos los datos de seguimiento de Hola Hola.
<br/><br/>
Cuando cree un servicio de BizTalk, puede usar un servidor de Azure SQL Server existente, una Base de datos SQL de Azure existente, o bien puede crear automáticamente un servidor o una base de datos nuevos.
<br/><br/>
Hola escala de base de datos SQL se configura automáticamente. Por lo general, la escala predeterminada de hello es suficiente para una BizTalk Service. Cambiar escala Hola afecta precios. Consulte <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=234930">Cuentas y facturación en Azure SQL Database</a>
<br/><br/>
<strong>Notas</strong>
<br/>
<ul>
<li> Cuando crea una nueva Base de datos SQL o SQL Server de Azure, Servicios de Azure se habilita automáticamente. Hola BizTalk Service requiere que los servicios de Azure habilitarse.</li>
<li>Si crea una nueva base de datos de SQL Azure en un servidor de SQL Azure existente, Hola reglas de firewall de hello Server no se cambian. Como resultado, es posible que otros servicios de Azure no se permiten las bases de datos del servidor de acceso toohello.</li>
</ul>
</td>
</tr>
<tr>
<td>Espacio de nombres del servicio de control de acceso de Azure</td>
<td>Autentica con los Servicios de BizTalk de Azure. Cuando implementa un proyecto de servicio de BizTalk desde Visual Studio, debe escribir este espacio de nombres del servicio de control de acceso. Cuando se crea un BizTalk Service, se crea automáticamente el espacio de nombres de Control de acceso de Hola.</td>
</tr>

<tr>
<td>Cuenta de almacenamiento de Azure</td>
<td>Proporciona acceso tootables, blobs y colas utilizadas por el texto siguiente Hola de BizTalk Service toosave:

<ul>
<li>Los archivos de registro de ese Hola monitor BizTalk Service. Hola supervisando resultados también se muestra en hello **supervisión** ficha Hola portal de Azure.</li>
<li>Al crear un X12 o acuerdo de AS2 entre socios comerciales, puede habilitar propiedades de mensaje de Hola archivado características toostore. Estos datos se guardan en hello cuenta de almacenamiento.</li>
</ul>
<br/>
Cuando crea un servicio de BizTalk, puede usar una cuenta de almacenamiento existente o puede crear automáticamente una nueva.
<br/><br/>
configuración de almacenamiento predeterminada de Hello es suficientes para un BizTalk Service.
<br/><br/>
Cuando crea una cuenta de almacenamiento, se crean automáticamente una clave primaria y una clave secundaria. Estas claves controlan el acceso tooyour cuenta de almacenamiento. Hola BizTalk Service usa automáticamente Hola Primary Key.
<br/><br/>
Consulte <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285671">Almacenamiento</a> para más información.
</td>
</tr>

<tr>
<td>Certificado privado de SSL</td>
<td>
Cuando se crea un servicio de Azure BizTalk, también se crea una URL HTTPS que incluye su nombre de Servicio de BizTalk. Esta dirección URL es toouse configurada automáticamente un certificado autofirmado sólo del desarrollo. Para producción, necesita un certificado SSL privado.
<br/><br/>
<strong>Información importante sobre el certificado SSL</strong>

<ul>
<li>fecha de expiración del certificado de Hello debe ser inferior a 5 años.</li>
<li>Todos los certificados privados requieren una contraseña. Apréndase esta contraseña y, como procedimiento recomendado, comparta esta contraseña con sus administradores.</li>
<li>Los certificados autofirmados se utilizan en un entorno de prueba o de desarrollo. Cuando se usan certificados autofirmados, importar el almacén de certificados personales de hello certificados tooyour y Hola almacén de certificados de entidades de certificación raíz de confianza.</li>
</ul>
<br/>Cuando se envía la entidad de certificación de tooyour de solicitud certificado de producción de hello, dar Hola propiedades de certificado siguientes:
<br/>

<ul>
<li><strong>Uso mejorado de clave</strong>: como mínimo, Azure BizTalk Services requiere la autenticación de servidor.</li>
<li><strong>Nombre común</strong>: escriba el nombre de dominio completo (FQDN) de Hola de su URL de servicio de BizTalk de Azure. Consulte <a HREF="#CreateService">Crear un servicio de BizTalk</a> en este artículo.</li>
</ul>
<br/>
Puede agregarse un certificado nuevo o diferente después de crea Hola BizTalk Service.
</td>
</tr>
</table>
<!---Loc Comment: Please, check link [Create a BizTalk Service] since it is not redirecting tooany location.--->



## <a name="hybrid-connections"></a>conexiones híbridas
Cuando se crea un servicio de BizTalk de Azure, Hola **conexiones híbridas** pestaña está disponible:

![Pestaña Conexiones híbridas][HybridConnectionTab]

Las conexiones híbridas son tooconnect usado un Azure sitio Web o servicio móvil de Azure tooany local recursos que usa un puerto TCP estático, como SQL Server, MySQL, las API de Web HTTP, servicios móviles y mayoría de los servicios Web personalizados.  Las conexiones híbridas y Hola servicio del adaptador de BizTalk son diferentes. Hola servicio del adaptador de BizTalk es el sistema de línea de negocio (LOB) de tooconnect usa servicios de BizTalk de Azure tooan local.

 Vea [conexiones híbridas](integration-hybrid-connection-overview.md) toolearn más, incluidas la creación y administración de conexiones híbridas.

## <a name="next-steps"></a>Pasos siguientes
Ahora que se crea un BizTalk Service, familiarícese con hello diferentes [servicios de BizTalk: pestañas panel, Monitor y escala](biztalk-dashboard-monitor-scale-tabs.md). Su servicio de BizTalk está listo para las aplicaciones. toostart crear aplicaciones, vaya demasiado[Azure BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=235197).

## <a name="see-also"></a>Otras referencias
* [Servicios de BizTalk: Gráfico de ediciones](biztalk-editions-feature-chart.md)<br/>
* [BizTalk Services: gráfico de estado](biztalk-service-state-chart.md)<br/>
* [Servicios de BizTalk: copias de seguridad y restauración](biztalk-backup-restore.md)<br/>
* [Servicios de BizTalk: limitaciones](biztalk-throttling-thresholds.md)<br/>
* [Servicios de BizTalk: nombre del emisor y clave del emisor](biztalk-issuer-name-issuer-key.md)<br/>
* [¿Cómo puedo comenzar a utilizar Hola SDK de servicios de BizTalk de Azure](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [Conexiones híbridas](integration-hybrid-connection-overview.md)

[NewBizTalkService]: ./media/biztalk-provision-services/WABS_NewBizTalkService.png
[NEWButton]: ./media/biztalk-provision-services/WABS_New.png
[ProgressComplete]: ./media/biztalk-provision-services/WABS_ProgressComplete.png
[ACSConnectInfo]: ./media/biztalk-provision-services/WABS_ACSConnectInformation.png
[QuickGlance]: ./media/biztalk-provision-services/WABS_QuickGlance.png
[ACSServiceIdentities]: ./media/biztalk-provision-services/WABS_ACSServiceIdentities.png
[HybridConnectionTab]: ./media/biztalk-provision-services/WABS_HybridConnectionTab.png
