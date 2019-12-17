<template>
   <transition name="modal">
      <div v-if="status">
        <div class="overlay" @click='$emit("close",status=false);'>
           <!-- Modal -->
            <div class="modal-dialog modal-dialog-centered  "  role="document">
                <div class="modal-content">
                <div class="modal-header">
                    <h5 class="modal-title" id="exampleModalCenterTitle">Modal title</h5>
                    <button type="button" class="close" data-dismiss="modal" aria-label="Close" @click='changeStatus();'>
                    <span aria-hidden="true">&times;</span>
                    </button>
                </div>
                <div class="modal-body"> 
                    <p>Are you sure you ?</p>  
                </div>
                <div class="modal-footer">
                    <button type="button" class="btn btn-secondary" data-dismiss="modal" @click='changeStatus();' >Close</button>
                    <button type="button" class="btn btn-primary" @click='changeStatus()'>Add</button>
                </div>
                </div>
            </div>
        </div>
      </div>
    </transition>
</template>


<script>
   export default{
       name: "ModalFav",
       props: {
            status: Boolean
       },
       methods: {
         changeStatus() {
            let modalStatus = this.status;
            modalStatus = false;
            this.$emit("close", modalStatus);
         }
       }
     
   }
</script>


<style scoped>
.modalstyle {
  width: 500px;
  margin: 0px auto;
  padding: 20px;
  background-color: #fff;
  border-radius: 2px;
  box-shadow: 0 2px 8px 3px;
  transition: all 0.2s ease-in;
  font-family: Helvetica, Arial, sans-serif;
}
.fadeIn-enter {
  opacity: 0;
}

.fadeIn-leave-active {
  opacity: 0;
  transition: all 0.2s step-end;
}

.fadeIn-enter .modal,
.fadeIn-leave-active.modal {
  transform: scale(1.1);
}


.overlay {
  position: fixed;
  top: 0;
  left: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 100%;
  background: #00000094;
  z-index: 999;
  transition: opacity 0.2s ease;
}

.modal-content {
   
    width: 500px;
}
</style>