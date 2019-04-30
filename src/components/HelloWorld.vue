<template>
  <div class="demo">
    <provide-and-city ref='provideAndCitys' @proviceAndCity="proviceAndCity"></provide-and-city>
  </div>
</template>

<script>
import provideAndCity from "./e-provice-and-city-pc/index";

export default {
  name: "index",
  components: {
    provideAndCity
  },
  data() {
    return {
      msg: ""
    };
  },
	created(){
		// this.getAddress('1','1')
	},
	mounted(){
		this.getAddress('','')
	},
	methods:{
		proviceAndCity(val){
			this.getAddress(val.typeAdnId.id , val.typeAdnId.type)
		},
		getAddress(id , type){
			// this.$axios('aaaa',{param:param}).then(res => {
				// this.$refs.provideAndCity.getAddressList(id , type , res)
				this.$refs.provideAndCitys.getAddressList(id , type)
			// })
		}
	}
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1,
h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
