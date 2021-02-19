<script>
	import { DropList, DragHandle } from 'svelte-reactive-dnd';
	export let items;
	export let identifier = undefined;
	
	const overrideDropPosition = (dragTarget, items) => {
		if (items.length === 0) {
			return { 
				index: 0, 
				placement: 'before', 
				scrollIntoView: true 
			};
		}
		const dragTitle = dragTarget.item.title;
		const index = items.findIndex((item) => {
			return item.title.localeCompare(dragTitle) >= 0;
		});
		console.log(dragTitle, index);
		return { 
			index: index === -1 ? items.length - 1 : index, 
			placement: index === -1 ? 'after' : 'before', 
			scrollIntoView: true 
		};
	};
	
</script>
	<div class="list">
	 <DropList
		{identifier}
		{items}
		{overrideDropPosition}
	 >
		 <div slot="listItem" let:data="{{ item }}">
			 <DragHandle itemId="{item.id}" disabled={item.disabled}>
				 <div class="item">
					 <p>{item.title}</p>
				 </div>
			 </DragHandle>
		 </div>
	</DropList>
</div>

<style>
    .list {
        height: 200px;
        width: 100px;
        border: solid black 1px;
        background-color: grey;
    }
    .item {
        margin: 2px;
				width: 78px;
        padding: 0px 8px;
        border: solid black 1px;
        background-color: burlywood;
    }
</style> 