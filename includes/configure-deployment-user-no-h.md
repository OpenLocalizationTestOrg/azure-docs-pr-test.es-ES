Crear credenciales de implementación con hello [conjunto de usuarios de implementación de aplicación Web de az](/cli/azure/webapp/deployment/user#set) comando.

Un usuario de implementación es necesario para FTP y Git implementación tooa la aplicación web local. nombre de usuario de Hola y la contraseña son el nivel de cuenta. _Son diferentes de las credenciales de suscripción de Azure._

Hola siguiente comando, reemplace  *\<nombre de usuario >* y  *\<contraseña >* con un nuevo nombre de usuario y una contraseña. nombre de usuario de Hello debe ser único. Hello contraseña debe tener al menos ocho caracteres, con dos Hola después de tres elementos: letras, números y símbolos. 

```azurecli-interactive
az webapp deployment user set --user-name <username> --password <password>
```

Si se produce un ` 'Conflict'. Details: 409` error, el nombre de usuario de cambio Hola. Si se produce un error ` 'Bad Request'. Details: 400`, use una contraseña más segura.

Solo es necesario crear este usuario de implementación una vez, y puede usarlo en todas las implementaciones de Azure.

> [!NOTE]
> Nombre de usuario de Hola de registro y la contraseña. Necesite toodeploy hello web aplicación más tarde.
>
>