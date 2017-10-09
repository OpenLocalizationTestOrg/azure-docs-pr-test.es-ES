Configurar Git implementación toohello la aplicación web local con hello [origen de implementación de aplicación Web en az config-local-git](/cli/azure/webapp/deployment/source#config-local-git) comando.

Servicio de aplicaciones admite varias maneras toodeploy tooa contenido aplicación web, como FTP, Git local, GitHub, Visual Studio Team Services y Bitbucket. Para esta guía de inicio rápido, va a realizar la implementación mediante el uso de Git local. Esto significa que se implementan con un toopush de comandos de Git desde un repositorio de tooa de repositorio local en Azure. 

Hola siguiente comando, reemplace  *\<app_name >* con el nombre de la aplicación web.

```azurecli-interactive
az webapp deployment source config-local-git --name <app_name> --resource-group myResourceGroup --query url --output tsv
```

salida de Hello tiene Hola siguiendo el formato:

```bash
https://<username>@<app_name>.scm.azurewebsites.net:443/<app_name>.git
```

Hola `<username>` es hello [usuario de implementación](#configure-a-deployment-user) que creó en el paso anterior.

Copiar Hola URI se muestra; se usará en el paso siguiente de saludo.
