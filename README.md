![](/assets/smart_invs.png)

## SmartInvs

SmartInvs is a modern API for easily using inventories with Bukkit to make awesome GUIs. This book contains a guide on how to use this API to create your own amazing GUIs!

_This API requires Java 8 to work._

---

### Features

* Inventories of any type \(workbench, chest, furnace, ...\)
* Customizable size when possible \(chest, ...\)
* Custom titles
* Allows to prevent the player from closing its inventory
* Custom listeners for the event related to the inventory
* Iterator for inventory slots
* Page system
* Util methods to fill an inventory's row/column/borders/...
* Actions when player clicks on an item
* Update methods to edit the content of the inventory every tick

### Preview

Here is a simple preview of an inventory.

```java
public class SimpleInventory implements InventoryProvider {

    public static final SmartInventory INVENTORY = SmartInventory.builder()
            .id("myInventory")
            .provider(new SimpleInventory())
            .size(3, 9)
            .title(ChatColor.BLUE + "My Awesome Inventory!")
            .build();

    private final Random random = new Random();

    @Override
    public void init(Player player, InventoryContents contents) {
        contents.fillBorders(ClickableItem.empty(new ItemStack(Material.STAINED_GLASS_PANE)));

        contents.set(1, 1, ClickableItem.of(new ItemStack(Material.CARROT_ITEM),
                e -> player.sendMessage(ChatColor.GOLD + "You clicked on a potato.")));

        contents.set(1, 7, ClickableItem.of(new ItemStack(Material.BARRIER),
                e -> player.closeInventory()));
    }

    private int ticks = 0;

    @Override
    public void update(Player player, InventoryContents contents) {
        if(++ticks % 5 != 0)
            return;

        short durability = (short) random.nextInt(15);

        ItemStack glass = new ItemStack(Material.STAINED_GLASS_PANE, 1, durability);
        contents.fillBorders(ClickableItem.empty(glass));
    }

}
```

And there is the result:

![](/assets/444ecfe1e103b.gif)

If we click on the carrot, we receive the message `You clicked on a potato`,
and if we click on the barrier, the inventory is closed.

<hr>