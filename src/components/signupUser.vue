<template>
    <div>
        <b-button v-b-modal.modal-prevent-closing>Signup</b-button>
       

        <b-modal id="modal-prevent-closing" ref="modal" title="SignUp" @show="resetModal" @hidden="resetModal"
            @ok="handleOk">
            <form ref="form" @submit.stop.prevent="handleSubmit">

                <b-form-group label="Name">
                    <b-form-input  v-model="user.name"  required></b-form-input>
                </b-form-group>

                <b-form-group label="Age" >
                    <b-form-input  v-model="user.age"  required></b-form-input>
                </b-form-group>

                <b-form-group label="Password">
                    <b-form-input v-model="user.pass" required></b-form-input>
                </b-form-group>

                <b-form-group label="Phone" >
                    <b-form-input  v-model="user.phone"  required></b-form-input>
                </b-form-group>

                <b-form-group label="Email" >
                    <b-form-input  v-model="user.email"  required></b-form-input>
                </b-form-group>

                <b-form-group label="Date" >
                    <b-form-input  v-model="user.date"  type="date" required></b-form-input>
                </b-form-group>

                <b-form-group label="Gender" >
                <select id="gender" v-model="user.gender">
                    <option >Men</option>
                    <option >Women</option>
                
                </select>
                </b-form-group>

                <b-form-group label="Address" >
                    <b-form-input  v-model="user.address"  required></b-form-input>
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