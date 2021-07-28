<template>
  <div class="about">
    <h1>This is an about page</h1>
    <div><button class="px-6 py-2 text-white bg-green-700 rounded hover:bg-green-900" @click="fetchItems">Retrieve GET Method</button></div>
    <div><button class="px-6 py-2 text-white bg-green-700 rounded hover:bg-green-900" @click="fetchItem">Retrieve GET One Item</button></div>
   <div><button class="px-6 py-2 text-white bg-green-700 rounded hover:bg-green-900" @click="fetchItemsPostMethod">Retrieve Post Method</button></div>
  </div>
</template>

<script>


export default {
  name: 'About',
  components: {
  },
  methods:{
    async alertMothod(){
      alert("Made it");
    },
    data() {
    return {
      section: "About",
      post: [],
    }
    },
    async fetchItems(){
      try {      
          const requestOptions = {
            method: "GET",
            headers: { "Content-Type": "application/json" },
          };

          fetch("https://localhost:44360/api/values", requestOptions)
            .then(async response =>{
              const data = await response.json()
              console.log("Data From endpoint:", data)

              // check for error response
              if (!response.ok) {
                // get error message from body or default to response status
                const error = (data && data.message) || response.status;
                return Promise.reject(error);
              }

              this.post= data;
                        
            })
      }catch(err){
        if (err.response) {
          // client received an error response (5xx, 4xx)
          console.log("Server Error:", err)
        } else if (err.request) {
          // client never received a response, or request never left
          console.log("Network Error:", err)
        } else {
          console.log("Client Error:", err)
        }
      }
    },
    async fetchItem(){
      try {      
          const requestOptions = {
            method: "GET",
            headers: { "Content-Type": "application/json" },
          };

          fetch("https://localhost:44360/api/values/value1", requestOptions)
            .then(async response =>{
              const data = await response.text()
              console.log("Data From endpoint:", data)

              // check for error response
              if (!response.ok) {
                // get error message from body or default to response status
                const error = (data && data.message) || response.status;
                return Promise.reject(error);
              }

              this.post= data;
                        
            })
      }catch(err){
        if (err.response) {
          // client received an error response (5xx, 4xx)
          console.log("Server Error:", err)
        } else if (err.request) {
          // client never received a response, or request never left
          console.log("Network Error:", err)
        } else {
          console.log("Client Error:", err)
        }
      }
    },
    async fetchItemsPostMethod(){
      try {      
          const requestOptions = {
            method: "POST",
            headers: {'Content-Type': 'application/json'},
            body: JSON.stringify('{ values: "value7" }')
          };

         fetch("https://localhost:44360/api/values/", requestOptions)
            .then( async response =>{
              const data =  await response.json()
              console.log("Data From endpoint:", data)

              // check for error response
              if (!response.ok) {
                // get error message from body or default to response status
                const error = (data && data.message) || response.status;
                return Promise.reject(error);
              }
              
              this.post= data;
                        
            })
      }catch(err){
        if (err.response) {
          // client received an error response (5xx, 4xx)
          console.log("Server Error:", err)
        } else if (err.request) {
          // client never received a response, or request never left
          console.log("Network Error:", err)
        } else {
          console.log("Client Error:", err)
        }
      }
    }
  }
}
</script>
