<template>
    <div class="projects">
        <div class="loader" v-if="loading"></div>
        <div class="user-data m-b-30 p-3">
          <div class="row">
            <div class="col-md-6">
                <div class="row">
                    <div class="col-md-6 mb-2">
                        <label for="filterBy">Lokasi</label>
                    </div>
                    <div class="col-md-6">
                        <model-select :options="options"
                                        placeholder="pilih lokasi..."
                                        @input="cekGudang()"
                                        v-model="form.gudang"
                                        :selected-options="form.gudang"
                                        >
                        </model-select>
                    </div>
                </div>
            </div>
          </div>
      </div>

      <div class="user-data m-b-30 p-3">
          <div v-if="form.gudang != ''">
                <vue-bootstrap4-table :rows="rows" :columns="columns" :config="config">
                </vue-bootstrap4-table>
          </div>
          <div v-else>
              <p class="text-center">Silahkan pilih lokasi</p>
          </div>
      </div>
    </div>
</template>

<script>
import Datatable from '../../../components/Datatables.vue';
import Pagination from '../../../components/Pagination.vue';
import DateRangePicker from 'vue2-daterange-picker'
// import Datepicker from 'vuejs-datepicker';
import DatePicker from 'vue2-datepicker';
import 'vue2-datepicker/index.css';
//you need to import the CSS manually (in case you want to override it)
import 'vue2-daterange-picker/dist/vue2-daterange-picker.css'
import { ModelSelect } from 'vue-search-select'
import VueBootstrap4Table from 'vue-bootstrap4-table'
export default {
    // name:{disabled_dates},
    components: { datatable: Datatable, pagination: Pagination, DatePicker, ModelSelect, VueBootstrap4Table },
    created() {
        this.cekGudang();
    },
    data() {
        return {
            form:{
                gudang:''
            },
            options: [
                { value: '1', text: 'gudang aa' + ' - ' + '1' },
                { value: '2', text: 'gudang ab' + ' - ' + '2' },
                { value: '3', text: 'gudang bc' + ' - ' + '3' },
                { value: '4', text: 'gudang cd' + ' - ' + '4' },
                { value: '5', text: 'gudang de' + ' - ' + '5' }
                ],
            loading: false,
            rows: [{
                        "no": 1,
                        "name": {
                            "first_name": "Bion-Up",
                        },
                        "batch": "BUP01",
                        "stock":100
                    },
                    {
                        "no": 2,
                        "name": {
                            "first_name": "Kuriza",
                        },
                        "age": 23,
                        "batch": "KA0001",
                        "stock":200
                    },
                    {
                        "no": 3,
                        "name": {
                            "first_name": "Nitrea Pupuk Urea",
                        },
                        "batch": "NPU01",
                        "stock":300
                    }],
            columns: [{
                    label: "No",
                    name: "no",
                    // filter: {
                    //     type: "simple",
                    //     placeholder: "No"
                    // },
                    sort: true,
                },
                {
                    label: "Jenis Pupuk",
                    name: "name.first_name",
                    // filter: {
                    //     type: "simple",
                    //     placeholder: "Enter Jenis Pupuk"
                    // },
                    sort: true,
                },
                {
                    label: "Batch",
                    name: "batch",
                    // filter: {
                    //     type: "simple",
                    //     placeholder: "Enter Batch"
                    // },
                    sort: true,
                },
                {
                    label: "Stock",
                    name: "stock",
                    // filter: {
                    //     type: "simple",
                    //     placeholder: "Enter Stok"
                    // },
                    sort: true,
                }
                ],
            config: {
                // checkbox_rows: true,
                rows_selectable: true,
                card_title: "Vue Bootsrap 4 advanced table"
            }
        }
    },
    methods: {
        cekGudang () {
            if(this.form.gudang != ''){
                this.config.card_title = this.options[parseInt(this.form.gudang)-1].text
            }
            return this.form.gudang
        },

    },
    computed: {
    }
};
</script>