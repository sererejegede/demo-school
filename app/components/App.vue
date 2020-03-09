<template>
	<Page>
		<StackLayout>
			<Button horizontalAligment="center" text="Login Page" @tap="goToLogin" ></Button>	
		</StackLayout>
	</Page>
</template>

<script lang="ts">
	import Login from './Login/Login.vue';

  export default {
    data() {
      return {
        msg: 'Hello World!'
      }
		},
		methods: {
			goToLogin() {
				this.$navigateTo(Login)
			}
		}
  }
</script>

<style scoped>
	
</style>
