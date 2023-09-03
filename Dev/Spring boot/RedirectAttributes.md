---
tags:
  - spring
Created Time: 2023-03-09T23:20
---
##### <font color="#2DC26B">Related Links</font>
___


```java
@PostMapping("/add")  
public String addItemV6(Item item, RedirectAttributes redirectAttributes) {  
    Item savedItem = itemRepository.save(item);  
    redirectAttributes.addAttribute("itemId", savedItem.getId());  
    redirectAttributes.addAttribute("status", true);  
    return "redirect:/basic/items/{itemId}";  
}
```
