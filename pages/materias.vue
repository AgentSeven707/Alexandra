<template>
  <v-data-table :headers="headers" :items="materias">
    <template v-slot:top>
      <v-toolbar flat color="#C35F2D">
        <v-toolbar-title>Materias</v-toolbar-title>
        <v-divider class="mx-4" inset vertical></v-divider>
        <v-spacer></v-spacer>
        <v-dialog v-model="dialog" max-width="500px">
          <v-card>
            <v-card-text>
              <v-container>
                <v-row>

                  <v-data-table :headers="headers2" :items="tareas">
                    <template v-slot:top>
                      <v-toolbar flat color="#8826FF">
                        <v-toolbar-title>Tareas</v-toolbar-title>
                          <v-divider class="mx-4" inset vertical></v-divider>
                          <v-spacer></v-spacer>
                      </v-toolbar>
                    </template>
                    <template v-slot:[`item.actions`]="{ item }">
                      <v-tooltip top color="#D22CFF">
                      <template v-slot:activator="{ on, attrs }">
                        <v-icon color="#D22CFF" small class="mr-2" v-bind="attrs" v-on="on" @click="criterios(item)">mdi-pencil</v-icon>
                      </template>
                      <span>Establecer Criterios</span>
                      </v-tooltip>
                    </template>
                  </v-data-table>

                </v-row>
              </v-container>
            </v-card-text>
            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn color="blue darken-1" text @click="leerMaterias(editedItem);close();">Ok</v-btn>
            </v-card-actions>
          </v-card>
        </v-dialog>

        <v-dialog v-model="dialog" max-width="500px">
          <v-card>
            <v-card-text>
              <v-container>
                <v-row>


                </v-row>
              </v-container>
            </v-card-text>
            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn color="blue darken-1" text @click="criterios();close();">Ok</v-btn>
            </v-card-actions>
          </v-card>
        </v-dialog>

      </v-toolbar>
    </template>

    <template v-slot:[`item.actions`]="{ item }">
      <v-tooltip top color="#15AE92">
      <template v-slot:activator="{ on, attrs }">
        <v-icon color="#00e69d" small class="mr-2" v-bind="attrs" v-on="on" @click="verTareas(item)">mdi-archive-arrow-up</v-icon>
      </template>
      <span>Ver Tareas</span>
      </v-tooltip>
    </template>
  </v-data-table>
</template>

<script>
export default {
  data: () => ({
    //Crea los datos asignados a la tabla creada con html
    dialog: false,
    headers: [
      { text: "Materia", value: "materia" },
      { text: "Tareas de la Materia", value: "actions", sortable: false },
    ],
    headers2: [
      { text: "Tareas", value: "tarea" },
      { text: "Criterios", value: "actions", sortable: false },
    ],
    materias: [],
    tareas: [],
    editedIndex: -1,
    editedItem: { materia: undefined },
    deletedItem: {},
    defaultItem: { materia: undefined },
  }),
  computed: {

  },
  watch: {
    //L??neas que nos permiten cerrar las cuadros de di??logos
    dialog(val) {
      val || this.close();
    }
  },
  created() {
    //LLena las tablas con el contenido correspondiente
    this.leerMaterias();
  },
  methods: {
    //Obtiene la informaci??n de las tareas
    verTareas() {
      this.dialog = true;
      this.tareas = [ {"tarea": "Tarea 1"}, {"tarea": "Tarea 2"} ];
    },
    //Obtiene la informaci??n de las tareas
    leerMaterias(item) {
      this.materias = [ {"materia": "Materia 1"}, {"materia": "Materia 2"} ];
    },
    //Establecer criterios
    criterios(item){

    },
    //Funci??n que cierra el cuadro de di??logo para agregar un item
    close() {
      this.dialog = false;
      this.$nextTick(() => {
        this.editedItem = Object.assign({}, this.defaultItem);
        this.editedIndex = -1;
      });
    },
    //Funci??n que guarda la informaci??n sacada del cuadro de di??logo para agregar un item
    save() {
      
    },
  },
};
</script>