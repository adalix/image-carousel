<template>
	<div class="w-full mx-auto mt-10 ">
		<div
			class="flex flex-col items-center relative "
		>
			<div class="flex items-center justify-center absolute top-2/4 left-40 h-10 w-10 bg-gray-700 rounded-full hover:bg-gray-500">
				<ArrowLeftIcon
				@click="previousImage"
				class=" text-white h-6 w-6 cursor-pointer"
			/>
			</div>
			
			
			<h1 class="mb-3 font-semibold text-2xl">{{ currentImage().name }}</h1>
			<img
				class="w-[1200px] h-[640px] bg-fixed object-cover rounded-lg border-8 border-white "
				:src="currentImage().url"
				alt=""
			/>
			<div class="flex items-center">

				<button v-for="(item, index) in images" :key="item.id"
					class="w-[10px] h-[10px] mt-6 mx-1 bg-gray-400 rounded-full transition-all duration-500 ease-in hover:w-[25px] hover:bg-blue-700"
					@click="currentIndex = index"
					:class="{'w-[25px] bg-blue-700': currentIndex===index}"
				></button>	
			</div>

			<div class="flex items-center justify-center absolute top-2/4 right-40 h-10 w-10 bg-gray-700 rounded-full hover:bg-gray-500">
				<ArrowRightIcon
				@click="nextImage"
				class=" text-white h-6 w-6 cursor-pointer"
			/>
			</div>
		</div>
	</div>
</template>

<script>
import { ArrowRightIcon, ArrowLeftIcon } from "@heroicons/vue/24/outline";
import { ref } from "vue";
export default {
	components: { ArrowRightIcon, ArrowLeftIcon },
	setup() {
		const currentIndex = ref(0);
		const images = ref([
			{
				id: 1,
				name: "Galaxy",
				url: "/src/assets/galaxy.jpg",
			},
			{ id: 2, name: "View", url: "/src/assets/view.jpg" },
			{
				id: 3,
				name: "Hookah",
				url: "/src/assets/hookah.jpg",
			},
			{
				id: 4,
				name: "Cloud",
				url: "/src/assets/cloud.jpg",
			},
		]);

		const currentImage = () => {
			return images.value[currentIndex.value];
		}

		const previousImage = () => {
			if (currentIndex.value === 0) {
				currentIndex.value = images.value.length -1;
			} else {
				currentIndex.value = currentIndex.value -1;
			}
		}

		

		const nextImage = () => {
			if (currentIndex.value === images.value.length -1) {
				currentIndex.value = 0;
			} else {
				currentIndex.value = currentIndex.value +1;
			}			
			
		}

		console.log(setInterval(nextImage, 5000));

		return {
			images,
			ArrowLeftIcon,
			ArrowRightIcon,
			previousImage,
			nextImage,
			currentImage,
			currentIndex,
		};
	},
};
</script>

<style scoped></style>
