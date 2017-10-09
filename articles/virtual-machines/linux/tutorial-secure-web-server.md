---
title: aaaSecure certificados de un servidor web con SSL en Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo certificados de servidor de toosecure hello NGINX web con SSL en una VM de Linux en Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/17/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: d3a62d77ac05c9aa2a44356b7c8e44cb485b81aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="secure-a-web-server-with-ssl-certificates-on-a-linux-virtual-machine-in-azure"></a>Protección de un servidor web con certificados SSL en una máquina virtual Linux en Azure
los servidores web toosecure, que puede ser un certificado Secure Sockets más adelante (SSL) utiliza el tráfico web tooencrypt. Estos certificados SSL pueden almacenarse en el almacén de claves de Azure y permiten implementaciones seguras de certificados tooLinux máquinas virtuales (VMs) en Azure. En este tutorial, aprenderá a:

> [!div class="checklist"]
> * Crear una instancia de Azure Key Vault
> * Generar o cargar un almacén de claves de certificado toohello
> * Crear una máquina virtual e instale el servidor de web NGINX Hola
> * Insertar certificado de hello en hello VM y configurar NGINX con un enlace SSL

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Si elige tooinstall y usar hello CLI localmente, este tutorial requiere que se ejecuta la versión de CLI de Azure de hello 2.0.4 o versiones posteriores. Ejecutar `az --version` toofind versión de Hola. Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli).  


## <a name="overview"></a>Información general
Azure Key Vault protege claves y secretos criptográficos, como certificados y contraseñas. El almacén de claves ayuda a simplificar el proceso de administración de certificados de Hola y permite toomaintain control de claves que tienen acceso a dichos certificados. Puede crear un certificado autofirmado en Key Vault o cargar un certificado de confianza existente que ya posea.

En lugar de usar una imagen de máquina virtual personalizada que incluya los certificados preparados, inserta los certificados en una máquina virtual en ejecución. Este proceso garantiza que los certificados más actualizados de hello están instalados en un servidor web durante la implementación. Si renovar o reemplazar un certificado, no tendrá también toocreate una nueva imagen de máquina virtual personalizada. los certificados más recientes de Hola se insertan automáticamente a medida que cree máquinas virtuales adicionales. Durante el proceso completo de hello, certificados de hello nunca deje Hola plataforma Windows Azure o se exponen en un script, el historial de la línea de comandos o la plantilla.


## <a name="create-an-azure-key-vault"></a>Crear una instancia de Azure Key Vault
Para poder crear una instancia de Key Vault y certificados, cree un grupo de recursos con [az group create](/cli/azure/group#create). Hello en el ejemplo siguiente se crea un grupo de recursos denominado *myResourceGroupSecureWeb* en hello *eastus* ubicación:

```azurecli-interactive 
az group create --name myResourceGroupSecureWeb --location eastus
```

Después, cree una instancia de Key Vault con [az keyvault create](/cli/azure/keyvault#create) y habilítela para usarla al implementar una máquina virtual. Cada instancia de Key Vault requiere un nombre único, que debe estar todo en minúsculas. Reemplace  *<mykeyvault>*  en el siguiente ejemplo con su propio nombre de almacén de claves único de hello:

```azurecli-interactive 
keyvault_name=<mykeyvault>
az keyvault create \
    --resource-group myResourceGroupSecureWeb \
    --name $keyvault_name \
    --enabled-for-deployment
```

## <a name="generate-a-certificate-and-store-in-key-vault"></a>Generación de un certificado y almacenamiento en Key Vault
Para usarlo en producción, debe importar un certificado válido firmado por un proveedor de confianza con [az keyvault certificate import](/cli/azure/certificate#import). Para este tutorial, hello en el ejemplo siguiente se muestra cómo puede generar un certificado autofirmado con [crear certificado de keyvault az](/cli/azure/certificate#create) que usa la directiva de certificado de hello predeterminada:

```azurecli-interactive 
az keyvault certificate create \
    --vault-name $keyvault_name \
    --name mycert \
    --policy "$(az keyvault certificate get-default-policy)"
```

### <a name="prepare-a-certificate-for-use-with-a-vm"></a>Preparación del certificado para usarlo con una máquina virtual
certificado de hello toouse durante Hola VM crear proceso, obtener Id. de hello del certificado con [az keyvault secreto lista versiones](/cli/azure/keyvault/secret#list-versions). Convertir el certificado de hello con [az de vm formato secreto](/cli/azure/vm#format-secret). Hola de ejemplo siguiente asigna a salida de hello de estos toovariables de comandos para facilitar su uso en hello pasos siguientes:

```azurecli-interactive 
secret=$(az keyvault secret list-versions \
          --vault-name $keyvault_name \
          --name mycert \
          --query "[?attributes.enabled].id" --output tsv)
vm_secret=$(az vm format-secret --secret "$secret")
```

### <a name="create-a-cloud-init-config-toosecure-nginx"></a>Crear un toosecure de configuración de nube init NGINX
[En la nube init](https://cloudinit.readthedocs.io) es un enfoque ampliamente utilizado toocustomize una VM Linux tal y como se arranca para hello primera vez. Puede usar en la nube init tooinstall paquetes y escribir archivos, o los usuarios de tooconfigure y seguridad. Como init de la nube se ejecuta durante el proceso de arranque inicial de hello, no hay ningún paso adicional o requiere la configuración de agentes tooapply.

Cuando se crea una máquina virtual, certificados y claves se almacenan en hello protegido */var/lib/waagent/* directory. Agregar tooautomate Hola certificado toohello VM y configuración de servidor web de hello, utilice init de la nube. En este ejemplo, se instalar y configura el servidor de web NGINX Hola. Puede usar hello mismo proceso tooinstall y configurar Apache. 

Cree un archivo denominado *nube-init-web-server.txt* y pegar Hola siguiente configuración:

```yaml
#cloud-config
package_upgrade: true
packages:
  - nginx
write_files:
  - owner: www-data:www-data
  - path: /etc/nginx/sites-available/default
    content: |
      server {
        listen 443 ssl;
        ssl_certificate /etc/nginx/ssl/mycert.cert;
        ssl_certificate_key /etc/nginx/ssl/mycert.prv;
      }
runcmd:
  - secretsname=$(find /var/lib/waagent/ -name "*.prv" | cut -c -57)
  - mkdir /etc/nginx/ssl
  - cp $secretsname.crt /etc/nginx/ssl/mycert.cert
  - cp $secretsname.prv /etc/nginx/ssl/mycert.prv
  - service nginx restart
```

### <a name="create-a-secure-vm"></a>Creación de una máquina virtual segura
Ahora cree una máquina virtual con el comando [az vm create](/cli/azure/vm#create). datos del certificado Hola se inyección desde el almacén de claves con hello `--secrets` parámetro. Se pasa en la configuración de nube init Hola con hello `--custom-data` parámetro:

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroupSecureWeb \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init-web-server.txt \
    --secrets "$vm_secret"
```

Se tarda unos minutos para hello VM toobe creado, tooinstall de paquetes de Hola y Hola toostart de aplicación. Cuando se ha creado Hola VM, tome nota de hello `publicIpAddress` muestra de Hola CLI de Azure. Esta dirección es tooaccess usa su sitio en un explorador web.

tooallow secure web tráfico tooreach la máquina virtual, abrir el puerto 443 de hello Internet con [az de vm abrir puerto](/cli/azure/vm#open-port):

```azurecli-interactive 
az vm open-port \
    --resource-group myResourceGroupSecureWeb \
    --name myVM \
    --port 443
```


### <a name="test-hello-secure-web-app"></a>Aplicación de prueba hello web segura
Ahora puede abrir un explorador web y escriba *https://<publicIpAddress>*  en la barra de direcciones de Hola. Proporcionar su propia público dirección IP de hello VM crear proceso. Acepte la advertencia de seguridad de hello si usa un certificado autofirmado:

![Aceptar la advertencia de seguridad del explorador web](./media/tutorial-secure-web-server/browser-warning.png)

El sitio NGINX seguro, a continuación, se muestra como en el siguiente ejemplo de Hola:

![Ver el sitio de NGINX seguro en funcionamiento](./media/tutorial-secure-web-server/secured-nginx.png)


## <a name="next-steps"></a>Pasos siguientes

En este tutorial, protegió un servidor web NGINX con un certificado SSL almacenado en Azure Key Vault. Ha aprendido a:

> [!div class="checklist"]
> * Crear una instancia de Azure Key Vault
> * Generar o cargar un almacén de claves de certificado toohello
> * Crear una máquina virtual e instale el servidor de web NGINX Hola
> * Insertar certificado de hello en hello VM y configurar NGINX con un enlace SSL

Siga este toosee vínculo pregeneradas ejemplos de script de máquina virtual.

> [!div class="nextstepaction"]
> [Ejemplos de scripts de máquina virtual Windows](./cli-samples.md)