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
          <i class="fa-sharp fa-solid fa-wind font-icon-humid-air mr-icon" ></i>
          <div class="ms-3">
            <p class="fw-bold mb-1 font-size-home  mr-icon">Air humidity</p>
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
          <i class="fa-solid fa-droplet font-icon-humid-ground mr-icon"></i>
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
        <button class="btn btn-primary right watering"> Watering </button>
      </div>
      </div>

  
 </div>
    
</template>
    
<style>
.watering{
  padding: 20px;
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
  color: rgb(31, 115, 250);
  margin-left: 8px;
}
.font-icon-humid-air{
  font-size: 45px;
  color: rgb(167, 195, 241);
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
  apiKey : "AIzaSyBo7uyi84oE9I6jIHVkyIny2hPKiVX5LGk" , 
  authDomain : "tslproject-959c3.firebaseapp.com" , 
  databaseURL : "https://tslproject-959c3-default-rtdb.firebaseio.com" , 
  projectId : "tslproject-959c3" , 
  storageBucket : "tslproject-959c3.appspot.com" , 
  messagingSenderId : "113915189951" , 
  appId : "1:113915189951:web:8f3d1a0a70561ac716040a" , 
  measurementId : "G-QPBMRW6XEX" 
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
            }
        },  
        mounted(){
          const self = this;
        app.database()
            .ref('test')
            .on('value', function(snapshot) {
                // const id = snapshot.key;
    
                //----------OR----------//
                self.tempurature = snapshot.val().int || null;
                self.air_humid = snapshot.val().air_humid || null;
                self.ground_humid = snapshot.val().ground_humid || null;
                // if (data) {
                //   const id = Object.keys(data)[0];
                // }
            });
    
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
    