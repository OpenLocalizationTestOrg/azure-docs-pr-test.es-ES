---
title: aaaAuthentication - herramienta de modelado de amenazas de Microsoft - Azure | Documentos de Microsoft
description: mitigaciones en busca de amenazas que se exponen en hello herramienta de modelado de amenazas
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: 06c1b1aebab25e6fb5b666d24ecd9d86085d656c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-authentication--mitigations"></a>Marco de seguridad: autenticación | Mitigaciones 
| Producto o servicio | Artículo |
| --------------- | ------- |
| **Aplicación web**    | <ul><li>[Considere el uso de un tooWeb de tooauthenticate del mecanismo de autenticación estándar aplicación](#standard-authn-web-app)</li><li>[Las aplicaciones deben administrar escenarios de errores de autenticación de forma segura](#handle-failed-authn)</li><li>[Habilitación de la autenticación adicional o adaptable](#step-up-adaptive-authn)</li><li>[Asegurarse de que las interfaces administrativas estén correctamente bloqueadas](#admin-interface-lockdown)</li><li>[Implementación de funcionalidades de contraseña olvidada de forma segura](#forgot-pword-fxn)</li><li>[Asegurarse de que se implementen directivas de cuenta y contraseña](#pword-account-policy)</li><li>[Implemente controles tooprevent nombre de usuario (enumeración)](#controls-username-enum)</li></ul> |
| **Base de datos** | <ul><li>[Cuando sea posible, utilice la autenticación de Windows para conectar tooSQL Server](#win-authn-sql)</li><li>[Cuando sea posible, utilice autenticación de Azure Active Directory para conectar tooSQL base de datos](#aad-authn-sql)</li><li>[Cuando se use el modo de autenticación de SQL, asegurarse de que se apliquen directivas de cuenta y contraseña en SQL Server](#authn-account-pword)</li><li>[No usar la autenticación SQL en bases de datos independientes](#autn-contained-db)</li></ul> |
| **Centro de eventos de Azure** | <ul><li>[Uso de credenciales de autenticación por dispositivo mediante tokens SaS](#authn-sas-tokens)</li></ul> |
| **Límites de confianza de Azure** | <ul><li>[Habilitación de Azure Multi-Factor Authentication para administradores de Azure](#multi-factor-azure-admin)</li></ul> |
| **Límites de confianza de Service Fabric** | <ul><li>[Restringir el acceso anónimo tooService clúster Fabric](#anon-access-cluster)</li><li>[Asegurarse de que el certificado de cliente a nodo de Service Fabric sea diferente del certificado de nodo a nodo](#fabric-cn-nn)</li><li>[Usar clústeres de los clientes de AAD tooauthenticate tooservice tejido](#aad-client-fabric)</li><li>[Asegurarse de que los certificados de Service Fabric se obtienen de una entidad de certificación (CA) aprobada](#fabric-cert-ca)</li></ul> |
| **Identity Server** | <ul><li>[Uso de escenarios de autenticación estándar admitidos por Identity Server](#standard-authn-id)</li><li>[Invalidar Hola Identity Server token memoria caché predeterminada con una alternativa escalable](#override-token)</li></ul> |
| **Límite de confianza de la máquina** | <ul><li>[Asegurarse de que los archivos binarios de la aplicación implementada están firmados digitalmente](#binaries-signed)</li></ul> |
| **WCF** | <ul><li>[Habilitar la autenticación al conectarse tooMSMQ colas en WCF](#msmq-queues)</li><li>[Realice de WCF no establece mensaje clientCredentialType toonone](#message-none)</li><li>[Realice de WCF no establece transporte clientCredentialType toonone](#transport-none)</li></ul> |
| **API web** | <ul><li>[Asegúrese de que las técnicas de autenticación estándar toosecure usa las API Web](#authn-secure-api)</li></ul> |
| **Azure AD** | <ul><li>[Uso de escenarios de autenticación estándar compatibles con Azure Active Directory](#authn-aad)</li><li>[Invalidar Hola AAL token memoria caché predeterminada con una alternativa escalable](#adal-scalable)</li><li>[Asegúrese de que TokenReplayCache es tooprevent usados al reproducir Hola de tokens de autenticación de ADAL](#tokenreplaycache-adal)</li><li>[Usar el token de bibliotecas de ADAL toomanage solicita de OAuth2 clientes tooAAD (o AD local)](#adal-oauth2)</li></ul> |
| **Puerta de enlace de campo de IoT** | <ul><li>[Autenticar los dispositivos que se conectan toohello puerta de enlace de campo](#authn-devices-field)</li></ul> |
| **Puerta de enlace de nube de IoT** | <ul><li>[Asegúrese de que se autentican los dispositivos que se conectan tooCloud puerta de enlace](#authn-devices-cloud)</li><li>[Uso de credenciales de autenticación por dispositivo](#authn-cred)</li></ul> |
| **Azure Storage** | <ul><li>[Asegúrese de que solo Hola requiera contenedores y blobs tienen acceso de lectura anónimo](#req-containers-anon)</li><li>[Conceder acceso limitado tooobjects en almacenamiento de Azure mediante SAS o SAP](#limited-access-sas)</li></ul> |

## <a id="standard-authn-web-app"></a>Considere el uso de un tooWeb de tooauthenticate del mecanismo de autenticación estándar aplicación

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Aplicación web | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | N/D  |
| Detalles | <p>La autenticación es el proceso Hola donde una entidad demuestre su identidad, normalmente a través de las credenciales, como un nombre de usuario y una contraseña. Hay varios protocolos de autenticación disponibles que se pueden considerar. A continuación se enumeran algunos de ellos:</p><ul><li>Certificados de cliente</li><li>Basado en Windows</li><li>Basado en formularios</li><li>Federación - ADFS</li><li>Federación - Azure AD</li><li>Federación - Identity Server</li></ul><p>Considere el uso de un proceso de autenticación estándar mecanismo tooidentify Hola origen</p>|

## <a id="handle-failed-authn"></a>Las aplicaciones deben administrar escenarios de errores de autenticación de forma segura

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Aplicación web | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | N/D  |
| Detalles | <p>Las aplicaciones que explícitamente autentican a los usuarios deben administrar escenarios de autenticación con errores securely.hello mecanismo de autenticación debe:</p><ul><li>Denegar el acceso tooprivileged recursos cuando se produce un error de autenticación</li><li>Mostrar un mensaje de error genérico después de que se produzca el error de autenticación y la denegación del acceso.</li></ul><p>Deberá comprobar:</p><ul><li>La protección de recursos con privilegios después de errores de inicios de sesión.</li><li>Se muestra un mensaje de error genérico en los eventos de error de autenticación y denegación del acceso.</li><li>Las cuentas se deshabilitan después de un número excesivo de intentos erróneos.</li><ul>|

## <a id="step-up-adaptive-authn"></a>Habilitación de la autenticación adicional o adaptable

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Aplicación web | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | N/D  |
| Detalles | <p>Compruebe la aplicación hello tiene autorización adicional (como paso hacia arriba o autenticación adaptable, a través de la autenticación multifactor como el envío de OTP de SMS, etc. de correo electrónico o solicite la reautenticación) por lo que supone un desafío usuario Hola antes de que se concede acceso información de toosensitive. Esta regla también se aplica para hacer que la cuenta de tooan cambios críticos o acción</p><p>Esto también significa que la adaptación Hola de autenticación tiene toobe implementa de tal forma que aplicación hello correctamente exige autorización contextual así como toonot permiten manipulación no autorizada por medio de en el ejemplo, la manipulación de parámetro</p>|

## <a id="admin-interface-lockdown"></a>Asegurarse de que las interfaces administrativas estén correctamente bloqueadas

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Aplicación web | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | N/D  |
| Detalles | Hola primera solución es toogrant acceso únicamente a partir de un determinado origen IP intervalo toohello interfaz administrativa. Si esta solución no es posible que siempre es recomendable tooenforce una autenticación superior o adaptable para iniciar sesión en la interfaz administrativa de Hola |

## <a id="forgot-pword-fxn"></a>Implementación de funcionalidades de contraseña olvidada de forma segura

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Aplicación web | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | N/D  |
| Detalles | <p>Hola lo primero es tooverify que olvidó la contraseña y otras rutas de acceso de recuperación envían un vínculo incluido una activación de tiempo limitado símbolo (token) en lugar de hello propia contraseña. Autenticación adicional basada en tokens de software (por ejemplo, aplicaciones móviles nativas, símbolo (token) de SMS, etc.) puede ser necesaria también antes vínculo Hola se envía a través. En segundo lugar, no debe bloquear cuenta de usuarios de hello al proceso de Hola de obtener una nueva contraseña está en curso.</p><p>Esto podría provocar tooa denegación de servicio cada vez que un atacante decide toointentionally de bloqueo a los usuarios de hello un ataque automatizado. En tercer lugar, cada vez que se estableció la nueva solicitud de contraseña de hello en curso, deben generalizarse con mensajes de bienvenida que se muestra en la enumeración de orden tooprevent nombre de usuario. En cuarto lugar, siempre que no Hola uso de las contraseñas antiguas e implemente una directiva de contraseña segura.</p> |

## <a id="pword-account-policy"></a>Asegurarse de que se implementen directivas de cuenta y contraseña

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Aplicación web | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | N/D  |
| Detalles | <p>Se deben implementar directivas de cuenta y contraseña en conformidad con la política de la organización y los procedimientos recomendados.</p><p>toodefend con fuerza bruta y de diccionario basado adivinen: directiva de contraseña segura debe estar implementado tooensure que los usuarios creen una contraseña compleja (por ejemplo, longitud mínima de 12 caracteres, los caracteres especiales y alfanuméricos).</p><p>Directivas de bloqueo de cuenta pueden implementarse en hello siguiente manera:</p><ul><li>**Bloqueo temporal**: puede ser una buena opción para proteger a los usuarios contra ataques por fuerza bruta. Por ejemplo, cada vez que el usuario Hola entra en una aplicación de hello tres veces una contraseña incorrecta podría bloquear cuenta de hello durante un minuto en orden tooslow proceso Hola de su contraseña realizar menos rentables para hello atacante tooproceed de fuerza bruta. Si se encontraba tooimplement disco duro contramedidas de espera de bloqueo en este ejemplo lograría un "Dos" by permanentemente el bloqueo de cuentas. Como alternativa, puede generar una OTP (contraseña temporal) y enviarlo fuera de banda aplicación (a través de correo electrónico, sms, etc.) toohello usuario. Otro enfoque podrá tooimplement CAPTCHA cuando se alcanza un número de umbral de intentos fallidos.</li><li>**Disco duro de espera de bloqueo:** este tipo de bloqueo se debe aplicar cada vez que detecta un usuario para atacar la aplicación y le contador por medio de bloquear permanentemente su cuenta hasta que un equipo de respuesta tenía tiempo toodo su análisis forense. Tras este proceso puede decidir su cuenta de usuario nuevo de toogive Hola o realizar más acciones legales frente a él. Este tipo de enfoque impide que el atacante de hello penetración aún más la aplicación e infraestructura.</li></ul><p>toodefend frente a ataques en de forma predeterminada y las cuentas de predicción, compruebe que todas las claves y contraseñas son reemplazables y se genera o reemplazadas después de la hora de instalación.</p><p>Si la aplicación hello tiene tooauto-generar contraseñas, asegúrese de que las contraseñas de hello generado son aleatorias y que tienen alta entropía.</p>|

## <a id="controls-username-enum"></a>Implemente controles tooprevent nombre de usuario (enumeración)

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Aplicación web | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | N/D  |
| **Pasos** | Todos los mensajes de error deben estar generalizados de enumeración de orden tooprevent nombre de usuario. También, no podrá evitar a veces la pérdida de información en funcionalidades tales como una página de registro. Aquí deberá métodos de limitación de velocidad de toouse como CAPTCHA tooprevent un ataque automatizado por un atacante. |

## <a id="win-authn-sql"></a>Cuando sea posible, utilice la autenticación de Windows para conectar tooSQL Server

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Base de datos | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | OnPrem |
| **Atributos**              | Versión de SQL: todas |
| **Referencias**              | [SQL Server: elegir un modo de autenticación](https://msdn.microsoft.com/library/ms144284.aspx) |
| **Pasos** | Autenticación de Windows usa el protocolo de seguridad de Kerberos, proporciona la aplicación de directivas de contraseña con la validación de toocomplexity de tener en cuenta para las contraseñas seguras, proporciona compatibilidad para el bloqueo de cuentas y admite la expiración de contraseña.|

## <a id="aad-authn-sql"></a>Cuando sea posible, utilice autenticación de Azure Active Directory para conectar tooSQL base de datos

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Base de datos | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | SQL Azure |
| **Atributos**              | Versión de SQL: V12 |
| **Referencias**              | [Conexión tooSQL base de datos mediante Active Directory autenticación de Azure](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/) |
| **Pasos** | **Versión mínima:** V12 de base de datos de SQL Azure requiere tooallow base de datos de SQL Azure toouse autenticación de AAD contra Hola Microsoft Directory |

## <a id="authn-account-pword"></a>Cuando se use el modo de autenticación de SQL, asegurarse de que se apliquen directivas de cuenta y contraseña en SQL Server

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Base de datos | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | [Directiva de contraseñas de SQL Server](https://technet.microsoft.com/library/ms161959(v=sql.110).aspx) |
| **Pasos** | Cuando se usa la autenticación de SQL Server, se crean inicios de sesión en SQL Server que no se basan en cuentas de usuario de Windows. Nombre de usuario de Hola y la contraseña de Hola se crean mediante el uso de SQL Server y se almacenan en SQL Server. SQL Server puede emplear mecanismos de directiva de contraseñas de Windows. Puede aplicar Hola mismas directivas de complejidad y expiración que se usan en toopasswords de Windows que se utiliza dentro de SQL Server. |

## <a id="autn-contained-db"></a>No usar la autenticación SQL en bases de datos independientes

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Base de datos | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | OnPrem, SQL Azure |
| **Atributos**              | Versión de SQL: MSSQL2012, Versión de SQL: V12 |
| **Referencias**              | [Prácticas recomendadas de seguridad con bases de datos independientes](http://msdn.microsoft.com/library/ff929055.aspx) |
| **Pasos** | ausencia de Hola de una directiva de contraseña obligatoria puede aumentar la probabilidad de Hola de una credencial no segura que se va a establecer en una base de datos independiente. Aproveche la autenticación de Windows. |

## <a id="authn-sas-tokens"></a>Uso de las credenciales de autenticación por dispositivo mediante tokens SaS

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Centro de eventos de Azure | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | [Introducción al modelo de autenticación y seguridad de Event Hubs](https://azure.microsoft.com/documentation/articles/event-hubs-authentication-and-security-model-overview/) |
| **Pasos** | <p>modelo de seguridad de los centros de eventos de Hola se basa en una combinación de símbolos (tokens) de firma de acceso compartido (SAS) y publicadores de eventos. nombre del publicador Hola representa Hola DeviceID que recibe el token de Hola. Esto contribuye a asociar los tokens de hello generados con dispositivos respectivos Hola.</p><p>Todos los mensajes se etiquetan con el originador en el lado del servicio, lo que permite la detección de los intentos de suplantación de origen en la carga. Al autenticar a los dispositivos, generar un por publicador exclusivo de token tooa con ámbito de SaS de dispositivo.</p>|

## <a id="multi-factor-azure-admin"></a>Habilitación de Azure Multi-Factor Authentication para administradores de Azure

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Límites de confianza de Azure | 
| **Fase de SDL**               | Implementación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | [¿Qué es Azure Multi-Factor Authentication?](https://azure.microsoft.com/documentation/articles/multi-factor-authentication/) |
| **Pasos** | <p>La autenticación multifactor (MFA) es un método de autenticación que requiere más de un método de comprobación y agrega una segunda capa crítica de inicios de sesión de seguridad toouser y las transacciones. Funciona solicitando dos o más de hello siguiendo métodos de comprobación:</p><ul><li>Un elemento que conoce (normalmente una contraseña).</li><li>Un elemento del que dispone (un dispositivo de confianza que no se puede duplicar con facilidad, como un teléfono).</li><li>Un elemento físico que le identifica (biométrica).</li><ul>|

## <a id="anon-access-cluster"></a>Restringir el acceso anónimo tooService clúster Fabric

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Límites de confianza de Service Fabric | 
| **Fase de SDL**               | Implementación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | Entorno: Azure  |
| **Referencias**              | [Escenarios de seguridad de los clústeres de Service Fabric](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security) |
| **Pasos** | <p>Clústeres siempre deben ser segura tooprevent no autorizado a los usuarios conecten clúster tooyour, especialmente cuando tiene las cargas de trabajo de producción en ejecución.</p><p>Al crear un clúster de service fabric, asegúrese de que el modo de seguridad Hola está establecido demasiado "seguro" y configurar certificado de servidor X.509 Hola necesario. Creación de un clúster de "inseguro" permitirá que cualquier tooit tooconnect de usuario anónimo si expone toohello de puntos de conexión de administración pública de Internet.</p>|

## <a id="fabric-cn-nn"></a>Asegurarse de que el certificado de cliente a nodo de Service Fabric sea diferente del certificado de nodo a nodo

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Límites de confianza de Service Fabric | 
| **Fase de SDL**               | Implementación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | Entorno: Azure, Entorno: independiente |
| **Referencias**              | [Seguridad de certificados de cliente para el nodo de Service Fabric](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/#_client-to-node-certificate-security), [conectar tooa clúster segura mediante el certificado de cliente](https://azure.microsoft.com/documentation/articles/service-fabric-connect-to-secure-cluster/) |
| **Pasos** | <p>Seguridad de los certificados de cliente para el nodo se configura al crear el clúster de hello ya sea a través del portal de Azure hello, plantillas de administrador de recursos o una plantilla JSON independiente mediante la especificación de un certificado de cliente de administración o un certificado de cliente.</p><p>Hola Administrador cliente y al usuario los certificados de cliente que especifique deben ser diferentes de certificados principales y secundarias de Hola que especifique para la seguridad de nodo a nodo.</p>|

## <a id="aad-client-fabric"></a>Usar clústeres de los clientes de AAD tooauthenticate tooservice tejido

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Límites de confianza de Service Fabric | 
| **Fase de SDL**               | Implementación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | Entorno: Azure |
| **Referencias**              | [Escenarios de seguridad de los clústeres de Service Fabric](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/#security-recommendations) |
| **Pasos** | Clústeres que se ejecutan en Azure también pueden proteger el acceso toohello puntos de conexión de administración mediante Azure Active Directory (AAD), además de los certificados de cliente. Para los clústeres de Azure, se recomienda usar los clientes tooauthenticate de seguridad AAD y certificados para la seguridad de nodo a nodo.|

## <a id="fabric-cert-ca"></a>Asegurarse de que los certificados de Service Fabric se obtienen de una entidad de certificación (CA) aprobada

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Límites de confianza de Service Fabric | 
| **Fase de SDL**               | Implementación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | Entorno: Azure |
| **Referencias**              | [Certificados X.509 y Service Fabric](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/#x509-certificates-and-service-fabric) |
| **Pasos** | <p>Service Fabric usa certificados de servidor X.509 para autenticar nodos y clientes.</p><p>Tooconsider de algunos aspectos importantes al uso de certificados de tejidos de servicio:</p><ul><li>Los certificados usados en clústeres que ejecutan cargas de trabajo de producción deberán crearse mediante un servicio de certificados de Windows Server correctamente configurado u obtenerse de una entidad de certificación (CA) autorizada. Hola CA puede ser una CA externa aprobada o un correctamente administrado interno clave infraestructura pública (PKI)</li><li>No use nunca certificados temporales o de pruebas en producción creados con herramientas como MakeCert.exe.</li><li>Puede usar un certificado autofirmado, pero solo para clústeres de prueba y no para los que se encuentran en fase de producción.</li></ul>|

## <a id="standard-authn-id"></a>Uso de escenarios de autenticación estándar admitidos por Identity Server

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Identity Server | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | [IdentityServer3 - Hola panorama general](https://identityserver.github.io/Documentation/docsv2/overview/bigPicture.html) |
| **Pasos** | <p>A continuación se muestran Hola interacciones típicas admitidas por el servidor de identidades:</p><ul><li>Los exploradores se comunican con las aplicaciones web.</li><li>Las aplicaciones web se comunican con las API web (unas veces por sí mismas y otras en nombre de un usuario).</li><li>Las aplicaciones basadas en explorador se comunican con las API web.</li><li>Las aplicaciones nativas se comunican con las API web.</li><li>Las aplicaciones basadas en servidor se comunican con las API web.</li><li>Las API web se comunican con las API web (una veces por sí mismas y otras en nombre del usuario).</li></ul>|

## <a id="override-token"></a>Invalidar Hola Identity Server token memoria caché predeterminada con una alternativa escalable

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Identity Server | 
| **Fase de SDL**               | Implementación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | [Identity Server Deployment - Caching](https://identityserver.github.io/Documentation/docsv2/advanced/deployment.html) (Identity Server: implementación y almacenamiento en caché) |
| **Pasos** | <p>IdentityServer incorpora una caché en memoria sencilla. Si bien esto es adecuado para aplicaciones nativas de pequeña escala, no se escalan mid capa y back-end para las aplicaciones de hello siguientes motivos:</p><ul><li>Muchos usuarios acceden a la vez a estas aplicaciones. Guardar todos los tokens de acceso en hello mismo almacén crea problemas de aislamiento y presenta desafíos al operar a escala: muchos usuarios, cada uno con tokens tantos como recursos de Hola Hola accesos a la aplicación en su nombre, puede significar números muy grandes y búsqueda consume muchos recursos operaciones</li><li>Estas aplicaciones se implementan normalmente en las topologías distribuidas, donde varios nodos deben tener acceso toohello misma caché</li><li>Los tokens almacenados en caché deben sobrevivir a los reciclajes y las desactivaciones de los procesos.</li><li>Para todos los Hola por encima de motivos, al implementar aplicaciones web, se recomienda caché de tokens del servidor de identidad de toooverride Hola predeterminado con una alternativa escalable como la caché en Redis de Azure</li></ul>|

## <a id="binaries-signed"></a>Asegurarse de que los archivos binarios de la aplicación implementada están firmados digitalmente

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Límite de confianza de la máquina | 
| **Fase de SDL**               | Implementación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | N/D  |
| **Pasos** | Asegúrese de que los archivos binarios de la aplicación implementada se firman digitalmente para que se puede comprobar integridad de Hola de archivos binarios de Hola|

## <a id="msmq-queues"></a>Habilitar la autenticación al conectarse tooMSMQ colas en WCF

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | WCF | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico, .NET Framework 3 |
| **Atributos**              | N/D |
| **Referencias**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx) |
| **Pasos** | Programa produce un error tooenable autenticación al conectarse a las colas de tooMSMQ, un atacante puede enviar de forma anónima cola de mensajes toohello para su procesamiento. Si no es usado tooconnect tooan MSMQ cola utilizada toodeliver un programa de tooanother de mensaje de autenticación, un atacante podría enviar un mensaje de anónimo es malintencionado.|

### <a name="example"></a>Ejemplo
Hola `<netMsmqBinding/>` elemento del archivo de configuración de WCF de hello siguiente indica autenticación toodisable WCF cuando se conecte tooan cola MSMQ para la entrega de mensajes.
```
<bindings>
    <netMsmqBinding>
        <binding>
            <security>
                <transport msmqAuthenticationMode=""None"" />
            </security>
        </binding>
    </netMsmqBinding>
</bindings>
```
Configurar la autenticación de dominio de Windows o el certificado de toorequire MSMQ en todo momento para los mensajes entrantes o salientes.

### <a name="example"></a>Ejemplo
Hola `<netMsmqBinding/>` elemento del archivo de configuración de WCF de hello siguiente indica a autenticación de certificado WCF tooenable al conectarse tooan cola MSMQ. cliente de Hola se autentica utilizando certificados X.509. certificado de cliente de Hello debe encontrarse en el almacén de certificados de saludo del servidor hello.
```
<bindings>
    <netMsmqBinding>
        <binding>
            <security>
                <transport msmqAuthenticationMode=""Certificate"" />
            </security>
        </binding>
    </netMsmqBinding>
</bindings>
```

## <a id="message-none"></a>Realice de WCF no establece mensaje clientCredentialType toonone

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | WCF | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | .NET Framework 3 |
| **Atributos**              | ClientCredentialType: Ninguno |
| **Referencias**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Pasos** | ausencia de Hola de autenticación significa que todo el mundo es capaz de tooaccess este servicio. Un servicio que no se autentica a sus clientes permite el acceso a los usuarios de tooall. Configurar hello tooauthenticate de aplicación con las credenciales del cliente. Puede hacerlo estableciendo Hola mensaje clientCredentialType tooWindows o certificado. |

### <a name="example"></a>Ejemplo
```
<message clientCredentialType=""Certificate""/>
```

## <a id="transport-none"></a>Realice de WCF no establece transporte clientCredentialType toonone

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | WCF | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico, .NET Framework 3 |
| **Atributos**              | ClientCredentialType: Ninguno |
| **Referencias**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Pasos** | ausencia de Hola de autenticación significa que todo el mundo es capaz de tooaccess este servicio. Un servicio que no se autentica a sus clientes permite tooaccess de todos los usuarios de su funcionalidad. Configurar hello tooauthenticate de aplicación con las credenciales del cliente. Puede hacerlo estableciendo Hola transporte clientCredentialType tooWindows o certificado. |

### <a name="example"></a>Ejemplo
```
<transport clientCredentialType=""Certificate""/>
```

## <a id="authn-secure-api"></a>Asegúrese de que las técnicas de autenticación estándar toosecure usa las API Web

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | API Web | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | [Authentication and Authorization in ASP.NET Web API](http://www.asp.net/web-api/overview/security/authentication-and-authorization-in-aspnet-web-api), (Autenticación y autorización en la API web de ASP.NET) [External Authentication Services with ASP.NET Web API (C#)](http://www.asp.net/web-api/overview/security/external-authentication-services) (Servicios de autenticación externos con la API web de ASP.NET [C#]) |
| **Pasos** | <p>La autenticación es el proceso Hola donde una entidad demuestre su identidad, normalmente a través de las credenciales, como un nombre de usuario y una contraseña. Hay varios protocolos de autenticación disponibles que se pueden considerar. A continuación se enumeran algunos de ellos:</p><ul><li>Certificados de cliente</li><li>Basado en Windows</li><li>Basado en formularios</li><li>Federación - ADFS</li><li>Federación - Azure AD</li><li>Federación - Identity Server</li></ul><p>Vínculos en la sección de referencias de hello proporcionan detalles de bajo nivel sobre cómo cada uno de los esquemas de autenticación de hello puede ser implementan toosecure una API Web.</p>|

## <a id="authn-aad"></a>Uso de escenarios de autenticación estándar compatibles con Azure Active Directory

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Azure AD | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | [Escenarios de autenticación para Azure AD](https://azure.microsoft.com/documentation/articles/active-directory-authentication-scenarios/), [Ejemplos de código de Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-code-samples/), [Guía del desarrollador de Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-developers-guide/) |
| **Pasos** | <p>Azure Active Directory (Azure AD) simplifica la autenticación para los desarrolladores al proporcionar identidad como servicio, con compatibilidad con protocolos estándar de la industria, como OAuth 2.0 y OpenID Connect. A continuación se muestran Hola cinco escenarios principales de aplicación compatibles con Azure AD:</p><ul><li>Web tooWeb aplicación de explorador: un usuario necesita toosign en aplicación web de tooa que está protegida por Azure AD</li><li>Aplicación de página única (SPA): Un usuario necesita toosign en la aplicación de una página tooa que está protegida por Azure AD</li><li>Native aplicación tooWeb API: una aplicación nativa que se ejecuta en un teléfono, tableta o PC necesidades tooauthenticate un tooget usuario recursos desde una API web protegida por Azure AD</li><li>Web API tooWeb de aplicación: una aplicación web necesita recursos tooget desde una API web protegida por Azure AD</li><li>Demonio o una aplicación de servidor tooWeb API: una aplicación de demonio o una aplicación de servidor sin interfaz de usuario web necesita recursos tooget desde una API web protegida por Azure AD</li></ul><p>Consulte toohello vínculos en la sección de referencias de Hola para obtener detalles de implementación de nivel inferior</p>|

## <a id="adal-scalable"></a>Invalidar Hola AAL token memoria caché predeterminada con una alternativa escalable

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Azure AD | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | [Modern Authentication with Azure Active Directory for Web Applications](https://blogs.msdn.microsoft.com/microsoft_press/2016/01/04/new-book-modern-authentication-with-azure-active-directory-for-web-applications/) (Autenticación moderna con Azure Active Directory para aplicaciones web), [Using Redis as ADAL token cache](https://blogs.msdn.microsoft.com/mrochon/2016/09/19/using-redis-as-adal-token-cache/) (Uso de Redis como caché de tokens ADAL)  |
| **Pasos** | <p>Hola memoria caché predeterminada que usa AAL (biblioteca de autenticación de Active Directory) es una caché en memoria que se basa en un almacén estático, disponible en todo el proceso. Si bien esto funciona para las aplicaciones nativas, no se escalan mid capa y back-end para las aplicaciones de hello siguientes motivos:</p><ul><li>Muchos usuarios acceden a la vez a estas aplicaciones. Guardar todos los tokens de acceso en hello mismo almacén crea problemas de aislamiento y presenta desafíos al operar a escala: muchos usuarios, cada uno con tokens tantos como recursos de Hola Hola accesos a la aplicación en su nombre, puede significar números muy grandes y búsqueda consume muchos recursos operaciones</li><li>Estas aplicaciones se implementan normalmente en las topologías distribuidas, donde varios nodos deben tener acceso toohello misma caché</li><li>Los tokens almacenados en caché deben sobrevivir a los reciclajes y las desactivaciones de los procesos.</li></ul><p>Para todos los Hola por encima de motivos, al implementar aplicaciones web, se recomienda toooverride Hola AAL token memoria caché predeterminada con una alternativa escalable como la caché en Redis de Azure.</p>|

## <a id="tokenreplaycache-adal"></a>Asegúrese de que TokenReplayCache es tooprevent usados al reproducir Hola de tokens de autenticación de ADAL

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Azure AD | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | [Modern Authentication with Azure Active Directory for Web Applications](https://blogs.msdn.microsoft.com/microsoft_press/2016/01/04/new-book-modern-authentication-with-azure-active-directory-for-web-applications/) (Autenticación moderna con Azure Active Directory para aplicaciones web) |
| **Pasos** | <p>la propiedad de TokenReplayCache Hola permite a los desarrolladores toodefine una memoria caché de reproducción de tokens, un almacén que se puede usar para no guardar ningún token de tokens para el propósito de Hola de comprobar que se puede utilizar más de una vez.</p><p>Se trata de una medida con respecto a un ataque habitual, hello muy apropiado denominar ataque de reproducción de tokens: un atacante intercepta el símbolo (token) de Hola se envía al inicio de sesión puede intentar toosend se toohello aplicación nuevo ("reproducirlo") para establecer una sesión nueva. Por ejemplo, en OIDC-concesión de código de flujo, después de la autenticación del usuario, una solicitud demasiado "/ signin-oidc" punto de conexión de usuario de confianza de Hola se realiza con "id_token", "código" y "state" parámetros.</p><p>Hola usuario de confianza valida esta solicitud y establece una sesión nueva. Si un adversario captura esta solicitud y reproduce, éste puede establecer una sesión correcta y el usuario de Hola de engaño. presencia de Hola de nonce Hola de OpenID Connect puede limitar aunque no totalmente elimina circunstancias Hola ataque hello en el que se puede establecida correctamente. tooprotect sus aplicaciones, los desarrolladores pueden proporcionar una implementación de ITokenReplayCache y asignar un tooTokenReplayCache de instancia.</p>|

### <a name="example"></a>Ejemplo
```C#
// ITokenReplayCache defined in ADAL
public interface ITokenReplayCache
{
bool TryAdd(string securityToken, DateTime expiresOn);
bool TryFind(string securityToken);
}
```

### <a name="example"></a>Ejemplo
Este es un ejemplo de implementación de interfaz de ITokenReplayCache Hola. (Personalice e implemente el marco de almacenamiento en caché específico del proyecto).
```C#
public class TokenReplayCache : ITokenReplayCache
{
    private readonly ICacheProvider cache; // Your project-specific cache provider
    public TokenReplayCache(ICacheProvider cache)
    {
        this.cache = cache;
    }
    public bool TryAdd(string securityToken, DateTime expiresOn)
    {
        if (this.cache.Get<string>(securityToken) == null)
        {
            this.cache.Set(securityToken, securityToken);
            return true;
        }
        return false;
    }
    public bool TryFind(string securityToken)
    {
        return this.cache.Get<string>(securityToken) != null;
    }
}
```
caché de Hello implementado tiene toobe al que hace referencia en las opciones de OIDC a través de la propiedad "TokenValidationParameters" hello como se indica a continuación.
```C#
OpenIdConnectOptions openIdConnectOptions = new OpenIdConnectOptions
{
    AutomaticAuthenticate = true,
    ... // other configuration properties follow..
    TokenValidationParameters = new TokenValidationParameters
    {
        TokenReplayCache = new TokenReplayCache(/*Inject your cache provider*/);
    }
}
```

Por favor, tenga en cuenta esa eficacia de hello tootest de esta configuración, el inicio de sesión en la aplicación protegida OIDC local y capturar solicitud Hola demasiado`"/signin-oidc"` extremo en fiddler. Cuando la protección de hello no está en su lugar, la reproducción de esta solicitud en fiddler establecerá una nueva cookie de sesión. Cuando la solicitud de saludo se reproduce una vez agregado hello TokenReplayCache protección, aplicación hello iniciará una excepción como sigue:`SecurityTokenReplayDetectedException: IDX10228: hello securityToken has previously been validated, securityToken: 'eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWmNBVGZNNXBPWWlKSE1iYTlnb0VLWSIsImtpZCI6Ik1uQ1......`

## <a id="adal-oauth2"></a>Usar el token de bibliotecas de ADAL toomanage solicita de OAuth2 clientes tooAAD (o AD local)

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Azure AD | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | [ADAL](https://azure.microsoft.com/documentation/articles/active-directory-authentication-libraries/) |
| **Pasos** | <p>Hola AD Azure authentication Library (AAL) permite cliente aplicación a los desarrolladores tooeasily autenticar usuarios toocloud o Active Directory (AD) local y, a continuación, obtener tokens de acceso para proteger las llamadas de API.</p><p>ADAL incluye muchas características que hacen que la autenticación resulte más fácil para los desarrolladores, como la compatibilidad asincrónica, una memoria caché de tokens configurable que almacena tokens de acceso y tokens de actualización, actualización automática de tokens cuando caduca un token de acceso y hay un token de actualización disponible, etc.</p><p>Al controlar la mayor parte de la complejidad de hello, ADAL puede ayudar a los desarrolladores a centrarse en la lógica de negocios en su aplicación y proteger fácilmente los recursos sin necesidad de ser un experto en seguridad. Otras bibliotecas están disponibles para. NET, JavaScript (cliente y Node.js), iOS, Android y Java.</p>|

## <a id="authn-devices-field"></a>Autenticar los dispositivos que se conectan toohello puerta de enlace de campo

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Puerta de enlace de campo de IoT | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | N/D  |
| **Pasos** | Asegúrese de que cada dispositivo es autenticado por hello puerta de enlace de campo antes de aceptar los datos contenidos en ellos y facilitar las comunicaciones de nivel superior con hello puerta de enlace de nube. Además, asegúrese de que los dispositivos se conectan con una credencial cada uno de forma que cada dispositivo se pueda identificar de manera unívoca.|

## <a id="authn-devices-cloud"></a>Asegúrese de que se autentican los dispositivos que se conectan tooCloud puerta de enlace

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Puerta de enlace de la nube de IoT | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico, C#, Node.JS,  |
| **Atributos**              | N/D, opción de puerta de enlace: Azure IoT Hub |
| **Referencias**              | N/D, [Introducción a Azure IoT Hub (.NET)](https://azure.microsoft.com/documentation/articles/iot-hub-csharp-csharp-getstarted/), [Introducción a Azure IoT Hub (Node)](https://azure.microsoft.com/documentation/articles/iot-hub-node-node-getstarted), [Protección de IoT con SAS y certificados](https://azure.microsoft.com/documentation/articles/iot-hub-sas-tokens/), [Repositorio de GIT](https://github.com/Azure/azure-iot-sdks/tree/master/node) |
| **Pasos** | <ul><li>**Genérico:** dispositivo de hello autenticar con seguridad de capa de transporte (TLS) o IPSec. La infraestructura debe admitir el uso de una clave precompartida (PSK) en los dispositivos que no pueden controlar la criptografía asimétrica completa. Aprovechamiento de Azure AD, OAuth</li><li>**C#:** al crear una instancia de DeviceClient, de forma predeterminada, Hola método Create crea una instancia de DeviceClient que usa hello AMQP protocolo toocommunicate con centro de IoT. Hola toouse protocolo HTTPS, use invalidación Hola de método de creación de Hola que le permite toospecify protocolo de Hola. Si utiliza el protocolo HTTPS de hello, también debe agregar hello `Microsoft.AspNet.WebApi.Client` Hola de NuGet paquete tooyour proyecto tooinclude `System.Net.Http.Formatting` espacio de nombres.</li></ul>|

### <a name="example"></a>Ejemplo
```C#
static DeviceClient deviceClient;

static string deviceKey = "{device key}";
static string iotHubUri = "{iot hub hostname}";

var messageString = "{message in string format}";
var message = new Message(Encoding.ASCII.GetBytes(messageString));

deviceClient = DeviceClient.Create(iotHubUri, new DeviceAuthenticationWithRegistrySymmetricKey("myFirstDevice", deviceKey));

await deviceClient.SendEventAsync(message);
```

### <a name="example"></a>Ejemplo
**Node.JS: autenticación**
#### <a name="symmetric-key"></a>Clave simétrica
* Cree un centro de IoT de Azure.
* Crear una entrada en el registro de identidad de dispositivo de Hola
    ```javascript
    var device = new iothub.Device(null);
    device.deviceId = <DeviceId >
    registry.create(device, function(err, deviceInfo, res) {})
    ```
* Cree un dispositivo simulado:
    ```javascript
    var clientFromConnectionString = require('azure-iot-device-amqp').clientFromConnectionString;
    var Message = require('azure-iot-device').Message;
    var connectionString = 'HostName=<HostName>DeviceId=<DeviceId>SharedAccessKey=<SharedAccessKey>';
    var client = clientFromConnectionString(connectionString);
    ```
#### <a name="sas-token"></a>Token de SAS
* Se genera internamente cuando se usa la clave simétrica pero también se puede generar y usar explícitamente.
* Defina un protocolo:`var Http = require('azure-iot-device-http').Http;`
* Cree un token de SAS:
    ```javascript
    resourceUri = encodeURIComponent(resourceUri.toLowerCase()).toLowerCase();
    var deviceName = "<deviceName >";
    var expires = (Date.now() / 1000) + expiresInMins * 60;
    var toSign = resourceUri + '\n' + expires;
    // using crypto
    var decodedPassword = new Buffer(signingKey, 'base64').toString('binary');
    const hmac = crypto.createHmac('sha256', decodedPassword);
    hmac.update(toSign);
    var base64signature = hmac.digest('base64');
    var base64UriEncoded = encodeURIComponent(base64signature);
    // construct authorization string
    var token = "SharedAccessSignature sr=" + resourceUri + "%2fdevices%2f"+deviceName+"&sig="
    + base64UriEncoded + "&se=" + expires;
    if (policyName) token += "&skn="+policyName;
    return token;
    ```
* Conéctese mediante el token de SAS: 
    ```javascript
    Client.fromSharedAccessSignature(sas, Http); 
    ```
#### <a name="certificates"></a>Certificados
* Generar un X509 firmado propio certificado mediante cualquier herramienta como OpenSSL toogenerate una .cert .key archivos toostore Hola hello y certificado de clave y respectivamente
* Aprovisione un dispositivo que acepte conexiones seguras mediante certificados.
    ```javascript
    var connectionString = '<connectionString>';
    var registry = iothub.Registry.fromConnectionString(connectionString);
    var deviceJSON = {deviceId:"<deviceId>",
    authentication: {
        x509Thumbprint: {
        primaryThumbprint: "<PrimaryThumbprint>",
        secondaryThumbprint: "<SecondaryThumbprint>"
        }
    }}
    var device = deviceJSON;
    registry.create(device, function (err) {});
    ```
* Conecte un dispositivo mediante un certificado.
    ```javascript
    var Protocol = require('azure-iot-device-http').Http;
    var Client = require('azure-iot-device').Client;
    var connectionString = 'HostName=<HostName>DeviceId=<DeviceId>x509=true';
    var client = Client.fromConnectionString(connectionString, Protocol);
    var options = {
        key: fs.readFileSync('./key.pem', 'utf8'),
        cert: fs.readFileSync('./server.crt', 'utf8')
    }; 
    // Calling setOptions with hello x509 certificate and key (and optionally, passphrase) will configure hello client //transport toouse x509 when connecting tooIoT Hub
    client.setOptions(options);
    //call fn tooexecute after hello connection is set up
    client.open(fn);
    ```

## <a id="authn-cred"></a>Uso de credenciales de autenticación por dispositivo

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Puerta de enlace de la nube de IoT  | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | Elección de puerta de enlace: Azure IoT Hub |
| **Referencias**              | [Tokens de seguridad de Azure IoT Hub](https://azure.microsoft.com/documentation/articles/iot-hub-sas-tokens/) |
| **Pasos** | Use credenciales de autenticación por dispositivo mediante tokens de SaS basados en la clave de dispositivo y el certificado de cliente, en lugar de directivas de acceso compartido de nivel de IoT Hub. Esto impide la reutilización de Hola de tokens de autenticación de una puerta de enlace de dispositivo o un campo por otro |

## <a id="req-containers-anon"></a>Asegúrese de que solo Hola requiera contenedores y blobs tienen acceso de lectura anónimo

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Azure Storage | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | StorageType: blob |
| **Referencias**              | [Administrar el acceso de lectura anónimo toocontainers y blobs](https://azure.microsoft.com/documentation/articles/storage-manage-access-to-resources/), [firmas de acceso compartido, parte 1: modelo de descripción Hola SAS](https://azure.microsoft.com/documentation/articles/storage-dotnet-shared-access-signature-part-1/) |
| **Pasos** | <p>De forma predeterminada, un contenedor y cualquiera de sus blobs puede tener acceso a solo el propietario Hola de cuenta de almacenamiento de Hola. contenedor de tooa de permisos de lectura de los usuarios anónimos toogive y sus blobs, uno puede establecer Hola permisos tooallow público el acceso al contenedor. Los usuarios anónimos pueden leer los blobs dentro de un contenedor es accesible públicamente sin autenticar la solicitud de Hola.</p><p>Los contenedores ofrecen Hola siguientes opciones para administrar el acceso al contenedor:</p><ul><li>Acceso de lectura público completo: los datos del contenedor y de los blobs se pueden leer mediante una solicitud anónima. Los clientes pueden enumerar blobs en el contenedor de hello mediante una solicitud anónima, pero no pueden enumerar contenedores dentro de la cuenta de almacenamiento de Hola.</li><li>Acceso de lectura público solo para blobs: los datos de blob dentro de este contenedor pueden leerse mediante una solicitud anónima, pero los datos del contenedor no están disponibles. Los clientes no pueden enumerar blobs en el contenedor de hello mediante una solicitud anónima</li><li>Acceso no público de lectura: solo el propietario Hola cuenta pueden leer los datos de contenedor y blob</li></ul><p>El acceso anónimo es mejor para escenarios donde ciertos blobs deben estar siempre disponibles para el acceso de lectura anónimo. Para un control más precisa, uno puede crear una firma de acceso compartido, que permite el acceso de toodelegate restringido mediante permisos diferentes y en un intervalo de tiempo especificado. Asegúrese de que los contenedores y blobs, que podrían contener datos confidenciales, no tengan acceso anónimo por accidente.</p>|

## <a id="limited-access-sas"></a>Conceder acceso limitado tooobjects en almacenamiento de Azure mediante SAS o SAP

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Azure Storage | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D |
| **Referencias**              | [Las firmas de acceso compartido, parte 1: El modelo SAS de descripción hello](https://azure.microsoft.com/documentation/articles/storage-dotnet-shared-access-signature-part-1/), [firmas de acceso compartido, parte 2: crear y utilizar una SAS con almacenamiento de blobs](https://azure.microsoft.com/documentation/articles/storage-dotnet-shared-access-signature-part-2/), [cómo toodelegate tener acceso a tooobjects en su cuenta mediante Firmas de acceso compartido y directivas de acceso almacenadas](https://azure.microsoft.com/documentation/articles/storage-security-guide/#_how-to-delegate-access-to-objects-in-your-account-using-shared-access-signatures-and-stored-access-policies) |
| **Pasos** | <p>El uso de una firma de acceso compartido (SAS) es un tooobjects de acceso de forma eficaz toogrant limitado en un almacenamiento cuenta tooother los clientes sin necesidad de tecla de acceso de cuenta tooexpose. Hola SAS es un URI que abarca el proceso en sus parámetros de consulta toda Hola información necesaria para autenticar acceso a recursos de almacenamiento de tooa. recursos de almacenamiento de tooaccess con hello SAS, cliente hello solo necesita toopass en el método o constructor adecuado de hello SAS toohello.</p><p>Puede usar una SAS cuando desee tooprovide acceso tooresources en el cliente de tooa de cuenta de almacenamiento que no es de confianza con la clave de la cuenta de hello. Las claves de cuenta de almacenamiento incluyen tanto una clave principal y secundaria, que conceden acceso administrativo tooyour cuenta y todos los recursos de hello en ella. Exposición de cualquiera de las claves de cuenta, abre la posibilidad de toohello de cuenta de uso malintencionado o por negligencia. Firmas de acceso compartido proporcionan una alternativa segura que permite a otros clientes tooread, escribir y eliminar datos en la cuenta de almacenamiento según los permisos de toohello que le ha concedido y sin necesidad de clave de la cuenta de hello.</p><p>Si tiene un conjunto lógico de parámetros que son siempre parecidos, es mejor usar una directiva de acceso almacenado (SAP). Ya mediante una SAS que se deriva de una directiva de acceso almacenada ofrece toorevoke de capacidad de Hola que SAS inmediatamente, resulta Hola recomienda tooalways de práctica recomendada usar almacena las directivas de acceso siempre que sea posible.</p>|
