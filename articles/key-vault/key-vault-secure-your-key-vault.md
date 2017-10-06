---
title: "la clave del almacén de aaaSecure | Documentos de Microsoft"
description: "Administrar permisos de acceso al almacén de claves para la administración de almacenes y claves y secretos. Modelo de autenticación y autorización para el almacén de claves y cómo toosecure su clave de almacén"
services: key-vault
documentationcenter: 
author: amitbapat
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: e5b4e083-4a39-4410-8e3a-2832ad6db405
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 01/07/2017
ms.author: ambapat
ms.openlocfilehash: 84f5fc18142a1ad89babbd11f4f65eca105afc32
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="secure-your-key-vault"></a>Protección de un almacén de claves
Azure Key Vault es un servicio en la nube que protege las claves de cifrado y los secretos (como certificados, cadenas de conexión y contraseñas) de las aplicaciones en la nube. Puesto que estos datos son cruciales para la empresa y sensibles, desea almacenes de claves de toosecure acceso tooyour para que sólo las aplicaciones autorizadas y los usuarios pueden tener acceso a almacén de claves. En este artículo se proporciona información general del modelo de almacén de claves de acceso, se explica la autenticación y autorización y describe cómo toosecure tookey de acceso del almacén de aplicaciones en la nube con un ejemplo.

## <a name="overview"></a>Información general
Almacén de claves de acceso tooa se controla mediante dos interfaces diferentes: plano de administración y plano de datos. Para ambos planos autorización y la autenticación correcta es necesario antes de que un autor de llamada (un usuario o una aplicación) puede obtener el almacén de tookey de acceso. La autenticación establece la identidad de hello del autor de llamada de hello, mientras que la autorización determina qué operaciones Hola autor de la llamada se permite tooperform.

Para la autenticación tanto del plano de administración como del plano de datos se usa Azure Active Directory. Para la autorización, el plano de administración usa el control de acceso basado en rol (RBAC), mientras que el plano de datos utiliza la directiva de acceso de Key Vault.

Esta es una breve descripción de hello temas:

[Autenticación con Azure Active Directory](#authentication-using-azure-active-directory) : esta sección explica cómo un llamador autentica con Azure Active Directory tooaccess un almacén de claves a través de plano de administración y plano de datos. 

[Plano de administración y plano de datos](#management-plane-and-data-plane): el plano de administración y el plano de datos son dos planos de acceso que se usan para acceder a un almacén de claves. Cada plano de acceso admite operaciones concretas. Esta sección describen los puntos de conexión de acceso de hello, las operaciones compatibles y tener acceso a método que utiliza cada plano. 

[Control de acceso de administración plano](#management-plane-access-control) : en esta sección veremos que las operaciones de plano toomanagement con control de acceso basado en roles permite el acceso.

[Control de acceso de datos plano](#data-plane-access-control) -esta sección describe cómo los datos de toocontrol de directivas de acceso de almacén de claves de toouse plano acceso.

[Ejemplo](#example) -en este ejemplo se describe cómo toosetup control de acceso para los almacén de claves tooallow tres distintos equipos (equipo de seguridad, los desarrolladores/operadores y auditores) tooperform toodevelop de tareas específicas, administrar y supervisar una aplicación en Azure .

## <a name="authentication-using-azure-active-directory"></a>Autenticación mediante Azure Active Directory
Cuando se crea un almacén de claves en una suscripción de Azure, se asocia automáticamente con el inquilino de Azure Active Directory de la suscripción de Hola. Todos los llamadores (usuarios y aplicaciones) deben estar registrado en este inquilino tooaccess este almacén de claves. Una aplicación o un usuario debe autenticarse con el almacén de claves de Azure Active Directory tooaccess. Esto aplica plano de administración de tooboth y plano de datos access. En ambos casos, una aplicación puede acceder al almacén de claves de dos maneras:

* **acceso a usuario + aplicación**: normalmente es para aplicaciones que acceden al almacén de claves en nombre del usuario que ha iniciado sesión. Algunos ejemplos de este tipo de acceso son Azure PowerShell y Azure Portal. Hay dos maneras toogrant acceso toousers: unidireccional es toogrant acceso toousers para que pueden acceder a almacén de claves desde cualquier aplicación y Hola otra manera es toogrant un almacén de tookey de acceso de usuario solo cuando usa una aplicación específica (identidad compuesta tooas que se hace referencia). 
* **acceso de solo aplicación** : para las aplicaciones que ejecutan servicios daemon, trabajos en segundo plano se concede la identidad de la aplicación hello etc. acceso toohello la clave de almacén.

En ambos tipos de aplicaciones, aplicación hello se autentica con Azure Active Directory con cualquiera de hello [métodos de autenticación admitidos](../active-directory/active-directory-authentication-scenarios.md) y adquiere un token. Método de autenticación utilizado depende del tipo de aplicación Hola. A continuación, aplicación hello usa este token y envía el almacén de tookey de solicitud de API de REST. En el caso de hello de acceso de administración plano las solicitudes se enrutan a través de punto de conexión de administrador de recursos de Azure. Al acceder a plano de datos, las aplicaciones de Hola habla directamente tooa punto de conexión de almacén de claves. Consulte más detalles sobre hello [flujo de autenticación completo](../active-directory/active-directory-protocols-oauth-code.md). 

nombre de recurso de Hello para el que la aplicación hello solicita un token es diferente en función de si la aplicación hello tiene acceso a plano de administración o un plano de datos. Por lo tanto, el nombre de recurso de hello es cualquier extremo administración plano o datos plano que se describe en la tabla de hello en una sección posterior, dependiendo de hello entorno de Azure.

Tener un mecanismo único para la autenticación tooboth plano de administración y de datos tiene sus propias ventajas:

* Las organizaciones pueden controlar de forma centralizada almacenes de claves de tooall de acceso de su organización
* Si un usuario deja, que al instante pierdan acceso tooall almacenes de claves en la organización de Hola
* Las organizaciones pueden personalizar la autenticación a través de opciones de hello en Azure Active Directory (por ejemplo, lo que permite la autenticación multifactor para una mayor seguridad)

## <a name="management-plane-and-data-plane"></a>Plano de administración y plano de datos
Azure Key Vault es un servicio de Azure disponible a través del modelo de implementación de Azure Resource Manager. Al crear un almacén de claves, se obtiene un contenedor virtual en el que se pueden crear otros objetos como certificados, claves y secretos. A continuación, tener acceso a su almacén de claves mediante administración plano y datos plano tooperform operaciones específicas. Interfaz de administración de plano es toomanage usa la clave del almacén de sí mismo, como crear, eliminar, actualizar los atributos del almacén de claves y configuración de directivas de acceso para el plano de datos. Interfaz de plano de datos es tooadd usado, eliminar, modificar y utilizar claves de hello, secretos y certificados almacenados en el almacén de claves.

interfaces del plano de plano y datos de administración Hola se obtiene acceso a través de extremos diferentes (consulte la tabla). Hola en segunda columna de tabla de hello describe los nombres DNS de Hola para estos extremos en diferentes entornos de Azure. Hola tercera columna describe operaciones de Hola que puede realizar en cada plano de acceso. Cada plano de acceso también tiene su propio mecanismo de control de acceso: el del control de acceso del plano de administración se establece mediante el control de acceso basado en rol (RBAC) de Azure Resource Manager, mientras que el del control de acceso al plano de datos se establece mediante la directiva de acceso del almacén de claves.

| Plano de acceso | Puntos de conexión de acceso | Operaciones | Mecanismo de control de acceso |
| --- | --- | --- | --- |
| Plano de administración |**Global:**<br> management.azure.com:443<br><br> **Azure China:**<br> management.chinacloudapi.cn:443<br><br> **Azure Gobierno de EE. UU.:**<br> management.usgovcloudapi.net:443<br><br> **Azure Alemania:**<br> management.microsoftazure.de:443 |Crear, leer, actualizar o eliminar un almacén de claves <br> Establecer directivas de acceso para un almacén de claves<br>Establecer etiquetas para un almacén de claves |Control de acceso basado en rol (RBAC) de Azure Resource Manager |
| Plano de datos |**Global:**<br> &lt;vault-name&gt;.vault.azure.net:443<br><br> **Azure China:**<br> &lt;vault-name&gt;.vault.azure.cn:443<br><br> **Azure Gobierno de EE. UU.:**<br> &lt;vault-name&gt;.vault.usgovcloudapi.net:443<br><br> **Azure Alemania:**<br> &lt;vault-name&gt;.vault.microsoftazure.de:443 |Para claves: Decrypt, Encrypt, UnwrapKey, WrapKey, Verify, Sign, Get, List, Update, Create, Import, Delete, Backup, Restore<br><br> Para secretos: Get, List, Set, Delete |Directiva de acceso de Key Vault |

Hola administración plano y datos plano controles de acceso trabajar de forma independiente. Por ejemplo, si desea toogrant una clave de toouse de acceso de aplicación en un almacén de claves, solo necesita permisos de acceso de plano toogrant datos mediante directivas de acceso del almacén de claves y ningún acceso al plano de administración es necesario para esta aplicación. Y a la inversa, si desea que un usuario toobe capaz de tooread del almacén de propiedades y etiquetas, pero no tiene acceso tookeys, secretos ni certificados, puede conceder a este usuario, se requiere el acceso 'read' utilizando RBAC y ningún plano toodata de acceso.

## <a name="management-plane-access-control"></a>Control de acceso del plano de administración
plano de administración de Hello consta de operaciones que afectan al almacén de claves de hello propio. Por ejemplo, puede crear o eliminar un almacén de claves. Puede obtener una lista de los almacenes de una suscripción. Puede recuperar las propiedades de almacén de claves (por ejemplo, SKU, etiquetas) y establecer directivas de acceso que controlan los usuarios de Hola y las aplicaciones que pueden tener acceso a las claves y secretos en el almacén de claves de Hola de almacén de claves. El control de acceso del plano de administración utiliza RBAC. Ver Hola lista completa de las operaciones de almacén de claves que se pueden realizar a través de plano de administración en la tabla de hello en la sección anterior. 

### <a name="role-based-access-control-rbac"></a>Control de acceso basado en rol (RBAC)
Cada una de las suscripciones de Azure está asociada a una instancia de Azure Active Directory. Los usuarios, grupos y aplicaciones desde este directorio pueden tener acceso a los recursos del toomanage Hola suscripción de Azure que usan el modelo de implementación de hello Azure Resource Manager. Este tipo de control de acceso es que se hace referencia tooas Control de acceso basado en roles (RBAC). toomanage este acceso, puede usar hello [portal de Azure](https://portal.azure.com/), hello [herramientas de Azure CLI](../cli-install-nodejs.md), [PowerShell](/powershell/azureps-cmdlets-docs), o hello [API de REST del Administrador de recursos de Azure](https://msdn.microsoft.com/library/azure/dn906885.aspx).

Con el modelo de Azure Resource Manager hello, crear el almacén de claves en un recurso grupo y control de acceso toohello plano de administración de este almacén de claves mediante el uso de Azure Active Directory. Por ejemplo, puede conceder a los usuarios o un grupo capacidad toomanage clave almacenes de credenciales en un grupo de recursos específico.

Puede conceder acceso toousers, grupos y las aplicaciones en un ámbito concreto mediante la asignación de roles RBAC correspondientes. Por ejemplo, toogrant tener acceso a almacenes de claves tooa usuario toomanage se podría asignar un rol predefinido 'almacén de claves colaborador' usuario toothis en un ámbito específico. ámbito de Hello en este caso sería una suscripción, un grupo de recursos o simplemente un almacén de claves específico. Un rol asignado en el nivel de suscripción aplica tooall grupos de recursos y recursos dentro de esa suscripción. Un rol asignado en el nivel de grupo de recursos aplica tooall recursos en ese grupo de recursos. Un rol asignado para un recurso concreto solo aplica a recursos de toothat. Hay varias funciones predefinidas (vea [RBAC: roles integrados](../active-directory/role-based-access-built-in-roles.md)), y si los roles predefinidos de hello no ajustarlo a sus necesidades puede definir sus propios roles.

> [!IMPORTANT]
> Tenga en cuenta que si un usuario tiene plano de administración de almacén de claves tooa de colaborador permisos (RBAC), puede concederse a sí mismo plano toodata de acceso, mediante el establecimiento de la directiva de acceso del almacén de claves, que controla el plano de toodata de acceso. Por lo tanto, se recomienda controlar tootightly quién tiene 'Colaborador' acceso tooyour almacenes clave tooensure sólo las personas autorizadas pueden tener acceso a y administrar almacenes de claves, claves, secretos y certificados.
> 
> 

## <a name="data-plane-access-control"></a>Control de acceso al plano de datos
plano de datos de almacén de claves de Hello consta de las operaciones que afectan a los objetos de hello en un almacén de claves, como certificados, claves y secretos.  Aquí se incluyen operaciones de claves como crear, importar, actualizar, enumerar, crear una copia de seguridad y restaurar dichas claves, operaciones criptográficas como firmar, comprobar, cifrar, descifrar, encapsular y desencapsular, y establecer etiquetas y otros atributos para las claves. De igual forma, para los secretos incluye obtener, establecer, enumerar o eliminar.

El acceso al plano de datos se concede mediante el establecimiento de directivas de acceso para un almacén de claves. Un usuario, grupo o una aplicación debe tener permisos de colaborador (RBAC) para el plano de administración de un almacén de claves toobe tooset capaz de directivas de acceso para ese almacén de claves. Un usuario, grupo o aplicación puede tener acceso tooperform operaciones específicas para las claves o secretos en un almacén de claves. Compatibilidad con el almacén de claves too16 las entradas de directiva de acceso para un almacén de claves. Cree un grupo de seguridad de Azure Active Directory y agregue los usuarios toothat grupo toogrant datos plano acceso tooseveral usuarios tooa el almacén de claves.

### <a name="key-vault-access-policies"></a>Directivas de acceso de almacén de claves
Las directivas de acceso del almacén de claves conceden certificados, secretos y permisos tookeys por separado. Por ejemplo, puede proporcionar un claves de tooonly de acceso de usuario, pero ningún permiso para los secretos. Sin embargo, las claves de tooaccess de permisos o secretos o certificados están en el nivel de almacén de Hola. En otras palabras, la directiva de acceso de un almacén de claves no admite permisos de nivel de objeto. Puede usar [portal de Azure](https://portal.azure.com/), hello [herramientas de Azure CLI](../cli-install-nodejs.md), [PowerShell](/powershell/azureps-cmdlets-docs), o hello [API de REST de administración de almacén de claves](https://msdn.microsoft.com/library/azure/mt620024.aspx) tooset las directivas de acceso para un almacén de claves.

> [!IMPORTANT]
> Tenga en cuenta que las directivas de acceso del almacén de claves se aplican en el nivel de almacén de Hola. Por ejemplo, cuando un usuario se concede permiso toocreate y eliminar las claves, puede realizar estas operaciones en todas las claves en ese almacén de claves.
> 
> 

## <a name="example"></a>Ejemplo
Supongamos que está desarrollando una aplicación que utiliza un certificado para SSL, Azure Storage para almacenar los datos y que usa una clave RSA de 2048 bits para las operaciones de firma. Supongamos que esta aplicación se ejecuta en una VM (o un conjunto de escalado de VM). Puede usar un toostore de almacén de claves que Hola a todos los secretos de la aplicación y usar el almacén de claves toostore Hola arranque el certificado utilizado por hello tooauthenticate de aplicación con Azure Active Directory.

Por lo tanto, este es un resumen de todos los toobe de claves y secretos de hello almacenados en un almacén de claves.

* **Certificado SSL**: se usa para SSL
* **Clave de almacenamiento** -utilizado tooget acceso tooStorage cuenta
* **Clave RSA de 2048 bits**: se usa para las operaciones de firma
* **Certificado de arranque** -utilizar tooauthenticate tooAzure Active Directory, clave de almacenamiento del almacén toofetch Hola de tooget acceso tookey y usar Hola RSA clave para firmar.

Ahora vamos a cumplir personas Hola que administrar, implementar y la auditoría de esta aplicación. En este ejemplo, vamos a usar tres roles.

* **Equipo de seguridad** : estos suelen ser el personal de TI de hello 'oficina de hello CSO (Director de seguridad)' o equivalente, responsable de Hola apropiado custodia de secretos, como los certificados SSL, las claves RSA que se utiliza para la firma, cadenas de conexión para bases de datos, las claves de cuenta de almacenamiento.
* **Los desarrolladores/operadores** -se trata de hello personas desarrollar esta aplicación y, a continuación, implementación en Azure. Por lo general, no forman parte del equipo de seguridad de hello y por lo tanto, no debería tener acceso tooany confidencial, como los certificados SSL, las claves RSA, pero hello las aplicaciones que implementan la tengan acceso toothose.
* **Auditores** -suele ser un conjunto diferente de personas, aisladas de los desarrolladores de Hola y el personal de TI general. Su responsabilidad es el uso correcto de tooreview y el mantenimiento de certificados, claves, etc. y garantizar el cumplimiento de normas de seguridad de datos. 

Hay un rol más que es externo Hola ámbito de esta aplicación, pero relevante toobe aquí mencionados, y que sería suscripción hello (o grupo de recursos) Administrador. Administrador de la suscripción se establece los permisos de acceso inicial para el equipo de seguridad de Hola. Aquí suponemos que Administrador de suscripción Hola concedió acceso toohello seguridad equipo tooa grupo de recursos en el que todos Hola recursos necesarios para este residan de aplicación.

Ahora veamos qué acciones realiza cada rol en el contexto de Hola de esta aplicación.

* **Equipo de seguridad**
  * Crear instancias de Key Vault
  * Activar el registro de Key Vault
  * Agregar claves y secretos
  * Crear una copia de seguridad de las claves para la recuperación ante desastres
  * Configurar el acceso de almacén de claves directiva toogrant permisos toousers y aplicaciones tooperform operaciones específicas
  * Rotación periódica las claves y los secretos
* **Desarrolladores y operadores**
  * Obtener referencias toobootstrap y los certificados SSL (las huellas digitales), clave de almacenamiento (secreto URI) y la firma clave (clave URI) del equipo de seguridad
  * Desarrollar e implementar una aplicación que acceda a las claves y los secretos por programación
* **Auditores**
  * Revisar el uso de registros de uso de clave/secreto correcto tooconfirm y cumplimiento de normas de seguridad de datos

Ahora veamos qué almacén de tookey de permisos de acceso se necesitan para cada rol (y la aplicación hello) tooperform sus tareas asignadas. 

| Rol de usuario | Permisos del plano de administración | Permisos del plano de datos |
| --- | --- | --- |
| Equipo de seguridad |Colaborador de almacén de claves |Claves: copia de seguridad, creación, eliminación, obtención, importación, lista y restauración <br> Secretos: todos |
| Desarrolladores u operador |almacén de claves implementar permiso para que las máquinas virtuales de Hola que implementan la pueden capturar secretos del almacén de claves de Hola |None |
| Auditores |None |Claves: enumeración<br>Secretos: enumeración |
| Application |None |Claves: firma<br>Secretos: obtención |

> [!NOTE]
> Auditores necesitan permiso de lista de claves y secretos para que puedan inspeccionar atributos para las claves y secretos que no se emiten en los registros de hello, como las etiquetas, las fechas de activación y expiración.
> 
> 

Además de almacén de tookey de permiso, todos los tres roles también necesitan tener acceso a tooother recursos. Por ejemplo, toobe puede toodeploy máquinas virtuales (o etcetera de aplicaciones Web.) Los desarrolladores/operadores también necesita tipos de recursos de toothose de acceso 'Colaborador'. Auditores necesitan acceso de lectura cuenta de almacenamiento toohello donde se almacenan los registros de almacén de claves de Hola.

Puesto que descrito en hello este artículo es la protección de almacén de claves de acceso tooyour, se muestran las partes relevantes de hello pertenecen toothis tema solo y omitir los detalles relacionados con la implementación de certificados, obtener acceso a las claves y secretos etcetera mediante programación. Dichos detalles ya están explican en otro lugar. Implementación de certificados almacenados en el almacén de claves tooVMs se trata en una [entrada de blog](https://blogs.technet.microsoft.com/kv/2016/09/14/updated-deploy-certificates-to-vms-from-customer-managed-key-vault/)y no hay [código de ejemplo](https://www.microsoft.com/download/details.aspx?id=45343) disponibles que ilustra cómo toouse arranque certificado tooauthenticate tooAzure AD tooget almacén de tookey de acceso.

Se pueden conceder la mayoría de los permisos de acceso de hello mediante el portal de Azure, pero puede que necesite Hola de tooachieve de PowerShell de Azure (o CLI de Azure) toouse de permisos granulares toogrant resultado deseado. 

Supongamos que Hola siguientes fragmentos de código de PowerShell:

* Administrador de Hello Azure Active Directory ha creado grupos de seguridad que representan Hola tres roles, es decir, equipo de seguridad de Contoso, Devops de aplicación de Contoso, Contoso App Auditors. Administrador de Hello también ha agregado grupos de toohello de los usuarios que pertenecen.
* **ContosoAppRG** es grupo de recursos de Hola que residen todos los recursos de Hola. **contosologstorage** es donde se almacenan los registros de Hola. 
* Almacén de claves **ContosoKeyVault** y cuenta de almacenamiento que se utiliza para los registros de almacén de claves **contosologstorage** debe estar en hello misma ubicación de Azure

Primer administrador de suscripción de hello asigna la clave del almacén de colaborador y equipo de seguridad de ' Administrador de acceso de usuario ' roles toohello. Esto permite tooother acceso a recursos de hello seguridad equipo toomanage y administrar los almacenes de claves en el grupo de recursos de hello ContosoAppRG.

```
New-AzureRmRoleAssignment -ObjectId (Get-AzureRmADGroup -SearchString 'Contoso Security Team')[0].Id -RoleDefinitionName "key vault Contributor" -ResourceGroupName ContosoAppRG
New-AzureRmRoleAssignment -ObjectId (Get-AzureRmADGroup -SearchString 'Contoso Security Team')[0].Id -RoleDefinitionName "User Access Administrator" -ResourceGroupName ContosoAppRG
```

Hello secuencia de comandos siguiente muestra cómo puede crear un almacén de claves, el registro de instalación y establecer permisos de acceso de otros roles y la aplicación hello equipo de seguridad de Hola. 

```
# Create key vault and enable logging
$sa = Get-AzureRmStorageAccount -ResourceGroup ContosoAppRG -Name contosologstorage
$kv = New-AzureRmKeyVault -VaultName ContosoKeyVault -ResourceGroup ContosoAppRG -SKU premium -Location 'westus' -EnabledForDeployment
Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent

# Data plane permissions for Security team
Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoKeyVault -ObjectId (Get-AzureRmADGroup -SearchString 'Contoso Security Team')[0].Id -PermissionsToKeys backup,create,delete,get,import,list,restore -PermissionsToSecrets all

# Management plane permissions for Dev/ops
# Create a new role from an existing role
$devopsrole = Get-AzureRmRoleDefinition -Name "Virtual Machine Contributor"
$devopsrole.Id = $null
$devopsrole.Name = "Contoso App Devops"
$devopsrole.Description = "Can deploy VMs that need secrets from key vault"
$devopsrole.AssignableScopes = @("/subscriptions/<SUBSCRIPTION-GUID>")

# Add permission for dev/ops so they can deploy VMs that have secrets deployed from key vaults
$devopsrole.Actions.Add("Microsoft.KeyVault/vaults/deploy/action")
New-AzureRmRoleDefinition -Role $devopsrole

# Assign this newly defined role tooDev ops security group
New-AzureRmRoleAssignment -ObjectId (Get-AzureRmADGroup -SearchString 'Contoso App Devops')[0].Id -RoleDefinitionName "Contoso App Devops" -ResourceGroupName ContosoAppRG

# Data plane permissions for Auditors
Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoKeyVault -ObjectId (Get-AzureRmADGroup -SearchString 'Contoso App Auditors')[0].Id -PermissionsToKeys list -PermissionsToSecrets list
```

roles personalizados de Hello definido, solo puede asignar toohello suscripción donde se crea el grupo de recursos de hello ContosoAppRG. Si hello mismos roles personalizados se utilizará para otros proyectos de otras suscripciones, su ámbito podría tener varias suscripciones agregadas.

asignación de roles personalizados de Hola para Hola a los desarrolladores y operadores para permiso de "Implementar/acción" hello es grupo de recursos de toohello con ámbito. Este modo solo los nodos Hola crean en grupo de recursos de hello 'ContosoAppRG' obtendrá secretos de hello (certificado de arranque y el certificado de SSL). Todas las máquinas virtuales que un miembro del equipo de profesionales y desarrolladores se crea en otro grupo de recursos no será capaz de tooget estos secretos incluso si conoce el secreto de hello URI.

En este ejemplo se muestra un escenario simple. Escenarios de la vida real pueden ser más complejos y puede que necesite almacén de claves tooadjust permisos tooyour según sus necesidades. Por ejemplo, en nuestro ejemplo, asumimos que ese equipo de seguridad proporcionará clave hello y secretas referencias (identificadores URI y huellas digitales) que tooreference de necesidad de equipo a los desarrolladores y operadores en sus aplicaciones. Por lo tanto, no deben toogrant a los desarrolladores/operadores ningún acceso de plano de datos. Además, tenga en cuenta que este ejemplo se centra en la protección de un almacén de claves. Similar prestarse toosecure [las máquinas virtuales](https://azure.microsoft.com/services/virtual-machines/security/), [cuentas de almacenamiento](../storage/common/storage-security-guide.md) y otros recursos de Azure demasiado.

> [!NOTE]
> Nota: En este ejemplo se muestra cómo se bloqueará el acceso a un almacén de claves en producción. los desarrolladores de Hello deben tener su propia suscripción o grupo de recursos que tengan permisos completos toomanage sus almacenes, las máquinas virtuales y cuenta de almacenamiento donde desarrolla la aplicación hello.
> 
> 

## <a name="resources"></a>Recursos
* [Control de acceso basado en roles de Azure Active Directory](../active-directory/role-based-access-control-configure.md)
  
  Este artículo explica Hola basada en roles de Azure Active Directory Access Control y cómo funciona.
* [RBAC: Roles integrados](../active-directory/role-based-access-built-in-roles.md)
  
  Hola a este artículo se detallan todas las funciones integradas disponibles en RBAC.
* [Descripción de la implementación de Resource Manager y la implementación clásica](../azure-resource-manager/resource-manager-deployment-model.md)
  
  Este artículo explica la implementación del Administrador de recursos de Hola y modelos de implementación clásica y explica las ventajas de Hola de uso de grupos de administrador de recursos y recursos de Hola
* [Administración del control de acceso basado en rol con Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md)
  
  Este artículo explica cómo toomanage basada en roles control de acceso con Azure PowerShell
* [Administración del Control de acceso basado en roles con hello API de REST](../active-directory/role-based-access-control-manage-access-rest.md)
  
  Este artículo muestra cómo toouse Hola toomanage RBAC de API de REST.
* [Role-Based Access Control for Microsoft Azure from Ignite (Control de acceso basado en rol para Microsoft Azure de Ignite)](https://channel9.msdn.com/events/Ignite/2015/BRK2707)
  
  Se trata de un vídeo de Channel 9 de la conferencia de Ignite de 2015 MS hello tooa de vínculo. En esta sesión, hablan sobre acceso a capacidades de administración y generación de informes en Azure y explorar las prácticas recomendadas en protección del acceso suscripciones tooAzure con Azure Active Directory.
* [Autorizar acceso tooweb aplicaciones mediante OAuth 2.0 y Azure Active Directory](../active-directory/active-directory-protocols-oauth-code.md)
  
  En este artículo se todo el flujo de OAuth 2.0 para realizar la autenticación con Azure Active Directory.
* [API de REST de administración de almacén de claves](https://msdn.microsoft.com/library/azure/mt620024.aspx)
  
  Este documento es la referencia de Hola para toomanage de las API de REST de hello su clave de almacén mediante programación, incluido el establecimiento de la directiva de acceso del almacén de claves.
* [API de REST de almacén de claves](https://msdn.microsoft.com/library/azure/dn903609.aspx)
  
  Almacén de vínculo tookey documentación de referencia de API de REST.
* [Control de acceso de claves](https://msdn.microsoft.com/library/azure/dn903623.aspx#BKMK_KeyAccessControl)
  
  Documentación de referencia de control de acceso de vínculo tooSecret.
* [Control de acceso de secretos](https://msdn.microsoft.com/library/azure/dn903623.aspx#BKMK_SecretAccessControl)
  
  Documentación de referencia de control de acceso de vínculo tooKey.
* [Establecer](https://msdn.microsoft.com/library/mt603625.aspx) y [quitar](https://msdn.microsoft.com/library/mt619427.aspx) una directiva de acceso de Key Vault mediante PowerShell
  
  Documentación de tooreference de vínculos de directiva de acceso de almacén de claves de toomanage de cmdlets de PowerShell.

## <a name="next-steps"></a>Pasos siguientes
Para ver un tutorial de introducción para administradores, consulte [Introducción a Azure Key Vault](key-vault-get-started.md).

Para más información acerca del registro de uso de Key Vault, consulte [Registro de Azure Key Vault](key-vault-logging.md).

Para más información acerca del uso de claves y secretos con Azure Key Vault, consulte [About keys, secrets, and certificates](https://msdn.microsoft.com/library/azure/dn903623.aspx) (Acerca de claves, secretos y certificados).

Si tiene alguna pregunta sobre el almacén de claves, visite hello [almacén de claves de Azure foros](https://social.msdn.microsoft.com/forums/azure/home?forum=AzureKeyVault)

