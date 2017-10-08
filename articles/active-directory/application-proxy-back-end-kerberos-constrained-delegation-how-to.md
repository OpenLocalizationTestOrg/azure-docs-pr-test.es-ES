---
title: "aaaHow tooconfigure una toouse de aplicación de Proxy de aplicación delegación limitada de Kerberos | Documentos de Microsoft"
description: "¿Cómo tooconfigure delegación limitada de Kerberos para una aplicación de Proxy de aplicación de Azure AD."
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 93dac264ff1d3b99dead1d9c759c37c59373cbd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-an-application-proxy-application-toouse-kerberos-constrained-delegation"></a>¿Cómo tooconfigure una toouse de aplicación de Proxy de aplicación delegación limitada de Kerberos

Hola métodos disponibles para lograr toopublished SSO las aplicaciones pueden variar un poco de tooapplication de aplicación y una de las opciones de Hola que el Proxy de aplicación de Azure ofrece desde el principio de hello, es la delegación limitada de Kerberos (KCD). Esto es que un host de conector configurado tooperform limitada kerberos authentication toobackend aplicaciones, en nombre de los usuarios.

procedimiento de Hello en Sí para habilitar KCD es relativamente sencillo y no requiere normalmente más de una descripción general del programa Hola a varios componentes y flujo de autenticación que facilita SSO. Encontrar buenas fuentes de información toohelp solucionar problemas de escenarios donde KCD SSO no funcione según lo previsto, puede ser dispersas.

Por lo tanto, este artículo intenta tooprovide un único punto de referencia que debe ayudar a solucionar problemas y corregir automáticamente algunos de los problemas más comunes de Hola que vemos. En hello mismas instrucciones adicionales de oferta de tiempo para diagnosticar Hola más compleja y con problemas de implementación.

Tenga en cuenta que este artículo hace Hola siguientes supuestos:

-   Proxy de aplicación de Azure se ha implementado según nuestro [documentación](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-enable) y las aplicaciones de acceso general toonon KCD funciona según lo previsto.

-   Hello destino publicado aplicación se basa en la implementación de IIS y de Microsoft de kerberos.

-   hosts de servidor y una aplicación Hola residen en un único dominio de Active Directory. Encontrará información detallada sobre los escenarios de bosque y entre dominios en nuestras [notas del producto para KCD](http://aka.ms/KCDPaper).

-   Hello aplicación en cuestión se publica en un Azure inquilino con autenticación previa está habilitada y los usuarios se esperan autenticación basada en tooauthenticate tooAzure a través de formularios. Escenarios de autenticación de cliente enriquecido no están cubiertos por este artículo, pero agregará en algún momento futuro Hola.

## <a name="prerequisites"></a>Requisitos previos

Proxy de aplicación de Azure se pueden implementar en prácticamente cualquier tipo de infraestructura o arquitecturas hello y entorno sin duda varían con respecto a tooorganization de organización. Uno de los motivos más comunes de Hola de KCD relacionados con problemas no son entornos Hola por sí mismos, pero bastante sencillas configuraciones mal o supervisión general.

Por esta razón, nuestro Consejo es siempre toostart asegurándose de que se cumplen todos los requisitos previos de hello dispuestos en nuestro main [mediante KCD SSO con el artículo de Proxy de aplicación Hola](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) antes de iniciar solución de problemas.

Sección sobre la configuración de KCD en 2012R2, tal y como se emplea un enfoque diferente tooconfiguring KCD en versiones anteriores de Windows, sino también al que se va a prestar atención a varias otras consideraciones se Hola especialmente:

-   No es raro que un servidor de miembro dominio tooopen un cuadro de diálogo de canal seguro con un controlador de dominio específico. A continuación, mueva tooanother diálogo en cualquier momento, para que hosts de conector generalmente no deben estar restringido toobeing toocommunicate capaz de controladores de dominio del sitio local solo específico.

-   Toohello similar por encima de punto, escenarios entre dominios se basan en las referencias a la que dirigir un tooDCs de host de conector que pueden residir fuera de perímetro de la red local de Hola. En este escenario es igualmente importante toomake seguro también va a permitir tráfico en adelante tooDCs que representan otros dominios respectivos, o bien delegación producirá un error.

-   Siempre que sea posible, debe evitar colocar dispositivos IPS/IDS activos entre los hosts de conector y los controladores de dominio, ya que en ocasiones son demasiado intrusivos e interfieren con el tráfico RPC central.

Nos gustaría tooresolve problemas rápidamente y de hecho, puede tardar tiempo, por lo que siempre que sea posible debe intente y probar la delegación en hello más sencilla de escenarios. Hola más variables que se va a introducir, hello más tendrá toocontend con. Por ejemplo, limitar el prueba tooa único conector puede ahorrar tiempo valioso y conectores adicionales pueden agregarse una vez resueltos los problemas de Hola.

Algunos factores del entorno podrían también estar contribuyendo tooan problema, por lo que si es posible intente y minimizar Hola arquitectura tooa mínimo para realizar pruebas. Por ejemplo, el firewall interno mal configurada ACL no son habituales, por lo que si es posible tener todo el tráfico de un conector permite directamente a través de los controladores de dominio de toohello y aplicación back-end. 

En realidad Hola absoluta mejor lugar tooposition conectores es tan cerca de tootheir de destinos, como puede ser. Tener un firewall en línea durante las pruebas simplemente agrega complejidad innecesaria y podría prolongarlas.

De todos modos, ¿qué constituye un problema de KCD? Bueno, hay varias indicaciones clásicas de SSO de KCD hello y error primeros síntomas de un problema normalmente se manifiestan en Hola explorador.

   ![Error de configuración de KCD incorrecta](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic1.png)

   ![Error debido a permisos toomissing de autorización](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic2.png)

todos los que lleven Hola mismo síntoma del error tooperform SSO y, por consiguiente, denegar Hola aplicación toohello de acceso de usuario.

## <a name="troubleshooting"></a>Solución de problemas

Cómo solucionar, a continuación, dependen de problema de Hola y observa síntomas. Antes de pasar cualquier más se indicaría Hola siguientes vínculos, ya que contienen información útil que no ha incluido en:

-   [Solución de problemas y mensajes de error de Proxy de aplicación](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-troubleshoot)

-   [Errores y síntomas de Kerberos](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-troubleshoot#kerberos-errors)

-   [Trabajar con SSO cuando las identidades locales y en la nube no son idénticas](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd#working-with-sso-when-on-premises-and-cloud-identities-are-not-identical)

Si tiene este extremo, a continuación, hello principal problema definitivamente existe. Necesita toodig más profundo, por lo que se inicie mediante la separación de flujo de hello en tres fases distintas que puede solucionar.

**Autenticación previa del cliente** -usuario externo Hola autenticar tooAzure a través de un explorador.

Que se va a toopre pueda-autenticar tooAzure es imprescindible toofunction KCD SSO. Esto es lo primero que se debe probar y solucionar, si hay algún problema. Tenga en cuenta que fase de autenticación previa de hello no tiene ninguna relación tooKCD o hello publicó la aplicación. Debería ser bastante fácil toocorrect cualquier discrepancia por integridad comprobando Hola sujeto cuenta existe en Azure y que no está deshabilitado o bloquean. respuesta de error de Hello en el Explorador de hello es normalmente lo suficientemente descriptivo toounderstand Hola. También puede comprobar nuestro otro tooverify de documentos de solución de problemas si no es seguro.

**Servicio de delegación** -Hola conector del Proxy de Azure de obtener un kerberos vale de servicio desde un KDC (centro de distribución de Kerberos), en nombre de los usuarios.

Hola las comunicaciones externas entre el cliente de Hola y Hola Azure front-end no tienen ninguna relación en KCD sea, distinto de asegurarse de que funciona. Se trata de modo que pueda validarse Hola servicio Proxy de Azure siempre con un Id. de usuario se va a tooobtain usa un vale de kerberos. Sin este KCD, no es posible y se produciría un error.

Tal y como se mencionó anteriormente, mensajes de error del explorador de Hola suelen proporcionan algunos buenos pistas sobre por qué se producen errores en acciones. Que seguro toonote hacia abajo el Id. de actividad de Hola y marca de tiempo de respuesta de hello como esto permitirá eventos tooactual de toocorrelate Hola comportamiento en el registro de eventos de Proxy de Azure de Hola.

   ![Error de configuración de KCD incorrecta](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic3.png)

Y registro de eventos de las entradas correspondientes de Hola Hola encontrada podría verse como eventos 13019 o 12027. Puede encontrar registros de eventos del conector en hello **registros de aplicaciones y servicios** &gt; **Microsoft** &gt; **AadApplicationProxy** &gt; **Conector**&gt;**administración**.

   ![Evento 13019 del registro de eventos del proxy de aplicación](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic4.png)

   ![Evento 12027 del registro de eventos del proxy de aplicación](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic5.png)

-   Usar un registro en su DNS interno para la dirección de la aplicación hello y no un CName

-   Vuelvan a confirmar que hospedan de conector Hola concedió Hola derechos toodelegate toohello designado SPN de la cuenta de destino y que **usar cualquier protocolo de autenticación** está seleccionada. Esto se trata en el artículo principal [sobre la configuración del SSO](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd).

-   Compruebe que hay una sola instancia de hello SPN existente en AD mediante la emisión de un **setspn - x** desde un símbolo del sistema en cualquier host de miembro de dominio

-   Comprobar toosee si se está configurando una directiva de dominio exige hello toolimit [tamaño máximo de tokens de kerberos emitido](https://blogs.technet.microsoft.com/askds/2012/09/12/maxtokensize-and-windows-8-and-windows-server-2012/), ya que este conector de hello impedir obtengan un token si encontró toobe excesivo

Un seguimiento de red capturar intercambios de hello entre el host de conector de Hola y un dominio KDC, a continuación, sería el siguiente paso recomendado hello en la obtención de más bajo nivel obtener detalles sobre problemas de Hola. Puede encontrarlo en el [artículo que profundiza en la solución de problemas](https://aka.ms/proxytshootpaper).

Si compra de vales aspecto atractivo, debería ver un evento en los registros de Hola que indica que la autenticación no se pudo debido aplicación toohello devuelve 401. Esto suele indicar que esa aplicación de destino de hello rechazando el vale, por lo que continúe con hello después de la siguiente fase.

**La aplicación de destino** -consumidor Hola de vale de kerberos de hello proporcionada por el conector de Hola

En este conector de hello fase ¿toohave esperado se envía un backend toohello de vale de servicio de kerberos, como un encabezado dentro de la primera solicitud de aplicación Hola.

-   Mediante la aplicación hello URL interna definido en el portal de hello, validar que la aplicación hello es accesible directamente desde el Explorador de hello en el host de conector de Hola. Entonces, puede iniciar sesión correctamente. Encontrará detalles sobre cómo hacer esto en la página de solución de problemas del conector de Hola.

-   Todavía en el host de conector de hello, confirme que la autenticación entre el Explorador de Hola Hola y aplicación hello está utilizando kerberos, llevando a cabo una de las siguientes de hello:

1.  Ejecutar herramientas de desarrollo (**F12**) en Internet Explorer o utilice [Fiddler](https://blogs.msdn.microsoft.com/crminthefield/2012/10/10/using-fiddler-to-check-for-kerberos-auth/) de host de conector de Hola. Vaya aplicación toohello con la dirección URL interna de hello e inspeccionar Hola ofrecida encabezados de autorización de World Wide Web devueltos una respuesta Hola de aplicación hello, tooensure que cualquiera negotiate o kerberos está presente. Un blob de kerberos posteriores se devuelve en respuesta de Hola de hello explorador toohello aplicación normalmente empieza con **YII**, por lo que se trata de una buena indicación de kerberos en play. NTLM en hello otra parte siempre se inician con **TlRMTVNTUAAB**, que lee NTLMSSP al descodificar de Base64. Si ve **TlRMTVNTUAAB** en un primer Hola de blob de hello, esto significa que es Kerberos **no** disponible. Si no lo ve, es probable que Kerberos esté disponible.

  * Tenga en cuenta que si usa Fiddler, este método requiere deshabilitar temporalmente la protección ampliada en configuración de la aplicación hello en IIS.

     ![Ventana de inspección de red del explorador](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic6.png)

    *Ilustración:* como no empieza por TIRMTVNTUAAB, en este ejemplo, Kerberos está disponible. Se trata de un ejemplo de blob de Kerberos que no empieza por YII.

2.  Quitar temporalmente NTLM de la lista de proveedores de hello en el sitio y acceso aplicación IIS directamente desde Internet Explorer en el host de conector. Con NTLM ya no está en la lista de proveedores de hello, debería tooaccess capaz de aplicación de hello sólo se utiliza Kerberos. Si se produce un error, a continuación, que indica que hay un problema con la configuración de la aplicación hello y la autenticación Kerberos no está funcionando.

Si Kerberos no está disponible, negociar la configuración de IIS toomake seguro de autenticación de la aplicación de verificación Hola aparece superior, con NTLM justo debajo de él. (No Negociar:Kerberos o Negociar:PKU2U). Continúe solamente si Kerberos es funcional.

   ![Proveedores de autenticación de Windows](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic7.png)
   
-   Con la autenticación Kerberos y NTLM en su lugar, permite ahora deshabilitar temporalmente la autenticación previa para la aplicación hello en el portal de Hola. Si puede tener acceso desde Hola internet con la dirección URL externa de Hola. Debe ser tooauthenticate solicitada y debe ser capaz de toodo para que con hello misma cuenta Hola utilizado en un paso anterior. Si no es así, esto indica un problema con la aplicación de back-end de hello y no KCD en absoluto.

-   Ahora vuelva a habilitar la autenticación previa en el portal de Hola y autenticarse a través de Azure al intentar tooconnect toohello aplicación a través de su URL externa. Si se produce un error de SSO, verá un mensaje de error prohibido en Explorador de hello, además de evento 13022 en el registro de hello:

    *Conector del Proxy de aplicación de AAD de Microsoft no puede autenticar el usuario de hello porque el servidor back-end de hello responde tooKerberos los intentos de autenticación con un error HTTP 401.*

    ![Error HTTTP 401: Prohibido](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic8.png)

-   Comprobar grupo de aplicaciones de hello IIS aplicación tooensure Hola configurado es hello toouse configurado misma cuenta que Hola SPN se ha configurado con en AD, desplazándose en IIS, como se muestra a continuación

    ![Ventana de configuración de la aplicación IIS](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic9.png)

    Una vez que sepa identidad hello, emitir siguiente Hola de toomake de símbolo del sistema de cmd que esta cuenta definitivamente esté configurada con hello SPN en cuestión. Por ejemplo, **setspn – q http/spn.wacketywack.com**

    ![Ventana de comando SetSPN](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic10.png)

-   Compruebe que Hola SPN definida en relación con la configuración de la aplicación hello en el portal de hello es Hola mismo SPN que se configura en la cuenta de AD de destino de hello en uso por grupo de aplicaciones de la aplicación hello

   ![Configuración del SPN en Azure Portal](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic11.png)
   
-   Vaya a IIS y seleccione hello **Editor de configuración de** opción aplicación hello y navegue demasiado**system.webServer/security/authentication/windowsAuthentication** toomake seguro de que **UseAppPoolCredentials** se establece tootrue

   ![Opción de credencial de grupos de aplicaciones en la configuración de IIS](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic12.png)

Al ser útiles para mejorar el rendimiento de Hola de operaciones de Kerberos, también deja habilitado el modo de Kernel hace vale de Hola para hello solicitado toobe servicio descifrado usando la cuenta de equipo. También se conoce como sistema Local de hello, por lo que tiene este salto de tootrue conjunto KCD cuando se hospeda la aplicación hello en varios servidores en una granja de servidores.

-   Como una comprobación adicional, puede que también desee hello toodisable **extendido** protección demasiado. Se han encontrado escenarios donde esto ha demostrado toobreak KCD cuando haya habilitado en configuraciones muy específicas, donde se publica una aplicación como una subcarpeta del sitio Web predeterminado de Hola. Este propio está configurado para la autenticación anónima, dejando Hola todo los cuadros de diálogo sugerir objetos secundarios no se heredan cualquier configuración activa en gris. Pero donde posibles siempre le recomendamos tener esta opción habilitada, por lo que en todo caso de prueba, pero no olvide toorestore esta tooenabled.

Estas comprobaciones adicionales deben haber ponerte en toostart de seguimiento mediante la aplicación publicada. Puede seguir adelante y acelerar conectores adicionales que también estén configurados toodelegate, pero si ningún otras las cosas son, a continuación, se indicaría una lectura de nuestro tutorial técnica más detallada [guía completa de Hola para solucionar problemas de Azure AD aplicación Proxy](https://aka.ms/proxytshootpaper)

Si está todavía no se puede tooprogress el problema, soporte técnico se puede superar los tooassist satisfecho y continuar desde aquí. Cree una incidencia de soporte técnico directamente en el portal de Hola y nuestros ingenieros se dirigirá tooyou.

## <a name="other-scenarios"></a>Otros escenarios

-   Proxy de aplicación de Azure, se solicita un vale de Kerberos antes de enviar su aplicación tooan de solicitud. Algunas aplicaciones de terceros 3rd como Tableau Server no le gusta este método de autenticación y en su lugar espera más convencional Hola negociaciones tootake lugar,. Hola primera solicitud es anónimo, permitir Hola aplicación toorespond con los tipos de autenticación de Hola que admite a través de 401.

-   Autenticación de dos saltos: se utiliza normalmente en escenarios con una aplicación en niveles, con un back-end y un front-end, ambos de los cuales requieren autenticación, como SQL Reporting Services.

## <a name="next-steps"></a>Pasos siguientes
[Configuración de la delegación limitada de Kerberos (KCD) en un dominio administrado](https://docs.microsoft.com/azure/active-directory-domain-services/active-directory-ds-enable-kcd)
