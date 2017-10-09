---
title: "el almacén de claves de aaaAccess detrás de un firewall | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooaccess almacén de claves de Azure desde una aplicación detrás de un firewall"
services: key-vault
documentationcenter: 
author: amitbapat
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 50d21774-2ee1-4212-8995-570c9de603c5
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 01/07/2017
ms.author: ambapat
ms.openlocfilehash: ab4bb0c27a41fef878a20dace6cab203df04e579
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="access-azure-key-vault-behind-a-firewall"></a>Acceso a Azure Key Vault desde detrás de un firewall
### <a name="q-my-key-vault-client-application-needs-toobe-behind-a-firewall-what-ports-hosts-or-ip-addresses-should-i-open-tooenable-access-tooa-key-vault"></a>P: ¿mi aplicación de cliente de almacén de claves necesita toobe detrás de un firewall. ¿Qué puertos, hosts o direcciones IP debo abrir el almacén de claves tooa tooenable acceso?
tooaccess un almacén de claves, la aplicación de cliente de almacén de claves tiene tooaccess varios puntos de conexión para diversas funcionalidades:

* Autenticación a través de Azure Active Directory (Azure AD).
* Administración de Azure Key Vault. Aquí se incluye la creación, lectura, actualización, eliminación y establecimiento de directivas de acceso a través de Azure Resource Manager.
* Obtener acceso y administrar objetos almacenados en el almacén de claves propio (claves y secretos), pasando por Hola extremo específico del almacén de claves (por ejemplo, [https://yourvaultname.vault.azure.net](https://yourvaultname.vault.azure.net)).  

En función de su configuración y entorno, hay algunas variaciones.   

## <a name="ports"></a>Puertos
Todos los almacén de claves de tooa tráfico para las tres funciones (acceso de autenticación, la administración y datos plano) pasa a través de HTTPS: el puerto 443. Sin embargo, ocasionalmente habrá tráfico HTTP (puerto 80) para CRL. Los clientes que admiten OCSP no deberían poder acceder a CRL, pero a veces pueden hacerlo a [http://cdp1.public-trust.com/CRL/Omniroot2025.crl](http://cdp1.public-trust.com/CRL/Omniroot2025.crl).  

## <a name="authentication"></a>Autenticación
Las aplicaciones de cliente de almacén de claves deberá tooaccess extremos de Azure Active Directory para la autenticación. punto de conexión de Hello utilizado depende de Hola configuración del inquilino de Azure AD, tipo hello de hello y entidad (entidad de seguridad de usuario o entidad de servicio) tipo de cuenta: por ejemplo, una cuenta de Microsoft o un trabajo o escuela cuenta.  

| Tipo de entidad de seguridad | Punto de conexión:puerto |
| --- | --- |
| Usuario que utiliza cuenta Microsoft<br> (por ejemplo, user@hotmail.com) |**Global:**<br> login.microsoftonline.com:443<br><br> **Azure China:**<br> login.chinacloudapi.cn:443<br><br>**Azure Gobierno de EE. UU.:**<br> login-us.microsoftonline.com:443<br><br>**Azure Alemania:**<br> login.microsoftonline.de:443<br><br> y <br>login.live.com:443 |
| Usuario o entidad de servicio con una cuenta profesional o educativa con Azure AD (por ejemplo, user@contoso.com) |**Global:**<br> login.microsoftonline.com:443<br><br> **Azure China:**<br> login.chinacloudapi.cn:443<br><br>**Azure Gobierno de EE. UU.:**<br> login-us.microsoftonline.com:443<br><br>**Azure Alemania:**<br> login.microsoftonline.de:443 |
| Usuario o entidad de servicio con un trabajo o cuenta del centro educativo, además de los servicios de federación de Active Directory (AD FS) u otro punto de conexión federado (por ejemplo, user@contoso.com) |Todos los puntos de conexión de una cuenta profesional o educativa, más AD FS u otros puntos de conexión federados |

Hay otros escenarios complejos posibles. Consulte demasiado[flujo autenticación de Azure Active Directory](/documentation/articles/active-directory-authentication-scenarios/), [integración de aplicaciones con Azure Active Directory](/documentation/articles/active-directory-integrating-applications/), y [protocolos de autenticación de Active Directory](https://msdn.microsoft.com/library/azure/dn151124.aspx) Para obtener información adicional.  

## <a name="key-vault-management"></a>Administración de Key Vault
Para la administración de almacén de claves (CRUD y establecer la directiva de acceso), la aplicación de cliente de almacén de claves de hello necesita tooaccess un punto de conexión de administrador de recursos de Azure.  

| Tipo de operación | Punto de conexión:puerto |
| --- | --- |
| Operaciones del plano de control de Key Vault<br> a través de Azure Resource Manager |**Global:**<br> management.azure.com:443<br><br> **Azure China:**<br> management.chinacloudapi.cn:443<br><br> **Azure Gobierno de EE. UU.:**<br> management.usgovcloudapi.net:443<br><br> **Azure Alemania:**<br> management.microsoftazure.de:443 |
| API Graph de Azure Active Directory |**Global:**<br> graph.windows.net:443<br><br> **Azure China:**<br> graph.chinacloudapi.cn:443<br><br> **Azure Gobierno de EE. UU.:**<br> graph.windows.net:443<br><br> **Azure Alemania:**<br> graph.cloudapi.de:443 |

## <a name="key-vault-operations"></a>Operaciones de Key Vault
Para toda la administración de objetos (claves y secretos) del almacén de claves y operaciones criptográficas, cliente de almacén de claves de hello debe punto de conexión de almacén de claves de tooaccess Hola. sufijo DNS del punto de conexión de Hello varía según la ubicación Hola de su almacén de claves. punto de conexión de almacén de claves de Hello tiene formato de hello *nombre del almacén de*. *región--sufijo dns específico de-*, tal y como se describe en hello en la tabla siguiente.  

| Tipo de operación | Punto de conexión:puerto |
| --- | --- |
| Operaciones que incluyen operaciones criptográficas en claves; crear, leer, actualizar y eliminar claves y secretos; establecer u obtener etiquetas y otros atributos de objetos de Key Vault (claves o secretos) |**Global:**<br> &lt;vault-name&gt;.vault.azure.net:443<br><br> **Azure China:**<br> &lt;vault-name&gt;.vault.azure.cn:443<br><br> **Azure Gobierno de EE. UU.:**<br> &lt;vault-name&gt;.vault.usgovcloudapi.net:443<br><br> **Azure Alemania:**<br> &lt;vault-name&gt;.vault.microsoftazure.de:443 |

## <a name="ip-address-ranges"></a>Intervalos de direcciones IP
servicio de almacén de claves de Hola utiliza otros recursos de Azure como infraestructura de PaaS. Por lo que no es posible tooprovide un específico intervalo de direcciones IP que el almacén de claves tendrán los extremos de servicio en un momento dado. Si el firewall admite sólo los intervalos de direcciones IP, consulte toohello [intervalos de IP de centro de datos de Microsoft Azure](https://www.microsoft.com/download/details.aspx?id=41653) documento. Para la autenticación y la identidad (Azure Active Directory), la aplicación debe ser capaz de tooconnect toohello extremos se describe en [direcciones de autenticación e identidad](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2).

## <a name="next-steps"></a>Pasos siguientes
Si tiene alguna pregunta sobre el almacén de claves, visite hello [foros de almacén de claves de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=AzureKeyVault).

