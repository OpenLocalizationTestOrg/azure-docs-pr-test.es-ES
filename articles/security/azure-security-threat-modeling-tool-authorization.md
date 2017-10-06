---
title: aaaAuthorization - herramienta de modelado de amenazas de Microsoft - Azure | Documentos de Microsoft
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
ms.openlocfilehash: 3ea7ae2b46baa8578e574e6006b98dfe172829e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-authorization--mitigations"></a>Marco de seguridad: Autorización | Mitigaciones 
| Producto o servicio | Artículo |
| --------------- | ------- |
| **Límite de confianza de la máquina** | <ul><li>[Asegúrese de que las ACL apropiadas toodata de acceso de toorestrict configurado no autorizado en el dispositivo de Hola](#acl-restricted-access)</li><li>[Comprobación de que el contenido de la aplicación confidencial del usuario se almacena en el directorio del perfil de usuario](#sensitive-directory)</li><li>[Asegúrese de que las aplicaciones de hello implementado se ejecutan con privilegios mínimos](#deployed-privileges)</li></ul> |
| **Aplicación web** | <ul><li>[Aplicación de un orden secuencial al procesar flujos de lógica empresarial](#sequential-logic)</li><li>[Implementar la enumeración de tooprevent del mecanismo de limitación de velocidad](#rate-enumeration)</li><li>[Comprobación de que se aplica la autorización adecuada y se cumple el principio de privilegios mínimos](#principle-least-privilege)</li><li>[Las decisiones sobre la autorización para acceder a recursos y lógicas empresariales no deben basarse en parámetros de solicitud entrantes](#logic-request-parameters)</li><li>[Comprobación de que no es posible enumerar ni acceder al contenido ni los recursos mediante navegación forzada](#enumerable-browsing)</li></ul> |
| **Base de datos** | <ul><li>[Asegúrese de que las cuentas con privilegios mínimos tooconnect usado tooDatabase server](#privileged-server)</li><li>[Inquilinos de implementar la seguridad de nivel de fila tooprevent tengan acceso a datos de todas las demás](#rls-tenants)</li><li>[El rol sysadmin solo debe tener a los usuarios válidos necesarios](#sysadmin-users)</li></ul> |
| **Puerta de enlace de nube de IoT** | <ul><li>[Conectar tooCloud puerta de enlace con tokens de privilegios mínimos](#cloud-least-privileged)</li></ul> |
| **Centro de eventos de Azure** | <ul><li>[Uso de una clave SAS de permisos solo de envío para generar tokens de dispositivo](#sendonly-sas)</li><li>[No use los tokens de acceso que proporcionan acceso directo toohello concentrador de eventos](#access-tokens-hub)</li><li>[Conectar tooEvent concentrador mediante SAS de claves que se requieren permisos mínimos Hola](#sas-minimum-permissions)</li></ul> |
| **Azure Document DB** | <ul><li>[Usar recursos tokens tooconnect tooDocumentDB siempre que sea posible](#resource-docdb)</li></ul> |
| **Límites de confianza de Azure** | <ul><li>[Habilitar la administración de acceso específico tooAzure suscripción mediante RBAC](#grained-rbac)</li></ul> |
| **Límites de confianza de Service Fabric** | <ul><li>[Restringir las operaciones de toocluster de acceso del cliente mediante RBAC](#cluster-rbac)</li></ul> |
| **Dynamics CRM** | <ul><li>[Realización de modelos de seguridad y uso de seguridad de nivel de campo cuando sea necesario](#modeling-field)</li></ul> |
| **Portal de Dynamics CRM** | <ul><li>[Realizar el modelo de seguridad de las cuentas de portal teniendo en cuenta ese modelo de seguridad de hello para el portal de hello es distinto del resto de Hola de CRM](#portal-security)</li></ul> |
| **Azure Storage** | <ul><li>[Concesión de permiso detallado en una serie de entidades de Azure Table Storage](#permission-entities)</li><li>[Habilitar la cuenta de almacenamiento de tooAzure de Control de acceso basado en roles (RBAC) con el Administrador de recursos de Azure](#rbac-azure-manager)</li></ul> |
| **Cliente para dispositivos móviles** | <ul><li>[Implementación de detección implícita de jailbreak o rooting](#rooting-detection)</li></ul> |
| **WCF** | <ul><li>[Referencia débil de clase en WCF](#weak-class-wcf)</li><li>[WCF: implementación de control de autorización](#wcf-authz)</li></ul> |
| **API web** | <ul><li>[Implementación del mecanismo de autorización adecuado en ASP.NET Web API](#authz-aspnet)</li></ul> |
| **Dispositivo de IoT** | <ul><li>[Realizar comprobaciones de autorización en el dispositivo de hello si admite varias acciones que requieren distintos niveles de permisos](#device-permission)</li></ul> |
| **Puerta de enlace de campo de IoT** | <ul><li>[Realizar comprobaciones de autorización en hello puerta de enlace de campo si es compatible con varias acciones que requieren distintos niveles de permisos](#field-permission)</li></ul> |

## <a id="acl-restricted-access"></a>Asegúrese de que las ACL apropiadas toodata de acceso de toorestrict configurado no autorizado en el dispositivo de Hola

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Límite de confianza de la máquina | 
| **Fase de SDL**               | Implementación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | N/D  |
| **Pasos** | Asegúrese de que las ACL apropiadas toodata de acceso de toorestrict configurado no autorizado en el dispositivo de Hola|

## <a id="sensitive-directory"></a>Comprobación de que el contenido de la aplicación confidencial del usuario se almacena en el directorio del perfil de usuario

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Límite de confianza de la máquina | 
| **Fase de SDL**               | Implementación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | N/D  |
| **Pasos** | Compruebe que el contenido de la aplicación confidencial del usuario se almacena en el directorio del perfil de usuario. Se trata de tooprevent varios usuarios de hello equipo tengan acceso a datos de todas las demás.|

## <a id="deployed-privileges"></a>Asegúrese de que las aplicaciones de hello implementado se ejecutan con privilegios mínimos

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Límite de confianza de la máquina | 
| **Fase de SDL**               | Implementación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | N/D  |
| **Pasos** | Asegúrese de que se ejecuta la aplicación hello implementado con los privilegios mínimos. |

## <a id="sequential-logic"></a>Aplicación de un orden secuencial al procesar flujos de lógica empresarial

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Aplicación web | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | N/D  |
| **Pasos** | En orden tooverify que esta fase se ha ejecutado a través de un usuario original que desee tooenforce Hola aplicación tooonly business lógica flujos del proceso en orden secuencial de paso, con todos los pasos que se procesan en tiempo humano realista y no procesa desordenados, omitir pasos, procesan los pasos de otro usuario o demasiado rápido envía las transacciones.|

## <a id="rate-enumeration"></a>Implementar la enumeración de tooprevent del mecanismo de limitación de velocidad

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Aplicación web | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | N/D  |
| **Pasos** | Asegúrese de que los identificadores sensibles son aleatorios. Implemente el control CAPTCHA en páginas anónimas. Asegúrese de que no se revelen datos específicos por errores y excepciones.|

## <a id="principle-least-privilege"></a>Comprobación de que se aplica la autorización adecuada y se cumple el principio de privilegios mínimos

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Aplicación web | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | N/D  |
| **Pasos** | <p>principio de Hello significa que sólo los privilegios que son esenciales toothat usuarios trabajo proporciona una cuenta de usuario. Por ejemplo, un usuario de copia de seguridad no es necesario software tooinstall: por lo tanto, usuario de copia de seguridad de hello tiene derechos toorun solo copia de seguridad y relacionados con la copia de seguridad de las aplicaciones. Los demás privilegios, como la instalación de software nuevo, se bloquean. Hello principio aplica también tooa PC usuario que normalmente trabajan en una cuenta de usuario normal y se abre una cuenta con privilegios, de protección por contraseña (es decir, un superusuario) solo cuando situación Hola absolutamente lo requiera. </p><p>Este principio también puede ser aplicaciones web de tooyour aplicado. En lugar de solamente dependiendo de los métodos de autenticación basada en roles con sesiones, en su lugar queremos tooassign privilegios toousers por medio de un sistema de autenticación basada en la base de datos. Las sesiones en orden tooidentify todavía se usan si Hola usuario inició sesión correctamente, solo ahora en lugar de asignar a ese usuario a un rol concreto que se asignarle con privilegios tooverify qué acciones es tooperform con privilegios en el sistema de Hola. Un profesional grande de este método también es cada vez que un usuario tiene toobe asignado menos privilegios que los cambios se aplicarán en marcha de hello como asignar Hola no dependen de sesión de Hola que tenía tooexpire en primer lugar en caso contrario.</p>|

## <a id="logic-request-parameters"></a>Las decisiones sobre la autorización para acceder a recursos y lógicas empresariales no deben basarse en parámetros de solicitud entrantes

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Aplicación web | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | N/D  |
| **Pasos** | Cada vez que se está comprobando si un usuario está restringido tooreview determinados datos, deben ser restricciones de acceso de hello procesan del servidor. Hola userID debería almacenarse dentro de una variable de sesión de inicio de sesión y debe ser tooretrieve usa datos de usuario de base de datos de Hola |

### <a name="example"></a>Ejemplo
```SQL
SELECT data 
FROM personaldata 
WHERE userID=:id < - session var 
```
Ahora un posible atacante no puede manipular y cambiar operación de la aplicación hello puesto que el identificador para recuperar Hola datos hello controlada del servidor.

## <a id="enumerable-browsing"></a>Comprobación de que no es posible enumerar ni acceder al contenido ni los recursos mediante navegación forzada

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Aplicación web | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | N/D  |
| **Pasos** | <p>Los archivos confidenciales estática y la configuración no se deben mantener en hello web raíz. Para toobe no se requiere contenido público, se deben aplicar controles de acceso adecuada o eliminación de hello contenido propio.</p><p>Además, exploración forzosa se suele combinar con por fuerza bruta técnicas toogather información al intentar tooaccess tantas direcciones URL como tooenumerate posibles directorios y archivos en un servidor. Los atacantes pueden buscar todas las variantes de archivos habituales. Por ejemplo, la búsqueda de un archivo de contraseña podría incluir archivos como contraseña.txt, contraseña.htm, contraseña.dat y otras variantes.</p><p>intentos de toomitigate esto, las capacidades para la detección de fuerza bruta se debe incluir.</p>|

## <a id="privileged-server"></a>Asegúrese de que las cuentas con privilegios mínimos tooconnect usado tooDatabase server

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Base de datos | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | [Jerarquía de permisos de SQL Database](https://msdn.microsoft.com/library/ms191465), [Elementos protegibles de SQL Database](https://msdn.microsoft.com/library/ms190401) |
| **Pasos** | Las cuentas con privilegios mínimos deben ser la base de datos de uso tooconnect toohello. Inicio de sesión de aplicación debe estar restringido en base de datos de Hola y solo debe ejecutar procedimientos almacenados seleccionados. El inicio de sesión de la aplicación no debe tener acceso directo a tablas. |

## <a id="rls-tenants"></a>Inquilinos de implementar la seguridad de nivel de fila tooprevent tengan acceso a datos de todas las demás

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Base de datos | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | SQL Azure, OnPrem |
| **Atributos**              | Versión de SQL: V12, versión de SQL: MsSQL2016 |
| **Referencias**              | [Seguridad de nivel de fila (RLS) de SQL Server](https://msdn.microsoft.com/library/azure/dn765131.aspx) |
| **Pasos** | <p>Seguridad de nivel de fila permite a los clientes toocontrol acceso toorows en una tabla de base de datos basada en características de Hola de usuario de Hola que se ejecuta una consulta (por ejemplo, grupo pertenencia o contexto de ejecución).</p><p>Seguridad de nivel de fila (RLS) simplifica el diseño de Hola y codificación de seguridad de la aplicación. RLS permite tooimplement restricciones de acceso de la fila de datos. Por ejemplo, garantizar que los trabajadores puedan acceder solamente las filas de datos que son pertinentes tootheir departamento o restringir una empresa del cliente con datos acceso tooonly Hola datos tootheir relevante.</p><p>lógica de la restricción de Hello acceso está ubicada en el nivel de base de datos de hello en lugar de estar alejado de los datos de hello en otro nivel de aplicación. sistema de bases de datos de Hello aplica restricciones de acceso de hello cada vez que se intenta que acceder a los datos desde cualquier nivel. Sistema de seguridad de hello Esto hace más sólido y confiable que reduce la superficie Hola Hola de sistema de seguridad.</p><p>|

Tenga en cuenta que RLS como una característica de base de datos de cuadro es tooSQL solo es aplicable a partir de 2016 de servidor y base de datos SQL de Azure. Si no se implementa la característica RLS de Hola de fábrica, es necesario garantizar que el acceso de datos está restringido mediante vistas y procedimientos

## <a id="sysadmin-users"></a>El rol sysadmin solo debe tener a los usuarios válidos necesarios

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Base de datos | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | [Jerarquía de permisos de SQL Database](https://msdn.microsoft.com/library/ms191465), [Elementos protegibles de SQL Database](https://msdn.microsoft.com/library/ms190401) |
| **Pasos** | Los miembros del rol fijo de servidor SysAdmin de Hola deben ser muy limitado y no debe contener las cuentas utilizadas por las aplicaciones.  Revise la lista de Hola de usuarios en función de Hola y quite todas las cuentas innecesarias|

## <a id="cloud-least-privileged"></a>Conectar tooCloud puerta de enlace con tokens de privilegios mínimos

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Puerta de enlace de la nube de IoT | 
| **Fase de SDL**               | Implementación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | Elección de puerta de enlace: Azure IoT Hub |
| **Referencias**              | [Control de acceso de IOT Hub](https://azure.microsoft.com/documentation/articles/iot-hub-devguide/#Security) |
| **Pasos** | Proporcionan componentes de toovarious de permisos que se conectan tooCloud (centro de IoT) de la puerta de enlace de privilegios mínimos. Un ejemplo típico es el de un componente de aprovisionamiento o administración de dispositivos que usa registryread/write, mientras que el procesador de eventos (ASA) usa la directiva Service Connect. Los dispositivos individuales se conectan mediante credenciales de dispositivo.|

## <a id="sendonly-sas"></a>Uso de una clave SAS de permisos solo de envío para generar tokens de dispositivo

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Centro de eventos de Azure | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | [Introducción al modelo de autenticación y seguridad de Event Hubs](https://azure.microsoft.com/documentation/articles/event-hubs-authentication-and-security-model-overview/) |
| **Pasos** | Una clave SAS es toogenerate usa tokens de dispositivos individuales. Usar una clave SAS de permisos de solo envío al token del dispositivo Hola generación de un publicador determinado|

## <a id="access-tokens-hub"></a>No use los tokens de acceso que proporcionan acceso directo toohello concentrador de eventos

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Centro de eventos de Azure | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | [Introducción al modelo de autenticación y seguridad de Event Hubs](https://azure.microsoft.com/documentation/articles/event-hubs-authentication-and-security-model-overview/) |
| **Pasos** | No se debe conceder a un token que concede el concentrador de eventos de acceso directo toohello toohello dispositivo. Mediante un token con privilegios mínimos para dispositivo Hola que proporciona acceso solo tooa publisher podría ayudar a identificar y generar una lista negra si encuentra toobe no fiable o puesto en peligro el dispositivo.|

## <a id="sas-minimum-permissions"></a>Conectar tooEvent concentrador mediante SAS de claves que se requieren permisos mínimos Hola

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Centro de eventos de Azure | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | [Introducción al modelo de autenticación y seguridad de Event Hubs](https://azure.microsoft.com/documentation/articles/event-hubs-authentication-and-security-model-overview/) |
| **Pasos** | Proporcionar aplicaciones de back-end de toovarious de permisos que se conectan toohello concentrador de eventos de privilegios mínimos. Generar claves SAS independientes para cada aplicación de back-end y solo proporcionan los permisos necesario de hello - toothem de envío, recepción o administrar.|

## <a id="resource-docdb"></a>Usar recursos tokens tooconnect tooCosmos DB siempre que sea posible

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Azure DocumentDB | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | N/D  |
| **Pasos** | Un token de recurso está asociado a un recurso de permiso de documentos y capturas Hola relación entre usuario Hola de un permiso de hello y base de datos que el usuario tiene para un recurso de aplicación de documentos específico (por ejemplo, collection, documento). Use siempre un hello tooaccess token de recurso documentos si cliente hello no es de confianza con el manejo de claves maestras o de solo lectura: al igual que una aplicación de usuario final como un cliente móvil o de escritorio. Utilice la clave maestra o las claves de solo lectura de las aplicaciones de back-end que pueden almacenar estas claves de forma segura.|

## <a id="grained-rbac"></a>Habilitar la administración de acceso específico tooAzure suscripción mediante RBAC

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Límites de confianza de Azure | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | [Usar recursos de rol asignaciones toomanage acceso tooyour suscripción de Azure](https://azure.microsoft.com/documentation/articles/role-based-access-control-configure/)  |
| **Pasos** | El control de acceso basado en roles (RBAC) de Azure permite realizar una administración detallada del acceso para Azure. Usar RBAC, puede conceder únicamente cantidad de Hola de acceso que los usuarios necesitan tooperform sus trabajos.|

## <a id="cluster-rbac"></a>Restringir las operaciones de toocluster de acceso del cliente mediante RBAC

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Límites de confianza de Service Fabric | 
| **Fase de SDL**               | Implementación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | Entorno: Azure |
| **Referencias**              | [Control de acceso basado en roles para clientes de Service Fabric](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security-roles/) |
| **Pasos** | <p>Azure Service Fabric admite dos tipos de control de acceso diferente para los clientes que están conectados tooa clúster de Service Fabric: administrador y usuario. Control de acceso permite Hola clúster administrador toolimit acceso toocertain las operaciones del clúster para los diferentes grupos de usuarios, mejorar la seguridad de clúster de Hola.</p><p>Los administradores tienen capacidades de toomanagement de acceso completa (incluidas las capacidades de lectura/escritura). Los usuarios, de forma predeterminada, tienen sólo capacidades de toomanagement de acceso de lectura (por ejemplo, capacidades de consulta) y las aplicaciones de tooresolve de capacidad de Hola y servicios.</p><p>Especificar las funciones de cliente hello dos (cliente y administrador) en tiempo de Hola de creación del clúster proporcionando certificados independientes para cada uno.</p>|

## <a id="modeling-field"></a>Realización de modelos de seguridad y uso de seguridad de nivel de campo cuando sea necesario

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Dynamics CRM | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | N/D  |
| **Pasos** | Realice modelos de seguridad y use seguridad de nivel de campo cuando sea necesario.|

## <a id="portal-security"></a>Realizar el modelo de seguridad de las cuentas de portal teniendo en cuenta ese modelo de seguridad de hello para el portal de hello es distinto del resto de Hola de CRM

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Portal de Dynamics CRM | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | N/D  |
| **Pasos** | Realizar el modelo de seguridad de las cuentas de portal teniendo en cuenta ese modelo de seguridad de hello para el portal de hello es distinto del resto de Hola de CRM|

## <a id="permission-entities"></a>Concesión de permiso detallado en una serie de entidades de Azure Table Storage

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Azure Storage | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | StorageType: tabla |
| **Referencias**              | [Cómo toodelegate tener acceso a tooobjects en su cuenta de almacenamiento de Azure mediante SAS](https://azure.microsoft.com/documentation/articles/storage-security-guide/#_data-plane-security) |
| **Pasos** | En determinados escenarios empresariales, almacenamiento de tabla de Azure puede ser necesario toostore datos confidenciales que se encarga de toodifferent partes. Por ejemplo, datos confidenciales pertenecen toodifferent países. En tales casos, las firmas SAS se pueden construir especificando Hola partición y fila intervalos de claves, tal que un usuario pueda acceder país determinado tooa específico de datos.| 

## <a id="rbac-azure-manager"></a>Habilitar la cuenta de almacenamiento de tooAzure de Control de acceso basado en roles (RBAC) con el Administrador de recursos de Azure

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Azure Storage | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | [Cómo toosecure su cuenta de almacenamiento, con Control de acceso basado en roles (RBAC)](https://azure.microsoft.com/documentation/articles/storage-security-guide/#management-plane-security) |
| **Pasos** | <p>Cuando se crea una nueva cuenta de almacenamiento, se selecciona un modelo de implementación clásico o de Azure Resource Manager. modelo clásico de Hola de creación de recursos en Azure solo permite suscripciones de toohello de acceso de todo o nada y Hola a su vez, la cuenta de almacenamiento.</p><p>Con el modelo de Azure Resource Manager hello, coloca cuenta de almacenamiento de hello en un recurso grupo y control de acceso toohello administración plano de esa cuenta de almacenamiento específico con Azure Active Directory. Por ejemplo, se pueden proporcionar a usuarios específicos Hola capacidad tooaccess Hola almacenamiento cuenta las claves, mientras que otros usuarios pueden ver información acerca de la cuenta de almacenamiento de hello, pero no pueden tener acceso a claves de cuenta de almacenamiento de Hola.</p>|

## <a id="rooting-detection"></a>Implementación de detección implícita de jailbreak o rooting

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Cliente móvil | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | N/D  |
| **Pasos** | <p>La aplicación debe proteger sus propios datos de configuración y de usuario en caso de rooting o jailbreak del teléfono. El rooting o jailbreak implican un acceso no autorizado, que los usuarios normales no realizarían en su propio teléfono. Por lo tanto, la aplicación debe tener lógica de detección implícita al iniciar la aplicación, toodetect si se ha modificado el teléfono de Hola.</p><p>lógica de detección de Hello puede tener solo tiene acceso a archivos que normalmente solo raíz puede acceder el usuario, por ejemplo:</p><ul><li>/system/app/Superuser.apk</li><li>/sbin/su</li><li>/system/bin/su</li><li>/system/xbin/su</li><li>/data/local/xbin/su</li><li>/data/local/bin/su</li><li>/system/sd/xbin/su</li><li>/system/bin/failsafe/su</li><li>/data/local/su</li></ul><p>Si la aplicación hello puede tener acceso a cualquiera de estos archivos, indica que la aplicación hello está ejecutando como usuario raíz.</p>|

## <a id="weak-class-wcf"></a>Referencia débil de clase en WCF

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | WCF | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico, .NET Framework 3 |
| **Atributos**              | N/D  |
| **Referencias**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Pasos** | <p>sistema de Hello usa una referencia de clase débil, que podría permitir que un atacante al código tooexecute no autorizado. programa Hello hace referencia a una clase definida por el usuario que no se identifica de forma única. Cuando se carga esta clase débilmente identificada, Hola CLR tipo cargador busca clase Hola Hola siguientes ubicaciones en hello .NET especifica orden:</p><ol><li>Si se conoce el ensamblado hello del tipo hello, búsquedas de cargador de Hola Hola de redirección ubicaciones, GAC, Hola ensamblado actual del archivo de configuración utilizando información de configuración y Hola directorio base de la aplicación</li><li>Si el ensamblado de hello es desconocido, búsquedas de cargador de Hola Hola ensamblado actual, mscorlib y la ubicación de hello devuelto por el controlador de eventos de hello TypeResolve</li><li>Este orden de búsqueda CLR se puede modificar con enlaces como mecanismo de tipo reenvío hello y evento AppDomain.TypeResolve de Hola</li></ol><p>Si un atacante aprovecha el orden de búsqueda CLR de hello mediante la creación de una clase alternativa con Hola mismo nombre y colocarlo en una ubicación alternativa que Hola CLR se cargará en primer lugar, Hola CLR involuntariamente ejecutará el código proporcionado por el atacante de Hola</p>|

### <a name="example"></a>Ejemplo
Hola `<behaviorExtensions/>` elemento del archivo de configuración de WCF de hello siguiente indica a WCF tooadd una extensión determinada de WCF de comportamiento personalizado clase tooa.
```
<system.serviceModel>
    <extensions>
        <behaviorExtensions>
            <add name=""myBehavior"" type=""MyBehavior"" />
        </behaviorExtensions>
    </extensions>
</system.serviceModel>
```
Al utilizar nombres completos (seguros), se identifica exclusivamente a un tipo, lo que mejora la seguridad del sistema. Utilice nombres de ensamblado completo al registrar los tipos en los archivos machine.config y app.config Hola.

### <a name="example"></a>Ejemplo
Hola `<behaviorExtensions/>` elemento del archivo de configuración de WCF de hello siguiente indica a WCF tooadd fuertemente hace referencia a clase tooa determinado WCF extensión de comportamiento personalizado.
```
<system.serviceModel>
    <extensions>
        <behaviorExtensions>
            <add name=""myBehavior"" type=""Microsoft.ServiceModel.Samples.MyBehaviorSection, MyBehavior,
            Version=1.0.0.0, Culture=neutral, PublicKeyToken=null"" />
        </behaviorExtensions>
    </extensions>
</system.serviceModel>
```

## <a id="wcf-authz"></a>WCF: implementación de control de autorización

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | WCF | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico, .NET Framework 3 |
| **Atributos**              | N/D  |
| **Referencias**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Pasos** | <p>Este servicio no usa un control de autorización. Cuando un cliente llama a un determinado servicio WCF, WCF proporciona varios esquemas de autorización que comprueben que llamador hello tiene método de servicio de permiso tooexecute hello en el servidor de Hola. Si los controles de autorización no están habilitados para los servicios de WCF, un usuario autenticado puede lograr una elevación de privilegios.</p>|

### <a name="example"></a>Ejemplo
Hola siguiente configuración indica a WCF toonot Hola autorización el nivel de comprobación de cliente hello cuando se ejecuta el servicio de hello:
```
<behaviors>
    <serviceBehaviors>
        <behavior>
            ...
            <serviceAuthorization principalPermissionMode=""None"" />
        </behavior>
    </serviceBehaviors>
</behaviors>
```
Use un tooverify de esquema de autorización de servicio que Hola llamador del método de servicio de hello es toodo autorizado para. WCF ofrece dos modos y permite la definición de Hola de un esquema de autorización personalizada. modo de Hello UseWindowsGroups utiliza usuarios y roles de Windows y el modo de hello UseAspNetRoles utiliza un proveedor de funciones ASP.NET, como SQL Server, tooauthenticate.

### <a name="example"></a>Ejemplo
Hello configuración siguiente indica que ese cliente hello es parte del grupo de administradores de hello antes de ejecutar Hola Agregar servicio WCF toomake:
```
<behaviors>
    <serviceBehaviors>
        <behavior>
            ...
            <serviceAuthorization principalPermissionMode=""UseWindowsGroups"" />
        </behavior>
    </serviceBehaviors>
</behaviors>
```
servicio de Hello, a continuación, se declara como siguiente hello:
```
[PrincipalPermission(SecurityAction.Demand,
Role = ""Builtin\\Administrators"")]
public double Add(double n1, double n2)
{
double result = n1 + n2;
return result;
}
```

## <a id="authz-aspnet"></a>Implementación del mecanismo de autorización adecuado en ASP.NET Web API

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | API Web | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico, MVC5 |
| **Atributos**              | N/D; Proveedor de identidades; ADFS, Proveedor de identidades; Azure AD |
| **Referencias**              | [Autenticación y autorización en ASP.NET Web API](http://www.asp.net/web-api/overview/security/authentication-and-authorization-in-aspnet-web-api) |
| **Pasos** | <p>Información de usuarios de la aplicación hello roles se puede derivar de Azure AD o notificaciones ADFS si la aplicación hello se basa en ellos como proveedor de identidades o aplicación hello propio, es posible que proporcionan. En cualquiera de estos casos, implementación de autorización personalizada hello debe validar información de roles de usuario de Hola.</p><p>Información de usuarios de la aplicación hello roles se puede derivar de Azure AD o notificaciones ADFS si la aplicación hello se basa en ellos como proveedor de identidades o aplicación hello propio, es posible que proporcionan. En cualquiera de estos casos, implementación de autorización personalizada hello debe validar información de roles de usuario de Hola.</p>

### <a name="example"></a>Ejemplo
```C#
[AttributeUsage(AttributeTargets.Class | AttributeTargets.Method, Inherited = true, AllowMultiple = true)]
public class ApiAuthorizeAttribute : System.Web.Http.AuthorizeAttribute
{
        public async override Task OnAuthorizationAsync(HttpActionContext actionContext, CancellationToken cancellationToken)
        {
            if (actionContext == null)
            {
                throw new Exception();
            }

            if (!string.IsNullOrEmpty(base.Roles))
            {
                bool isAuthorized = ValidateRoles(actionContext);
                if (!isAuthorized)
                {
                    HandleUnauthorizedRequest(actionContext);
                }
            }

            base.OnAuthorization(actionContext);
        }

public bool ValidateRoles(actionContext)
{
   //Authorization logic here; returns true or false
}

}
```
Hola a todos los controladores y métodos de acción que debe tooprotected deben ser representativos con por encima del atributo.
```C#
[ApiAuthorize]
public class CustomController : ApiController
{
     //Application code goes here
}
```

## <a id="device-permission"></a>Realizar comprobaciones de autorización en el dispositivo de hello si admite varias acciones que requieren distintos niveles de permisos

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Dispositivo IoT | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | N/D  |
| **Pasos** | <p>Hola dispositivo debe autorizar Hola llamador toocheck si el llamador de hello tiene acción de Hola Hola requiere permisos tooperform solicitado. Para p. ej. permite decir Hola dispositivo es un bloqueo de puerta inteligente que se puede supervisar desde la nube de hello, además proporciona funcionalidades como remotamente bloquear puerta de Hola.</p><p>Hola Smart Lock puerta proporciona funcionalidad desbloquear sólo cuando alguien viene físicamente cerca de la puerta de hello con una tarjeta. En este caso, hello implementación del comando remoto de Hola y el control debe realizarse de manera que no proporciona ninguna puerta de hello toounlock funcionalidad como puerta de enlace de hello en la nube no es toosend autorizado una puerta de hello toounlock de comando.</p>|

## <a id="field-permission"></a>Realizar comprobaciones de autorización en hello puerta de enlace de campo si es compatible con varias acciones que requieren distintos niveles de permisos

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Puerta de enlace de campo de IoT | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | N/D  |
| **Pasos** | Hola puerta de enlace de campo debe autorizar Hola llamador toocheck si el llamador de hello tiene acción de Hola Hola requiere permisos tooperform solicitado. Para p. ej. debería haber permisos diferentes para un usuario Administrador de interfaz/API usar tooconfigure dispositivos de puerta de enlace v/s un campo que se conectan tooit.|
