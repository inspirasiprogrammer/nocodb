<template>
  <v-card style="width: 100%">
    <v-toolbar height="40" class="elevation-0 toolbar-border-bottom">
      <v-spacer></v-spacer>


      <x-btn outlined tooltip="Reload log settings"
             color="primary"
             small
             :disabled="loading"
             @click="load"
             v-ge="['roles','reload']"
             @click.prevent>
        <v-icon small left>refresh</v-icon>
        Reload
      </x-btn>
      <x-btn outlined tooltip="Toggle all checkbox"
             color="primary"
             small
             :disabled="loading"
             @click="toggleAll = !toggleAll; edited=true"
             v-ge="['roles','add new']"
             @click.prevent>
        <v-icon small left>{{ toggleAll ? 'mdi-toggle-switch-outline' : 'mdi-toggle-switch-off-outline' }}</v-icon>
        Toggle All
      </x-btn>
      <x-btn outlined tooltip="Save Changes"
             color="primary"
             small
             @click="save"
             :disabled="!edited || loading"

             v-ge="['rows','save']"
             @click.prevent>
        <v-icon small left>save</v-icon>
        Save
      </x-btn>

    </v-toolbar>
    <div class="d-flex justify-center pa-2">
      <v-simple-table dense style="min-width: 500px;margin:0 auto">
        <thead>
        <tr>
          <th></th>
          <th>Name</th>
        </tr>
        </thead>
        <tbody>
        <tr v-for="(v, key) in names">
          <td>
            <v-checkbox @change="edited = true" v-model="names[key]" class="mt-0 pt-0" dense hide-details></v-checkbox>
          </td>
          <td>{{ key }}</td>
        </tr>
        </tbody>
      </v-simple-table>
    </div>
  </v-card>
</template>

<script>
export default {
  name: "logs",
  data: () => ({
    names: null,
    loading: false,
    edited: false
  }),
  async created() {
    await this.load()
  },
  methods: {
    async load() {
      this.loading = true;
      try {
        const res = await this.$store.dispatch('sqlMgr/ActSqlOp', [null, 'xcDebugGet'])
        this.names = JSON.parse(res.value);
      } catch (e) {
      }

      this.loading = false;
    },
    async save() {
      this.loading = true;
      try {
        const res = await this.$store.dispatch('sqlMgr/ActSqlOp', [null, 'xcDebugSet', this.names])
        this.$toast.success('Updated debug log settings successfully').goAway(3000);
        this.edited = false;
      } catch (e) {
        this.$toast.error('Some error occurred while updating debug log settings').goAway(3000);
      }
      this.loading = false;
    }
  },
  computed: {
    toggleAll: {
      get() {
        return this.names && Object.values(this.names).some(v => v)
      }, set(val) {
        this.names && Object.keys(this.names).forEach(k => this.$set(this.names, k, val));
      }
    }
  }
}
</script>

<style scoped>

</style>
<!--
/**
 * @copyright Copyright (c) 2021, Xgene Cloud Ltd
 *
 * @author Naveen MR <oof1lab@gmail.com>
 * @author Pranav C Balan <pranavxc@gmail.com>
 *
 * @license GNU AGPL version 3 or any later version
 *
 * This program is free software: you can redistribute it and/or modify
 * it under the terms of the GNU Affero General Public License as
 * published by the Free Software Foundation, either version 3 of the
 * License, or (at your option) any later version.
 *
 * This program is distributed in the hope that it will be useful,
 * but WITHOUT ANY WARRANTY; without even the implied warranty of
 * MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
 * GNU Affero General Public License for more details.
 *
 * You should have received a copy of the GNU Affero General Public License
 * along with this program. If not, see <http://www.gnu.org/licenses/>.
 *
 */
-->
