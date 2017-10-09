---
title: Notas de aaaRelease de servicios de BizTalk de Azure | Documentos de Microsoft
description: Hola de listas de los problemas conocidos para los servicios de BizTalk de Azure
services: biztalk-services
documentationcenter: 
author: msftman
manager: erikre
editor: 
ms.assetid: f4906fdc-4cd9-4a57-a007-a88c2e51a18f
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2016
ms.author: deonhe
ms.openlocfilehash: ea53d6c40ed58badf4141453dc77d28dcfc6407f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="release-notes-for-azure-biztalk-services"></a>Notas de la versión de Azure BizTalk Services

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

notas de la versión de Hola de hello Microsoft Azure BizTalk Services contienen Hola problemas conocidos de esta versión.

## <a name="whats-new-in-hello-november-update-of-biztalk-services"></a>Novedades de la actualización de noviembre de hello de servicios de BizTalk
* Cifrado en reposo puede habilitarse en hello Portal de servicios de BizTalk. Consulte [Habilitación del cifrado en reposo en el Portal de Servicios de BizTalk](https://msdn.microsoft.com/library/azure/dn874052.aspx).

## <a name="update-history"></a>Historial de actualizaciones
### <a name="october-update"></a>Actualización de octubre
* Se admiten cuentas de la organización:  
  * **Escenario**: ha registrado la implementación de un servicio de BizTalk mediante una cuenta Microsoft (como user@live.com). En este escenario, Account de Microsoft solo los usuarios pueden administrar Hola BizTalk Service mediante el portal de servicios de BizTalk Hola. No se puede usar una cuenta de la organización.  
  * **Escenario**: ha registrado la implementación de un servicio de BizTalk mediante una cuenta de organización en Azure Active Directory (como user@fabrikam.com o user@contoso.com). En este escenario, solo los usuarios de Azure Active Directory de hello puede administrar la misma organización Hola BizTalk Service mediante el portal de servicios de BizTalk Hola. No se puede usar una cuenta Microsoft.  
* Cuando creas un BizTalk Service Hola portal de Azure clásico, se registra automáticamente en hello Portal de servicios de BizTalk.
  * **Escenario**: Regístrese en hello portal de Azure clásico, cree un BizTalk Service y, a continuación, seleccione **administrar** para hello primera vez. Cuando se abre el portal de servicios de BizTalk de hello, Hola BizTalk Service se registra automáticamente y está listo para las implementaciones de.  
    Vea [registrar y actualizar una implementación de servicio de BizTalk en el Portal de servicios de BizTalk de Hola](https://msdn.microsoft.com/library/azure/hh689837.aspx).  

### <a name="august-14-update"></a>Actualización del 14 de agosto
* Ahora se desvinculan acuerdo y puente desacoplamiento: puentes y acuerdos de socios comerciales en hello Portal de servicios de BizTalk. Ahora cree acuerdos y puentes de forma independiente y en tiempo de ejecución puentes resolver el acuerdo de tooan basada en valores de hello de mensaje de bienvenida de EDI. Vea [Crear acuerdos en Azure BizTalk Services](https://msdn.microsoft.com/library/azure/hh689908.aspx), [Crear un puente EDI mediante el portal de BizTalk Services](https://msdn.microsoft.com/library/azure/dn793986.aspx), [Creación de un puente AS2 mediante el portal de BizTalk Services](https://msdn.microsoft.com/library/azure/dn793993.aspx) y [¿Cómo resuelven los puentes acuerdos en tiempo de ejecución?](https://msdn.microsoft.com/library/azure/dn794001.aspx)  
* plantillas de toocreate de opción de Hola de acuerdos ya no está disponible.  
* Acuerdo de envío de hello, ahora puede especificar conjuntos de delimitadores distintos para cada esquema. Esta configuración se especifica en la configuración del protocolo del contrato de envío. Para más información, vea [Crear un acuerdo X12 en Azure BizTalk Services](https://msdn.microsoft.com/library/azure/hh689847.aspx) y [Crear un acuerdo EDIFACT en Azure BizTalk Services](https://msdn.microsoft.com/library/azure/dn606267.aspx). Dos nuevas entidades también se agregan toohello API OM TPM para hello mismo propósito. Vea [X12DelimiterOverrides](https://msdn.microsoft.com/library/azure/dn798749.aspx) y [EDIFACTDelimiterOverride](https://msdn.microsoft.com/library/azure/dn798748.aspx).  
* Ahora se admiten construcciones XSD estándar, incluidos los tipos derivados. Vea [Uso de construcciones XSD estándar en las asignaciones](https://msdn.microsoft.com/library/azure/dn793987.aspx) y [Uso de tipos derivados en escenarios y ejemplos de asignaciones](https://msdn.microsoft.com/library/azure/dn793997.aspx).  
* AS2 admite nuevos algoritmos MIC para la firma del mensaje y nuevos algoritmos de cifrado. Consulte [Crear un contrato AS2 en Servicios de BizTalk de Azure](https://msdn.microsoft.com/library/azure/hh689890.aspx).  
  ## <a name="know-issues"></a>Problemas conocidos

### <a name="connectivity-issues-after-biztalk-services-portal-update"></a>Problemas de conectividad después de la actualización del Portal de Servicios de BizTalk
  Si tiene Hola abrir el Portal de servicios de BizTalk mientras se actualicen los servicios de BizTalk tooroll en cambia toohello servicio, es posible que tenga problemas de conectividad con hello Portal de servicios de BizTalk.  
  Como alternativa, puede reiniciar el Explorador de hello, eliminar la memoria caché del explorador de Hola o iniciar el portal de hello en modo privado.  

### <a name="visual-studio-ide-cannot-locate-hello-artifact-if-you-click-an-error-or-warning-in-a-biztalk-services-project"></a>IDE de Visual Studio no puede encontrar el artefacto de hello si hace clic en un error o advertencia en un proyecto de servicios de BizTalk
Instalar Visual Studio 2012 Update 3 RC 1 Hola toofix Hola.  

### <a name="custom-binding-project-reference"></a>Referencia al proyecto de enlace personalizado
Considere la posibilidad de hello después situaciones con un proyecto de servicios de BizTalk en una solución de Visual Studio:  

* En Hola la misma solución de Visual Studio, hay un proyecto de servicios de BizTalk y un enlace personalizado. Hola proyecto de BizTalk Service tiene un archivo de proyecto de referencia toothis enlace personalizado.
* Hola proyecto de BizTalk Service tiene un referencia tooa enlace/comportamiento personalizado DLL.

Solución en Visual Studio se 'Compilación' hello correctamente. A continuación, 'Rebuild' o 'Limpiar' solución Hola. Después de eso, al volver a generar o limpiar de nuevo, Hola después de error:  
  No se puede toocopy archivo <Path tooDLL> too"bin\Debug\FileName.dll". proceso de Hello no puede tener acceso a archivo hello 'bin\Debug\FileName.dll' porque está siendo utilizado por otro proceso.  

#### <a name="workaround"></a>Solución alternativa
* Si [Visual Studio 2012 Update 3](https://www.microsoft.com/download/details.aspx?id=39305) está instalado, tienes que Hola dos opciones siguientes:
  
  * Reiniciar Visual Studio, o
  * Solución de Hola de reinicio. A continuación, realizar solo una compilación en la solución de Hola.  
* Si [Visual Studio 2012 Update 3](https://www.microsoft.com/download/details.aspx?id=39305) no es instalado, abra el Administrador de tareas, haga clic en la pestaña de procesos de hello, haga clic en procesos de MSBuild.exe Hola y, a continuación, haga clic en botón de Terminar proceso Hola.  

### <a name="routing-toobasichttprelay-endpoints-is-not-supported-from-bridges-and-biztalk-services-portal-if-non-printable-characters-are-promoted-as-http-headers"></a>Los puntos de conexión de tooBasicHttpRelay no admiten el enrutamiento de puentes y el Portal de servicios de BizTalk si se promueven caracteres no imprimibles como encabezados HTTP
Si usa caracteres no imprimibles como parte de las propiedades promocionadas de mensajes, los mensajes no pueden ser enrutado toorelay destinos que utilizan un enlace BasicHttpRelay Hola. Además, Hola propiedades promocionadas, que están disponibles como parte del seguimiento están codificados de dirección URL para blobs y descodificadas para destinos.  

### <a name="mdn-is-sent-asynchronously-even-if-hello-send-asynchronous-mdn-option-is-unchecked"></a>MDN se envía asincrónicamente aunque Hola enviar está desactivada la opción de MDN asincrónico
Considere este escenario: Si selecciona hello **enviar MDN asincrónico** casilla de verificación y especifique un MDN asincrónico de Hola de dirección URL toosend y, a continuación, desactive la opción hello **enviar MDN asincrónico** casilla nuevo, Hola MDN sigue siendo toohello enviado especifica dirección URL aunque Hola opción toosend async MDN no está seleccionada.  
Como alternativa, debe borrar Hola especifica la dirección URL antes de desactivar hello **enviar MDN asincrónico** casilla de verificación y, a continuación, implementar el acuerdo de hello AS2.  

### <a name="whitespace-characters-beyond-a-valid-interchange-cause-an-empty-message-toobe-sent-toohello-suspend-endpoint"></a>Caracteres de espacio en blanco más allá de una causa de intercambio válido un toohello de toobe enviado un mensaje vacío suspensión el punto de conexión
Si hay espacios en blanco más allá de un segmento de IEA, Desensamblador de hello tratará como el final del intercambio actual y busca en el conjunto siguiente de Hola de espacios en blanco como un mensaje nuevo. Puesto que esto no es intercambio válido, puede observar que se envía un mensaje correcto toohello ruta destino y se envía a un mensaje vacío Hola suspender el punto de conexión.  

### <a name="tracking-in-biztalk-services-portal"></a>Seguimiento en el Portal de Servicios de BizTalk
Eventos de seguimiento se capturan toohello procesamiento de mensajes EDI y las posibles correlaciones. Si se produce un error en un mensaje fuera de la fase de protocolo de hello, seguimiento aún lo mostrará como correcto. En esta situación, consulte la sección de registro de toohello en hello **detalles** columna en **seguimiento** para obtener información detallada del error.
Hola X12 de recepción y configuración de envío ([cree una X12 contrato en los servicios de BizTalk de Azure](https://msdn.microsoft.com/library/azure/hh689847.aspx)) ofrece información sobre la fase de protocolo Hola.  

### <a name="update-agreement"></a>Actualización del contrato
Hola Portal de servicios de BizTalk permite toomodify Hola calificador de una identidad cuando se configura un acuerdo. Esto puede dar lugar a propiedades de incoherencia. Por ejemplo, hay un acuerdo que usa zz: 1234567 y ZZ: 7654321 Hola calificador. En configuración del perfil de Portal de servicios de BizTalk de hello, cambia zz: 1234567 toobe 01:ChangedValue. Abra el acuerdo de Hola y 01:ChangedValue se muestra en lugar de zz: 1234567.
actualizar toomodify Hola calificador de una identidad, el acuerdo de hello delete, **identidades** Hola perfil de socio comercial y, a continuación, vuelva a crear el acuerdo de Hola.  

> AZURE.WARNING Este comportamiento afecta a X12 y AS2.  
> 
> 

### <a name="as2-attachments"></a>Datos adjuntos de AS2
Los datos adjuntos de AS2 no se admiten en el envío o la recepción. En concreto, los datos adjuntos se ignoran en silencio y el cuerpo del mensaje Hola se procesa como un mensaje AS2 normal.  

### <a name="resources-remembering-path"></a>Recursos: recuerdo de la ruta de acceso
Al agregar **recursos**, cuadro de diálogo de hello no puede recordar Hola ruta utilizada previamente tooadd un recurso. tooremember Hola usaban ruta de acceso, intente agregar el sitio web de Portal de servicios de BizTalk de hello demasiado**sitios de confianza** en Internet Explorer.  

### <a name="if-you-rename-hello-entity-name-of-a-bridge-and-close-hello-project-without-saving-changes-opening-hello-entity-again-results-in-an-error"></a>Si cambia el nombre de la entidad de Hola de un puente y el proyecto de hello cerrar sin guardar los cambios, vuelva a abrir la entidad de hello produce un error
Considere un escenario en hello siguiente orden:  

* Agregar un proyecto de BizTalk Service tooa de puente (por ejemplo un puente unidireccional XML)  
* Cambiar el nombre de puente Hola especificando un valor para hello propiedad de nombre de la entidad. Esto cambia el nombre de archivo .bridgeconfig asociado de hello con nombre hello especificado.  
* Cerrar archivo .bcs de hello (cerrar pestaña de hello en Visual Studio) sin guardar los cambios de Hola.  
* Abrir archivo .bcs de Hola de nuevo desde el Explorador de soluciones de Hola.  
  Observará que mientras archivo .bridgeconfig asociado de hello tiene el nombre del nuevo Hola que especificó, nombre de la entidad en la superficie de diseño de Hola Hola sigue siendo nombre antiguo de Hola. Si intentas tooopen Hola configuración del puente haciendo doble clic en el componente de puente de hello, obtendrá Hola siguiente error:  
  `‘<old name>’ Entity’s associated file ‘<old name>.bridgeconfig’ does not exist`tooavoid que se ejecuta en este escenario, asegúrese de guardar los cambios después de cambiar el nombre de las entidades de hello en un proyecto de BizTalk Service.  
  
### <a name="biztalk-service-project-builds-successfully-even-if-an-artifact-has-been-excluded-from-a-visual-studio-project"></a>El proyecto de Servicios de BizTalk se compila correctamente incluso si un artefacto se ha excluido de un proyecto de Visual Studio
Considere un escenario donde agregar un proyecto de BizTalk Service tooa de artefacto (por ejemplo, un archivo XSD), incluye el artefacto en hello configuración del puente (por ejemplo, especificándolo como un tipo de mensaje de solicitud) y, a continuación, se excluir del proyecto de Visual Studio de Hola. En tal caso, compilar el proyecto de hello no proporcionará cualquier error siempre que el artefacto Hola eliminar está disponible en disco de hello en hello misma ubicación desde donde se había incluido en el proyecto de Visual Studio Hola.
  
### <a name="hello-biztalk-service-project-does-not-check-for-schema-availability-while-configuring-hello-bridges"></a>Hola proyecto de BizTalk Service no comprueba disponibilidad de esquemas mientras configura puentes Hola
En un proyecto de BizTalk Service, si un esquema que se agrega toohello proyecto importa otro esquema, Hola proyecto de BizTalk Service no comprueba si el esquema importado Hola se agrega toohello proyecto. Si intenta toobuild dicho proyecto, no obtendrá los errores de compilación.
  
### <a name="hello-response-message-for-a-xml-request-reply-bridge-is-always-of-charset-utf-8"></a>mensaje de respuesta de Hola para un puente de solicitud y respuesta XML siempre es del juego de caracteres UTF-8
En esta versión, charset Hola de mensaje de respuesta de saludo de un puente de solicitud y respuesta XML siempre se establece tooUTF-8.
  
### <a name="user-defined-datatypes"></a>Tipos de datos definidos por el usuario
los adaptadores de BizTalk Adapter Pack Hola de característica del servicio de adaptador de BizTalk Hola pueden utilizar tipos de datos definidos por el usuario para operaciones del adaptador.
Al utilizar tipos de datos definidos por el usuario, copiar archivos (.dll) de hello toodrive:\Program Files\Microsoft Files\Microsoft BizTalk Adapter Service\BAServiceRuntime\bin\ o toohello caché de ensamblados Global (GAC) en servidor hello hospedaje de servicio del servicio de adaptador de BizTalk de Hola. En caso contrario, Hola siguiente error puede producirse en el cliente de hello:  
```
<s:Fault xmlns:s="http://schemas.xmlsoap.org/soap/envelope/">
<faultcode>s:Client</faultcode>
<faultstring xml:lang="en-US">hello UDT with FullName "File, FileUDT, Version=Value, Culture=Value, PublicKeyToken=Value" could not be loaded. Try placing hello assembly containing hello UDT definition in hello Global Assembly Cache.</faultstring>
<detail>
  <AFConnectRuntimeFault xmlns="http://Microsoft.ApplicationServer.Integration.AFConnect/2011" xmlns:i="http://www.w3.org/2001/XMLSchema-instance">
    <ExceptionCode>ERROR_IN_SENDING_MESSAGE</ExceptionCode>
  </AFConnectRuntimeFault>
</detail>
</s:Fault>
```  
  
> [!IMPORTANT]
> Es toouse recomendada GACUtil.exe tooinstall un archivo en hello caché Global de ensamblados. GACUtil.exe documentos cómo toouse esta opción de línea de comandos hello y herramienta de Visual Studio.  
> 
> 

### <a name="restarting-hello-biztalk-adapter-service-web-site"></a>Hola reiniciar el sitio de Web del servicio de adaptador de BizTalk
Hola instalación **en tiempo de ejecución del servicio de adaptador de BizTalk*** crea hello **servicio de adaptador de BizTalk** sitio web de IIS que contiene Hola **BAService** aplicación. **BAService** aplicación usa internamente el alcance de Hola de tooextend de enlace de retransmisión de nube de toohello de punto de conexión de servicio local. Para un servicio hospedado de forma local, se registrará extremo de retransmisión correspondiente de hello en hello Service Bus solo cuando Hola inicie el servicio local.  

Si detiene e inicia una aplicación, no se respeta la configuración de Hola para inicio automático de una aplicación. Por lo que cuando **BAService** está detenido, siempre debe reiniciar hello **servicio de adaptador de BizTalk** sitio web en su lugar. No se inicie o detenga hello **BAService** aplicación.

### <a name="special-characters-should-not-be-used-for-address-and-entity-names-of-lob-components"></a>No deben usarse caracteres especiales en nombres de direcciones y entidades de componentes LOB
No debe usar caracteres especiales en nombres de direcciones y entidades de componentes LOB. Si lo hace, obtendrá un error durante la implementación de proyecto de BizTalk Service Hola. Para ciertos caracteres como '%', que es posible que vaya sitio Web de servicio de adaptador de BizTalk de hello en estado detenido y tendrá que toomanually iniciarlo.

### <a name="test-map-with-get-context-property"></a>Prueba de asignación con la propiedad de obtención de contexto
Si una transformación contiene una operación de asignación de **propiedad de obtención de contexto**, la **comprobación de asignación** producirá un error. Como solución temporal, reemplace hello **obtener propiedad de contexto** operación de asignación con una operación de asignación de concatenación de cadena que contiene datos ficticios. Esto rellenar el esquema de destino de Hola y permitirá que comprobar otras funcionalidades de transformación.

### <a name="test-map-property-does-not-display"></a>No se muestra la propiedad Comprobar asignación
Hola **comprobar asignación** propiedades no se muestran en Visual Studio. Esto puede ocurrir si hello **propiedades** hello y ventana **el Explorador de soluciones** ventana no se acoplan simultáneamente. tooresolve, Hola acoplar **propiedades** hello y **el Explorador de soluciones** windows.  

### <a name="datetime-reformat-drop-down-is-grayed-out"></a>La lista desplegable para volver a aplicar formato de fecha y hora está atenuada
Cuando se agrega una operación de asignación de cambiar el formato de fecha y hora toohello diseñar Hola expuesta y configurado, formato de lista desplegable puede mostrarse en gris. Esto puede ocurrir si se establece la pantalla del equipo hello **mediano: 125%** o **más grande: 150%**. tooresolve, establecer la presentación de hello demasiado**más pequeño: 100% (predeterminado)** mediante Hola pasos a continuación:  

1. Abra hello **el Panel de Control** y haga clic en **apariencia y personalización**.
2. Haga clic en **Pantalla**.
3. Haga clic en **Más pequeño: 100 % (predeterminado)** y haga clic en **Aplicar**.

Hola **formato** lista desplegable debe mostrarse según lo esperado.

### <a name="duplicate-agreements-in-hello-biztalk-services-portal"></a>Duplicar acuerdos en hello Portal de servicios de BizTalk
Considere la posibilidad de hello siguiendo el escenario:

1. Crear un acuerdo mediante la API de OM de administración de socios comerciales de Hola.
2. Abra acuerdo Hola Hola Portal de servicios de BizTalk en dos pestañas diferentes.
3. Implementar el acuerdo de Hola de ambas fichas Hola.
4. Como resultado, ambos acuerdos Hola se implementan y generan entradas duplicadas en hello Portal de servicios de BizTalk

**Solución alternativa**. Abra uno de los acuerdos duplicados de Hola Hola Portal de servicios de BizTalk y anular la implementación.  

### <a name="bridges-do-not-use-updated-certificate-even-after-a-certificate-has-been-updated-in-hello-artifact-store"></a>Los puentes no utilizan certificados actualizados incluso después de que se ha actualizado un certificado en el almacén del artefacto de Hola
Considere la posibilidad de hello los escenarios siguientes:  

**Escenario 1: Uso de certificados basados en huella digital para proteger la transferencia de mensajes de un extremo de servicio de puente tooa**  
Considere un escenario donde usa certificados basados en huella digital en el proyecto de servicio de BizTalk. Actualizar certificado de Hola Hola Portal de servicios de BizTalk con hello mismo nombre y una huella digital diferente, pero no actualizan Hola proyecto de BizTalk Service en consecuencia. En este escenario, puente Hola podría seguir mensajes de Hola tooprocess porque los datos del certificado anterior Hola podrían seguir siendo en memoria caché del canal Hola. Después de eso, el procesamiento de mensajes da error.  

**Solución alternativa**: actualizar certificado de Hola Hola proyecto de BizTalk Service y volver a implementar el proyecto de Hola.  

**Escenario 2: Uso de certificados de tooidentify de comportamientos basados en nombre para proteger la transferencia de mensajes de un extremo de servicio de puente tooa**

Considere un escenario donde usa certificados de tooidentify comportamientos basados en el nombre del proyecto de BizTalk Service. Actualizar certificado de Hola Hola BizTalk Services Portal pero no actualizan Hola proyecto de BizTalk Service en consecuencia. En este escenario, puente Hola podría seguir mensajes de Hola tooprocess porque los datos del certificado anterior Hola podrían seguir siendo en memoria caché del canal Hola. Después de eso, el procesamiento de mensajes da error.  

**Solución alternativa**: actualizar certificado de Hola Hola proyecto de BizTalk Service y volver a implementar el proyecto de Hola.  

### <a name="bridges-continue-tooprocess-messages-even-when-hello-sql-database-is-offline"></a>Los puentes continúan tooprocess mensajes incluso cuando la base de datos SQL de hello está sin conexión
puentes de servicios de BizTalk de Hello continuarán tooprocess mensajes durante un tiempo, aunque Hola Microsoft Azure SQL Database (que almacena Hola ejecuta información como artefactos y canalizaciones implementados), está sin conexión. Esto es porque los servicios de BizTalk usa artefactos de hello en caché y la configuración del puente.
Si no desea Hola puentes tooprocess los mensajes cuando Hola base de datos SQL está sin conexión, puede utilizar toostop de cmdlets de PowerShell de servicios de BizTalk de Hola o suspender Hola BizTalk Service. Vea [ejemplo de administración de servicios de BizTalk de Azure](http://go.microsoft.com/fwlink/p/?LinkID=329019) para las operaciones toomanage de cmdlets de Windows PowerShell de Hola.  

### <a name="reading-hello-xml-message-within-a-bridges-custom-code-component-includes-an-extra-bom-character"></a>Mensaje XML de Hola de lectura en el componente de código personalizado de un puente incluye un carácter BOM adicional
Considere un escenario en el que desea tooread un mensaje XML dentro de código personalizado del puente. Si usas hello System.Text.Encoding.UTF8.GetString(bytes) de API de .NET un carácter BOM adicional se incluye en el resultado de hello al principio de Hola de mensaje de bienvenida. Por lo tanto, si no desea Hola de tooinclude de salida de hello carácter BOM adicional, debe usar ```System.IO.StreamReader().ReadToEnd()```.

### <a name="sending-messages-tooa-bridge-using-wcf-does-not-scale"></a>Enviar mensajes puente tooa con WCF no se escala
Los mensajes se envían puente tooa con WCF no se escala. Si quiere un cliente escalable, debe usar en su lugar HttpWebRequest.

### <a name="upgrade-token-provider-error-after-upgrading-from-biztalk-services-preview-toogeneral-availability-ga"></a>ACTUALIZACIÓN: Error de proveedor de Token después de actualizar desde la vista previa de los servicios de BizTalk tooGeneral disponibilidad (GA)
Existe un contrato EDI o AS2 con lotes activos. Cuando se actualiza Hola BizTalk Service de tooGA de vista previa, puede producirse siguiente hello:

* Error: el proveedor de tokens de Hola fue no se puede tooprovide un token de seguridad. Proveedor de tokens devolvió el mensaje: no se pudo resolver el nombre remoto Hola.
* Las tareas de Lote se cancelan.

**Solución alternativa**: una vez Hola BizTalk Service tooGeneral actualizada disponibilidad (GA), volver a implementar el acuerdo de Hola.  

### <a name="upgrade-toolbox-shows-hello-old-bridge-icons-after-upgrading-hello-biztalk-services-sdk"></a>ACTUALIZACIÓN: Cuadro de herramientas muestra hello iconos del puente anterior después de actualizar Hola SDK de servicios de BizTalk
Después de actualizar una versión anterior de hello SDK de servicios de BizTalk, que usaba iconos anteriores para representar los puentes de hello, cuadro de herramientas de hello continúa iconos anteriores para tooshow Hola para puentes Hola. Sin embargo, si agrega una puente tooBizTalk servicio proyecto superficie del diseñador, superficie de hello muestra icono nuevo Hola.  

**Solución alternativa**. Puede solucionar este problema mediante la eliminación de archivos de hello .tbd en <system drive>: \Users\<usuario > \AppData\Local\Microsoft\VisualStudio\11.0.  

### <a name="upgrade-biztalk-portal-update-from-preview-tooga-might-show-an-error-indicating-that-hello-edi-capability-is-not-available"></a>ACTUALIZACIÓN: Actualización de BizTalk Portal de vista previa tooGA podría mostrar un error que indica que Hola capacidad EDI no está disponible
Si se registran en el Portal de servicios de BizTalk de hello mientras se actualicen los servicios de BizTalk de Hola de tooGA de vista previa, podría obtener Hola siguiente error en el portal de hello:  

Esta función no se encuentra disponible como parte de esta edición de Servicios de BizTalk de Microsoft Azure. toouse estas capacidades cambiar edición adecuada de tooan.  

**Resolución**: la sesión del portal de Hola, explorador Hola cerrar y abrir y, a continuación, inicie sesión en el portal de Hola.  

### <a name="upgrade-new-tracking-data-does-not-show-up-after-biztalk-services-is-upgraded-tooga"></a>ACTUALIZACIÓN: Nuevos datos de seguimiento se muestran después de servicios de BizTalk es tooGA actualizado
Supongamos un escenario donde ha implementado un puente XML en la suscripción de la versión preliminar de Servicios de BizTalk. Enviar mensajes toohello puente y los datos de seguimiento correspondientes Hola están disponibles en hello Portal de servicios de BizTalk. Ahora, si los bits de en tiempo de ejecución de servicios de BizTalk y el Portal de servicios de BizTalk de hello tooGA actualizado y enviar un toohello mensaje mismo extremo de puente implementado anteriormente, Hola datos de seguimiento no se muestra para los mensajes enviados después de la actualización.  

### <a name="pipelines-versus-bridges"></a>Canalizaciones frente a puentes
En este documento, el término de hello 'canalizaciones' y 'puentes' se usan indistintamente. Ambos significan básicamente Hola misma acción, que es una unidad de procesamiento de mensaje implementada en servicios de BizTalk.  

### <a name="concepts"></a>Conceptos
[Servicios de BizTalk](https://msdn.microsoft.com/library/azure/hh689864.aspx)   

