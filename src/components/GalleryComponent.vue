<template>
	<div class="page-box">
		<span class="gallery-intro">
			Morbi faucibus dolor nec efficitur consectetur. In hac habitasse platea
			dictumst. Pellentesque feugiat risus non ipsum facilisis, ut bibendum enim
			vulputate. Proin nec rhoncus eros, vitae vehicula elit. Vestibulum at
			ipsum ac justo feugiat pharetra sed id quam. Nulla eu tellus sollicitudin,
			tincidunt ex et, egestas lectus. Pellentesque bibendum erat ac dapibus
			venenatis. Aenean vel est id tortor posuere congue. Aliquam convallis et
			metus quis pharetra. Sed tortor nisi, laoreet vitae dolor quis, ultricies
			vehicula massa.
		</span>
		<div class="card" v-for="member of members" :key="member.id">
			<router-link :to="'/details/' + member.id" 
				><div class='blue-box'><img
					class="shane"
					src="@/assets/sudheer.webp"
					alt="avatar"
					style="width: 100%"
			/></div></router-link>
			<div class="nameAndTitle">
				<h4 class="memName">
					<b>{{ member.firstName }}</b>
				</h4>
				<h4 class="memTitle">{{ member.title }}</h4>
			</div>
		</div>
	</div>

</template>

<script>
import { UserService } from "@/services/UserServices";

export default {
	name: "GalleryComponent",
	data() {
		return {
			loading: false,
			members: [],
			errorMessage: null,
		};
	},

	created: async function () {
		try {
			this.loading = true;
			let response = await UserService.getAllMembers();
			this.loading = false;
			this.members = response.data;
		} catch (error) {
			this.loading = false;
			this.errorMessage = error;
		}
	},

	/*computed: {
		sortedArray() {
			let sortedMembers = this.members;
			sortedMembers = sortedMembers.sort((a,b) => {
				let fa = a.firstName.toLowerCase(), fb = b.firstName.toLowerCase();
				if (fa < fb) {
					return -1
				}
				if (fa > fb) {
					return 1
				}
				return 0
				})
		}
	}*/
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Poppins&display=swap");

.page-box {
	display: flex;
	flex-wrap: wrap;
	justify-content: space-between;
	gap: 20px;
	padding-left: 10%;
	padding-right: 10%;
	padding-bottom: 10%;
	font-family: "Poppins", sans-serif;
}

.gallery-intro {
	width: 100%;
	text-align: center;
	padding-top: 10vh;
	padding-bottom: 12vh;
	font-size: 20px;
}

.card {
	transition: 0.3s;
	width: 300px;

}

.shane {
	transition: 0.3s;
	width: 100%;

}
.shane:hover{
	box-shadow: 10px 10px 30px 0px rgba(5, 17, 22, 0.15);
	transform: scale(1.07);
	background-color: grey;
}

.nameAndTitle {
	text-align: center;
}

.memName {
	font-size: 18px;
	margin-top: 5px;
	margin-bottom: 0;
}

.memTitle {
	font-size: 16px;
	font-weight: 600;
	color: gray;
	margin-top: 1px;
	margin-bottom: 0;
}

.blue-box{
	width: 300px;
	height: 300px;
	overflow: hidden;
	border-radius: 10px;


}

</style>
