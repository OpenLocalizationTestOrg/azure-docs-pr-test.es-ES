## <a name="push-to-azure-from-git"></a><span data-ttu-id="e09c7-101">Inserción en Azure desde Git</span><span class="sxs-lookup"><span data-stu-id="e09c7-101">Push to Azure from Git</span></span>

<span data-ttu-id="e09c7-102">Agregue una instancia remota de Azure en el repositorio de Git local.</span><span class="sxs-lookup"><span data-stu-id="e09c7-102">Add an Azure remote to your local Git repository.</span></span>

```bash
git remote add azure <URI from previous step>
```

<span data-ttu-id="e09c7-103">Inserte en la instancia remota de Azure para implementar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e09c7-103">Push to the Azure remote to deploy your app.</span></span> <span data-ttu-id="e09c7-104">Se le pedirá la contraseña que proporcionó anteriormente al crear el usuario de implementación.</span><span class="sxs-lookup"><span data-stu-id="e09c7-104">You are prompted for the password you created earlier when you created the deployment user.</span></span> <span data-ttu-id="e09c7-105">Asegúrese de escribir la contraseña que creó en [Configuración de un usuario de implementación](#configure-a-deployment-user), no la contraseña que usa para iniciar sesión en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="e09c7-105">Make sure that you enter the password you created in [Configure a deployment user](#configure-a-deployment-user), not the password you use to log in to the Azure portal.</span></span>

```bash
git push azure master
```

<span data-ttu-id="e09c7-106">El comando anterior muestra información similar a la del ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="e09c7-106">The preceding command displays information similar to the following example:</span></span>
