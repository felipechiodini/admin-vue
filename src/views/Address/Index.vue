<template>
  <BaseIndex title="Endereço da Loja" subtitle="">
    <div class="d-flex flex-column" v-if="address">
      <span>
        {{ address.street }},
        {{ address.number }},
        {{ address.complement }},
        {{ address.neighborhood }}
      </span>
      <span>
        CEP - {{ address.cep }}
      </span>
      <span>
        {{ address.city }} - {{ address.state }}
      </span>
    </div>
    <button class="btn btn-primary w-25 mt-3" @click="$router.push({ name: 'address.update' })">
      Editar Endereço
    </button>
  </BaseIndex>
</template>

<script>
import BaseIndex from '@/components/BaseIndex.vue'
import { requesFromStore } from '@/js/api.js'
import Loading from '@/js/Mixins/Loading'

export default {
  components: {
    BaseIndex
  },
  mixins: [Loading],
  data: () => {
    return {
      address: null,
      loading: true
    }
  },
  mounted() {
    this.fetchAddress()
  },
  methods: {
    fetchAddress() {
      this.setLoading(true)
      requesFromStore()
        .get('address')
        .then(({ data }) => this.address = data.address)
        .finally(() => this.setLoading(false))
    }
  }
}
</script>
