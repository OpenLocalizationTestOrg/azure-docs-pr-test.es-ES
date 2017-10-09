Usar dirección URL de implementación remota de hello Azure CLI tooget hello para la API App. Hola siguiente comando, reemplace  *\<app_name >* con el nombre de la aplicación web.

```azurecli-interactive
az webapp deployment source config-local-git --name <app_name> --resource-group myResourceGroup --query url --output tsv
```

Configure su local Git implementación toobe toopush pueda toohello remoto.

```bash
git remote add azure <URI from previous step>
```

Insertar toohello Azure toodeploy remoto de la aplicación. Se le pediremos que creó anteriormente cuando se creó el usuario de la implementación de Hola de contraseña de Hola. Asegúrese de que escriba la contraseña de Hola que creó en versiones anteriores del tutorial de Hola y Hola una contraseña no usar toolog en toohello portal de Azure.

```bash
git push azure master
```
