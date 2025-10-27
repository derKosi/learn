One of the main tasks you'll want to do while running virtual machines is to start and stop them.

[!INCLUDE[](../../../includes/azure-optional-exercise-subscription-note.md)]

[!INCLUDE[](../../../includes/azure-cloud-shell-terminal-note.md)]

> [!NOTE]
> Throughout this exercise, replace **myResourceGroupName** in the examples with the name of an existing resource group, or the name of the resource group that you created for this exercise.

## Stop a VM

We can stop a running VM with the `vm stop` command. You must pass the name and resource group or the unique ID for the VM:

```azurecli
az vm stop \
    --name SampleVM \
    --resource-group "myResourceGroupName"
```

You can verify the VM has stopped by attempting to ping the public IP address, using `ssh`, or through the `vm get-instance-view` command. This final approach returns the same basic data as `vm show`, but includes details about the instance itself. Try entering the following command into Azure Cloud Shell to see the current running state of your VM:

```azurecli
az vm get-instance-view \
    --name SampleVM \
    --resource-group "myResourceGroupName" \
    --query "instanceView.statuses[?starts_with(code, 'PowerState/')].displayStatus" -o tsv
```

This command should return `VM stopped` as the result.

## Start a VM

We can do the reverse through the `vm start` command.

```azurecli
az vm start \
    --name SampleVM \
    --resource-group "myResourceGroupName"
```

This command starts a stopped VM. You can verify it through the `vm get-instance-view` query you used in the last section, which should now return `VM running`.

## Restart a VM

Finally, we can restart a VM if we've made changes that require a reboot by running the `vm restart` command. You can add the `--no-wait` flag if you want the Azure CLI to return immediately without waiting for the VM to reboot.
