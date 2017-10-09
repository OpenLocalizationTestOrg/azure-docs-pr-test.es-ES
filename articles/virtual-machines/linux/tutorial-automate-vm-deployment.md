---
title: aaaCustomize una VM de Linux en el primer inicio en Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse nube-init y Hola de máquinas virtuales de Linux de almacén de claves toocustomze primera vez que se inicien en Azure"
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
ms.date: 08/11/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: 280189723ac0205226f9c0068bd605da13249ace
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocustomize-a-linux-virtual-machine-on-first-boot"></a>¿Cómo toocustomize una máquina virtual de Linux en el primer arranque
En un tutorial anterior, se habrá aprendido cómo tooSSH tooa virtual machine (VM) e instalar manualmente NGINX. Normalmente se desea toocreate máquinas virtuales de una manera rápida y coherente, alguna forma de automatización. Un toocustomize enfoque común una máquina virtual en el primer inicio es toouse [init de la nube](https://cloudinit.readthedocs.io). En este tutorial, aprenderá a:

> [!div class="checklist"]
> * Crear un archivo de configuración cloud-init
> * Crear una máquina virtual que usa un archivo cloud-init
> * Ver una aplicación en ejecución Node.js después de hello que VM.
> * Usar el almacén de claves toosecurely almacén de certificados
> * Automatizar implementaciones seguras de NGINX con cloud-init


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Si elige tooinstall y usar hello CLI localmente, este tutorial requiere que se ejecuta la versión de CLI de Azure de hello 2.0.4 o versiones posteriores. Ejecutar `az --version` toofind versión de Hola. Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli).  



## <a name="cloud-init-overview"></a>Introducción a cloud-init
[En la nube init](https://cloudinit.readthedocs.io) es un enfoque ampliamente utilizado toocustomize una VM Linux tal y como se arranca para hello primera vez. Puede usar en la nube init tooinstall paquetes y escribir archivos, o los usuarios de tooconfigure y seguridad. Como init de la nube se ejecuta durante el proceso de arranque inicial de hello, no hay ningún paso adicional o requiere la configuración de agentes tooapply.

cloud-init también funciona entre distribuciones. Por ejemplo, no usar **install apt get** o **yum instalar** tooinstall un paquete. En su lugar, puede definir una lista de paquetes tooinstall. Init de la nube usa automáticamente herramienta de administración del paquete nativo de Hola para distribución de Hola que seleccione.

Estamos trabajando con nuestro socios tooget nube-init incluida y estamos trabajando en las imágenes de Hola que proporcionan tooAzure. Hello en la tabla siguiente describe la disponibilidad de hello actual init de la nube en las imágenes de la plataforma Windows Azure:

| Alias | Publicador | Oferta | SKU | Versión |
|:--- |:--- |:--- |:--- |:--- |:--- |
| UbuntuLTS |Canonical |UbuntuServer |16.04-LTS |más reciente |
| UbuntuLTS |Canonical |UbuntuServer |14.04.5-LTS |más reciente |
| CoreOS |CoreOS |CoreOS |Stable |más reciente |


## <a name="create-cloud-init-config-file"></a>Creación de un archivo de configuración cloud-init
en la nube de toosee-init en acción, cree una máquina virtual que NGINX se instala y se ejecuta una aplicación sencilla de Node.js de "Hello World". Hola siguiente configuración de nube init instala los paquetes de saludo necesario, crea una aplicación Node.js, a continuación, inicializa e inicia la aplicación hello.

En el shell actual, cree un archivo denominado *init.txt nube* y pegar Hola siguiente configuración. Por ejemplo, crear archivo hello en hello Shell en la nube, no en el equipo local. Puede utilizar el editor que prefiera. Escriba `sensible-editor cloud-init.txt` toocreate Hola archivo y ver una lista de editores disponibles. Asegúrese de que ese archivo de nube-init todo Hola se copia correctamente, especialmente Hola primera línea:

```yaml
#cloud-config
package_upgrade: true
packages:
  - nginx
  - nodejs
  - npm
write_files:
  - owner: www-data:www-data
  - path: /etc/nginx/sites-available/default
    content: |
      server {
        listen 80;
        location / {
          proxy_pass http://localhost:3000;
          proxy_http_version 1.1;
          proxy_set_header Upgrade $http_upgrade;
          proxy_set_header Connection keep-alive;
          proxy_set_header Host $host;
          proxy_cache_bypass $http_upgrade;
        }
      }
  - owner: azureuser:azureuser
  - path: /home/azureuser/myapp/index.js
    content: |
      var express = require('express')
      var app = express()
      var os = require('os');
      app.get('/', function (req, res) {
        res.send('Hello World from host ' + os.hostname() + '!')
      })
      app.listen(3000, function () {
        console.log('Hello world app listening on port 3000!')
      })
runcmd:
  - service nginx restart
  - cd "/home/azureuser/myapp"
  - npm init
  - npm install express -y
  - nodejs index.js
```

Para más información sobre las opciones de configuración de cloud-init, consulte los [ejemplos de configuración de cloud-init](https://cloudinit.readthedocs.io/en/latest/topics/examples.html).

## <a name="create-virtual-machine"></a>Create virtual machine
Antes de poder crear una máquina virtual, cree un grupo de recursos con [az group create](/cli/azure/group#create). Hello en el ejemplo siguiente se crea un grupo de recursos denominado *myResourceGroupAutomate* en hello *eastus* ubicación:

```azurecli-interactive 
az group create --name myResourceGroupAutomate --location eastus
```

Ahora cree una máquina virtual con el comando [az vm create](/cli/azure/vm#create). Hola de uso `--custom-data` toopass de parámetro en el archivo de configuración de nube init. Proporcionar toohello de ruta de acceso completa de hello *init.txt nube* config si guarda el archivo hello fuera de su directorio de trabajo actual. Hello en el ejemplo siguiente se crea una máquina virtual denominada *myAutomatedVM*:

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroupAutomate \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

Se tarda unos minutos para hello VM toobe creado, tooinstall de paquetes de Hola y Hola toostart de aplicación. Hay tareas en segundo plano que continúan toorun después de hello CLI de Azure devuelve toohello símbolo del sistema. Es posible que otro par de minutos antes de que se puede tener acceso a la aplicación hello. Cuando se ha creado Hola VM, tome nota de hello `publicIpAddress` muestra de Hola CLI de Azure. Esta dirección es tooaccess usado hello Node.js aplicación a través de un explorador web.

tooallow web tooreach de tráfico de la máquina virtual, abrir el puerto 80 de hello Internet con [az de vm abrir puerto](/cli/azure/vm#open-port):

```azurecli-interactive 
az vm open-port --port 80 --resource-group myResourceGroupAutomate --name myVM
```

## <a name="test-web-app"></a>Prueba de la aplicación web
Ahora puede abrir un explorador web y escriba *http://<publicIpAddress>*  en la barra de direcciones de Hola. Proporcionar su propia público dirección IP de hello VM crear proceso. La aplicación Node.js se muestra como en el siguiente ejemplo de Hola:

![Ver sitio de NGINX en funcionamiento](./media/tutorial-automate-vm-deployment/nginx.png)


## <a name="inject-certificates-from-key-vault"></a>Inserción de certificados desde Key Vault
Esta sección opcional muestra cómo se puede almacenar certificados en el almacén de claves de Azure y se insertan durante la implementación de VM de Hola forma segura. En lugar de usar una imagen personalizada que incluye los certificados de hello preparadas, este proceso garantiza que los certificados más actualizados de Hola se insertan tooa VM en el primer arranque. Durante el proceso de hello, certificado de hello nunca deja Hola plataforma Windows Azure o se expone en un script, el historial de la línea de comandos o la plantilla.

Azure Key Vault protege claves y secretos criptográficos, como certificados y contraseñas. El almacén de claves ayuda a simplificar el proceso de administración de claves de Hola y permite toomaintain control de claves que tienen acceso y cifrar los datos. Este escenario se presentan algunos toocreate de conceptos de almacén de claves y usar un certificado, aunque no es exhaustiva información general acerca de cómo toouse el almacén de claves.

Hola siguientes pasos muestra cómo se puede:

- Crear una instancia de Azure Key Vault
- Generar o cargar un almacén de claves de certificado toohello
- Crear un secreto de hello certificado tooinject en tooa VM
- Crear una máquina virtual e insertar certificado de Hola

### <a name="create-an-azure-key-vault"></a>Crear una instancia de Azure Key Vault
En primer lugar, cree una instancia de Key Vault con [az keyvault create](/cli/azure/keyvault#create) y habilítela para su uso al implementar una máquina virtual. Cada instancia de Key Vault requiere un nombre único, que debe estar todo en minúsculas. Reemplace *mykeyvault* en el siguiente ejemplo con su propio nombre de almacén de claves único de hello:

```azurecli-interactive 
keyvault_name=mykeyvault
az keyvault create \
    --resource-group myResourceGroupAutomate \
    --name $keyvault_name \
    --enabled-for-deployment
```

### <a name="generate-certificate-and-store-in-key-vault"></a>Generación de un certificado y su almacenamiento en Key Vault
Para usarlo en producción, debe importar un certificado válido firmado por un proveedor de confianza con [az keyvault certificate import](/cli/azure/keyvault/certificate#import). Para este tutorial, hello en el ejemplo siguiente se muestra cómo puede generar un certificado autofirmado con [crear certificado de keyvault az](/cli/azure/keyvault/certificate#create) que usa la directiva de certificado de hello predeterminada:

```azurecli-interactive 
az keyvault certificate create \
    --vault-name $keyvault_name \
    --name mycert \
    --policy "$(az keyvault certificate get-default-policy)"
```


### <a name="prepare-certificate-for-use-with-vm"></a>Preparación del certificado para usarlo con la máquina virtual
certificado de hello toouse durante Hola VM crear proceso, obtener Id. de hello del certificado con [az keyvault secreto lista versiones](/cli/azure/keyvault/secret#list-versions). Hola VM necesita certificado de hello en un determinado tooinject de formato que se arranque el sistema, por lo que convertir el certificado de hello con [az de vm formato secreto](/cli/azure/vm#format-secret). Hola de ejemplo siguiente asigna a salida de hello de estos toovariables de comandos para facilitar su uso en hello pasos siguientes:

```azurecli-interactive 
secret=$(az keyvault secret list-versions \
          --vault-name $keyvault_name \
          --name mycert \
          --query "[?attributes.enabled].id" --output tsv)
vm_secret=$(az vm format-secret --secret "$secret")
```


### <a name="create-cloud-init-config-toosecure-nginx"></a>Crear configuración de nube init toosecure NGINX
Cuando se crea una máquina virtual, certificados y claves se almacenan en hello protegido */var/lib/waagent/* directory. tooautomate agregar Hola certificado toohello máquina virtual y configurar NGINX, puede usar una configuración actualizada en la nube al inicio del ejemplo anterior de Hola.

Cree un archivo denominado *nube-init-secured.txt* y pegar Hola siguiente configuración. De nuevo, si usas Hola Shell en la nube, crear el archivo de configuración de nube init Hola localizada ahí y no en el equipo local. Use `sensible-editor cloud-init-secured.txt` toocreate Hola archivo y ver una lista de editores disponibles. Asegúrese de que ese archivo de nube-init todo Hola se copia correctamente, especialmente Hola primera línea:

```yaml
#cloud-config
package_upgrade: true
packages:
  - nginx
  - nodejs
  - npm
write_files:
  - owner: www-data:www-data
  - path: /etc/nginx/sites-available/default
    content: |
      server {
        listen 80;
        listen 443 ssl;
        ssl_certificate /etc/nginx/ssl/mycert.cert;
        ssl_certificate_key /etc/nginx/ssl/mycert.prv;
        location / {
          proxy_pass http://localhost:3000;
          proxy_http_version 1.1;
          proxy_set_header Upgrade $http_upgrade;
          proxy_set_header Connection keep-alive;
          proxy_set_header Host $host;
          proxy_cache_bypass $http_upgrade;
        }
      }
  - owner: azureuser:azureuser
  - path: /home/azureuser/myapp/index.js
    content: |
      var express = require('express')
      var app = express()
      var os = require('os');
      app.get('/', function (req, res) {
        res.send('Hello World from host ' + os.hostname() + '!')
      })
      app.listen(3000, function () {
        console.log('Hello world app listening on port 3000!')
      })
runcmd:
  - secretsname=$(find /var/lib/waagent/ -name "*.prv" | cut -c -57)
  - mkdir /etc/nginx/ssl
  - cp $secretsname.crt /etc/nginx/ssl/mycert.cert
  - cp $secretsname.prv /etc/nginx/ssl/mycert.prv
  - service nginx restart
  - cd "/home/azureuser/myapp"
  - npm init
  - npm install express -y
  - nodejs index.js
```

### <a name="create-secure-vm"></a>Creación de una máquina virtual segura
Ahora cree una máquina virtual con el comando [az vm create](/cli/azure/vm#create). datos del certificado Hola se inyección desde el almacén de claves con hello `--secrets` parámetro. Como en el ejemplo anterior de hello, también pasar en la configuración de nube init Hola con hello `--custom-data` parámetro:

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroupAutomate \
    --name myVMSecured \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init-secured.txt \
    --secrets "$vm_secret"
```

Se tarda unos minutos para hello VM toobe creado, tooinstall de paquetes de Hola y Hola toostart de aplicación. Hay tareas en segundo plano que continúan toorun después de hello CLI de Azure devuelve toohello símbolo del sistema. Es posible que otro par de minutos antes de que se puede tener acceso a la aplicación hello. Cuando se ha creado Hola VM, tome nota de hello `publicIpAddress` muestra de Hola CLI de Azure. Esta dirección es tooaccess usado hello Node.js aplicación a través de un explorador web.

tooallow secure web tráfico tooreach la máquina virtual, abrir el puerto 443 de hello Internet con [az de vm abrir puerto](/cli/azure/vm#open-port):

```azurecli-interactive 
az vm open-port \
    --resource-group myResourceGroupAutomate \
    --name myVMSecured \
    --port 443
```

### <a name="test-secure-web-app"></a>Prueba de la aplicación web segura
Ahora puede abrir un explorador web y escriba *https://<publicIpAddress>*  en la barra de direcciones de Hola. Proporcionar su propia público dirección IP de hello VM crear proceso. Acepte la advertencia de seguridad de hello si usa un certificado autofirmado:

![Aceptar la advertencia de seguridad del explorador web](./media/tutorial-automate-vm-deployment/browser-warning.png)

El sitio NGINX y Node.js protegida, a continuación, se muestra la aplicación como en el siguiente ejemplo de Hola:

![Ver el sitio de NGINX seguro en funcionamiento](./media/tutorial-automate-vm-deployment/secured-nginx.png)


## <a name="next-steps"></a>Pasos siguientes
En este tutorial, ha configurado las máquinas virtuales en el primer inicio con cloud-init. Ha aprendido a:

> [!div class="checklist"]
> * Crear un archivo de configuración cloud-init
> * Crear una máquina virtual que usa un archivo cloud-init
> * Ver una aplicación en ejecución Node.js después de hello que VM.
> * Usar el almacén de claves toosecurely almacén de certificados
> * Automatizar implementaciones seguras de NGINX con cloud-init

Avanzar toohello siguiente tutorial toolearn cómo toocreate imágenes de máquina virtual personalizadas.

> [!div class="nextstepaction"]
> [Creación de imágenes personalizadas de máquinas virtuales](./tutorial-custom-images.md)
