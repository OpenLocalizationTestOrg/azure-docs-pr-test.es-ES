---
title: aaaCreate y administrar la base de datos de Azure con las reglas de firewall de MySQL con CLI de Azure | Documentos de Microsoft
description: "Este artículo se describe cómo toocreate y administrar la base de datos de Azure con las reglas de firewall de MySQL mediante la línea de comandos de CLI de Azure."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: b2f0b4ccf34ce88e3a5e72a64d3f8c78a5bc2a54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-mysql-firewall-rules-using-azure-cli"></a>Creación y administración de reglas de firewall de Azure Database for MySQL mediante la CLI de Azure
Las reglas de firewall de nivel de servidor habilitar administradores toomanage acceso tooan base de datos de MySQL Server desde una dirección IP específica o intervalo de direcciones IP. Usar comandos de CLI de Azure adecuadas, puede crear, actualizar, eliminar, enumerar y mostrar toomanage de reglas de firewall en el servidor. Para obtener información general sobre los firewalls de Azure Database for MySQL, consulte [Reglas de firewall de un servidor de Azure Database for MySQL](./concepts-firewall-rules.md).

## <a name="prerequisites"></a>Requisitos previos
* [Instalación de la CLI de Azure 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli)
* Instalación del SDK de Python para Azure para los servicios PostgreSQL y MySQL
* Instalar el componente de CLI de Azure de Hola para servicios PostgreSQL y MySQL
* Creación de un servidor de Azure Database for MySQL

## <a name="firewall-rule-commands"></a>Comandos de reglas de firewall:
Hola **az mysql server regla de firewall** se usa el comando de CLI de Azure toocreate, eliminar, enumerar, mostrar y actualizar las reglas de firewall.

Comandos:
- **create**: crear una regla de firewall de servidor de Azure para MySQL.
- **delete**: eliminar una regla de firewall de servidor de Azure para MySQL.
- **lista** : lista de reglas de firewall de servidor hello MySQL de Azure.
- **Mostrar** : mostrar detalles de Hola de un servidor de MySQL de Azure de regla de firewall.
- **update**: actualizar una regla de firewall de servidor de Azure para MySQL.

## <a name="login-tooazure-and-list-your-azure-database-for-mysql-servers"></a>TooAzure de inicio de sesión y la lista de la base de datos de Azure para los servidores de MySQL
Conecte de forma segura con la CLI de Azure con su cuenta de Azure. Hola de uso **inicio de sesión de az** comando toodo esto.

1. Ejecute hello siguiente comando desde la línea de comandos de Hola.
```azurecli
az login
```
Este comando dará como resultado un toouse de código en el paso siguiente de saludo.

2. Utilizar una página de hello web explorador tooopen [https://aka.ms/devicelogin](https://aka.ms/devicelogin) y escriba el código de hello.

3. En el símbolo del sistema de hello, inicie sesión con sus credenciales de Azure.

4. Una vez que se autoriza su inicio de sesión, se imprimirá una lista de suscripciones en la consola de Hola. Copie el identificador de Hola de hello deseado suscripción tooset Hola actual suscripción toobe utilizado en el futuro.
   ```azurecli-interactive
   az account set --subscription {your subscription id}
   ```

5. Si no está seguro de los nombres de Hola se enumeran hello las bases de datos de Azure para servidores de MySQL Server para el grupo de recursos y de suscripción.

   ```azurecli-interactive
   az mysql server list --resource-group myResourceGroup
   ```

   Tenga en cuenta atributo de nombre de Hola Hola enumerar, que será usado toospecify qué toowork de servidor MySQL en. Si es necesario, confirme los detalles de Hola para ese nombre tooconfirm del atributo de nombre de servidor toousing hello es correcta:

   ```azurecli-interactive
   az mysql server show --resource-group myResourceGroup --name mysqlserver4demo
   ```

## <a name="list-firewall-rules-on-azure-database-for-mysql-server"></a>Lista de reglas de firewall en el servidor de Azure Database for MySQL 
Utilizando el nombre del servidor de Hola y nombre de grupo de recursos de hello, reglas de firewall servidor existente de lista de hello en el servidor de Hola. Observe cómo se especifica dicho atributo de nombre de servidor de Hola Hola **--servidor** cambia y no Hola **--nombre** cambiar.
```azurecli-interactive
az mysql server firewall-rule list --resource-group myResourceGroup --server mysqlserver4demo
```
salida de Hello mostrará las reglas de hello si los hay, de forma predeterminada en JSON de formato. Puede usar el modificador de hello **: tabla de salida** para un formato más legible de la tabla como resultado de hello.
```azurecli-interactive
az mysql server firewall-rule list --resource-group myResourceGroup --server mysqlserver4demo --output table
```
## <a name="create-firewall-rule-on-azure-database-for-mysql-server"></a>Creación de reglas de firewall en el servidor de Azure Database for MySQL
Con nombre del servidor de MySQL de Azure de Hola y el nombre de grupo de recursos de hello, cree una nueva regla de firewall en el servidor de Hola. Proporcione un nombre para la regla de Hola y Hola inicio IP, IP final para hello regla toocover un intervalo de direcciones IP tooallow acceda.
```azurecli-interactive
az mysql server firewall-rule create --resource-group myResourceGroup  --server mysqlserver4demo --name "Firewall Rule 1" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.15
```
Para una dirección IP singular direcciones toobe puede tener acceso, proporcione Hola la misma dirección como Hola IP inicial y final de IP, como en este ejemplo.
```azurecli-interactive
az mysql server firewall-rule create --resource-group myResourceGroup  
--server mysql --name "Firewall Rule with a Single Address" --start-ip-address 1.1.1.1 --end-ip-address 1.1.1.1
```
Cuando se realiza correctamente, el resultado del comando de hello mostrará detalles Hola Hola de regla de firewall que ha creado, de forma predeterminada en formato JSON. Si se produce un error, el resultado de hello mostrará el texto del mensaje de error.

## <a name="update-firewall-rule-on-azure-database-for-mysql-server"></a>Actualización de reglas de firewall en el servidor de Azure Database for MySQL 
Con nombre del servidor de MySQL de Azure de Hola y el nombre de grupo de recursos de hello, actualizar una regla de firewall existente en el servidor de Hola. Proporcione el nombre de Hola de regla de firewall existente hello como entrada y Hola inicio IP y final IP atributos tooupdate.
```azurecli-interactive
az mysql server firewall-rule update --resource-group myResourceGroup --server mysqlserver4demo --name "Firewall Rule 1" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.1
```
Cuando se realiza correctamente, el resultado del comando de hello mostrará detalles Hola Hola de regla de firewall que ha actualizado, de forma predeterminada en formato JSON. Si se produce un error, el resultado de hello mostrará el texto del mensaje de error.

> [!NOTE]
> Si la regla de firewall de hello no existe, se creará mediante el comando de actualización de Hola.

## <a name="show-firewall-rule-details-on-azure-database-for-mysql-server"></a>Presentación de los detalles de las reglas de firewall en el servidor de Azure Database for MySQL
Con el nombre del servidor de MySQL de Azure de Hola y el nombre de grupo de recursos de hello, mostrar detalles de regla de firewall existente de Hola desde servidor hello. Proporcione el nombre de Hola de regla de firewall existente hello como entrada.
```azurecli-interactive
az mysql server firewall-rule show --resource-group myResourceGroup --server mysqlserver4demo --name "Firewall Rule 1"
```
Cuando se realiza correctamente, el resultado del comando de hello mostrará detalles Hola Hola de regla de firewall que ha especificado, de forma predeterminada en formato JSON. Si se produce un error, el resultado de hello mostrará el texto del mensaje de error.

## <a name="delete-firewall-rule-on-azure-database-for-mysql-server"></a>Eliminación de reglas de firewall en el servidor de Azure Database for MySQL
Con el nombre del servidor de MySQL de Azure de Hola y el nombre de grupo de recursos de hello, quite una regla de firewall existente del servidor de Hola. Proporcione el nombre de Hola Hola existente de regla de firewall.
```azurecli-interactive
az mysql server firewall-rule delete --resource-group myResourceGroup --server mysqlserver4demo --name "Firewall Rule 1"
```
Cuando se realiza correctamente, no hay ninguna salida. En caso de error, se devolverá el texto del mensaje de error de Hola.

## <a name="next-steps"></a>Pasos siguientes
- Para más información, consulte [Reglas de firewall de servidor de Azure Database for MySQL](./concepts-firewall-rules.md).
- [Crear y administrar la base de datos de Azure para las reglas de firewall de MySQL con hello portal de Azure](./howto-manage-firewall-using-portal.md)
