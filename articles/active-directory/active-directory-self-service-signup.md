---
title: "¿aaaWhat es la suscripción de autoservicio de Azure? | Microsoft Docs"
description: "Una suscripción de autoservicio de información general de Azure, cómo toomanage Hola proceso de suscripción y cómo tootake a través de un nombre de dominio DNS."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: b9f01876-29d1-4ab8-8b74-04d43d532f4b
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/08/2017
ms.author: curtand
ms.openlocfilehash: dbf3b59e3807e98f7bf39f3d5591fcde01667323
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-self-service-signup-for-azure"></a>¿Qué es la suscripción de autoservicio de Azure?
Este tema explica el proceso de suscripción de autoservicio de Hola y cómo tootake a través de un nombre de dominio DNS.  

## <a name="why-use-self-service-signup"></a>Razones para usar la suscripción de autoservicio
* Get tooservices de los clientes que deseen con mayor rapidez.
* Cree ofertas basadas en correo electrónico para un servicio.
* Crear flujos de suscripción basada en correo electrónico que permiten rápidamente a los usuarios identidades toocreate utilizando sus alias de correo electrónico de trabajo fácil de recordar.
* Los directorios de Azure no administrados se pueden convertir en directorios administrados más adelante y reutilizarse para otros servicios.

## <a name="terms-and-definitions"></a>Términos y definiciones
* **Registro de autoservicio**: se trata de método de hello por el que un usuario se suscribe a un servicio de nube y una identidad que se crean automáticamente para ellos en Azure Active Directory (Azure AD) en función de su dominio de correo electrónico.
* **Directorio de Azure no administrado**: se trata de directorio de hello en el que se crea esa identidad. Un directorio no administrado es un directorio que no tiene administrador global.
* **Usuario comprobado por correo electrónico**: tipo de cuenta de usuario en Azure AD. Un usuario que tiene una identidad que se crean automáticamente después de suscribirse a una oferta de autoservicio se conoce como usuario comprobado por correo electrónico. Un usuario comprobado por correo electrónico es un miembro regular de un directorio etiquetado con creationmethod = EmailVerified.

## <a name="user-experience"></a>Experiencia del usuario
Por ejemplo, supongamos que un usuario cuyo correo electrónico es Dan@BellowsCollege.com recibe archivos confidenciales por correo electrónico. archivos de Hola se protegieron con Azure Rights Management (Azure RMS). Pero la organización de Dan, Bellows College, no se ha suscrito a Azure RMS ni ha implementado Active Directory RMS. En este caso, Dan puede solicitar para una tooRMS suscripción gratuita para usuarios de archivos de pedido tooread Hola protegido.

Si se Dan es el primer usuario con una dirección de correo electrónico de BellowsCollege.com toosign hacia arriba para esta oferta de autoservicio de hello, se creará un directorio no administrado para BellowsCollege.com en Azure AD. Si otros usuarios del dominio de BellowsCollege.com Hola registran para esta oferta o una oferta similar de autoservicio, también tendrán las cuentas de usuario comprobados por correo electrónico creadas en hello administrados por el mismo directorio en Azure.

## <a name="admin-experience"></a>Experiencia del administrador
Un administrador que posee el nombre de dominio DNS de Hola de un directorio de Azure no administrado puede asumir o combinar el directorio de hello después de probar la propiedad. Hola siguiente sección explica la experiencia de administración de hello con más detalle, pero este es un resumen:

* Cuando tome el control de un directorio de Azure no administrado, se convierte simplemente en hello administrador global del directorio de hello no administrado. Esto se denomina a veces adquisición interna.
* Cuando se combina un directorio de Azure no administrado, Agregar nombre de dominio DNS de Hola Hola directorio no administrado tooyour administrado directorio de Azure y se crea una asignación de recursos de los usuarios por lo que los usuarios pueden seguir tooaccess servicios sin interrupción. Esto se denomina a veces adquisición externa.

## <a name="what-gets-created-in-azure-active-directory"></a>¿Qué se crea en Azure Active Directory?
#### <a name="directory"></a>Directorio
* Se crea un directorio de Azure Active Directory para el dominio de hello, un directorio por dominio.
* directorio de Azure AD de Hello no tiene ningún administrador global.

#### <a name="users"></a>Usuarios
* Para cada usuario que se registra, se crea un objeto de usuario en el directorio de Azure AD Hola.
* Cada objeto de usuario se marca como externo.
* Cada usuario recibe servicio de toohello de acceso que se inició en.

### <a name="how-do-i-claim-a-self-service-azure-ad-directory-for-a-domain-i-own"></a>¿Cómo puedo reclamar un directorio de Azure AD de autoservicio para un dominio de mi propiedad?
Puede reclamar un directorio de Azure AD de autoservicio realizando la validación del dominio. Validación del dominio demuestra dominio propio hello mediante la creación de registros DNS.

Hay dos maneras toodo una adquisición DNS de un directorio de Azure AD:

* adquisición interno (Admin detecta un directorio de Azure no administrado y desea tooturn en un directorio administrado)
* adquisición externo (Admin intenta tooadd un nuevo dominio tootheir administrado directorio de Azure)

Puede que esté interesado en la validación que posee un dominio dado que va a realizar en un directorio no administrado después de que un usuario realiza la suscripción de autoservicio o agregar un nuevo dominio tooan administrado directorio existente. Por ejemplo, tiene un dominio llamado contoso.com y desea tooadd un nuevo dominio denominado contoso.es o contoso.uk.

## <a name="what-is-domain-takeover"></a>¿Qué es la adquisición de un dominio?
Esta sección trata sobre cómo toovalidate que posee un dominio

### <a name="what-is-domain-validation-and-why-is-it-used"></a>¿Qué es la validación de dominios y por qué se usa?
En operaciones de orden tooperform en un directorio, Azure AD necesita que valida la propiedad de dominio DNS de Hola.  La validación del dominio de hello permite directory hello tooclaim y o bien promover Hola autoservicio tooa administrado directorio o directorios de autoservicio Hola de mezcla en una existente administrada directorio.

## <a name="examples-of-domain-validation"></a>Ejemplos de validación de dominio
Hay dos toodo formas una adquisición DNS de un directorio:

* adquisición interno (por ejemplo, un administrador detecta un directorio de autoservicio y no administrado y desea tooturn en directorio administrado)
* adquisición externo (por ejemplo, un administrador intenta tooadd un nuevo directorio administrado de tooa de dominio)

### <a name="internal-takeover---promote-a-self-service-unmanaged-directory-toobe-a-managed-directory"></a>Adquisición interno - promover un toobe un directorio administrado de directorio de autoservicio y no administrado
Al hacerlo adquisición interno, directorio de Hola se convierte desde un directorio administrado tooa de directorio no administrado. Se necesita validación de nombre de dominio DNS toocomplete, y en el que crea un registro MX o un registro TXT en zona DNS de Hola. Esa acción:

* Valida que posee el dominio de Hola
* Hace directory Hola administrado
* Hace Hola administrador global del directorio de Hola

Supongamos que un administrador de TI de la Universidad de fuelles detecta que los usuarios de la escuela de hello registrarse para obtener ofertas de autoservicio. Hola registrados propietario de hello DNS nombre BellowsCollege.com, Hola, Administrador de TI puede validar la propiedad de nombre DNS de hello en Azure y, a continuación, asumen el directorio de hello no administrado. Hello directorio, a continuación, se convierte en un directorio administrado y hello Administrador de TI se asigna rol de administrador global de hello para el directorio de BellowsCollege.com Hola.

### <a name="external-takeover---merge-a-self-service-directory-into-an-existing-managed-directory"></a>Adquisición externa: fusión de un directorio de autoservicio en un directorio administrado existente
En una adquisición externo, ya tiene un directorio administrado y desea que todos los usuarios y grupos de un toojoin de directorio no administrado que administran el directorio, en lugar de dos propios directorios independientes.

Como administrador de un directorio administrado, se agrega un dominio y ese dominio ocurre toohave un directorio no administrado asociado a él.

Por ejemplo, supongamos que es un administrador de TI y ya tiene un directorio administrado para un nombre de dominio que está registrado tooyour organización Contoso.com. Descubre que los usuarios de su organización han realizado una suscripción de autoservicio a una oferta con un nombre de dominio de correo electrónico user@contoso.co.uk, que es otro nombre de dominio que posee su organización. Actualmente, esos usuarios tienen cuentas en un directorio no administrado para contoso.co.uk.

No desea toomanage dos directorios independientes, por lo que combine directorio no administrado de hello contoso.co.uk con el directorio de TI administrados existente para contoso.com.

Externo sigue adquisición Hola mismo proceso de validación de DNS como adquisición interno.  Va a las diferencias: usuarios y servicios son toohello reasignado TI directorio administrado.

#### <a name="whats-hello-impact-of-performing-an-external-takeover"></a>¿Cuál es el impacto de Hola de llevar a cabo una adquisición externo?
Con una adquisición externo, se crea una asignación de los usuarios a recursos de forma que los usuarios puedan seguir tooaccess servicios sin interrupción. Muchas aplicaciones, como RMS para individuos, controlan asignación de Hola de recursos de los usuarios también, y los usuarios pueden seguir tooaccess esos servicios sin cambios. Si una aplicación no controla asignación Hola de los usuarios a recursos de forma eficaz, adquisición externo puede ser tooprevent explícitamente bloqueados los usuarios una experiencia deficiente.

#### <a name="directory-takeover-support-by-service"></a>Admisión de la adquisición del directorio por servicio
Hola actualmente después de adquisición de soporte técnico de servicios:

* RMS

Hola después services admitirá pronto adquisición:

* PowerBI

siguiente Hello no garantizan ni necesita datos de usuario de toomigrate de acción de administración adicionales después de una adquisición externo.

* SharePoint/OneDrive

## <a name="how-tooperform-a-dns-domain-name-takeover"></a>¿Cómo tooperform un dominio DNS nombre adquisición
Tiene unas cuantas opciones de cómo tooperform una validación de dominio (y realice una adquisición si lo desea):

1. Portal de administración de Azure

   Una adquisición se desencadena  agregando un dominio.  Si ya existe un directorio para el dominio de hello, tendrá Hola opción tooperform una adquisición externo.

   Inicie sesión en toohello portal de Azure con sus credenciales.  Navegue tooyour de directorio existente y, a continuación, demasiado**Agregar dominio**.
2. Office 365

   Puede utilizar opciones de hello en hello [administrar dominios](https://support.office.com/article/Navigate-to-the-Office-365-Manage-domains-page-026af1f2-0e6d-4f2d-9b33-fd147420fac2/) página en Office 365 toowork con los dominios y registros DNS. Consulte [Comprobar el dominio en Office 365](https://support.office.com/article/Verify-your-domain-in-Office-365-6383f56d-3d09-4dcb-9b41-b5f5a5efd611/).
3. Windows PowerShell

   Hola pasos es necesario tooperform una validación mediante Windows PowerShell.

   | Paso | Cmdlet toouse |
   | --- | --- |
   | Crear un objeto de credencial |Get-Credential |
   | Conectar tooAzure AD |Connect-MsolService |
   | Obtener una lista de dominios |Get-MsolDomain |
   | Crear un desafío |Get-MsolDomainVerificationDns |
   | Crear un registro DNS |Realice esta acción en su servidor de DNS |
   | Comprobar el desafío de Hola |Confirm-MsolEmailVerifiedDomain |

Por ejemplo:

1. Conectar tooAzure AD mediante credenciales de Hola que estaban toorespond usado toohello autoservicio oferta:

        import-module MSOnline
        $msolcred = get-credential
        connect-msolservice -credential $msolcred
2. Obtenga una lista de dominios:

    Get-MsolDomain
3. A continuación, ejecute toocreate de cmdlet Get-MsolDomainVerificationDns Hola un desafío:

    Get-MsolDomainVerificationDns –DomainName *nombre_de_dominio* –Mode DnsTxtRecord

    Por ejemplo:

    Get-MsolDomainVerificationDns –DomainName contoso.com –Mode DnsTxtRecord
4. Copiar valor de hello (desafío Hola) que se devuelve de este comando.

    Por ejemplo:

    MS=32DD01B82C05D27151EA9AE93C5890787F0E65D9
5. En el espacio de nombres DNS público, cree un registro txt DNS que contiene el valor de Hola que copió en el paso anterior de Hola.

    nombre de Hola para este registro es el nombre del dominio primario de Hola de Hola, por lo que si crea este registro de recursos con rol de hello DNS de Windows Server, deje el nombre del registro de hello en blanco y simplemente pegue el valor de hello en el cuadro de texto hello
6. Ejecute el desafío hello tooverify de hello Confirm-MsolDomain cmdlet:

    Confirm-MsolEmailVerifiedDomain -DomainName *nombre_de_dominio*

    Por ejemplo:

    Confirm-MsolEmailVerifiedDomain -DomainName contoso.com

Un desafío correcto le devuelve toohello aviso sin errores.

## <a name="how-do-i-control-self-service-settings"></a>¿Cómo controlo la configuración de autoservicio?
Actualmente, los administradores tienen dos controles de autoservicio . Pueden controlar:

* Si los usuarios pueden unirse al directorio de Hola a través de correo electrónico.
* Si los usuarios pueden concederse o no licencias para aplicaciones y servicios.

### <a name="how-can-i-control-these-capabilities"></a>¿Cómo puedo controlar estas capacidades?
Un administrador puede configurar estas capacidades con estos parámetros Set-MsolCompanySettings de cmdlet de Azure AD:

* **AllowEmailVerifiedUsers** controla si un usuario puede crear o unirse a un directorio no administrado. Si se establece ese parámetro demasiado$ false, no comprobados por correo electrónico a los usuarios pueden unirse al directorio de Hola.
* **AllowAdHocSubscriptions** controla la capacidad de Hola para los usuarios registrarse tooperform self-service. Si se establece ese parámetro demasiado$ false, ningún usuario puede realizar la suscripción de autoservicio.

### <a name="how-do-hello-controls-work-together"></a>¿Cómo controles Hola funcionan juntas?
Estos dos parámetros se pueden usar en conjunción toodefine un control más preciso sobre autoservicio suscribirse. Por ejemplo, hello siguiente comando permitirá que los usuarios tooperform registro de autoservicio, pero solo si los usuarios ya tienen una cuenta de Azure AD (en otras palabras, los usuarios que tendría un toobe cuenta comprobados por correo electrónico creado no pueden realizar sin intervención del Administrador de inicio de sesión seguridad):

    Set-MsolCompanySettings -AllowEmailVerifiedUsers $false -AllowAdHocSubscriptions $true

Hello diagrama de flujo siguiente explica todas las combinaciones diferentes de Hola para estos parámetros y Hola resultante condiciones para el directorio de Hola y de registro de autoservicio.

![][1]

Para obtener más información y ejemplos de cómo toouse estos parámetros, consulte [Set-MsolCompanySettings](/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0).

## <a name="see-also"></a>Otras referencias
* [¿Cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview)
* [Azure PowerShell](/powershell/azure/overview)
* [Referencia de cmdlets de Azure](/powershell/azure/get-started-azureps)
* [Set-MsolCompanySettings](/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0)

<!--Image references-->
[1]: ./media/active-directory-self-service-signup/SelfServiceSignUpControls.png
