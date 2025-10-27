Let's start with the most obvious task: creating an Azure Virtual Machine.

[!INCLUDE[](../../../includes/azure-optional-exercise-subscription-note.md)]

[!INCLUDE[](../../../includes/azure-optional-exercise-create-resource-group-note.md)]

[!INCLUDE[](../../../includes/azure-cloud-shell-terminal-note.md)]

> [!NOTE]
> Throughout this exercise, replace **myResourceGroupName** in the examples with the name of an existing resource group, or the name of the resource group that you created for this exercise.

## Create a Linux VM with the Azure CLI

The Azure CLI includes the `vm` command to work with virtual machines in Azure. We can supply several subcommands to do specific tasks. The most common include:

| Sub-command | Description |
|-------------|-------------|
| `create`    | Create a new virtual machine |
| `deallocate` | Deallocate a virtual machine |
| `delete` | Delete a virtual machine |
| `list` | List the created virtual machines in your subscription |
| `open-port` | Open a specific network port for inbound traffic |
| `restart` | Restart a virtual machine |
| `show` | Get the details for a virtual machine |
| `start` | Start a stopped virtual machine |
| `stop` | Stop a running virtual machine |
| `update` | Update a property of a virtual machine |

> [!NOTE]
> For a complete list of commands, you can check the [Azure CLI reference documentation](/cli/azure/reference-index).

Let's start with the first one: `az vm create`. You can use this command to create a virtual machine in a resource group. There are several parameters you can pass to configure all the aspects of the new VM. The four parameters that you must supply are:

> [!div class="mx-tableFixed"]
> | Parameter | Description |
> |-----------|-------------|
> | `--resource-group` | The resource group that will own the virtual machine; use **myResourceGroupName**. |
> | `--name` | The name of the virtual machine; must be unique within the resource group. |
> | `--image` | The operating system image to use to create the VM. |
> | `--location` | The region in which to place the VM. Typically, this would be close to the VM's consumer. |

In addition, it's helpful to add the `--verbose` flag to see progress while the VM is being created.

## Create a Linux virtual machine

Let's create a new Linux virtual machine. Execute the following command in Azure Cloud Shell to create an Ubuntu VM in the *West US* location.

```azurecli
az vm create \
  --resource-group "myResourceGroupName" \
  --location westus \
  --name SampleVM \
  --image Ubuntu2204 \
  --admin-username azureuser \
  --generate-ssh-keys \
  --verbose 
```

[!INCLUDE[](../../../includes/azure-cloudshell-copy-paste-tip.md)]

This command creates a new **Ubuntu** Linux virtual machine with the name `SampleVM`. Notice that the Azure CLI tool waits while the VM is being created. You can add the `--no-wait` option to tell the Azure CLI tool to return immediately and have Azure continue creating the VM in the background. This is useful if you're executing the command in a script.

We're specifying the administrator account name through the `--admin-username` flag to be `azureuser`. If you omit this, the `az vm create` command will use your *current user name*. Because the rules for account names are different for each OS, it's safer to specify a specific name.

> [!NOTE]
> Common names such as "root" and "admin" aren't allowed for most images.

We're also using the `generate-ssh-keys` flag. Linux distributions use this parameter, and it creates a pair of security keys so we can use the `ssh` tool to access the virtual machine remotely. The two files are placed into the `.ssh` folder on your machine and in the VM. If you already have an SSH key named `id_rsa` in the target folder, then that SSH key will be used rather than generating a new key.

Once Azure CLI finishes creating the VM, you'll get a JSON response which includes the current state of the virtual machine and its public and private IP addresses assigned by Azure:

```json
{
  "fqdns": "",
  "id": "/subscriptions/aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e/resourceGroups/Learn-bbbb1b1b-cc2c-dd3d-ee4e-ffffff5f5f5f/providers/Microsoft.Compute/virtualMachines/SampleVM",
  "location": "westus",
  "macAddress": "00-0D-3A-58-F8-45",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "40.83.165.85",
  "resourceGroup": "bbbb1b1b-cc2c-dd3d-ee4e-ffffff5f5f5f",
  "zones": ""
}
```
