<template>
    <div class="category-checkboxes">
        <input type="checkbox" :id="cat" :value="cat" />
		<label :for="cat">{{cat}}</label>
    </div>
</template>

<script>
export default {
    name: "CheckBox",
    props: {
		cat: String
	}
		

	
};
</script>

<style>
	.category-checkboxes {
		margin: 0 5px;
	}
</style>
