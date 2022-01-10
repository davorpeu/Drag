<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>Netgen</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content :fullscreen="true">
      <ion-grid>
        <ion-row>
          <ion-col size="1">
            <div>Menu</div>
            <ion-button
              class="menuItems"
              id="draggable"
              draggable="true"
              ondragstart="event.dataTransfer.setData('text/plain',null)"
              >Placeholder</ion-button
            >
            <ion-button
              class="menuItems"
              id="image"
              draggable="true"
              ondragstart="event.dataTransfer.setData('text/plain',null)"
              >Image</ion-button
            >
            <ion-button
              class="menuItems"
              id="text"
              draggable="true"
              ondragstart="event.dataTransfer.setData('text/plain',null)"
              >Text</ion-button
            >
          </ion-col>
          <ion-col size="10">
            <div class="dropzone">Upload</div>

            <ion-col> </ion-col>
          </ion-col>
          <ion-col size="1">
            <div class="delete">Delete</div>
          </ion-col>
        </ion-row>
      </ion-grid>
    </ion-content>
  </ion-page>
</template>


<script lang="js">
import {
  IonPage,
  IonHeader,
  IonToolbar,
  IonTitle,
  IonContent,
  // IonMenu, 
  // IonReorder,
  // IonReorderGroup,
} from "@ionic/vue";

// import { camera, trash, close, pizza } from "ionicons/icons";
import { defineComponent } from "vue";

export default defineComponent({
  order: 2,
  name: "Tab3",
  components: {
    IonPage,
    IonHeader,
    // IonMenu, 
    IonToolbar,
    IonTitle,
    IonContent,
    // IonReorder,
    // IonReorderGroup,
  },

 
});


let dragged;

document.addEventListener(
    "dragstart",
    function (event) {
        // store a ref. on the dragged elem
        dragged = event.target;
        // make it half transparent
        event.target.style.opacity = 0.5;
    },
    false
);

document.addEventListener(
    "dragend",
    function (event) {
        // reset the transparency
        event.target.style.opacity = "";
    },
    false
);

/* events fired on the drop targets */
document.addEventListener(
    "dragover",
    function (event) {
        // prevent default to allow drop
        event.preventDefault();
    },
    false
);

document.addEventListener(
    "dragenter",
    function (event) {
        // highlight potential drop target when the draggable element enters it
        if (event.target.className == "dropzone" || event.target.className == "delete" || event.target.className == "placeholder md hydrated") {
            event.target.style.background = "gray";
        }
    },
    false
);

document.addEventListener(
    "dragleave",
    function (event) {
        // reset background of potential drop target when the draggable element leaves it
        if (event.target.className == "dropzone") {
            event.target.style.background = "";
        }
    },
    false
);


     
      
// const input = this.$refs.fileInput
// const file = input.files
// if (file && file[0]) {
// const reader = new FileReader
// reader.onload = e => {
//   this.previewImage = e.target.result
//     }
//   reader.readAsDataURL(file[0])
//   this.$emit('input', file[0])
//   }
      
      


// const loadFile = function(event) {
//      const output = document.getElementById('output');
//      output.src = URL.createObjectURL(event.target.files[0]);
//      output.onload = function() {
//        URL.revokeObjectURL(output.src) // free memory
//      }
//  };

//  document.getElementById("imgInp").addEventListener("onchange", loadFile);



document.addEventListener(
    "drop",
    function (event) {
        // prevent default action (open as link for some elements)
        event.preventDefault();
        // Create text input
        if (event.target.className == "ion-inherit-color md hydrated" && dragged.id == "text") {
            const content = document.createElement("ion-card-content");
            const text = document.createElement("ion-input");
            content.appendChild(text)
          
            document.body.appendChild(content);
            event.target.appendChild(content);
        }
        // Create image input
        if (event.target.className == "ion-inherit-color md hydrated" && dragged.id == "image") {
            const content = document.createElement("ion-card-content");
            const input = document.createElement("input");
            const img = document.createElement("img");
            img.id = "output"
            // input.@change = "loadFile(event)"
            //  input.addEventListener('onchange', loadFile(event))
            input.id = "imgInp"
            input.type = "file"
            input.accept = "image/*"
            input.input = "pickFile"
            // input.ionChange = "loadFile(event)"
            // input.capture = "camera"
            // const label = document.createElement("label");
            // label.for="fileInput"
            input.appendChild(img)
            content.appendChild(input)
            document.body.appendChild(content);
            event.target.appendChild(content);
        }
        // Create  placeholder
        if (event.target.className == "dropzone" && dragged.id !== "image" && dragged.id !== "text") {
            event.target.style.background = "";
            const card = document.createElement("ion-card");
            const header = document.createElement("ion-card-header");

           card.className = "placeholder"
            // card.className = ""
            card.draggable = "true"
            card.appendChild(header)
            card.innerHtml = header
            document.body.appendChild(card);
            
            event.target.appendChild(card);
            
            // dragged.parentNode.removeChild(dragged);
            // event.target.appendChild(dragged);
        }
        if (event.target.className == "delete") {
            event.target.style.background = "";
            
             dragged.parentNode.removeChild(dragged);
            //  event.target.appendChild(dragged);
           
 
        }
    },
    false
);



</script>
<style scoped>
#draggable {
  width: 200px;
  height: 20px;
  text-align: center;
  background: black;
}

.dropzone {
}
.menuItems {
  max-width: 100%;
  width: 200px;
  height: 20px;
  text-align: center;
  background: black;
}
.image {
  max-width: 100%;
}
.test {
  border: 2 px dashed #bbb;
  -moz-border-radius: 5px;
  -webkit-border-radius: 5 px;
  border-radius: 5 px;
  padding: 25 px;
  text-align: center;
  font: 20pt bold "Vollkorn";
  color: #bbb;
}
</style>
