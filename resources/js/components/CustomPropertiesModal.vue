<template>
    <modal @modal-close="handleClose">
        <card>
            <form class="bg-white rounded-lg shadow-lg w-full w-action-fields"
                @submit.prevent="handleUpdate"
                autocomplete="off"
            >

                <div v-for="field in fields" :key="field.attribute" class="action">
                    <component :is="'form-' + field.component" :field="field"/>
                </div>

                <div class="bg-30 px-6 py-3 flex">
                    <div class="flex items-center ml-auto">
                        <button type="button" class="btn text-80 font-normal h-9 px-3 mr-3 btn-link" @click.prevent="handleClose">
                            {{__('Cancel')}}
                        </button>

                        <button type="submit" class="btn btn-default btn-primary">
                            {{__('Update')}}
                        </button>
                    </div>
                </div>

            </form>
        </card>
    </modal>
</template>

<script>
  export default {
    props: {
        fields: {
            type: Array,
            required: true,
        }
    },

    mounted() {
          setInterval(function(){
              let modal = document.getElementsByClassName('z-20')[0];

              if(!modal.className.includes('w-2/5')){
                  modal.className+= " w-2/5 ";
              }
              console.log(modal.className);
          }, 100);
      },

    methods: {
        handleClose () {
            this.$emit('close')
        },

        handleUpdate () {
            let formData = new FormData()

            this.fields.forEach(field => field.fill(formData))

            this.$emit('update', formData)
        }
    }
  }
</script>
