---
title: "Adquisición por parte del administrador de un directorio no autorizado o un inquilino paralelo en Azure Active Directory | Microsoft Docs"
description: "Adquisición de un nombre de dominio DNS en un directorio no administrado (inquilino paralelo) en Azure Active Directory."
services: active-directory
documentationcenter: 
author: curtand
manager: mtillman
editor: 
ms.assetid: b9f01876-29d1-4ab8-8b74-04d43d532f4b
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 11/14/2017
ms.author: curtand
ms.reviewer: elkuzmen
ms.custom: it-pro
ms.openlocfilehash: f18e5883fca9291eb1447c1eebfe0883936fe84f
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/11/2017
---
# <a name="take-over-an-unmanaged-directory-as-administrator-in-azure-active-directory"></a>Adquisición de un directorio no administrado como administrador en Azure Active Directory
En este artículo se describen dos maneras de adquirir un nombre de dominio DNS en un directorio no administrado en Azure Active Directory (Azure AD). Cuando un usuario de autoservicio se regista en un servicio en la nube que usa Azure AD, se agrega a un directorio de Azure AD no administrado en función del dominio de su correo electrónico. Para más información sobre el registro de autoservicio o "viral" en un servicio, consulte [¿Qué es el registro de autoservicio de Azure Active Directory?]()

## <a name="decide-how-you-want-to-take-over-an-unmanaged-directory"></a>Decida cómo desea adquirir un directorio no administrado
Durante el proceso de adquisición de un administrador, puede comprobar la propiedad tal como se describe en [Incorporación de un nombre de dominio personalizado a Azure Active Directory](add-custom-domain.md). En las secciones siguientes se explica con más detalle la experiencia del administrador, pero a continuación se incluye un resumen:

* Cuando realiza una [adquisición de administración "interna"](#internal-admin-takeover)de un directorio de Azure no administrado, se le agrega como el administrador global del directorio no administrado. Ningún usuario, dominio ni plan de servicio se migra a ningún otro directorio que administra.

* Cuando realiza una [adquisición de administración "externa"](#external-admin-takeover) de un directorio de Azure no administrado, agrega el nombre de dominio de DNS del directorio no administrado a su directorio de Azure administrado. Cuando agrega el nombre de dominio, se crea una asignación de usuarios a recursos en el directorio de Azure administrado para que los usuarios puedan seguir teniendo acceso a los servicios sin interrupción. 

## <a name="internal-admin-takeover"></a>Adquisición de administración interna

Algunos productos que incluyen SharePoint y OneDrive, como Office 365, no admiten la adquisición externa. Si su escenario es ese o si es administrador y desea adquirir un inquilino no administrado o "paralelo" al que hayan creado usuarios que usaron el registro de autoservicio, puede hacerlo con una adquisición de administración interna.

1. Cree un contexto de usuario en el inquilino no administrado mediante el registro con, por ejemplo, Power BI. Para facilitar el ejemplo, en estos pasos se presupone que esa es la ruta.

2. Abra el [sitio de Power BI](https://powerbi.com) y seleccione **Empiece gratis**. Escriba una cuenta de usuario en la que se use el nombre de dominio de la organización, por ejemplo, `admin@fourthcoffee.xyz`. Escriba el código de verificación y, luego, revise su correo electrónico para recibir el código de confirmación.

3. En el correo electrónico de confirmación de Power BI, seleccione la opción que indica que **es el destinatario del mensaje**.

4. Inicie sesión en el [centro de administración de Office 365](https://portal.office.com/adminportal/Home) con la cuenta de usuario de Power BI. Recibe un mensaje que le indica que debe **convertirse en el administrador** del nombre de dominio que ya se comprobó en el inquilino no administrado. Seleccione la opción que indica que **desea convertirse en el administrador**.
  
  ![primera captura de pantalla para convertirse en el administrador](./media/domains-admin-takeover/become-admin-first.png)
  
5. Agregue el registro TXT para comprobar que el nombre de dominio **fourthcoffee.xyz** en el registrador de nombres de dominio es de su propiedad. En este ejemplo, es GoDaddy.com.
  
  ![Agregar un registro TXT para el nombre de dominio](./media/domains-admin-takeover/become-admin-txt-record.png)

Una vez que los registros TXT de DNS se comprueban en el registrador de nombres de dominio, puede administrar el inquilino de Azure AD.

Después de completar los pasos anteriores, ya es el administrador global del inquilino Fourth Coffee en Office 365. Para integrar el nombre de dominio con los otros servicios de Azure, puede quitarlo de Office 365 y agregarlo a un inquilino administrado distinto en Azure.

### <a name="adding-the-domain-name-to-a-managed-tenant-in-azure-ad"></a>Incorporación del nombre de dominio a un inquilino administrado en Azure AD 

1. Abra el [Centro de administración de Office 365](https://portal.office.com/adminportal/Home).
2. Seleccione la pestaña **Usuarios** y cree una cuenta de usuario con un nombre como *user@fourthcoffeexyz.onmicrosoft.com* que no usa el nombre de dominio personalizado. 
3. Asegúrese de que la cuenta de usuario nueva tiene privilegios administrativos globales en el inquilino de Azure AD.
4. Abra la pestaña **Dominios** del Centro de administración de Office 365 y seleccione **Quitar**. 
  
  ![quitar el nombre de dominio de Office 365](./media/domains-admin-takeover/remove-domain-from-o365.png)
  
5. Si tiene usuarios o grupos en Office 365 que haga referencia al nombre de dominio que se quitó, se les debe cambiar el nombre al dominio .onmicrosoft.com. Si se fuerza la eliminación del nombre de dominio, se cambia automáticamente el nombre de todos los usuarios, como en este ejemplo a *user@fourthcoffeexyz.onmicrosoft.com*.
  
6. Inicie sesión en el [Centro de administración de Azure AD](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview) con una cuenta que sea la del administrador global del inquilino de Azure AD.
  
7. Seleccione **Nombres de dominio personalizados** y, luego, agregue el nombre de dominio. Deberá especificar los registros TXT de DNS para comprobar la propiedad del nombre de dominio. 
  
  ![el dominio se agregó a Azure AD](./media/domains-admin-takeover/add-domain-to-azure-ad.png)
  
> [!NOTE]
> Cualquier usuario de Power BI o del servicio Azure Rights Management que tenga licencias asignadas en el inquilino de Office 365 debe guardar los paneles si se quita el nombre de dominio. Debe iniciar sesión con un nombre de usuario *user@fourthcoffeexyz.onmicrosoft.com* en lugar de *user@fourthcoffee.xyz*.

## <a name="external-admin-takeover"></a>Adquisición de administración externa

Si ya administra un inquilino con los servicios de Azure u Office 365, no puede agregar un nombre de dominio personalizado si ya se comprobó en otro inquilino de Azure AD. Sin embargo, desde el inquilino administrado en Azure AD puede adquirir un inquilino no administrado como una adquisición de administración externa. El procedimiento general sigue lo que se indica en el artículo [Incorporación de un dominio personalizado a Azure AD](add-custom-domain.md).

Cuando se comprueba la propiedad del nombre de dominio, Azure AD quita el nombre de dominio del inquilino no administrado y lo mueve al inquilino existente. La adquisición de administración externa de un directorio no administrado requiere el mismo proceso de validación de TXT de DNS que la adquisición de administración interna. La diferencia es que los siguientes elementos también se mueven con el nombre de dominio:

- Usuarios
- Suscripciones
- Asignaciones de licencia
 
La opción [**ForceTakeover** ](#azure-ad-powershell-cmdlets-for-the-forcetakeover-option) para la adquisición de administración externa del nombre de dominio solo es compatible con dos servicios: Power BI y Azure RMS.

### <a name="support-for-external-admin-takeover"></a>Compatibilidad con la adquisición de administración externa
La adquisición de administración externa es compatible con los servicios en línea siguientes:

- Power BI
- Azure Rights Management Service (RMS)
- Exchange Online

Los planes de servicio compatibles incluyen:

- Power BI Free
- Power BI Pro
- PowerApps Free
- PowerFlow Free
- Azure Rights Management Service Basic (RMS)
- Azure Rights Management Service Enterprise (RMS)
- Microsoft Stream
- Evaluación gratuita de Dynamics 365

La adquisición de administración externa no es compatible con ningún servicio con planes de servicio que incluyan SharePoint, OneDrive o Skype Empresarial, por ejemplo, con una suscripción gratuita de Office o la SKU de Office Basic.

### <a name="azure-ad-powershell-cmdlets-for-the-forcetakeover-option"></a>Cmdlets de Azure AD PowerShell para la opción ForceTakeover
Puede ver estos cmdlets en uso en el [ejemplo de PowerShell](#powershell-example).


cmdlet | Uso 
------- | -------
`connect-msolservice` | Cuando se le solicite, inicie sesión en el inquilino administrado.
`get-msoldomain` | Muestra los nombres de dominio asociados con el inquilino actual.
`new-msoldomain –name <domainname>` | Agrega el nombre de dominio al inquilino como No comprobado (todavía no se realiza ninguna comprobación DNS).
`get-msoldomain` | El nombre de dominio ahora se incluye en la lista de los nombres de dominio asociada con el inquilino administrado, pero aparece como **No comprobado**.
`get-msoldomainverificationdns –Domainname <domainname> –Mode DnsTxtRecord` | Proporciona la información que se va a ingresar en el registro TXT de DNS para el dominio (MS=xxxxx). Es posible que la comprobación no suceda de inmediato porque el registro TXT tarda un tiempo en propagarse. Por lo tanto, debe esperar unos minutos antes de considerar la opción **-ForceTakeover**. 
`confirm-msoldomain –Domainname <domainname> –ForceTakeover Force` | <li>Si todavía no es posible comprobar el nombre de dominio, puede continuar con la opción **-ForceTakeover**. Comprueba que se creó el registro TXT e inicia el proceso de adquisición.<li>La opción **-ForceTakeover** se debe agregar al cmdlet solo cuando se fuerza una adquisición de administración externa, por ejemplo cuando el inquilino no administrado tiene servicios de Office 365 que bloquean la adquisición.
`get-msoldomain` | La lista de dominios ahora muestra el nombre de dominio como **Comprobado**.

### <a name="powershell-example"></a>Ejemplo de PowerShell

1. Conéctese a Azure AD con las credenciales que se usaron para responder a la oferta de autoservicio:
  ````
    import-module MSOnline
    $msolcred = get-credential
    
    connect-msolservice -credential $msolcred
  ````
2. Obtenga una lista de dominios:
  
  ````
    Get-MsolDomain
  ````
3. Ejecute el cmdlet Get-MsolDomainVerificationDns para crear un desafío:
  ````
    Get-MsolDomainVerificationDns –DomainName *your_domain_name* –Mode DnsTxtRecord
  
    For example:
  
    Get-MsolDomainVerificationDns –DomainName contoso.com –Mode DnsTxtRecord
  ````

4. Copie el valor (el desafío) que se devuelve desde este comando. Por ejemplo:
  ````
    MS=32DD01B82C05D27151EA9AE93C5890787F0E65D9
  ````
5. En el espacio de nombres DNS público, cree un registro txt de DNS que contenga el valor que copió en el paso anterior. El nombre de este registro es el nombre del dominio principal, por lo que si crea este registro de recursos con el rol DNS desde Windows Server, deje el nombre del registro en blanco y pegue el valor en el cuadro de texto.
6. Ejecute el cmdlet Confirm-MsolDomain para comprobar el desafío:
  
  ````
    Confirm-MsolEmailVerifiedDomain -DomainName *your_domain_name*
  ````
  
  Por ejemplo:
  
  ````
    Confirm-MsolEmailVerifiedDomain -DomainName contoso.com
  ````

Un desafío correcto le devuelve el mensaje sin errores.

## <a name="next-steps"></a>Pasos siguientes
* [Incorporación de su nombre de dominio personalizado a Azure Active Directory](add-custom-domain.md)
* [Cómo instalar y configurar Azure PowerShell](/powershell/azure/overview)
* [Azure PowerShell](/powershell/azure/overview)
* [Referencia de cmdlets de Azure](/powershell/azure/get-started-azureps)
* [Set-MsolCompanySettings](/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0)

<!--Image references-->
[1]: ./media/active-directory-self-service-signup/SelfServiceSignUpControls.png
