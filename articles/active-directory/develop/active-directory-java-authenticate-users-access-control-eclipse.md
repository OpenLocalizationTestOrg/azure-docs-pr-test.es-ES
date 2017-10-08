---
title: aaaHow toouse el Control de acceso (Java) | Documentos de Microsoft
description: "Obtenga información acerca de cómo toodevelop y el uso de Control de acceso con Java en Azure."
services: active-directory
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 247dfd59-0221-4193-97ec-4f3ebe01d3c7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.custom: aaddev
ms.openlocfilehash: cbbce3b1a05eabf3b86a8cb91db1bde92dbb8960
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooauthenticate-web-users-with-azure-access-control-service-using-eclipse"></a>¿Cómo tooAuthenticate usuarios Web con Azure Access Control Service mediante Eclipse
Esta guía le mostrará cómo toouse hello Azure Access Control Service (ACS) dentro de hello Azure Toolkit for Eclipse. Para obtener más información sobre ACS, vea hello [pasos siguientes](#next_steps) sección.

> [!NOTE]
> Hola filtro de Control de servicios de acceso de Azure es community technology preview. Como versión preliminar de software, no cuenta formalmente con el respaldo de Microsoft.
> 
> 

## <a name="what-is-acs"></a>¿Qué es ACS?
La mayoría de los desarrolladores ni son expertos en identidad ni generalmente quieren dedicar demasiado tiempo a desarrollar mecanismos de autenticación y autorización para sus aplicaciones y servicios. ACS es un servicio de Azure que proporciona una manera sencilla de autenticar a los usuarios que necesitan tooaccess sus aplicaciones web y servicios sin necesidad de lógica de autenticación compleja toofactor en el código.

Hola siguientes características está disponible en ACS:

* Integración con Windows Identity Foundation (WIF).
* Compatibilidad con los proveedores de identidades (IP) habituales, entre los que se incluyen Windows Live ID, Google, Yahoo! y Facebook.
* Compatibilidad con los servicios de federación de Active Directory (AD FS) 2.0.
* Un Open Data Protocol (OData)-servicio de administración que proporciona acceso mediante programación los valores de tooACS basado en.
* Un Portal de administración que permita el acceso administrativo toohello configuración de ACS.

Para más información acerca de ACS, consulte [Access Control Service 2.0][Access Control Service 2.0].

## <a name="concepts"></a>Conceptos
ACS de Azure se basa en hello las entidades de seguridad de la identidad basada en notificaciones - de un enfoque coherente toocreating los mecanismos de autenticación para aplicaciones que se ejecutan en local o en la nube de Hola. Identidad basada en notificaciones proporciona una forma común para las aplicaciones y servicios tooacquire la información de identidad que necesitan sobre los usuarios dentro de su organización, en otras organizaciones y en hello Internet.

tareas de hello toocomplete en esta guía, debe conocer Hola siguientes conceptos:

**Cliente** -en hello el contexto de este tooguide cómo, esto es un explorador que está tratando de aplicación web tooyour toogain.

**Aplicación de confianza (RP)** -aplicación de RP una es un sitio Web o servicio que externalice la autoridad de autenticación tooone externo. En jerga de identidad, se dice que Hola RP confía en esa entidad. Esta guía se explica cómo tooconfigure su tootrust aplicación ACS.

**Token** : un token es una colección de datos de seguridad que normalmente se emite después de la autenticación correcta de un usuario. Contiene un conjunto de *notificaciones*, atributos de hello usuario autentican. Una notificación puede representar el nombre de un usuario, un identificador para el rol al que pertenece un usuario, la edad del usuario, etc. Un token está firmado digitalmente por lo general, lo que significa que siempre puede ser origen tooits atrás emisor y su contenido no se pueden manipular. Una usuario mejoras tooa RP aplicación access presentando un token válido emitido por una entidad que confía en aplicación de RP de hello.

**Proveedor de identidades (IP)** : un proveedor de identidades es una autoridad que autentica las identidades de los usuarios y emite los tokens de seguridad. trabajo real de Hola de emisión de tokens se implementa aunque un servicio especial denominado servicio de Token de seguridad (STS). Ejemplos típicos de proveedores de identidades incluyen Windows Live ID; Facebook, repositorios de usuarios profesionales (como Active Directory), etc.
Una vez ACS tootrust configurada una dirección IP, el sistema de hello aceptará y validará tokens emitidos por esa dirección IP. ACS puede confiar en varias direcciones IP al mismo tiempo, lo que significa que cuando la aplicación confía en ACS, puede ofrecer al instante la hello tooall de aplicación autentica a los usuarios de hello todas las direcciones IP que ACS confía en su nombre.

**Proveedor de federación (FP)** : los IP conocen directamente a los usuarios, los autentican usando sus credenciales y emiten notificaciones sobre lo que saben de ellos. Un proveedor de federación (FP) es un tipo de entidad diferente: en lugar de autenticar a los usuarios directamente, actúa como un intermediario y negocia la autenticación entre un RP y uno o más IP. Tanto los IP como los FP emiten tokens de seguridad, por lo tanto, ambos utilizan los servicios de token de seguridad (STS). ACS es un FP.

**Motor de reglas de ACS** -reglas de transformación de notificaciones de lógica de hello tootransform usa los tokens entrantes de tootokens de direcciones IP de confianza diseñado toobe consumido por Hola RP está codificado en forma de simple. ACS incluye un motor de reglas que se ocupa de aplicar cualquier lógica de transformación que se haya especificado para su RP.

**Espacio de nombres de ACS** : un espacio de nombres es una partición de nivel superior de ACS que se utiliza para organizar su configuración. Un espacio de nombres contiene una lista de direcciones IP que confía, Hola RP aplicaciones tooserve, reglas de Hola que espera Hola regla motor tooprocess los tokens entrantes y así sucesivamente. Un espacio de nombres expone varios extremos que serán utilizado por la aplicación hello y el tooperform tooget ACS de desarrollador su función.

Hello en la ilustración siguiente se muestra cómo funciona la autenticación de ACS con una aplicación web:

![Diagrama de flujo de ACS][acs_flow]

1. cliente de Hello (en este caso, un explorador) solicita una página de Hola RP.
2. Puesto que la solicitud de hello no está autenticada todavía, Hola RP redirige autoridad Hola de toohello del usuario que confía, que es ACS. Hola ACS presenta usuario Hola con la elección de Hola de direcciones IP que se han especificado para este RP. usuario de Hello selecciona Hola adecuado IP.
3. Hola cliente examina la página de autenticación toohello direcciones IP y solicita Hola usuario toolog en.
4. Una vez autenticado el cliente hello (por ejemplo, se introducen las credenciales de identidad de hello), IP Hola emite un token de seguridad.
5. Después de emitir un token de seguridad, Hola IP redirige tooACS de cliente de Hola y Hola cliente envía los token de seguridad de hello emitido por hello tooACS IP.
6. ACS valida el token de seguridad de hello emitido por IP hello, entradas identidad Hola notificaciones en este token en el motor de reglas de hello ACS, calcula las notificaciones de identidad de salida de hello y emite un token de seguridad nuevo que contiene estas notificaciones de salida.
7. ACS redirige toohello de cliente de Hola RP. cliente de Hello envía Hola nuevo token emitido por ACS toohello RP. Hola RP valida la firma de Hola Hola token de seguridad emitido por ACS, valida Hola notificaciones del token y devuelve una página de Hola que se solicitó originalmente.

## <a name="prerequisites"></a>Requisitos previos
tareas de hello toocomplete en esta guía, se necesita Hola siguiente:

* Un kit para desarrolladores de Java (JDK) v1.6 o superior.
* Eclipse IDE para Java EE Developers, Indigo o superior. Se puede descargar en <http://www.eclipse.org/downloads/>. 
* Una distribución de un servidor de aplicaciones o servidor web basado en Java, como Apache Tomcat, GlassFish, JBoss Application Server o Jetty.
* Una suscripción de Azure, que se puede adquirir en <http://www.microsoft.com/windowsazure/offers/>.
* Hello Azure Toolkit for Eclipse, abril de 2014 de la versión o una versión posterior. Para obtener más información, consulte [instalar hello Azure Toolkit for Eclipse](http://msdn.microsoft.com/library/windowsazure/hh690946.aspx).
* Toouse de un certificado X.509 con la aplicación. Necesitará este certificado en formato de certificado público (.cer) e intercambio de información personal (.PFX). (Las opciones para crear este certificado se describirán más adelante en este tutorial).
* Familiaridad con hello Azure compute emulator e implementación técnicas descritas en [crear una aplicación Hello World de Azure en Eclipse](http://msdn.microsoft.com/library/windowsazure/hh690944.aspx).

## <a name="create-an-acs-namespace"></a>Creación de un espacio de nombres de ACS
toobegin mediante Access Control Service (ACS) en Azure, debe crear un espacio de nombres de ACS. espacio de nombres de Hello proporciona un único ámbito para tener acceso a recursos de ACS desde dentro de la aplicación.

1. Inicie sesión en hello [Portal de administración de Azure][Azure Management Portal].
2. Haga clic en **Active Directory**. 
3. toocreate un nuevo espacio de nombres de Control de acceso, haga clic en **New**, haga clic en **servicios de aplicaciones**, haga clic en **el Control de acceso**y, a continuación, haga clic en **creación rápida** . 
4. Escriba un nombre para el espacio de nombres de Hola. Azure comprueba que el nombre hello es único.
5. Seleccione la región de hello en qué Hola se utiliza el espacio de nombres. Para obtener el mejor rendimiento de hello, utilice región hello en el que va a implementar la aplicación.
6. Si tiene más de una suscripción, seleccione suscripción Hola que quiere toouse de espacio de nombres de hello ACS.
7. Haga clic en **Crear**.

Azure crea y activa el espacio de nombres de Hola. Espere hasta que el estado de Hola de Hola de nuevo espacio de nombres es **Active** antes de continuar. 

## <a name="add-identity-providers"></a>Incorporación de proveedores de identidades
En esta tarea, agregará toouse de direcciones IP con la aplicación de RP para la autenticación. Con fines de demostración, esta tarea muestra cómo tooadd Windows Live como una dirección IP, pero puede utilizar cualquiera de hello que direcciones IP aparecen en el Portal de administración de ACS de Hola.

1. Hola [Portal de administración de Azure][Azure Management Portal], haga clic en **Active Directory**, seleccione un espacio de nombres de Control de acceso y, a continuación, haga clic en **administrar**. se abre el Portal de administración de ACS de Hola.
2. En el panel de navegación izquierdo de Hola de hello Portal de administración de ACS, haga clic en **proveedores de identidades**.
3. Windows Live ID está habilitado de manera predeterminada y no se puede eliminar. Para los fines de este tutorial, solo se utiliza Windows Live ID. Sin embargo, esta pantalla, es donde puede agregar otras direcciones IP, haciendo clic en hello **agregar** botón.

Windows Live ID ahora está habilitado como un IP para su espacio de nombres de ACS. A continuación, especifique la aplicación web de Java (toobe posteriormente) como un punto de reunión.

## <a name="add-a-relying-party-application"></a>Incorporación de una aplicación de usuario de confianza
En esta tarea, configurará ACS toorecognize la aplicación web de Java como una aplicación de RP válida.

1. En el Portal de administración de ACS de hello, haga clic en **aplicaciones de usuario de confianza**.
2. En hello **aplicaciones de usuario autenticado** página, haga clic en **agregar**.
3. En hello **Agregar aplicación de usuario de confianza** página, Hola siguientes:
   
   1. En **nombre**, nombre de tipo hello de Hola RP. Para los fines de este tutorial, escriba **Azure Web App**.
   2. En **Modo**, seleccione **Enter settings manually** (Especificar la configuración manualmente).
   3. En **territorio**, se aplica el tipo hello URI toowhich Hola token de seguridad emitido por ACS. Para esta tarea, escriba **http://localhost:8080/**.
      ![El dominio de usuario de confianza para utilizar en el emulador de proceso][relying_party_realm_emulator]
   4. En **dirección URL de retorno,** toowhich de dirección URL de tipo hello ACS devuelve el token de seguridad de Hola. Para esta tarea, escriba **http://localhost:8080/MyACSHelloWorld/index.jsp**
      ![, que es la dirección URL de retorno de usuario de confianza para utilizar en el emulador de proceso][relying_party_return_url_emulator].
   5. Acepte valores predeterminados de hello en el resto de Hola de campos de Hola.
4. Haga clic en **Guardar**.

Se ha configurado correctamente la aplicación web de Java cuando se ejecuta en el emulador de proceso de Azure de hello (en http://localhost: 8080 /) toobe RP en el espacio de nombres de ACS. A continuación, crear reglas de Hola que ACS usa tooprocess notificaciones para Hola RP.

## <a name="create-rules"></a>Creación de reglas
En esta tarea, debe definir reglas de Hola que controlan cómo se pasan las notificaciones de direcciones IP tooyour RP. A fin de Hola de esta guía, simplemente configuraremos valores y tipos de notificaciones de entrada de ACS toocopy Hola directamente en el símbolo (token) de la salida de hello, sin filtrar ni modificarlos.

1. En la página principal del Portal de administración de ACS de hello, haga clic en **grupos de reglas**.
2. En hello **grupos de reglas** página, haga clic en **grupo de reglas predeterminado para la aplicación Web de Azure**.
3. En hello **Editar grupo de reglas** página, haga clic en **generar**.
4. En hello **generar reglas: grupo de reglas predeterminado para la aplicación Web de Azure** página, asegúrese de Windows Live ID está activada y, a continuación, haga clic en **generar**.    
5. En hello **Editar grupo de reglas** página, haga clic en **guardar**.

## <a name="upload-a-certificate-tooyour-acs-namespace"></a>Cargar un espacio de nombres de certificado tooyour ACS
En esta tarea, se carga una. Certificado PFX que será las solicitudes de tokens de toosign usado creadas por el espacio de nombres de ACS.

1. En la página principal del Portal de administración de ACS de hello, haga clic en **certificados y claves**.
2. En hello **certificados y claves** página, haga clic en **agregar** anteriormente **firma de tokens**.
3. En hello **clave o certificado de firma de Token agregar** página:
   1. Hola **destinadas** sección, haga clic en **aplicación de usuario de confianza** y seleccione **aplicación Web de Azure** (que ha establecido previamente como nombre de saludo de la aplicación del usuario autenticado).
   2. Hola **tipo** sección, seleccione **certificado X.509**.
   3. Hola **certificado** sección, haga clic en el botón de examinar hello y navegar por el archivo de certificado X.509 toohello que desea toouse. Este será un archivo .PFX. Seleccione el archivo hello, haga clic en **abiertos**y a continuación, escriba la contraseña del certificado Hola Hola **contraseña** cuadro de texto. Observe que, para fines de prueba, puede utilizar un certificado autofirmado. toocreate un certificado autofirmado, utilice hello **New** botón en hello **biblioteca de filtro de ACS** diálogo (descrita más adelante), o usar hello **encutil.exe** utilidad de hello [sitio Web de proyecto] [ project website] de hello Azure Starter Kit para Java.
   4. Asegúrese de que la opción **Hacer principal** esté activada. Su **clave o certificado de firma de Token agregar** página debe tener un aspecto similar siguiente toohello.
       ![Agregar certificado de firma de tokens][add_token_signing_cert]
   5. Haga clic en **guardar** toosave la configuración y cerrar hello **clave o certificado de firma de Token agregar** página.

A continuación, revise la información de Hola Hola integración de aplicaciones página y copiar Hola URI que necesitará tooconfigure su toouse de aplicación web de Java ACS.

## <a name="review-hello-application-integration-page"></a>Página de integración de aplicaciones de Hola de revisión
Puede encontrar toda la información de Hola y Hola código necesarios tooconfigure su toowork de aplicación (aplicación de RP de Hola) web de Java con ACS en la página de integración de aplicaciones de Hola de hello Portal de administración de ACS. Necesitará esta información cuando configure la aplicación web de Java para la autenticación federada.

1. En el Portal de administración de ACS de hello, haga clic en **integración de aplicaciones**.  
2. Hola **integración de aplicaciones** página, haga clic en **páginas de inicio de sesión**.
3. Hola **integración de la página de inicio de sesión** página, haga clic en **aplicación Web de Azure**.

Hola **integración de la página de inicio de sesión: aplicación Web de Azure** dirección URL de hello enumerado en la página **opción 1: página de inicio de sesión hospedada en ACS de vínculo tooan** se utilizarán en la aplicación web de Java. Necesitará este valor cuando se agrega la biblioteca tooyour aplicación Java de hello filtro de servicios de Control de acceso de Azure.

## <a name="create-a-java-web-application"></a>Creación de una aplicación web de Java
1. En Eclipse, en el menú de hello, haga clic en **archivo**, haga clic en **New**y, a continuación, haga clic en **Dynamic Web Project**. (Si no ve **Dynamic Web Project** aparece como proyecto disponible después de hacer clic **archivo**, **New**, a continuación, Hola después: haga clic en **archivo**, haga clic en **New**, haga clic en **proyecto**, expanda **Web**, haga clic en **Dynamic Web Project**y haga clic en  **A continuación**.) Para fines de este tutorial, denomine el proyecto de hello **MyACSHelloWorld**. (Asegúrese de usar este nombre, los pasos posteriores de este tutorial esperan su toobe de archivo WAR denominado MyACSHelloWorld). La pantalla aparecerá a continuación toohello similar:
   
    ![Ejemplo: Crear un proyecto Hello World para ACS][create_acs_hello_world]
   
    Haga clic en **Finalizar**
2. En la vista del explorador de proyectos de Eclipse, expanda **MyACSHelloWorld**. Haga clic con el botón derecho en **WebContent**, haga clic en **New** (Nuevo) y, después, en **JSP File** (Archivo JSP).
3. Hola **New JSP File** cuadro de diálogo, archivo de nombre hello **index.jsp**. Mantener carpeta primaria de hello como MyACSHelloWorld/WebContent, tal y como se muestra en hello siguiente:
   
    ![Ejemplo: Agregar un archivo JSP para ACS][add_jsp_file_acs]
   
    Haga clic en **Siguiente**.
4. Hola **Select JSP Template** cuadro de diálogo, seleccione **New JSP File (html)** y haga clic en **finalizar**.
5. Cuando se abre el archivo index.jsp de hello en Eclipse, agregar en texto toodisplay **ACS ¡Hello World!** dentro de hello existente `<body>` elemento. Su actualizada `<body>` debería aparecer el contenido siguiente hello:
   
        <body>
          <b><% out.println("Hello ACS World!"); %></b>
        </body>
   
    Guarde el archivo index.jsp.

## <a name="add-hello-acs-filter-library-tooyour-application"></a>Agregar hello tooyour aplicación de biblioteca de filtro de ACS
1. En el explorador de proyectos de Eclipse, haga clic con el botón derecho en **MyACSHelloWorld** y, a continuación, haga clic en **Build Path** (Ruta de acceso de compilación) y luego en **Configure Build Path** (Configurar ruta de acceso de compilación).
2. Hola **Java Build Path** cuadro de diálogo, haga clic en hello **bibliotecas** ficha.
3. Haga clic en **Agregar biblioteca**.
4. Haga clic en **Azure Access Control Services Filter (by MS Open Tech)** (Filtro de servicios de control de acceso de Azure [de MS Open Tech]) y, a continuación, en **Next** (Siguiente). Hola **filtro de servicios de Control de acceso de Azure** se muestra el cuadro de diálogo.  (hello **ubicación** campo puede tener una ruta de acceso diferente, dependiendo de dónde instalado Eclipse, y número de versión de Hola podría ser diferente, dependiendo de las actualizaciones de software.)
   
    ![Agregar biblioteca de filtros de ACS][add_acs_filter_lib]
5. Mediante un explorador abierto toohello **integración de la página de inicio de sesión** página del programa Hola a Portal de administración, copiar dirección URL de hello enumerado en hello **opción 1: página de inicio de sesión hospedada en ACS de vínculo tooan** campo y pegarlos en hello **Extremo de autenticación ACS** campo del cuadro de diálogo de hello Eclipse.
6. Mediante un explorador abierto toohello **Editar aplicación de usuario de confianza** página del programa Hola a Portal de administración, copiar dirección URL de hello enumerado en hello **territorio** campo y pegarlos en hello **dominio Kerberos del usuario de confianza**  campo del cuadro de diálogo de hello Eclipse.
7. Dentro de hello **seguridad** sección del cuadro de diálogo de Eclipse hello, si desea que toouse un certificado existente, haga clic en **examinar**, navegue toohello certificado desea toouse, selecciónelo y haga clic en  **Abra**. O bien, si desea que toocreate un nuevo certificado, haga clic en **New** toodisplay hello **nuevo certificado** cuadro de diálogo, a continuación, especifique la contraseña de hello, nombre de archivo .cer de hello y nombre del archivo .pfx Hola Hola de nuevo certificado.
8. Comprobar **insertar certificado de hello en el archivo WAR de hello**. Incrustación certificado Hola de esta manera incluye en la implementación sin necesidad de toomanually agregarlo como un componente. (Si en su lugar, debe almacenar el certificado externamente desde su archivo WAR, puede agregar el certificado de Hola como un componente de rol y desactive **insertar certificado de hello en el archivo WAR de hello**.)
9. [Opcional] Mantenga activada la opción **Requerir conexiones HTTPS** . Si establece esta opción, deberá tooaccess la aplicación mediante el protocolo HTTPS de Hola. Si no desea que las conexiones HTTPS de toorequire, desactive esta opción.
10. Para una implementación de emulador, de proceso toohello su **filtro de ACS de Azure** configuración tendrá un aspecto similar a continuación toohello.
    
    ![Emulador de proceso de configuración de filtro de ACS de Azure para una implementación toohello][add_acs_filter_lib_emulator]
11. Haga clic en **Finalizar**
12. Haga clic en **Sí** cuando aparezca un cuadro de diálogo que indique que se creará un archivo web.xml.
13. Haga clic en **Aceptar** tooclose hello **Java Build Path** cuadro de diálogo.

## <a name="deploy-toohello-compute-emulator"></a>Implementar toohello del emulador de proceso
1. En el explorador de proyectos de Eclipse, haga clic con el botón derecho en **MyACSHelloWorld** y luego haga clic en **Azure** y en **Package for Azure** (Paquete de Azure).
2. En **Project name** (Nombre de proyecto), escriba **MyAzureACSProject** y haga clic en **Next** (Siguiente).
3. Seleccione un JDK y un servidor de aplicaciones. (Estos pasos se explican en detalle en hello [crear una aplicación Hello World de Azure en Eclipse](http://msdn.microsoft.com/library/windowsazure/hh690944.aspx) tutorial).
4. Haga clic en **Finalizar**
5. Haga clic en hello **Run in Azure Emulator** botón.
6. Después de la aplicación web de Java se inicia en el emulador de proceso de hello, cierre todas las instancias del explorador (de modo que las sesiones del explorador actual no interfieren con la prueba de inicio de sesión de ACS).
7. Para ejecutar la aplicación, abra <http://localhost:8080/MyACSHelloWorld/> en el explorador (o <https://localhost:8080/MyACSHelloWorld/> si ha activado **Require HTTPS connections** [Requerir conexiones HTTPS]). Se le pedirá un inicio de sesión de Windows Live ID, a continuación, se deben tener dirección URL de retorno de toohello especificado para la aplicación del usuario autenticado.
8. Cuando haya terminado de ver la aplicación, haga clic en hello **Reset Azure Emulator** botón.

## <a name="deploy-tooazure"></a>Implementar tooAzure
toodeploy tooAzure, necesitará toochange Hola confianza entidad territorio y devuelven una URL para el espacio de nombres de ACS.

1. Dentro de hello Portal de administración de Azure, en hello **Editar aplicación de usuario de confianza** , modifique **territorio** toobe Hola URL del sitio implementado. Reemplace **ejemplo** con el nombre DNS de Hola que especificó para la implementación.
   
    ![El dominio de usuario de confianza para utilizar en producción][relying_party_realm_production]
2. Modificar **dirección URL de retorno** toobe Hola URL de la aplicación. Reemplace **ejemplo** con el nombre DNS de Hola que especificó para la implementación.
   
    ![La URL de retorno de usuario de confianza para utilizar en producción][relying_party_return_url_production]
3. Haga clic en **guardar** toosave los usuarios de confianza entidad territorio y valores devueltos URL actualizada cambia.
4. Mantener hello **integración de la página de inicio de sesión** página abierta en el explorador, deberá toocopy de él en breve.
5. En el explorador de proyectos de Eclipse, haga clic con el botón derecho en **MyACSHelloWorld** y, a continuación, haga clic en **Build Path** (Ruta de acceso de compilación) y luego en **Configure Build Path** (Configurar ruta de acceso de compilación).
6. Haga clic en hello **bibliotecas** , haga clic en **filtro de servicios de Control de acceso de Azure**y, a continuación, haga clic en **editar**.
7. Mediante un explorador abierto toohello **integración de la página de inicio de sesión** página del programa Hola a Portal de administración, copiar dirección URL de hello enumerado en hello **opción 1: página de inicio de sesión hospedada en ACS de vínculo tooan** campo y pegarlos en hello **Extremo de autenticación ACS** campo del cuadro de diálogo de hello Eclipse.
8. Mediante un explorador abierto toohello **Editar aplicación de usuario de confianza** página del programa Hola a Portal de administración, copiar dirección URL de hello enumerado en hello **territorio** campo y pegarlos en hello **dominio Kerberos del usuario de confianza**  campo del cuadro de diálogo de hello Eclipse.
9. Dentro de hello **seguridad** sección del cuadro de diálogo de Eclipse hello, si desea que toouse un certificado existente, haga clic en **examinar**, navegue toohello certificado desea toouse, selecciónelo y haga clic en  **Abra**. O bien, si desea que toocreate un nuevo certificado, haga clic en **New** toodisplay hello **nuevo certificado** cuadro de diálogo, a continuación, especifique la contraseña de hello, nombre de archivo .cer de hello y nombre del archivo .pfx Hola Hola de nuevo certificado.
10. Mantener **insertar certificado de hello en el archivo WAR de hello** activa, suponiendo que desea tooembed Hola certificado en el archivo WAR de hello.
11. [Opcional] Mantenga activada la opción **Requerir conexiones HTTPS** . Si establece esta opción, deberá tooaccess la aplicación mediante el protocolo HTTPS de Hola. Si no desea que las conexiones HTTPS de toorequire, desactive esta opción.
12. Para una tooAzure de implementación, la configuración de filtro de ACS de Azure tendrá un aspecto similar a continuación toohello.
    
    ![Configuración del filtro de ACS de Azure para una implementación en producción][add_acs_filter_lib_production]
13. Haga clic en **finalizar** tooclose hello **editar la biblioteca de** cuadro de diálogo.
14. Haga clic en **Aceptar** tooclose hello **propiedades de MyACSHelloWorld** cuadro de diálogo.
15. En Eclipse, haga clic en hello **publicar tooAzure nube** botón. Responder mensajes toohello, tal como hace en hello **toodeploy su aplicación tooAzure** sección de hello [crear una aplicación Hello World de Azure en Eclipse](http://msdn.microsoft.com/library/windowsazure/hh690944.aspx) tema. 

Después de que se ha implementado la aplicación web, cierre las sesiones del explorador abierta, ejecute la aplicación web y se le pedirá toosign con las credenciales de Windows Live ID, seguido por la que se envían toohello devolver la dirección URL de la aplicación del usuario autenticado.

Cuando haya terminado mediante la aplicación de ACS Hello World, recuerde la implementación de hello toodelete (aprenderá cómo toodelete una implementación en hello [crear una aplicación Hello World de Azure en Eclipse](http://msdn.microsoft.com/library/windowsazure/hh690944.aspx) tema).

## <a name="next_steps"></a>Pasos siguientes
Para un examen de hello devuelto por la aplicación de ACS tooyour la lenguaje de marcado de aserción de seguridad (SAML), consulte [cómo tooview SAML devuelve hello Azure Access Control Service][How tooview SAML returned by hello Azure Access Control Service]. toofurther explorar la funcionalidad de ACS y tooexperiment con escenarios más complejos, vea [Access Control Service 2.0][Access Control Service 2.0].

Además, este hello en el ejemplo se utiliza **insertar certificado de hello en el archivo WAR de hello** opción. Esta opción facilita certificado de hello toodeploy simple. Si en su lugar desea tookeep el certificado de firma independiente de su archivo WAR, puede usar Hola después técnica:

1. Dentro de hello **seguridad** sección de hello **filtro de servicios de Control de acceso de Azure** cuadro de diálogo, escriba **${env. JAVA_HOME}/myCert.cer** y desactive la opción **insertar certificado de hello en el archivo WAR de hello**. (Ajuste mycert.cer si el nombre del archivo de certificado es distinto). Haga clic en **finalizar** el cuadro de diálogo de tooclose Hola.
2. Certificado de copia Hola como un componente en la implementación: en el Explorador de proyectos de Eclipse, expanda **MyAzureACSProject**, haga clic en **WorkerRole1**, haga clic en **propiedades** , expanda **rol Azure**y haga clic en **componentes**.
3. Haga clic en **Agregar**.
4. Dentro de hello **Agregar componente** cuadro de diálogo:
   
   1. Hola **importación** sección:
      1. Hola de uso **archivo** certificado toohello botón toonavigate que desea toouse. 
      2. En **Method** (Método) seleccione **copy** (copiar).
   2. Para **como nombre**, haga clic en el cuadro de texto de Hola y acepte el nombre predeterminado de Hola.
   3. Hola **implementar** sección:
      1. En **Method** (Método) seleccione **copy** (copiar).
      2. Para **toodirectory**, tipo **JAVA_HOME %**.
   4. Su **Agregar componente** cuadro de diálogo debe tener un aspecto similar a continuación toohello.
      
       ![Agregar componente de certificado][add_cert_component]
   5. Haga clic en **Aceptar**.

En este punto, su certificado se incluiría en la implementación. Tenga en cuenta que independientemente de que insertar certificado de hello en archivo WAR de Hola o agregarlo como una implementación de tooyour de componente, debe tooupload Hola certificado tooyour espacio de nombres como se describe en hello [cargar un espacio de nombres de certificado tooyour ACS] [ Upload a certificate tooyour ACS namespace] sección.

[What is ACS?]: #what-is
[Concepts]: #concepts
[Prerequisites]: #pre
[Create a Java web application]: #create-java-app
[Create an ACS Namespace]: #create-namespace
[Add Identity Providers]: #add-IP
[Add a Relying Party Application]: #add-RP
[Create Rules]: #create-rules
[Upload a certificate tooyour ACS namespace]: #upload-certificate
[Review hello Application Integration Page]: #review-app-int
[Configure Trust between ACS and Your ASP.NET Web Application]: #config-trust
[Add hello ACS Filter library tooyour application]: #add_acs_filter_library
[Deploy toohello compute emulator]: #deploy_compute_emulator
[Deploy tooAzure]: #deploy_azure
[Next steps]: #next_steps
[project website]: http://wastarterkit4java.codeplex.com/releases/view/61026
[How tooview SAML returned by hello Azure Access Control Service]: active-directory-java-view-saml-returned-by-access-control.md
[Access Control Service 2.0]: http://go.microsoft.com/fwlink/?LinkID=212360
[Windows Identity Foundation]: http://www.microsoft.com/download/en/details.aspx?id=17331
[Windows Identity Foundation SDK]: http://www.microsoft.com/download/en/details.aspx?id=4451
[Azure Management Portal]: https://manage.windowsazure.com
[acs_flow]: ./media/active-directory-java-authenticate-users-access-control-eclipse/ACSFlow.png

<!-- Eclipse-specific -->
[add_acs_filter_lib]: ./media/active-directory-java-authenticate-users-access-control-eclipse/AddACSFilterLibrary.png
[add_acs_filter_lib_emulator]: ./media/active-directory-java-authenticate-users-access-control-eclipse/AddACSFilterLibraryEmulator.png
[add_acs_filter_lib_production]: ./media/active-directory-java-authenticate-users-access-control-eclipse/AddACSFilterLibraryProduction.png

[relying_party_realm_emulator]: ./media/active-directory-java-authenticate-users-access-control-eclipse/RelyingPartyRealmEmulator.png
[relying_party_return_url_emulator]: ./media/active-directory-java-authenticate-users-access-control-eclipse/RelyingPartyReturnURLEmulator.png
[relying_party_realm_production]: ./media/active-directory-java-authenticate-users-access-control-eclipse/RelyingPartyRealmProduction.png
[relying_party_return_url_production]: ./media/active-directory-java-authenticate-users-access-control-eclipse/RelyingPartyReturnURLProduction.png
[add_cert_component]: ./media/active-directory-java-authenticate-users-access-control-eclipse/AddCertificateComponent.png
[add_jsp_file_acs]: ./media/active-directory-java-authenticate-users-access-control-eclipse/AddJSPFileACS.png
[create_acs_hello_world]: ./media/active-directory-java-authenticate-users-access-control-eclipse/CreateACSHelloWorld.png
[add_token_signing_cert]: ./media/active-directory-java-authenticate-users-access-control-eclipse/AddTokenSigningCertificate.png

