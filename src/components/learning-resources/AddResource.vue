<template>
    <base-dialog v-if="inputIsInvalid" title="Invalid Input" @closeDialog="closeBaseDialog">
        <!-- here is the slot in section, with no name so default -->
        <template #default>
            <p>There is an empty field somewhere!</p>
            <p>Please enter something in each input of the form</p>
        </template>
        <!-- here is the slot named 'actions' -->
        <template #actions>
            <base-button @click="closeBaseDialog">Okay</base-button>
        </template>    
    </base-dialog>
    <base-card>
        <form @submit.prevent="submitData()">
            <div class="form-control">
                <label for="title">Title</label>
                <input type="text" id="title" name="title" ref="titleInput"/>
            </div>
            <div class="form-control">
                <label for="description">Description</label>
                <textarea id="description" name="description" rows="3" ref="descInput"></textarea>
            </div>
            <div class="form-control">
                <label for="link">Link</label>
                <input type="url" id="link" name="link" ref="linkInput"/>
            </div>
            <div>
                <base-button type="submit">Add Resource</base-button>
            </div>
        </form>
    </base-card>
</template>

<script>
export default {
    inject: ['addResource'],
    data() {
        return {
            inputIsInvalid: false,
        }
    },
    methods: {
        submitData() {
            const enteredTitle = this.$refs.titleInput.value;
            const enteredDesc = this.$refs.descInput.value;
            const enteredUrl = this.$refs.linkInput.value;

            if(enteredTitle.trim() === '' || enteredDesc.trim() === '' || enteredUrl.trim() === ''){
                this.inputIsInvalid = true
                return;
            }

            this.addResource(enteredTitle, enteredDesc, enteredUrl);
        },
        closeBaseDialog() {
            this.inputIsInvalid = false;
        }
    }
}
</script>

<style scoped>
label {
  font-weight: bold;
  display: block;
  margin-bottom: 0.5rem;
}

input,
textarea {
  display: block;
  width: 100%;
  font: inherit;
  padding: 0.15rem;
  border: 1px solid #ccc;
}

input:focus,
textarea:focus {
  outline: none;
  border-color: #3a0061;
  background-color: #f7ebff;
}

.form-control {
  margin: 1rem 0;
}
</style>