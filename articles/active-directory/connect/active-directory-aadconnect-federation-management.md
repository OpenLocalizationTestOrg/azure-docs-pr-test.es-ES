---
title: "aaaActive Directory Federation Services personalización con Azure AD Connect y administración | Documentos de Microsoft"
description: "Administración de AD FS con Azure AD Connect y personalización del inicio de sesión de AD FS del usuario con Azure AD Connect y PowerShell."
keywords: "AD FS, ADFS, administración de AD FS, AAD Connect, Connect, inicio de sesión, personalización de AD FS, reparación de la confianza, Office 365, federación, usuario de confianza"
services: active-directory
documentationcenter: 
author: anandyadavmsft
manager: femila
editor: 
ms.assetid: 2593b6c6-dc3f-46ef-8e02-a8e2dc4e9fb9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 361a2bfd6d7a6993dbe773d6ea039ad1afc6346a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-and-customize-active-directory-federation-services-by-using-azure-ad-connect"></a>Administre y personalice Servicios de federación de Active Directory con Azure AD Connect
Este artículo se describe cómo toomanage y personalizar los servicios de federación de Active Directory (AD FS) mediante el uso de Connect de Azure Active Directory (Azure AD). También incluye otras tareas habituales de AD FS que puede ser necesario toodo para completar la configuración de una granja de servidores de AD FS.

| Tema. | Qué trata |
|:--- |:--- |
| **Administración de AD FS** | |
| [Confianza de Hola de reparación](#repairthetrust) |La federación de hello toorepair confiar con Office 365. |
| [Federación con Azure AD mediante un identificador de inicio de sesión alternativo](#alternateid) | Configuración de la federación con un identificador de inicio de sesión alternativo  |
| [Adición de un servidor de AD FS](#addadfsserver) |¿Cómo tooexpand AD FS de granja de servidores con un servidor de AD FS adicional. |
| [Incorporación de un servidor proxy de aplicación web de AD FS](#addwapserver) |¿Cómo tooexpand AD FS de granja de servidores con un servidor Proxy de aplicación Web (WAP) adicional. |
| [Adición de un dominio federado](#addfeddomain) |¿Cómo tooadd un dominio federado. |
| [Actualiza el certificado SSL de Hola](active-directory-aadconnectfed-ssl-update.md)| ¿Cómo tooupdate Hola SSL de certificados para una granja de servidores de AD FS. |
| **Personalización de AD FS** | |
| [Adición de un logotipo de la compañía personalizado o una ilustración](#customlogo) |¿Cómo inicio de sesión toocustomize AD FS en la página con un logotipo de empresa y la ilustración. |
| [Adición de la descripción de inicio de sesión](#addsignindescription) |¿Cómo tooadd un inicio de sesión en la página de descripción. |
| [Modificación de las reglas de notificaciones de AD FS](#modclaims) |¿Cómo toomodify AD FS notificaciones para los distintos escenarios de federación. |

## <a name="manage-ad-fs"></a>Administración de AD FS
Puede realizar diversas tareas de AD FS-relacionados en Azure AD Connect con intervención mínima del usuario mediante el Asistente de hello Azure AD Connect. Cuando haya terminado de instalar Azure AD Connect mediante la ejecución del Asistente para hello, puede ejecutar el Asistente de hello nuevo tooperform las tareas adicionales.

## Confianza de Hola de reparación<a name=repairthetrust></a>
Puede usar Azure AD Connect toocheck Hola actual estado Hola AD FS y confianza de Azure AD y tomar las medidas oportunas toorepair Hola confianza. Siga estos pasos toorepair Azure AD y AD FS de confianza.

1. Seleccione **AAD de reparación y confiar en AD FS** de lista de Hola de tareas adicionales.
   ![Reparar AAD y confianza de ADFS](media/active-directory-aadconnect-federation-management/RepairADTrust1.PNG)

2. En hello **conectar tooAzure AD** página, proporcione las credenciales de administrador global de Azure AD y haga clic en **siguiente**.
   ![Conectar tooAzure AD](media/active-directory-aadconnect-federation-management/RepairADTrust2.PNG)

3. En hello **las credenciales de acceso remoto** página, escriba las credenciales de hello para el Administrador de dominio de Hola.

   ![Credenciales de acceso remoto](media/active-directory-aadconnect-federation-management/RepairADTrust3.PNG)

    Cuando hace clic en **Siguiente**, Azure AD Connect comprueba el estado del certificado y muestra los problemas que existen.

    ![Estado de los certificados](media/active-directory-aadconnect-federation-management/RepairADTrust4.PNG)

    Hola **tooconfigure listo** página muestra hello lista de acciones que realiza la confianza de hello toorepair.

    ![Tooconfigure listo](media/active-directory-aadconnect-federation-management/RepairADTrust5.PNG)

4. Haga clic en **instalar** confianza de hello toorepair.

> [!NOTE]
> Azure AD Connect solo puede reparar o actuar en los certificados autofirmados. Azure AD Connect no puede reparar certificados de terceros.

## Federación con Azure AD mediante un identificador de inicio de sesión alternativo<a name=alternateid></a>
Se recomienda que hello Principal de usuario Name(UPN) local y nombre Principal de usuario se mantienen en la nube Hola Hola igual. Si Hola UPN local usa un dominio no enrutables (p. ej. Contoso.local) o no se puede cambiar debido a las dependencias de aplicación toolocal, se recomienda configurar el Id. de inicio de sesión alternativo. Id. de inicio de sesión alternativo permite tooconfigure un inicio de sesión de experimentar donde los usuarios puedan iniciar sesión con un atributo que no sea su UPN, por ejemplo, correo electrónico. elección de Hello para el nombre Principal de usuario en el atributo de Azure AD Connect valores predeterminados toohello userPrincipalName en Active Directory. Si elige cualquier otro atributo como nombre principal de usuario y está realizando una federación mediante AD FS, Azure AD Connect configurará AD FS para el identificador de inicio de sesión alternativo. A continuación, se muestra un ejemplo de elección de un atributo diferente para el nombre principal de usuario:

![Selección de atributo de identificador alternativo](media/active-directory-aadconnect-federation-management/attributeselection.png)

La configuración del identificador de inicio de sesión alternativo para AD FS consta de dos pasos principales:
1. **Configurar el conjunto correcto de Hola de notificaciones de emisión**: reglas de notificación de emisión de Hola de usuario de confianza de hello Azure AD de confianza son atributo UserPrincipalName de toouse modificado Hola seleccionado como Hola Id. alternativo del usuario de Hola.
2. **Habilitar el Id. de inicio de sesión alternativo en la configuración de AD FS Hola**: Hola AD FS configuración se ha actualizado para que AD FS puede buscar usuarios en bosques adecuado hello mediante identificador de hello alternativo. Esta configuración se admite en AD FS en Windows Server 2012 R2 (con KB2919355) o versiones posteriores. Si hay servidores de hello AD FS 2012 R2, las comprobaciones de Azure AD Connect presencia de Hola de hello necesarias KB. Si hello KB no se detecta, se mostrará una advertencia cuando finalice la configuración, tal y como se muestra a continuación:

    ![Advertencia de que falta la KB en 2012 R2](media/active-directory-aadconnect-federation-management/kbwarning.png)

    toorectify configuración de hello en el caso de KB que faltan, instalar Hola necesario [KB2919355](http://go.microsoft.com/fwlink/?LinkID=396590) y, a continuación, repare Hola confianza usando [reparar AAD y confianza de AD FS](#repairthetrust).

> [!NOTE]
> Para obtener más información sobre toomanually alternateID y pasos, configurar, leer [configurar Id. de inicio de sesión alternativo](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configuring-alternate-login-id)

## Adición de un servidor de AD FS <a name=addadfsserver></a>

> [!NOTE]
> servidor de tooadd AD FS, Azure AD Connect requiere el certificado PFX Hola. Por lo tanto, puede realizar esta operación solo si configuró la granja de servidores de hello AD FS mediante el uso de Azure AD Connect.

1. Seleccione **Implementar un servidor de federación adicional** y haga clic en **Siguiente**.

   ![Servidor de federación adicional](media/active-directory-aadconnect-federation-management/AddNewADFSServer1.PNG)

2. En hello **conectar tooAzure AD** página, escriba sus credenciales de administrador global de Azure AD y haga clic en **siguiente**.

   ![Conectar tooAzure AD](media/active-directory-aadconnect-federation-management/AddNewADFSServer2.PNG)

3. Proporcione las credenciales de administrador de dominio de Hola.

   ![Credenciales del administrador de dominio](media/active-directory-aadconnect-federation-management/AddNewADFSServer3.PNG)

4. Azure AD Connect pedirá una contraseña de hello del archivo PFX de Hola que proporcionó al configurar la nueva granja de AD FS con Azure AD Connect. Haga clic en **escribir la contraseña** tooprovide contraseña de hello para el archivo PFX de Hola.

   ![Contraseña del certificado](media/active-directory-aadconnect-federation-management/AddNewADFSServer4.PNG)

    ![Especificar certificado SSL](media/active-directory-aadconnect-federation-management/AddNewADFSServer5.PNG)

5. En hello **servidores de AD FS** página, escriba el nombre del servidor de Hola o toobe de dirección IP agrega granja de servidores de toohello AD FS.

   ![Servidores de AD FS](media/active-directory-aadconnect-federation-management/AddNewADFSServer6.PNG)

6. Haga clic en **siguiente**y pasar por hello final **configurar** página. Después de Azure AD Connect ha terminado de agregar el conjunto de servidores de hello servidores toohello AD FS, se le ofrecerá la conectividad de hello opción tooverify Hola.

   ![Tooconfigure listo](media/active-directory-aadconnect-federation-management/AddNewADFSServer7.PNG)

    ![Instalación completada](media/active-directory-aadconnect-federation-management/AddNewADFSServer8.PNG)

## Incorporación de un servidor de AD FS <a name=addwapserver></a>

> [!NOTE]
> tooadd un servidor WAP, Azure AD Connect requiere el certificado PFX Hola. Por lo tanto, solo puede realizar esta operación si configuró la granja de servidores de hello AD FS mediante el uso de Azure AD Connect.

1. Seleccione **implementar Web Application Proxy** desde la lista de Hola de tareas disponibles.

   ![Implementación de Proxy de aplicación web](media/active-directory-aadconnect-federation-management/WapServer1.PNG)

2. Proporcione las credenciales de administrador global de Azure de Hola.

   ![Conectar tooAzure AD](media/active-directory-aadconnect-federation-management/wapserver2.PNG)

3. En hello **certificado SSL especificar** página, proporcione la contraseña de hello para el archivo PFX de Hola que proporcionó cuando configuró la granja de servidores de hello AD FS con Azure AD Connect.
   ![Contraseña del certificado](media/active-directory-aadconnect-federation-management/WapServer3.PNG)

    ![Especificar certificado SSL](media/active-directory-aadconnect-federation-management/WapServer4.PNG)

4. Agregar Hola server toobe agregado como un servidor WAP. Como servidor WAP de hello no puede ser toohello Unidos a un dominio, Hola asistente pregunta server toohello de credenciales administrativas que se va a agregar.

   ![Credenciales administrativas del servidor](media/active-directory-aadconnect-federation-management/WapServer5.PNG)

5. En hello **las credenciales de confianza de Proxy** , proporcione el proxy de credenciales administrativas tooconfigure Hola confianza y el acceso de servidor principal hello en la granja de servidores de AD FS Hola.

   ![Credenciales de confianza del proxy](media/active-directory-aadconnect-federation-management/WapServer6.PNG)

6. En hello **tooconfigure listo** página, el Asistente de hello muestra lista Hola de acciones que se llevará a cabo.

   ![Tooconfigure listo](media/active-directory-aadconnect-federation-management/WapServer7.PNG)

7. Haga clic en **instalar** configuración de toofinish Hola. Una vez completada la configuración de hello, Hola asistente le proporciona Hola tooverify opción Hola servidores toohello de conectividad. Haga clic en **compruebe** toocheck conectividad.

   ![Instalación completada](media/active-directory-aadconnect-federation-management/WapServer8.PNG)

## Adición de un dominio federado <a name=addfeddomain></a>

Es fácil tooadd toobe de un dominio federado con Azure AD mediante el uso de Azure AD Connect. Azure AD Connect agrega el dominio de hello para la federación y modifica la notificación de hello toocorrectly reglas reflejar a emisor hello cuando tiene varios dominios federados con Azure AD.

1. tooadd un dominio federado, tarea hello seleccione **agregar otro dominio de Azure AD**.

   ![Dominio de Azure AD adicional](media/active-directory-aadconnect-federation-management/AdditionalDomain1.PNG)

2. En hello siguiente página del Asistente de hello, proporcione las credenciales de administrador global de Hola para Azure AD.

   ![Conectar tooAzure AD](media/active-directory-aadconnect-federation-management/AdditionalDomain2.PNG)

3. En hello **las credenciales de acceso remoto** , proporcione credenciales de administrador de dominio de Hola.

   ![Credenciales de acceso remoto](media/active-directory-aadconnect-federation-management/additionaldomain3.PNG)

4. En la página siguiente de hello, Asistente Hola proporciona una lista de dominios de Azure AD que se pueden federar su directorio local con. Elija el dominio de hello en lista de Hola.

   ![Dominio de Azure AD](media/active-directory-aadconnect-federation-management/AdditionalDomain4.PNG)

    Después de elegir el dominio de hello, Asistente Hola proporciona información adecuada sobre otras acciones que Hola asistente tomará y Hola impacto de la configuración de Hola. En algunos casos, si selecciona un dominio que aún no está comprobado en Azure AD, Hola le proporciona información toohelp comprobar dominio Hola. Vea [agregar su tooAzure de nombre de dominio personalizado Active Directory](../active-directory-add-domain.md) para obtener más detalles.

5. Haga clic en **Siguiente**. Hola **tooconfigure listo** página muestra la lista de Hola de acciones que llevará a cabo Azure AD Connect. Haga clic en **instalar** configuración de toofinish Hola.

   ![Tooconfigure listo](media/active-directory-aadconnect-federation-management/AdditionalDomain5.PNG)

> [!NOTE]
> Agregar usuarios de hello debe estar sincronizada dominio federado para que puedan estar tooAzure toologin capaz de AD.

## <a name="ad-fs-customization"></a>Personalización de AD FS
Hello las secciones siguientes se proporcionan detalles sobre algunas de las tareas comunes de Hola que es posible que tenga tooperform si desea personalizar la página de inicio de sesión de AD FS.

## Adición de un logotipo de la compañía personalizado o una ilustración <a name=customlogo></a>
logotipo de hello toochange de empresa de Hola que se muestra en hello **inicio de sesión** , utilice el siguiente cmdlet de Windows PowerShell y la sintaxis de Hola.

> [!NOTE]
> Hola recomendada dimensiones para el logotipo de hello son 260 × 35 a 96 PPP con un tamaño de archivo no superior a 10 KB.

    Set-AdfsWebTheme -TargetName default -Logo @{path="c:\Contoso\logo.PNG"}

> [!NOTE]
> Hola *TargetName* parámetro es obligatorio. tema predeterminado de Hola que se lanzó con AD FS se denomina de forma predeterminada.

## Adición de la descripción de inicio de sesión <a name=addsignindescription></a>
tooadd un toohello de descripción de la página de inicio de sesión **página de inicio de sesión**, usar hello siguiente cmdlet de Windows PowerShell y la sintaxis.

    Set-AdfsGlobalWebContent -SignInPageDescriptionText "<p>Sign-in tooContoso requires device registration. Click <A href='http://fs1.contoso.com/deviceregistration/'>here</A> for more information.</p>"

## Modificación de las reglas de notificaciones de AD FS <a name=modclaims></a>
AD FS es compatible con un lenguaje de notificación enriquecida que puede usar las reglas de notificación toocreate personalizado. Para obtener más información, consulte [Hola rol de lenguaje de reglas de notificación de hello](https://technet.microsoft.com/library/dd807118.aspx).

Hello secciones siguientes describen cómo se pueden escribir reglas personalizadas para algunos escenarios que relacionan tooAzure AD y federación de AD FS.

### <a name="immutable-id-conditional-on-a-value-being-present-in-hello-attribute"></a>Id. inmutable condicional en un valor que esté presente en el atributo de Hola
Azure AD Connect le permite especificar un toobe de atributo que se utiliza como un delimitador de origen cuando los objetos están sincronizados tooAzure AD. Si el valor de hello en el atributo personalizado de hello no está vacío, conviene tooissue una notificación de identificador inmutable.

Por ejemplo, puede seleccionar **ms-ds-consistencyguid** como atributo de hello para el delimitador de origen de Hola y emitir **ImmutableID** como **ms-ds-consistencyguid** en mayúscula Hola el atributo tiene un valor en él. Si no hay ningún valor en el atributo de hello, emitir **objectGuid** como Hola inmutable identificador. Puede crear conjunto de Hola de reglas de notificación personalizada tal y como se describe en los pasos de la sección de Hola.

**Regla 1: Consultar atributos**

    c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname"]
    => add(store = "Active Directory", types = ("http://contoso.com/ws/2016/02/identity/claims/objectguid", "http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid"), query = "; objectGuid,ms-ds-consistencyguid;{0}", param = c.Value);

En esta regla, que está consultando los valores de hello de **ms-ds-consistencyguid** y **objectGuid** para el usuario de Hola desde Active Directory. Cambiar nombre hello almacén nombre tooan almacén adecuado en la implementación de AD FS. Cambiar tipo hello notificaciones tipo tooa notificaciones adecuadas para la federación, tal como se define para **objectGuid** y **ms-ds-consistencyguid**.

Además, mediante el uso de **agregar** y no **problema**, evitar la adición de un problema saliente para la entidad de Hola y pueden usar valores de hello como valores intermedios. Se van a emitir notificaciones de hello en una regla más adelante después de establecer qué toouse valor como identificador inmutable de Hola

**Regla 2: Comprobar si ms-ds-consistencyguid existe para el usuario de Hola**

    NOT EXISTS([Type == "http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid"])
    => add(Type = "urn:anandmsft:tmp/idflag", Value = "useguid");

Esta regla define una marca temporal denominada **idflag** que se establece demasiado**useguid** si no hay ningún **ms-ds-consistencyguid** rellena para usuario Hola. lógica de Hello detrás de esto es hechos Hola que AD FS no permitir notificaciones vacías. Por lo que al agregar notificaciones http://contoso.com/ws/2016/02/identity/claims/objectguid y http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid en la regla 1, terminará con un **msdsconsistencyguid** notificación solo si valor de Hola se rellena para usuario Hola. Si no se rellena, AD FS ve que tiene un valor vacío y lo coloca inmediatamente. Todos los objetos tendrán el atributo **objectGuid**, así que esa notificación seguirá estando después de que se ejecute la regla 1.

**Regla 3: Emitir el atributo ms-ds-consistencyguid como identificador inmutable si está presente**

    c:[Type == "http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid"]
    => issue(Type = "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier", Value = c.Value);

Se trata de una comprobación **Exist** implícita. Si existe el valor de Hola de notificación de Hola, a continuación, emita que como Hola inmutable identificador. Hola anterior en el ejemplo se usa hello **nameidentifier** de notificación. Tendrá toochange este tipo de notificación adecuadas toohello de identificador inmutable de hello en su entorno.

**Regla 4: Emitir el atributo objectGUID como identificador inmutable si ms-ds-consistencyguid no está presente**

    c1:[Type == "urn:anandmsft:tmp/idflag", Value =~ "useguid"]
    && c2:[Type == "http://contoso.com/ws/2016/02/identity/claims/objectguid"]
    => issue(Type = "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier", Value = c2.Value);

En esta regla, simplemente está comprobando marca temporal hello **idflag**. Decide si tooissue Hola notificación basada en su valor.

> [!NOTE]
> secuencia de Hola de estas reglas es importante.

### <a name="sso-with-a-subdomain-upn"></a>SSO con un UPN de subdominio
Puede agregar más de un toobe de dominio federado mediante el uso de Azure AD Connect, tal y como se describe en [agregar un nuevo dominio federado](active-directory-aadconnect-federation-management.md#addfeddomain). Deberá modificar notificación de nombre principal (UPN) del usuario de Hola para que hello Id. del emisor corresponde toohello dominio de raíz y no el subdominio de hello, porque dominio federado raíz de hello también cubre a secundarios Hola.

De forma predeterminada, Hola de reglas de notificaciones para emisor Id. se establece como:

    c:[Type
    == “http://schemas.xmlsoap.org/claims/UPN“]

    => issue(Type = “http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid“, Value = regexreplace(c.Value, “.+@(?<domain>.+)“, “http://${domain}/adfs/services/trust/“));

![Notificación del identificador de emisor predeterminado](media/active-directory-aadconnect-federation-management/issuer_id_default.png)

regla predeterminada de Hello simplemente toma el sufijo UPN de Hola y utiliza en la notificación de Id. de emisor de Hola. Por ejemplo, John es un usuario de sub.contoso.com y contoso.com está federado con Azure AD. Entra en John john@sub.contoso.com como Hola nombre de usuario al iniciar sesión en tooAzure AD. regla de notificación de Id. de emisor de Hola de forma predeterminada en AD FS lo tratará de hello siguiente manera:

    c:[Type
    == “http://schemas.xmlsoap.org/claims/UPN“]

    => issue(Type = “http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid“, Value = regexreplace(john@sub.contoso.com, “.+@(?<domain>.+)“, “http://${domain}/adfs/services/trust/“));

**Valor de notificación:** http://sub.contoso.com/adfs/services/trust/

toohave solo dominio de raíz de hello en emisor Hola valor de notificación, cambiar Hola notificación regla toomatch Hola siguiente:

    c:[Type == “http://schemas.xmlsoap.org/claims/UPN“]

    => issue(Type = “http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid“, Value = regexreplace(c.Value, “^((.*)([.|@]))?(?<domain>[^.]*[.].*)$”, “http://${domain}/adfs/services/trust/“));

## <a name="next-steps"></a>Pasos siguientes
Obtenga más información sobre las [opciones de inicio de sesión del usuario](active-directory-aadconnect-user-signin.md).
