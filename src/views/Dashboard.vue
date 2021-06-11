<template>
  <b-container fluid>
    <b-row>
      <b-col cols="3" sm="2" lg="3">
        <SideBar />
      </b-col>
      <b-col cols="12" lg="12" >
        <Header />
      </b-col>
    </b-row>
  </b-container>
</template>

<script>
// @ is an alias to /src

import Header from './header';
import SideBar from './template';

export default {
  name: 'Dashboard',
  components: {
   Header,
   SideBar,
  }
}
</script>
