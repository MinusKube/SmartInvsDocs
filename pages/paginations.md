# Paginations

With the pagination systeme of SmartInvs, you can easily create pages for your inventories.

### Get a Pagination
To get the Pagination object of your `InventoryContents`, simply call its `pagination()` method.

### Use a Pagination
Now, we'll see how to use this pagination in our inventory.

First, we need to set some informations for our pagination:
...

Okay, let's see the available getters:

| Method Name   | Description  |
| ------------- |:-------------|
| getPage       | Returns the actual page |
| getPageItems  | Returns the items for the actual page, the returned array will always be of the size of the pagination's items per page   |
| isFirst       | Returns true if the actual page is the first page, else it returns false |
| isLast        | Returns true if the actual page is the first page for the given items, else it returns false                             |

To change the actual page, several methods are availables:
* `first()` to set the page to the first
* `last()` to set the page to the last non-empty
* `previous()` to go one page backward, if possible
* `next()` to go one page forward, if possible