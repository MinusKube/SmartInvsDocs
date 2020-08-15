# 5. Inventory Openers

`InventoryOpener` is an interface used by SmartInvs to open the inventories. When an inventory is trying to be opened for a player, the `InventoryManager` will try to find an `InventoryOpener` that supports the `InventoryType` of the inventory, if no opener is found, the inventory will not be opened and an exception will be thrown.

This is the list of the InventoryOpeners currently supported by SmartInvs:

| Name | Supported Types |
| :--- | :--- |
| ChestInventoryOpener | `CHEST`, `ENDER_CHEST` |
| SpecialInventoryOpener | `FURNACE`, `WORKBENCH`, `DISPENSER`, `DROPPER`,   `ENCHANTING`, `BREWING`, `ANVIL`, `BEACON`, `HOPPER` |

## Adding an Inventory Opener

If the inventory type you need to open is not supported by default, you can define your own support by creating a new Inventory Opener, to do this, you need to implement the `InventoryOpener` interface, like this:

```java
public class CustomInventoryOpener implements InventoryOpener {

    @Override
    public Inventory open(SmartInventory inv, Player player) {
        InventoryManager manager = SmartInvsPlugin.manager();
        Inventory handle = Bukkit.createCustomInventory(player, inv.getRows() * inv.getColumns(), inv.getTitle());

        fill(handle, manager.getContents(player).get());

        player.openInventory(handle);
        return handle;
    }

    @Override
    public boolean supports(InventoryType type) {
        return type == InventoryType.CUSTOM;
    }

}
```

_\(The InventoryType.CUSTOM and the Bukkit.createCustomInventory methods don't exist, it's just for the example\)_

Then, when your `InventoryOpener` is done, register it using:

```java
SmartInvsPlugin.manager().registerOpeners(new CustomInventoryOpener());
```

And it's all, now SmartInvs will handle all the other things for you!

