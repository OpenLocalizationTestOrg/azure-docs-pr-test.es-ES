---
title: "lista de comprobación de seguridad de tejido de servicio de aaaAzure | Documentos de Microsoft"
description: "En este artículo se proporciona un conjunto de comprobaciones de la seguridad de Azure Service Fabric."
services: security
documentationcenter: na
author: unifycloud
manager: swadhwa
editor: tomsh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/04/2017
ms.author: tomsh
ms.openlocfilehash: 10ffaea9e7e4de6d758b0a57a79e269c87bfd14d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-fabric-security-checklist"></a>Lista de comprobación de seguridad de Azure Service Fabric
En este artículo se proporciona una sencilla lista de comprobación que le ayudará a proteger el entorno de Azure Service Fabric.

## <a name="introduction"></a>Introducción
Azure Service Fabric es una plataforma de sistemas distribuidos que resulta fácil toopackage, implementar y administrar microservicios escalables y confiables. Service Fabric también aborda retos significativos de hello en desarrollar y administrar aplicaciones en la nube. Los desarrolladores y administradores pueden evitar problemas complejos de infraestructura y centrarse en su lugar en las cargas de trabajo más exigentes y críticas que son escalables, confiables y fáciles de administrar.

## <a name="checklist"></a>Lista de comprobación
Usar hello después toohelp de lista de comprobación, asegurarse de que aún no se pasa por alto cualquier problema importante en la administración y configuración de una solución de Azure Service Fabric segura.


|Categoría de la lista de comprobación| Descripción |
| ------------ | -------- |
|[Control de acceso basado en roles (RBAC)](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-security-roles) | <ul><li>Control de acceso permite Hola clúster administrador toolimit acceso toocertain las operaciones del clúster para los diferentes grupos de usuarios, mejorar la seguridad de clúster de Hola.</li><li>Los administradores tienen capacidades de toomanagement de acceso completa (incluidas las capacidades de lectura/escritura). </li><li>   Los usuarios, de forma predeterminada, tienen sólo capacidades de toomanagement de acceso de lectura (por ejemplo, capacidades de consulta) y las aplicaciones de tooresolve de capacidad de Hola y servicios.</li></ul>|
|[Certificados X.509 y Service Fabric](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-security) | <ul><li>Los [certificados](https://docs.microsoft.com/en-us/dotnet/framework/wcf/feature-details/working-with-certificates) usados en clústeres que ejecutan cargas de trabajo de producción deben crearse mediante un servicio de certificados de Windows Server configurado correctamente u obtenerse de una [entidad de certificación (CA)](https://en.wikipedia.org/wiki/Certificate_authority) autorizada.</li><li>No use nunca en producción [certificados temporales o de pruebas](https://docs.microsoft.com/en-us/dotnet/framework/wcf/feature-details/how-to-create-temporary-certificates-for-use-during-development) creados con herramientas como [MakeCert.exe](https://msdn.microsoft.com/library/windows/desktop/aa386968.aspx). </li><li>Puede usar un [certificado autofirmado](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-windows-cluster-x509-security), pero solo para los clústeres de prueba y no para los que se encuentran en fase de producción.</li></ul>|
|[Seguridad de clúster](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-security) | <ul><li>escenarios de seguridad de clúster de Hola incluyen seguridad nodo a nodo seguridad en el nodo de cliente, [control de acceso basado en roles (RBAC)](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-security-roles).</li></ul>|
|[Autenticación del clúster](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-creation-via-arm) | <ul><li>Autentica la [comunicación de nodo a nodo](https://github.com/MicrosoftDocs/azure-docs/blob/master/articles/service-fabric/service-fabric-cluster-security.md) para la federación del clúster. </li></ul>|
|[Autenticación de servidor](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-creation-via-arm) | <ul><li>Autentica hello [extremos de administración de clúster](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-creation-via-portal) tooa cliente de administración.</li></ul>|
|[Seguridad de las aplicaciones](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-creation-via-arm)| <ul><li>Cifrado y descifrado de los valores de configuración de aplicación.</li><li> Cifrado de datos entre nodos durante la replicación.</li></ul>|
|[Certificado de clúster](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-windows-cluster-x509-security) | <ul><li>Este certificado es necesario toosecure Hola comunicación entre los nodos de hello en un clúster.</li><li>  Establecer huella digital de hello del certificado principal de hello en la sección de huella digital de Hola y de hello secundaria en variables de ThumbprintSecondary Hola.</li></ul>|
|[ServerCertificate](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-windows-cluster-x509-security)| <ul><li>Este certificado se presenta a toohello cliente cuando intente tooconnect toothis clúster. Puede utilizar dos certificados de servidor diferentes, uno principal y otro secundario para la actualización.</li></ul>|
|ClientCertificateThumbprints| <ul><li>Se trata de un conjunto de certificados que desea tooinstall en los clientes de hello autenticado. </li></ul>|
|ClientCertificateCommonNames| <ul><li>Establecer nombre común Hola Hola primera del certificado de cliente para hello CertificateCommonName. Hola CertificateIssuerThumbprint es huella de hello certificado de emisor de Hola de este certificado. </li></ul>|
|ReverseProxyCertificate| <ul><li>Se trata de un certificado opcional que se puede especificar si desea que toosecure su [un Proxy inverso](https://docs.microsoft.com/en-in/azure/service-fabric/service-fabric-reverseproxy). </li></ul>|
|Key Vault| <ul><li>Usa certificados de toomanage para clústeres de Service Fabric en Azure.  </li></ul>|


## <a name="next-steps"></a>Pasos siguientes
- [Proceso de actualización del clúster de Service Fabric y expectativas del usuario](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-upgrade)
- [Administración de aplicaciones de Service Fabric en Visual Studio](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-manage-application-in-visual-studio).
- [Introducción al modelo de mantenimiento de Service Fabric](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-health-introduction).
