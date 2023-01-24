<script>
    let items = [
      { id: 1, name: "Item 1" },
      { id: 2, name: "Item 2" },
      { id: 3, name: "Item 3" }
    ];
  
    let selected;
  
    function handleDragStart(event) {
      selected = event.target.dataset.item;
    }
  
    function handleDrop(event) {
      event.preventDefault();
      let target = event.target.dataset.item;
      let selectedIndex = items.findIndex(i => i.id === selected);
      let targetIndex = items.findIndex(i => i.id === target);
      items.splice(targetIndex, 0, items.splice(selectedIndex, 1)[0]);
    }
  </script>
  
  <div on:dragstart={handleDragStart} on:drop={handleDrop} on:dragover={event => event.preventDefault()}>
    {#each items as item}
      <div data-item={item.id} draggable>
        {item.name}
      </div>
    {/each}
  </div>
  