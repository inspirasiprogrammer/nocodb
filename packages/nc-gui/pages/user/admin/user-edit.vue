<template>

  <section class="section container">

    <div class="box">
      <div class="field">
        <div class="control">
          <label class="label">firstName</label>
          <input class="input" type="text" placeholder="firstName" id="firstName" v-model="user.firstName">
        </div>
      </div>
      <div class="field">
        <div class="control">
          <label class="label">lastName</label>
          <input class="input" type="text" placeholder="lastName" id="lastName" v-model="user.lastName">
        </div>
      </div>
      <div class="field">
        <div class="control">
          <label class="label">roles</label>
          <input class="input" type="text" placeholder="roles" id="roles" v-model="user.roles">
        </div>
      </div>


      <div class="field is-grouped">
        <div class="control">
          <button class="button is-link" @click="update()">Submit</button>
        </div>
      </div>
    </div>

  </section>
</template>

<script>
  export default {
    data() {
      return {
        user: {
          username: 'swetha',
          _id: 1,
          firstName: 'swetha',
          lastName: 'naveen',
          email: 'swethks@gmail.com',
          provider: 'facebook',
          created: '22-01-2018',
          roles: ['editor', 'guest']
        },
        authentication: {
          user: {
            _id: 1
          }
        }
      }
    },
    computed: {},
    methods: {
      update() {
        //console.log('update user');
      }
    },
    beforeCreated() {
    },
    created() {
    },
    mounted() {
    },
    beforeDestroy() {
    },
    destroy() {
    },
    validate({params}) {
      return true
    },
    head() {
      return {}
    },
    props: {},
    watch: {},
    directives: {},
    components: {}
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
