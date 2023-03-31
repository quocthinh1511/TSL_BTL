<template>


    <div> {{ count }}</div>
    
    </template>
    
    
    
    
    
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
                count: 7,
            }
        },  
        mounted(){
          const self = this;
        app.database()
            .ref('test')
            .on('value', function(snapshot) {
                // const id = snapshot.key;
    
                //----------OR----------//
                self.count = snapshot.val().int || null;
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
    