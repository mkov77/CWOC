<template>
  <div id="app">
    <header>
		  <h1>FALCON<span>NET</span></h1>
	  </header>
    <div>
      <body>
        <h2>Accountability Overview</h2>
      </body>
      <section>
        <b-table
              :data="data"
              ref="table"
              detailed
              hoverable
              custom-detail-row
              :default-sort="['Unit', 'asc']"
              detail-key="Unit"
              @details-open="(row, index) => $buefy.toast.open(`Expanded ${row.Unit}`)"
              :show-detail-icon="showDetailIcon">

              <b-table-column
                  field="Unit"
                  :visible="columnsVisible['Unit'].display"
                  :label="columnsVisible['Unit'].title"
                  width="200"
                  v-slot="props"
              >
                  <template v-if="showDetailIcon">
                      {{ props.row.Unit }}
                  </template>
                  <template v-else>
                      <a @click="toggle(props.row)">
                          {{ props.row.Unit }}
                      </a>
                  </template>
              </b-table-column>

              <b-table-column
                  :visible="columnsVisible['reported'].display"
                  :label="columnsVisible['reported'].title"
                  centered
                  v-slot="props"
              >
                  <span :class="
                          [
                              'tag',
                              {'is-warning': props.row.count / props.row.assigned == 0.0},
                              {'is-success': props.row.count / props.row.assigned == 1.0},
                              {'is-danger': props.row.count / props.row.assigned > 0.0 && props.row.count / props.row.assigned < 1.0}
                          ]">
                      {{ Math.round((props.row.count / props.row.assigned) * 100) }}%
                  </span>
              </b-table-column>

              <b-table-column
                  field="count"
                  :visible="columnsVisible['count'].display"
                  :label="columnsVisible['count'].title"
                  centered
                  v-slot="props"
              >
                  {{ props.row.count }}
              </b-table-column>

              <b-table-column
                  field="assigned"
                  :visible="columnsVisible['assigned'].display"
                  :label="columnsVisible['assigned'].title"
                  centered
                  v-slot="props"
              >
                  {{ props.row.assigned }}
              </b-table-column>

              <template slot="detail" slot-scope="props">
                  <tr v-for="item in props.row.items" :key="item.Unit">
                      <td v-if="showDetailIcon"></td>
                      <td v-show="columnsVisible['Unit'].display" >&nbsp;&nbsp;&nbsp;&nbsp;{{ item.Unit }}</td>
                      <td v-show="columnsVisible['reported'].display" class="has-text-centered">
                          <span :class="
                              [
                                  'tag',
                                  {'is-warning': item.count / item.assigned == 0.0},
                                  {'is-success': item.count / item.assigned == 1.0},
                                  {'is-danger': item.count / item.assigned > 0.00 && item.count / item.assigned  < 1.0}
                              ]">
                              {{ Math.round((item.count / item.assigned) * 100) }}%
                          </span>
                      </td>
                      <td v-show="columnsVisible['count'].display" class="has-text-centered">{{ item.count }}</td>
                      <td v-show="columnsVisible['assigned'].display" class="has-text-centered">{{ item.assigned }}</td>
                  </tr>
              </template>
          </b-table>
      </section>
      <body>
        <h2>Unit Records</h2>
        <h3>Showing Records for <span>CS-24</span></h3>
      </body>
      <section>
        <b-table :data="records" :columns="fields"></b-table>
      </section>
    </div>
  </div>
</template>

<style>
    * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }
  header {
    background-color: #231E23;
    display: flex;
    justify-content: left;
    align-items: left;
    padding: 15px;
  }
  header h1 {
    color: #A0A3A5;
    font-size: 28px;
    font-weight: 300;
    text-transform: uppercase;
  }
  header h1 span {
    color: #243E6B;
    font-weight: 900;
  }
  body h2 {
    background-color: #A0A3A5;
    font-family: Arial, sans-serif;
    font-weight: bold;
  }
  body h3 {
    background-color: #E6E6E6;
    font-style: italic;
  }
  body h3 span{
    color: #231E23;
    font-weight: bold;
  }
</style>

<script>
import Vue from 'vue'
import Buefy from 'buefy'
import 'buefy/dist/buefy.css'

Vue.use(Buefy)

  export default {
    data() {
        return {
            data: [
                {
                    Unit: "Wing",
                    count: 434,
                    assigned: 721,
                    items: [
                        {
                            Unit: "CW Staff",
                            count: 101,
                            assigned: 187
                        }
                    ]
                },
                {
                    Unit: "Group 1",
                    count: 301,
                    assigned: 301,
                    items: [
                        {
                            Unit: "CG1",
                            count: 90,
                            assigned: 90
                        },
                        {
                            Unit: "CS01",
                            count: 0,
                            assigned: 84
                        },
                        {
                            Unit: "CS02",
                            count: 0,
                            assigned: 95
                        },
                        {
                            Unit: "CS03",
                            count: 99,
                            assigned: 100
                        },
                        {
                            Unit: "CS04",
                            count: 0,
                            assigned: 95
                        },
                        {
                            Unit: "CS05",
                            count: 0,
                            assigned: 95
                        },
                        {
                            Unit: "CS06",
                            count: 0,
                            assigned: 95
                        },
                        {
                            Unit: "CS07",
                            count: 0,
                            assigned: 95
                        },
                        {
                            Unit: "CS08",
                            count: 0,
                            assigned: 95
                        },
                        {
                            Unit: "CS09",
                            count: 0,
                            assigned: 95
                        },
                        {
                            Unit: "CS10",
                            count: 0,
                            assigned: 95
                        }
                    ]
                },
                {
                    Unit: "Group 2",
                    count: 88,
                    assigned: 167,
                    items: [
                        {
                            Unit: "CG2 Staff",
                            count: 31,
                            assigned: 38
                        },
                        {
                            Unit: "CS11",
                            count: 23,
                            assigned: 29
                        },
                        {
                            Unit: "CS12",
                            count: 20,
                            assigned: 44
                        },
                        {
                            Unit: "CS13",
                            count: 14,
                            assigned: 56
                        },
                        {
                            Unit: "CS14",
                            count: 14,
                            assigned: 56
                        },
                        {
                            Unit: "CS15",
                            count: 14,
                            assigned: 56
                        },
                        {
                            Unit: "CS16",
                            count: 14,
                            assigned: 56
                        },
                        {
                            Unit: "CS17",
                            count: 14,
                            assigned: 56
                        },
                        {
                            Unit: "CS18",
                            count: 14,
                            assigned: 56
                        },
                        {
                            Unit: "CS19",
                            count: 14,
                            assigned: 56
                        },
                        {
                            Unit: "CS20",
                            count: 14,
                            assigned: 56
                        }
                    ]
                },
                {
                    Unit: "Group 3",
                    count: 88,
                    assigned: 167,
                    items: [
                        {
                            Unit: "CG3 Staff",
                            count: 31,
                            assigned: 38
                        },
                        {
                            Unit: "CS21",
                            count: 23,
                            assigned: 29
                        },
                        {
                            Unit: "CS22",
                            count: 20,
                            assigned: 44
                        },
                        {
                            Unit: "CS23",
                            count: 14,
                            assigned: 56
                        },
                        {
                            Unit: "CS24",
                            count: 14,
                            assigned: 56
                        },
                        {
                            Unit: "CS25",
                            count: 14,
                            assigned: 56
                        },
                        {
                            Unit: "CS26",
                            count: 14,
                            assigned: 56
                        },
                        {
                            Unit: "CS27",
                            count: 14,
                            assigned: 56
                        },
                        {
                            Unit: "CS28",
                            count: 14,
                            assigned: 56
                        },
                        {
                            Unit: "CS29",
                            count: 14,
                            assigned: 56
                        },
                        {
                            Unit: "CS30",
                            count: 14,
                            assigned: 56
                        }
                    ]
                },
                {
                    Unit: "Group 4",
                    count: 88,
                    assigned: 167,
                    items: [
                        {
                            Unit: "CG4 Staff",
                            count: 31,
                            assigned: 38
                        },
                        {
                            Unit: "CS31",
                            count: 23,
                            assigned: 29
                        },
                        {
                            Unit: "CS32",
                            count: 20,
                            assigned: 44
                        },
                        {
                            Unit: "CS33",
                            count: 14,
                            assigned: 56
                        },
                        {
                            Unit: "CS34",
                            count: 14,
                            assigned: 56
                        },
                        {
                            Unit: "CS35",
                            count: 14,
                            assigned: 56
                        },
                        {
                            Unit: "CS36",
                            count: 14,
                            assigned: 56
                        },
                        {
                            Unit: "CS37",
                            count: 14,
                            assigned: 56
                        },
                        {
                            Unit: "CS38",
                            count: 14,
                            assigned: 56
                        },
                        {
                            Unit: "CS39",
                            count: 14,
                            assigned: 56
                        },
                        {
                            Unit: "CS40",
                            count: 14,
                            assigned: 56
                        }
                    ],
                }
            ],
            records: [
                    { 'report_time': '2016-12-15 06:00:53', 'reporter_name': "Michaela Kovalsky", 'unit_present': 86, 'unit_count': 90, 'unit_assigned': 90 },
                    { 'report_time': '2016-12-15 06:00:53', 'reporter_name': "Michaela Kovalsky", 'unit_present': 86, 'unit_count': 90, 'unit_assigned': 90 },
                    { 'report_time': '2016-12-15 06:00:53', 'reporter_name': "Michaela Kovalsky", 'unit_present': 86, 'unit_count': 90, 'unit_assigned': 90 }
            ],
            fields: [
                    {
                        field: 'report_time',
                        label: 'Report Time',
                        centered: true
                    },
                    {
                        field: 'reporter_name',
                        label: 'Reporter',
                        centered: true
                    },
                    {
                        field: 'unit_present',
                        label: 'Present',
                        numerical: true
                    },
                    {
                        field: 'unit_count',
                        label: 'Count',
                        numerical: true
                    },
                    {
                        field: 'unit_assigned',
                        label: 'Assigned',
                        numerical: true
                    }
                ],
            columnsVisible: {
                Unit: { title: "Unit", display: true },
                reported: { title: "Reported", display: true },
                count: { title: "Count", display: true },
                assigned: { title: "Assigned", display: true },
            },
            showDetailIcon: false
        };
    },
    methods: {
        toggle(row) {
            this.$refs.table.toggleDetails(row);
        }
    }
}
</script>