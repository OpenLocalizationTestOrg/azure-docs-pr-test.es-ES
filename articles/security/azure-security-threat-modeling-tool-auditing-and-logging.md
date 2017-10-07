---
title: aaaAuditing y registro - herramienta de modelado de amenazas de Microsoft - Azure | Documentos de Microsoft
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
ms.openlocfilehash: f28988833eba251b6ceb8bbd47cde37e871af609
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-auditing-and-logging--mitigations"></a>Marco de seguridad: Auditoría y registro | Mitigaciones 
| Producto o servicio | Artículo |
| --------------- | ------- |
| **Dynamics CRM**    | <ul><li>[Identificación de las entidades confidenciales de la solución e implementación de la auditoría de cambios](#sensitive-entities)</li></ul> |
| **Aplicación web** | <ul><li>[Asegúrese de que la auditoría y registro se aplican en la aplicación hello](#auditing)</li><li>[Comprobación de que la rotación de registros y la separación están en funcionamiento](#log-rotation)</li><li>[Asegúrese de que la aplicación hello no registra información confidencial del usuario](#log-sensitive-data)</li><li>[Comprobación de que los archivos de registro y auditoría tienen acceso restringido](#log-restricted-access)</li><li>[Comprobación de que se registran los eventos de administración de usuario](#user-management)</li><li>[Asegúrese de que tiene el sistema de hello defensas integradas contra el uso indebido](#inbuilt-defenses)</li><li>[Habilitación del registro de diagnóstico para aplicaciones web en Azure App Service](#diagnostics-logging)</li></ul> |
| **Base de datos** | <ul><li>[Comprobación de que está habilitada la auditoría de inicio de sesión en SQL Server](#identify-sensitive-entities)</li><li>[Habilitamiento de la detección de amenazas en Azure SQL](#threat-detection)</li></ul> |
| **Azure Storage** | <ul><li>[Usar el análisis de almacenamiento de Azure tooaudit acceso de almacenamiento de Azure](#analytics)</li></ul> |
| **WCF** | <ul><li>[Implementación de suficientes registros](#sufficient-logging)</li><li>[Implementación de un control suficiente de errores de auditoría](#audit-failure-handling)</li></ul> |
| **API web** | <ul><li>[Comprobación de que la auditoría y el registro se aplican en Web API](#logging-web-api)</li></ul> |
| **Puerta de enlace de campo de IoT** | <ul><li>[Comprobación de que se aplican la auditoría y registro adecuados en la puerta de enlace de campo](#logging-field-gateway)</li></ul> |
| **Puerta de enlace de nube de IoT** | <ul><li>[Comprobación de que se aplican la auditoría y registro adecuados en la puerta de enlace de nube](#logging-cloud-gateway)</li></ul> |

## <a id="sensitive-entities"></a>Identificación de las entidades confidenciales de la solución e implementación de la auditoría de cambios

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Dynamics CRM | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | N/D  |
| **Pasos**                   | Identificación de las entidades de la solución que contienen datos confidenciales e implementación de la auditoría de cambios en esas entidades y campos |

## <a id="auditing"></a>Asegúrese de que la auditoría y registro se aplican en la aplicación hello

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Aplicación web | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | N/D  |
| **Pasos**                   | Habilite la auditoría y el registro en todos los componentes. Los registros de auditoría deben reflejar el contexto de usuario. Identifique todos los eventos importantes y regístrelos. Implemente el registro centralizado. |

## <a id="log-rotation"></a>Comprobación de que la rotación de registros y la separación están en funcionamiento

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Aplicación web | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | N/D  |
| **Pasos**                   | <p>La rotación de registros es un proceso automatizado que se usa en la administración del sistema en el que se archivan los archivos de registro con fecha. Todas las solicitudes de registro de servidores que ejecutan aplicaciones de gran tamaño a menudo: en la cara de Hola de registros voluminosos, rotación de registros es un hello de toolimit de manera tamaño total de registros de hello mientras sigue permitiendo el análisis de eventos recientes. </p><p>Separación de registro básicamente significa que tendrá que toostore atacan o bienvenida degradar de la aplicación, su rendimiento a los archivos de registro en una partición diferente como donde la aplicación o del SO se está quedando en orden tooavert una denegación de servicio</p>|

## <a id="log-sensitive-data"></a>Asegúrese de que la aplicación hello no registra información confidencial del usuario

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Aplicación web | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | N/D  |
| **Pasos**                   | <p>Compruebe que el registro de los datos confidenciales que un usuario envía tooyour sitio no. Compruebe para ver si hay algún registro intencionado, o efectos secundarios causados por problemas de diseño. Ejemplos de datos confidenciales incluyen:</p><ul><li>Credenciales de usuario</li><li>Número del seguro social u otra información de identificación</li><li>Números de tarjeta de crédito u otra información financiera</li><li>Información relacionada con la salud</li><li>Las claves privadas u otros datos que pudieron ser utilizado toodecrypt información cifrada</li><li>Información del sistema o aplicación que se puede usar toomore eficazmente ataques aplicación hello</li></ul>|

## <a id="log-restricted-access"></a>Comprobación de que los archivos de registro y auditoría tienen acceso restringido

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Aplicación web | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | N/D  |
| **Pasos**                   | <p>Comprobar tooensure archivos de toolog de derechos de acceso se ha establecido correctamente. Las cuentas de la aplicación deben tener operadores y acceso de solo escritura y el personal de soporte técnico debe tener acceso de solo lectura según sea necesario.</p><p>Los administradores tienen Hola solo las cuentas que deben tener acceso total. Compruebe la que ACL de Windows en el registro de archivos tooensure están restringidos correctamente:</p><ul><li>Las cuentas de la aplicación deben tener acceso de solo escritura</li><li>Los operadores y el personal de soporte técnico deben tener acceso de solo lectura según sea necesario</li><li>Los administradores son Hola únicas cuentas que deben tener acceso total</li></ul>|

## <a id="user-management"></a>Comprobación de que se registran los eventos de administración de usuario

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Aplicación web | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | N/D  |
| **Pasos**                   | <p>Asegurarse de que la aplicación hello supervisa los eventos de administración de usuario, como los inicios de sesión de usuario correctos y erróneos, restablecimiento de contraseñas, los cambios de contraseña, bloqueo de cuentas, registro de usuario. Esto ayuda a toodetect y reacciona toopotentially un comportamiento sospechoso. También permite que los datos de las operaciones de toogather; Por ejemplo, tootrack quién tiene acceso a la aplicación hello</p>|

## <a id="inbuilt-defenses"></a>Asegúrese de que tiene el sistema de hello defensas integradas contra el uso indebido

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Aplicación web | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | N/D  |
| **Pasos**                   | <p>Los controles deben funcionar de forma que generen excepciones de seguridad en caso de uso incorrecto de una aplicación. Por ejemplo, si la validación de entrada está en su lugar y un atacante intenta tooinject código malintencionado que no coincide con regex hello, una excepción de seguridad puede producirá que puede ser un indicativo de uso indebido del sistema</p><p>Por ejemplo, se recomienda registradas las excepciones de seguridad de toohave y las acciones realizadas para hello problemas siguientes:</p><ul><li>Validación de entradas</li><li>Infracciones de CSRF</li><li>Fuerza bruta (límite superior en relación con el número de solicitudes por usuario y recurso)</li><li>Infracciones de carga de archivos</li><ul>|

## <a id="diagnostics-logging"></a>Habilitación del registro de diagnóstico para aplicaciones web en Azure App Service

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Aplicación web | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | EnvironmentType: Azure |
| **Referencias**              | N/D  |
| **Pasos** | <p>Azure proporciona diagnósticos integrados tooassist con la depuración de un servicio de aplicaciones de aplicación web. También se aplica tooAPI aplicaciones y aplicaciones móviles. Aplicaciones de servicio de aplicaciones web proporcionan funcionalidad de diagnóstico para registrar información de servidor web de Hola y de aplicación web de hello.</p><p>De forma lógica, estos diagnósticos se dividen en diagnósticos del servidor web y diagnósticos de aplicaciones.</p>|

## <a id="identify-sensitive-entities"></a>Comprobación de que está habilitada la auditoría de inicio de sesión en SQL Server

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Base de datos | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | [Configuración de la auditoría de inicio de sesión](https://msdn.microsoft.com/library/ms175850.aspx) |
| **Pasos** | <p>Auditoría de inicio de sesión de servidor de base de datos debe ser habilitado toodetect/Confirmar contraseña adivinen ataques. Es importante de intentos de inicio de sesión fallidos toocapture. Capturar los intentos de inicio de sesión correctos e incorrectos proporciona una ventaja adicional durante las investigaciones</p>|

## <a id="threat-detection"></a>Habilitamiento de la detección de amenazas en Azure SQL

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Base de datos | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | SQL Azure |
| **Atributos**              | Versión de SQL: V12 |
| **Referencias**              | [Introducción a Detección de amenazas de SQL Database](https://azure.microsoft.com/documentation/articles/sql-database-threat-detection-get-started/)|
| **Pasos** |<p>La detección de amenazas detecta actividades anómalas de la base de datos que indica la base de datos toohello amenazas de seguridad potenciales. Proporciona una nueva capa de seguridad, lo cual permite toodetect de los clientes y responde a amenazas de toopotential cuando se producen al proporcionar alertas de seguridad en actividades anómalas.</p><p>Los usuarios pueden explorar eventos sospechosos hello mediante Azure proceso de auditoría de base de datos de SQL toodetermine se deriven de un tooaccess de intento de infracción o vulnerabilidad de seguridad de datos en la base de datos de Hola.</p><p>La detección de amenazas resulta sencillo tooaddress posibles amenazas toohello base de datos sin necesidad de hello toobe un experto en seguridad o administrar sistemas de supervisión de seguridad avanzada</p>|

## <a id="analytics"></a>Usar el análisis de almacenamiento de Azure tooaudit acceso de almacenamiento de Azure

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Azure Storage | 
| **Fase de SDL**               | Implementación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D |
| **Referencias**              | [Uso de tipo de análisis de almacenamiento de autorización toomonitor](https://azure.microsoft.com/documentation/articles/storage-security-guide/#storage-analytics) |
| **Pasos** | <p>Para cada cuenta de almacenamiento, uno puede habilitar el registro de tooperform de análisis de almacenamiento de Azure y almacenar datos de métricas. registros de análisis de almacenamiento de Hello proporcionan información importante como método de autenticación usado por alguien cuando tienen acceso a almacenamiento de información.</p><p>Esto puede ser muy útil si está protegiendo estrechamente toostorage de acceso. Por ejemplo, en almacenamiento de blobs puede establecer todos Hola contenedores tooprivate y la implementación de un uso Hola de un servicio SAS a lo largo de las aplicaciones. A continuación, puede comprobar Hola con regularidad registra toosee si los blobs son accesibles mediante claves de cuenta de almacenamiento de hello, lo que pueden indicar una infracción de seguridad, o blobs de hello son públicos pero no debe ser.</p>|

## <a id="sufficient-logging"></a>Implementación de suficientes registros

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | WCF | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | .NET Framework |
| **Atributos**              | N/D  |
| **Referencias**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Pasos** | <p>falta de Hola de una pista de auditoría correcta después de un incidente de seguridad, puede reducir esfuerzos forenses. Windows Communication Foundation (WCF) ofrece Hola capacidad toolog correcto o error de intentos de autenticación.</p><p>Si registra los intentos de autenticación incorrectos puede advertir a los administradores de posibles ataques de fuerza bruta. Del mismo modo, el registro de eventos de autenticación correctos puede proporcionar una traza de auditoría útil cuando está en peligro una cuenta legítima. Habilite la característica de auditoría de seguridad del servicio de WCF. |

### <a name="example"></a>Ejemplo
Hola aquí te mostramos un ejemplo de configuración está habilitada la auditoría
```
<system.serviceModel>
    <behaviors>
        <serviceBehaviors>
            <behavior name=""NewBehavior"">
                <serviceSecurityAudit auditLogLocation=""Default""
                suppressAuditFailure=""false"" 
                serviceAuthorizationAuditLevel=""SuccessAndFailure""
                messageAuthenticationAuditLevel=""SuccessAndFailure"" />
                ...
            </behavior>
        </servicebehaviors>
    </behaviors>
</system.serviceModel>
```

## <a id="audit-failure-handling"></a>Implementación de un control suficiente de errores de auditoría

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | WCF | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | .NET Framework |
| **Atributos**              | N/D  |
| **Referencias**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Pasos** | <p>Se configura la solución desarrollada no toogenerate una excepción cuando se produce un error de registro de auditoría de toowrite tooan. Si se configura WCF no toothrow una excepción cuando es registro de auditoría no se puede toowrite tooan, programa Hola no recibir una notificación de error de hello y no puede producirse la auditoría de eventos de seguridad críticas.</p>|

### <a name="example"></a>Ejemplo
Hola `<behavior/>` elemento del archivo de configuración de WCF de hello siguiente indica a WCF toonot notifiquen aplicación hello WCF produce un error en el registro de auditoría de toowrite tooan.
````
<behaviors>
    <serviceBehaviors>
        <behavior name="NewBehavior">
            <serviceSecurityAudit auditLogLocation="Application"
            suppressAuditFailure="true"
            serviceAuthorizationAuditLevel="Success"
            messageAuthenticationAuditLevel="Success" />
        </behavior>
    </serviceBehaviors>
</behaviors>
````
Configurar programa Hola WCF toonotify siempre que sea el registro de auditoría no se puede toowrite tooan. programa Hello debe tener un esquema de notificación alternativo en la organización de hello tooalert lugar que no se mantienen los seguimientos de auditoría. 

## <a id="logging-web-api"></a>Comprobación de que la auditoría y el registro se aplican en Web API

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | API Web | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | N/D  |
| **Pasos** | Habilite la auditoría y el registro en las Web API. Los registros de auditoría deben reflejar el contexto de usuario. Identifique todos los eventos importantes y regístrelos. Implemente el registro centralizado. |

## <a id="logging-field-gateway"></a>Comprobación de que se aplican la auditoría y registro adecuados en la puerta de enlace de campo

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Puerta de enlace de campo de IoT | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | N/D  |
| **Pasos** | <p>Cuando varios dispositivos conectan tooa puerta de enlace de campo, asegúrese de que los intentos de conexión y el estado de autenticación (éxito o error) para dispositivos individuales se registran y se mantienen en hello puerta de enlace de campo.</p><p>Además, en casos donde la puerta de enlace de campo es mantener Hola centro de IoT credenciales para los dispositivos individuales, asegúrese de que se realiza la auditoría cuando estas credenciales se recuperan. Desarrollar un tooAzure de la registros del Hola proceso tooperiodically carga centro de IoT y el almacenamiento para la retención a largo plazo.</p> |

## <a id="logging-cloud-gateway"></a>Comprobación de que se aplican la auditoría y registro adecuados en la puerta de enlace de nube

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Puerta de enlace de la nube de IoT | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | [Supervisión de operaciones de base de datos central de introducción tooIoT](https://azure.microsoft.com/documentation/articles/iot-hub-operations-monitoring/) |
| **Pasos** | <p>Diseño para recopilar y almacenar datos de auditoría recopilados mediante la supervisión de operaciones de IoT Hub. Habilitar Hola siguientes categorías de supervisión:</p><ul><li>Operaciones de identidad de dispositivos</li><li>Comunicaciones de dispositivo a nube</li><li>Comunicaciones de nube a dispositivo</li><li>Conexiones</li><li>Cargas de archivos</li></ul>|
