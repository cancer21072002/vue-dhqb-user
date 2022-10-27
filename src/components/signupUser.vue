<template>
    <div>
        <b-button v-b-modal.modal-prevent-closing>Signup</b-button>
       

        <b-modal id="modal-prevent-closing" ref="modal" title="SignUp" @show="resetModal" @hidden="resetModal"
            @ok="handleOk">
            <form ref="form" @submit.stop.prevent="handleSubmit">

                <b-form-group label="Name" invalid-feedback="Name is required"
          :state="nameState">
                    <b-form-input  v-model="user.name"  :state="nameState"
            required></b-form-input>
                </b-form-group>

                <b-form-group label="Age" invalid-feedback="Age is required"
          :state="nameState" >
                    <b-form-input  v-model="user.age"  :state="nameState" required></b-form-input>
                </b-form-group>

                <b-form-group label="Password" invalid-feedback="Password is required"
          :state="nameState">
                    <b-form-input v-model="user.pass" :state="nameState" required></b-form-input>
                </b-form-group>

                <b-form-group label="Phone" invalid-feedback="Phone is required"
          :state="nameState" >
                    <b-form-input  v-model="user.phone" :state="nameState" required></b-form-input>
                </b-form-group>

                <b-form-group label="Email" invalid-feedback="Email is required"
          :state="nameState">
                    <b-form-input  v-model="user.email" :state="nameState" required></b-form-input>
                </b-form-group>

                <b-form-group label="Date" invalid-feedback="Date is required"
          :state="nameState" >
                    <b-form-input  v-model="user.date"  type="date" :state="nameState" required></b-form-input>
                </b-form-group>

                <b-form-group label="Gender" invalid-feedback="Gender is required"
          :state="nameState" >
                <select id="gender" :state="nameState" v-model="user.gender">
                    <option >Men</option>
                    <option >Women</option>
                
                </select>
                </b-form-group>

                <b-form-group label="Address" invalid-feedback="Address is required"
          :state="nameState">
                    <b-form-input  v-model="user.address" :state="nameState" required></b-form-input>
                </b-form-group>

                
            </form>
        </b-modal>
    </div>
</template>

<script>
export default {
    props:{
        edit:{
            type:Object,
            default:null
        }
    },
    watch:{
        edit(){
            if(this.edit){
                this.user=Object.assign({},this.edit)
            }else{
                this.user={}
            }
        }
    },
    data () {
        return {
            user:{
                id:Math.floor(Math.random()*1000),
                name: '',
                age: '',
                email: '',
                phone: '',
                gender: '',
                
                address: '',
                date: '',
                pass:''

            },
            name: '',
            nameState: null,
            submittedNames: []
        }
    },
    methods: {
        checkFormValidity () {
            const valid = this.$refs.form.checkValidity()
            this.nameState = valid
            return valid
        },
        resetModal () {
            this.name = ''
            this.nameState = null
        },
        handleOk (bvModalEvent) {
            
            console.log(this.user);

            this.$emit("submit",this.user)


            this.user = {
                id: Math.floor(Math.random() * 1000),
                name: '',
                age: '',
                email: '',
                phone: '',
                gender: '',

                address: '',
                date: '',
                pass: ''
            }

            // Prevent modal from closing
            bvModalEvent.preventDefault()
            // Trigger submit handler
            this.handleSubmit()
        },
        handleSubmit () {
            // Exit when the form isn't valid
            if (!this.checkFormValidity()) {
                return
            }
            // Push the name to submitted names
            this.submittedNames.push(this.name)
            // Hide the modal manually
            this.$nextTick(() => {
                this.$bvModal.hide('modal-prevent-closing')
            })
        }
    }
}
</script>