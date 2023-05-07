<template>
 <div class="bg-img"> 
      <div class="padding rounded-5px size-back  "> 
        <table class="table align-middle mb-0 bg-white border-radius ">
  <thead class="bg-light">
    <!-- <tr>
      <th>Name</th>
      <th>Title</th>
      <th>Status</th>

    </tr> -->
  </thead>
  <tbody>
    <tr>
      <td>
        <div class="d-flex align-items-center">
          <i class="uil uil-temperature font-icon-tempurature mr-icon"></i>
          <div class="ms-3">
            <p class="fw-bold mb-1 font-size-home  mr-icon">Temperatuture</p>
          </div>
        </div>
      </td>
      <td>
        <p class="fw-normal mb-1 size-value">{{ tempurature }}  <span> °C</span></p>
      </td>
      <td>
        <span class="badge badge-success rounded-pill d-inline">Active</span>
      </td>
    </tr>
    <tr>
      <td>
        <div class="d-flex align-items-center">
          <!-- <i class="fa-sharp fa-solid fa-wind font-icon-humid-air mr-icon" ></i> -->
            <i class="fa-solid fa-droplet font-icon-humid-air mr-icon"></i>
          <div class="ms-3">
            <p class="fw-bold mb-1 font-size-home  mr-icon">Humidity</p>
          </div>
        </div>
      </td>
      <td>
        <p class="fw-normal mb-1 size-value">{{ air_humid }}  <span> %</span></p>
      </td>
      <td>
        <span class="badge badge-primary rounded-pill d-inline"
              >Onboarding</span
          >
      </td>
    </tr>
    <tr>
      <td>
        <div class="d-flex align-items-center">
          <!-- <i class="fa-solid fa-droplet font-icon-humid-ground mr-icon"></i> -->
          <i class="uil uil-mountains font-icon-humid-ground mr-icon"></i>
          <div class="ms-3">
            <p class="fw-bold mb-1 font-size-home  mr-icon">Ground Humid</p>
          </div>
        </div>
      </td>
      <td>
        <p class="fw-normal mb-1 size-value">{{ground_humid}} <span> %</span></p>
      </td>
      <td>
        <span class="badge badge-warning rounded-pill d-inline">Awaiting</span>
      </td>

    
    </tr>
  </tbody>
</table>
      <div class="mt-home flex"> 
        <button class="btn  right watering" :class="[watering === 1 ? 'btn-danger' :  'btn-primary']" @click="watering_func"> Watering </button>
      </div>
      <div  class="time_show">  
        <span id="span" class="span-time"></span>
      </div>

      </div>

  
 </div>
    
</template>
    
<style>
.watering{
  padding: 20px;
}
.time_show {
  display: block;
    text-align: center;
}
.span-time {
  display: inline-block;
    margin-left: auto;
    margin-right: auto;
    text-align: left;
    background-color: white; 
    padding : 80px;
    border-radius: 10px;
    background-image: url(https://media.istockphoto.com/id/1176645523/vector/black-empty-clock-isolated-on-white-for-pattern-and-design.jpg?s=612x612&w=0&k=20&c=KbVtZd6GwY4H1qa1ynUSHPPHYiH_zh5-rwCA20YFK1U=) !important;
    background-position: center;
    background-size: 80%; 
    background-repeat: no-repeat
}
.mt-home{
  margin-top: 20px;

}
.bg-img{
  background-image: url(https://thuthuatnhanh.com/wp-content/uploads/2021/12/background-cay-xanh-dep-don-gian.jpg);
  background-repeat: no-repeat;
  background-size: 100%;
}
.padding{
  padding: 150px 300px !important;
  border-radius: 10px;
}
.font-icon-tempurature{
  font-size: 50px;
  color: red;
}
.font-icon-humid-ground{
  font-size: 45px;
  color: rgb(164, 79, 0);
  margin-left: 8px;
}
.font-icon-humid-air{
  font-size: 45px;
  color: rgb(74, 143, 255);
  margin-left: 8px;
}
.border-radius {
  border-radius: 10px !important;
}
.font-size-home{
  font-weight: 800;
  font-size: 20px;
}
.mr-icon{
  margin-right: 40px;
}
.size-value{
  font-weight: 700;
  font-size: 20px
}
</style>
  
    
    
    <script>
    
// Import the functions you need from the SDKs you need\

import firebase from 'firebase'
// TODO: Add SDKs for Firebase products that you want to use
// https://firebase.google.com/docs/web/setup#available-libraries

// Your web app's Firebase configuration
// For Firebase JS SDK v7.20.0 and later, measurementId is optional
const firebaseConfig = { 
  apiKey: "AIzaSyBruMJZszXjft9YogY27gAsM4MMFed9LEI",
  authDomain: "tsl-b2fdf.firebaseapp.com",
  databaseURL: "https://tsl-b2fdf-default-rtdb.europe-west1.firebasedatabase.app",
  projectId: "tsl-b2fdf",
  storageBucket: "tsl-b2fdf.appspot.com",
  messagingSenderId: "17640750701",
  appId: "1:17640750701:web:84dc35965bede867fdc964"
};

// Initialize Firebase

    let app = firebase.initializeApp(firebaseConfig)
    let db = app.database()
    let ref_test = db.ref('test')
    // Initialize Firebase
    
    // export const firestore = getFirestore(firebase)
    
    export default {
    
        data(){
            return{
                tempurature: 7,
                air_humid: 7,
                ground_humid: 7,
                watering: 0, 
                d: 0, 
                s:0,
                m:0 ,
                h:0
            }
        },  
        mounted(){
          var span = document.getElementById('span');

function time() {
  this.d = new Date();
  var s = d.getSeconds();
  var m = d.getMinutes();
  var h = d.getHours();
  span.textContent = 
    ("0" + h).substr(-2) + ":" + ("0" + m).substr(-2) + ":" + ("0" + s).substr(-2);
}

setInterval(time, 1000);

          const self = this;
        app.database()
            .ref('test')
            .on('value', function(snapshot) {
                // const id = snapshot.key;
    
                //----------OR----------//
                self.tempurature = snapshot.val().temp ;
                self.air_humid = snapshot.val().humid ;
                self.ground_humid = snapshot.val().ground;
                // if (data) {
                //   const id = Object.keys(data)[0];
                // }
            });
    
      }, 
      methods: {
    async watering_func(){
      if(this.watering ==1 ){
        this.watering = 0;
      }
      else  {
        this.watering = 1;
      }
      app.database()
            .ref('test').set({watering : this.watering})
      } 
    }
       
        // methods: function getData(){  
        // const starCountRef = ref(database,'posts/' + postId + '/starCount');
        // onValue(starCountRef, (snapshot) => {
        // const data = snapshot.val();
        // updateStarCount(count, data);
        // });
        // return starCountRef;
        // },
    
    }
    
    
      
    
    </script>
    