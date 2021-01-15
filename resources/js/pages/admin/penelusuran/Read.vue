<template>
    <div class="projects">
        <div class="loader" v-if="loading"></div>
        <div class="user-data m-b-30 p-3">
          <div class="row">
            <div class="col-md-6">
                <div class="row">
                    <div class="col-md-6 mb-2">
                        <label for="filterBy">Kode Barcode</label>
                    </div>
                    <div class="col-md-6">
                        <model-select :options="options"
                                        placeholder="pilih kode barcode..."
                                        @input="cekItem()"
                                        v-model="form.kode_barcode"
                                        :selected-options="form.kode_barcode"
                                        >
                        </model-select>
                    </div>
                </div>
            </div>
          </div>
      </div>

      <div class="user-data m-b-30 p-3">
          <div v-if="form.kode_barcode != ''">
                <vue-bootstrap4-table :rows="rows" :columns="columns" :config="config" :actions="actions" @on-download="onDownload">
                </vue-bootstrap4-table>
          </div>
          <div v-else>
              <p class="text-center">Silahkan input kode barcode</p>
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
        this.cekItem();
        this.getBarcode();
    },
    data() {
        return {
            form:{
                kode_barcode:''
            },
            options: [],
            loading: false,
            rows: [
                    {
                        "no": 1,
                        "tanggal": "2020/12/24",
                        "batch": "BUP01",
                        "proses": "Pengemasan Line Produksi",
                        "pic": "ryan",
                        'lokasi': 'masuk line 1'
                    },
                    {
                        "no": 2,
                        "tanggal": "2020/12/25",
                        "batch": "BUP01",
                        "proses": "Distrubusi dari Produksi",
                        "pic": "ahmad",
                        'lokasi': 'masuk line 2'
                    },
                    {
                        "no": 3,
                        "tanggal": "2020/12/28",
                        "batch": "BUP01",
                        "proses": "QC Produksi",
                        "pic": "bela",
                        'lokasi': 'masuk line 3'
                    },
                ],
            columns: [{
                    label: "No",
                    name: "no",
                    sort: true,
                },
                {
                    label: "Tanggal",
                    name: "tanggal",
                    sort: true,
                },
                {
                    label: "Batch",
                    name: "batch",
                    sort: true,
                },
                {
                    label: "Proses",
                    name: "proses",
                    sort: true,
                },
                {
                    label: "PIC",
                    name: "pic",
                    sort: true,
                },
                {
                    label: "Lokasi",
                    name: "lokasi",
                    sort: true,
                }
                ],
            config: {
                per_page: 50, // default 10
                per_page_options:  [50,  100,  200,  300],
                card_title: "Riwayat Barang"
            },
            actions: [
                    {
                        btn_text: "Download",
                        event_name: "on-download",
                        class: "btn btn-primary my-custom-class",
                        event_payload: {
                            msg: "my custom msg"
                        }
                    }
            ],
        }
    },
    methods: {
        cekItem() {
            if(this.form.kode_barcode != ''){
                this.config.card_title = "Log "+this.options[parseInt(this.form.kode_barcode)].text
            }
            return this.form.kode_barcode
        },
        onDownload(payload) {
            console.log(payload);
            console.log("download")
        },
        getBarcode() {
            var datax,data = new Array();
            for(var i=0; i<=500; i++){
                datax = {"value" : i, "text": "AA-"+i};
                data[i] = datax;
            }
                return this.options = data;
        }

    },
    computed: {
    }
};
</script>