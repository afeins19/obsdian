# ViewHolder Creation
```kotlin 
override fun onCreateViewHolder(parent: ViewGroup, viewType: Int): ItemViewHolder {  
    val view = LayoutInflater.from(parent.context).inflate(R.layout.activity_list_view, parent, false)  
    return ItemViewHolder(view)  
}
```
- The Viewholder is created for each visible ui item in the RecyclerView. Its made every time we call onCreateViewHolder. That holds references to the textviews, buttons, etc. for each items layout
- *we dont create a viewholder for every item. the recyclerview is made to be efficient so we only create viewholders for items on the screen (and a few extra for buffer). As the user scrolls, the RecyclerView reuses the viewholders that were created and need to be dispalyed*

# Data Binding
```Kotlin 
override fun onBindViewHolder(holder: ItemViewHolder, position: Int) {  
    val item: TextView = holder.itemView.findViewById(R.id.itemName)  
    val quantity: TextView = holder.itemView.findViewById(R.id.itemQuantity)  
    holder.itemView.apply {  
        item.text = items[position].name  
        quantity.text = items[position].quantity.toString()  
    }  
    holder.itemView.findViewById<Button>(R.id.itemDeleteButton).setOnClickListener {  
        // Notify the main activity or whoever is listening about the deletion  
        itemListener.onItemDelete(position)  
    }  
}
```
- when an item is about to be displayed OR its data has changed, the onBindViewHolder() method is called. Data from the Item object is bound to specific views of the viewholder (items name text gets bound to the itemname textview and items quantity text gets bound to a quantity textview). 
- when something goes off the screen, the recyclerview lets itemadapter know of this and onBindViewHolder allocates a new items data to that view so we dont have to create a new one from scratch! 