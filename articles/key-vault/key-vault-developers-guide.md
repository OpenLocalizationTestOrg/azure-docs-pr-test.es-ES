---
title: "Guía del desarrollador de almacén de aaaAzure clave"
description: "Los desarrolladores pueden utilizar claves criptográficas de almacén de claves de Azure toomanage dentro del entorno de Microsoft Azure Hola."
services: key-vault
author: BrucePerlerMS
manager: mbaldwin
ms.service: key-vault
ms.topic: article
ms.workload: identity
ms.date: 08/04/2017
ms.author: bruceper
ms.openlocfilehash: 631cea1315964cd0b97e8b2cf3311754230fb801
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-developers-guide"></a>Guía del desarrollador de Azure Key Vault

El almacén de claves permite toosecurely acceso a información confidencial de sus aplicaciones:

- Claves y secretos están protegidos sin necesidad de código de hello toowrite usted mismo y es capaz de fácilmente toouse ellas desde sus aplicaciones.
- Son toohave capaz de sus propios clientes y administrar sus propias claves para que pueda centrarse en proporcionar características de software de hello principales. De esta manera, las aplicaciones será el propietario no responsabilidad de Hola o responsabilidad posible para las claves de inquilino de sus clientes y secretos.
- La aplicación puede usar claves de firma y cifrado aún mantiene la administración de claves de hello externo desde su aplicación, lo que permite su toobe de solución es adecuado para una aplicación distribuida geográficamente.
- A partir de la versión de septiembre de 2016 de Hola de almacén de claves, las aplicaciones ahora pueden usar el almacén de claves [certificados](https://docs.microsoft.com/rest/api/keyvault/certificate-operations). Para más información, consulte el artículo [About keys, secrets, and certificates](https://docs.microsoft.com/rest/api/keyvault/about-keys--secrets-and-certificates) (Claves, secretos y certificados).

Para obtener más información sobre Azure Key Vault, consulte [¿Qué es Key Vault?](key-vault-whatis.md)

## <a name="public-previews"></a>Versiones preliminares públicas

Periódicamente se publica una versión preliminar pública de una nueva característica de Key Vault. Pruébelas y díganos su opinión a través de azurekeyvault@microsoft.com, la dirección de correo electrónico de comentarios.

### <a name="storage-account-keys---july-10-2017"></a>Claves de cuenta de almacenamiento: 10 de julio de 2017

>[!NOTE]
>Para esta actualización de hello de almacén de claves de Azure solo **claves de la cuenta de almacenamiento** característica se encuentra en vista previa.

Esta versión preliminar incluye nuestra nueva característica Claves de cuenta de almacenamiento, disponible a través de estas interfaces; [.NET/C#](https://docs.microsoft.com/dotnet/api/microsoft.azure.keyvault/), [REST](https://docs.microsoft.com/rest/api/keyvault/) y [PowerShell](https://docs.microsoft.com/powershell/module/azurerm.keyvault/). 

Para obtener más información sobre la nueva característica de claves de la cuenta de almacenamiento hello, consulte [introducción de las claves de cuenta de almacenamiento de almacén de claves de Azure](key-vault-ovw-storage-keys.md).

## <a name="videos"></a>Vídeos

Este vídeo muestra cómo toocreate su propia clave de seguridad del almacén y cómo toouse desde la aplicación de ejemplo 'Hello el almacén de claves' hello.

- [Desarrollador de Key Vault: guía de inicio rápido](https://channel9.msdn.com/Blogs/Azure/Azure-Key-Vault-Developer-Quick-Start/player)

Recursos mencionados en el vídeo anterior:

- [Azure PowerShell](http://go.microsoft.com/fwlink/p/?linkid=320376&clcid=0x409)
- [Código de ejemplo de Azure Key Vault](http://go.microsoft.com/fwlink/?LinkId=521527&clcid=0x409)

## <a name="creating-and-managing-key-vaults"></a>Creación y administración de almacenes de claves

Antes de trabajar con el almacén de claves de Azure en el código, puede crear y administrar almacenes de credenciales a través de REST, plantillas de administrador de recursos, PowerShell o CLI, como se describe en hello siguientes artículos:

- [Crear y administrar almacenes de claves con CLI](https://docs.microsoft.com/rest/api/keyvault/)
- [Crear y administrar almacenes claves con PowerShell](key-vault-get-started.md)
- [Crear y administrar almacenes claves con CLI](key-vault-manage-with-cli2.md)
- [Creación de un almacén de claves e incorporación de un secreto mediante una plantilla de Azure Resource Manager](../azure-resource-manager/resource-manager-template-keyvault.md)

> [!NOTE]
> Las operaciones en los almacenes de claves se autentican mediante AAD y se autorizan mediante la propia directiva de acceso de Key Vault, definida para cada almacén.

## <a name="coding-with-key-vault"></a>Codificación con Key Vault

Hola sistema de administración de almacén de claves para los programadores consta de varias interfaces, con el resto como foundation Hola. A través de la interfaz REST de hello, todos los recursos de almacenes de clave son accesibles. claves, secretos y certificados. [Referencia de la API de REST de Key Vault](https://docs.microsoft.com/rest/api/keyvault/). 

### <a name="supported-programming-languages"></a>Lenguajes de programación admitidos

#### <a name="net"></a>.NET

- [Referencia de API de .NET para Key Vault](https://docs.microsoft.com/dotnet/api/microsoft.azure.keyvault) 

Para obtener más información sobre la versión 2.x de Hola de hello .NET SDK, vea hello [notas de la versión](key-vault-dotnet2api-release-notes.md).

#### <a name="java"></a>Java

- [SDK de Java para Key Vault](https://docs.microsoft.com/java/api/com.microsoft.azure.keyvault)

#### <a name="nodejs"></a>Node.js

En Node.js, API de administración de almacén de Hola y API de objeto de almacén de hello son independientes. Administración de Key Vault permite crear y actualizar el almacén de claves. La API de operaciones de Key Vault es para trabajar con objetos del almacén como: claves, secretos y certificados. 

- [Referencia de API de Node.js para administración de Key Vault](http://azure.github.io/azure-sdk-for-node/azure-arm-keyvault/latest/)
- [Referencia de API de Node.js para operaciones de Key Vault](http://azure.github.io/azure-sdk-for-node/azure-keyvault/latest/) 

### <a name="quick-start"></a>Inicio rápido

- [Create Key Vault](https://github.com/Azure/azure-quickstart-templates/tree/master/101-key-vault-create)
- [Introducción a Key Vault en Node.js](https://azure.microsoft.com/en-us/resources/samples/key-vault-node-getting-started/)

### <a name="code-examples"></a>Ejemplos de código

Para obtener ejemplos completos de cómo usar Key Vault con las aplicaciones, vea:

- [Ejemplos de código de Azure Key Vault](http://www.microsoft.com/download/details.aspx?id=45343) - Aplicación .NET de ejemplo *HelloKeyVault* y un ejemplo de servicio web de Azure. 
- [Usar el almacén de claves de Azure desde una aplicación Web](key-vault-use-from-web-application.md) -toohelp tutorial aprenderá cómo toouse almacén de claves de Azure desde una aplicación web en Azure. 

## <a name="how-tos"></a>Procedimientos

Hello escenarios y los artículos siguientes proporcionan orientación específica de la tarea para trabajar con el almacén de claves de Azure:

- [Id. de inquilino del almacén de claves de cambio después de la suscripción mover](key-vault-subscription-move-fix.md) : si se mueve la suscripción de Azure de inquilino un tootenant B, los almacenes de claves existentes son inaccesibles hello las entidades de seguridad (usuarios y aplicaciones) en el inquilino corrección B. este uso de esta guía.
- [Obtener acceso a almacén de claves detrás de firewall](key-vault-access-behind-firewall.md) -tooaccess una clave del almacén de su almacén de claves cliente aplicación necesidades toobe tooaccess capaz de varios extremos para diversas funcionalidades.
- [Cómo tooGenerate Transfer HSM-Protected claves para el almacén de claves de Azure y](key-vault-hsm-protected-keys.md) -Esto le ayudará a planear, generar y, a continuación, transferir su propios toouse claves protegidas con HSM al almacén de claves de Azure.
- [¿Cómo toopass proteger valores (como contraseñas) durante la implementación](../azure-resource-manager/resource-manager-keyvault-parameter.md) : cuando se necesita toopass un valor seguro (por ejemplo, una contraseña) como un parámetro durante la implementación, puede almacenar ese valor como un secreto en un valor de Hola de almacén de claves de Azure y referencia en otras Plantillas de administrador de recursos.
- [Cómo toouse el almacén de claves para la administración extensible de claves con SQL Server](https://msdn.microsoft.com/library/dn198405.aspx) -Hola conector de SQL Server para el almacén de claves de Azure permite a SQL Server y SQL en VM tooleverage hello Azure servicio Almacén de claves como proveedor de administración Extensible de claves (EKM) claves de su cifrado de tooprotect de vínculo de las aplicaciones; Cifrado de datos transparente, cifrado de copia de seguridad y cifrado de nivel de columna.
- [Cómo toodeploy tooVMs de certificados desde el almacén de claves](https://blogs.technet.microsoft.com/kv/2015/07/14/deploy-certificates-to-vms-from-customer-managed-key-vault/) : una aplicación de nube que se ejecuta en una máquina virtual en Azure necesidades un certificado. Sepa cómo añadirlo a la máquina virtual hoy mismo.
- [Cómo tooset el almacén de claves con tooend final clave rotación y auditoría](key-vault-key-rotation-log-monitoring.md) -este tutorial se muestran cómo tooset la auditoría al almacén de claves de Azure y rotación de claves.
- [Deploying Azure Web App Certificate through Key Vault]( https://blogs.msdn.microsoft.com/appserviceteam/2016/05/24/deploying-azure-web-app-certificate-through-key-vault/) (Implementación de certificado Azure Web App a través de Key Vault) proporciona instrucciones paso a paso para implementar certificados almacenados en Key Vault como parte de la oferta de [App Service Certificate](https://azure.microsoft.com/blog/internals-of-app-service-certificate/).
- [Conceder permiso toomany aplicaciones tooaccess un almacén de claves](key-vault-group-permissions-for-apps.md) directiva de control de acceso de almacén de claves solo admite 16 entradas. Sin embargo, puede crear un grupo de seguridad de Azure Active Directory. Agregue todos los hello asociado el grupo de seguridad de toothis de entidades de seguridad de servicio y, a continuación, concede acceso toothis seguridad grupo tooKey almacén.
- Para obtener más instrucciones específicas sobre las tareas de integración y el uso de los almacenes de claves con Azure, consulte los [ejemplos de plantillas de Azure Resource Manager de Ryan Jones para Key Vault](https://github.com/rjmax/ArmExamples/tree/master/keyvaultexamples).
- [Cómo toouse el almacén de claves soft-delete con CLI](key-vault-soft-delete-cli.md) le guiará por el uso de Hola y ciclo de vida de un almacén de claves y varios objetos de almacén de claves con la eliminación de software habilitada.
- [Cómo toouse el almacén de claves soft-delete con PowerShell](key-vault-soft-delete-powershell.md) le guiará por el uso de Hola y ciclo de vida de un almacén de claves y varios objetos de almacén de claves con la eliminación de software habilitada.

## <a name="integrated-with-key-vault"></a>Integración con Key Vault

En estos artículos se describen otros escenarios y servicios que usan Key Vault o se integran en este servicio.

- [Cifrado del disco Azure](../security/azure-security-disk-encryption.md) aprovecha Hola estándar del sector [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) característica de Windows y Hola [DM Crypt](https://en.wikipedia.org/wiki/Dm-crypt) característica de cifrado de volumen de Linux tooprovide hello sistema operativo y datos de Hola discos. solución de Hola se integra con el almacén de claves de Azure toohelp controlar y administrar claves de cifrado de disco de Hola y secretos en su suscripción de almacén de claves, asegurándose de que todos los datos en discos de máquina virtual de Hola se cifran en reposo en el almacenamiento de Azure.
- [Almacén de Azure Data Lake](../data-lake-store/data-lake-store-get-started-portal.md) proporciona la opción para el cifrado de datos que se almacenan en la cuenta de hello. Administración de claves, el almacén de Data Lake proporciona dos modos para administrar las claves de cifrado maestra (MEKs), que son necesarias para descifrar los datos que se almacenan en el almacén de Data Lake Hola. Se puede permitir que almacén de Data Lake administra hello MEKs por usted, o elija la propiedad tooretain de MEKs Hola con su cuenta de almacén de claves de Azure. Debe especificar el modo de saludo de administración de claves al crear una cuenta de almacén de Data Lake. 
- [Azure Information Protection](/information-protection/plan-design/plan-implement-tenant-key) permite toomanager su propia clave de inquilino. Por ejemplo, en lugar de Microsoft Administre su clave de inquilino (valor predeterminado de hello), puede administrar su propios toocomply clave de inquilino con las normas específicas que se aplican tooyour organización. Administrar su propia clave de inquilino también es tooas lo que se conoce aportar su propia clave, o BYOK.

## <a name="key-vault-overviews-and-concepts"></a>Conceptos y datos globales de Key Vault

- [Comportamiento de eliminación de software de almacén de claves](key-vault-ovw-soft-delete.md) describe una característica que permite la recuperación de objetos eliminados, si la eliminación de hello ha sido accidental o intencionado.
- [Cliente de almacén de claves de limitación](key-vault-ovw-throttling.md) le orienta toohello conceptos básicos de la limitación y ofrece un método para la aplicación.
- [Introducción de las claves de cuenta de almacenamiento de almacén de claves](key-vault-ovw-storage-keys.md) describe claves de cuentas de almacenamiento de Azure de integración de hello el almacén de claves.
- [Espacios de seguridad del almacén de claves](key-vault-ovw-security-worlds.md) describe Hola relaciones entre las regiones y zonas de seguridad.

## <a name="social"></a>Redes sociales

- [Blog de Key Vault](http://aka.ms/kvblog)
- [Foro sobre Key Vault](http://aka.ms/kvforum)

## <a name="supporting-libraries"></a>Bibliotecas compatibles

- [Microsoft Azure Key Vault Core Library](http://www.nuget.org/packages/Microsoft.Azure.KeyVault.Core) (biblioteca principal Microsoft Azure Key Vault) proporciona las interfaces **IKey** e **IKeyResolver** para localizar las claves de los identificadores y realizar operaciones con ellas.
- [Microsoft Azure Key Vault Extensions](http://www.nuget.org/packages/Microsoft.Azure.KeyVault.Extensions) (extensiones de Microsoft Azure Key Vault) proporcionan capacidades ampliadas para Azure Key Vault.


