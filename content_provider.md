# Content Provider

Now, you maybe want to know how to put items in your new inventory.
To do that, you'll need to create a new InventoryProvider.

InventoryProvider is an interface, so you just need to implements it, example:
```java
public class MyProvider implements InventoryProvider {

    @Override
    public void init(Player player, InventoryContents contents) {}

    @Override
    public void update(Player player, InventoryContents contents) {}

}
```

Here, the method `init` will be called when an inventory is opened for the player, and the method `update` will be called every tick for the players with the inventory opened.

To put the items in the inventory, you just have to use the methods of the given `InventoryContents`, like `fillRow(row, item)`. Theses methods requires a `ClickableItem`, which is just an `ItemStack` combined with a `Consumer<InventoryClickEvent>`.

To create a `ClickableItem`, you just have to use `ClickableItem.of(ItemStack, Consumer<InventoryClickEvent>)`, or `Clickable.empty(ItemStack)` to create an item with an empty consumer, example:
```java
ClickableItem item = ClickableItem.of(new ItemStack(Material.POTATO_ITEM, 2), e -> {
    Bukkit.broadcastMessage(ChatColor.DARK_AQUA + "A potato has been clicked");
});
```

### Example
```java
public class MyProvider implements InventoryProvider {

    @Override
    public void init(Player player, InventoryContents contents) {
        
    }
    
    @Override
    public void update(Player player, InventoryContents contents) {
    
    }

}
```