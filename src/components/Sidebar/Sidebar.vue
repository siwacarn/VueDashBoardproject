<template>
  <div class="sidebar-wrapper">
    <nav
      :class="{ sidebar: true, sidebarStatic, sidebarOpened }"
      @mouseenter="sidebarMouseEnter"
      @mouseleave="sidebarMouseLeave"
    >
      <header class="logo">
        <router-link to="/app"
          ><span class="primary-word">Farmming Dashboard</span></router-link
        >
      </header>
      <ul class="nav">
        <NavLink
          :activeItem="activeItem"
          header="Dashboard"
          link="/app/dashboard"
          iconName="flaticon-home"
          index="dashboard"
          isHeader
        />
        <NavLink
          :activeItem="activeItem"
          header="Real Time Dashboard"
          link="/app/RealtimeDashboard"
          iconName="flaticon-home"
          index="dashboard"
          isHeader
        />
        <!-- <NavLink
          :activeItem="activeItem"
          header="Typography"
          link="/app/typography"
          iconName="flaticon-list"
          index="typography"
          isHeader
        /> -->
        <!-- <NavLink
          :activeItem="activeItem"
          header="Tables Basic"
          link="/app/tables"
          iconName="flaticon-equal-1"
          index="tables"
          isHeader
        /> -->
       
      </ul>
    

      <div class="sidebarAlerts">
        <!-- <b-alert
            v-for="alert in alerts"
            :key="alert.id"
            class="sidebarAlert" variant="transparent"
            show dismissible
        >
          <span>{{alert.title}}</span><br/>
          <b-progress class="sidebarProgress progress-xs mt-1"
                      :variant="alert.color" :value="alert.value" :max="100"/>
          <small>{{alert.footer}}</small>
        </b-alert> -->
      </div>
    </nav>
  </div>
</template>

<script>
import { mapState, mapActions } from "vuex";
import isScreen from "@/core/screenHelper";
import NavLink from "./NavLink/NavLink";

export default {
  name: "Sidebar",
  components: { NavLink },
  data() {
    return {
      alerts: [
        {
          id: 0,
          title: "Sales Report",
          value: 15,
          footer: "Calculating x-axis bias... 65%",
          color: "danger",
        },
        {
          id: 1,
          title: "Personal Responsibility",
          value: 20,
          footer: "Provide required notes",
          color: "primary",
        },
      ],
    };
  },
  methods: {
    ...mapActions("layout", ["changeSidebarActive", "switchSidebar"]),
    setActiveByRoute() {
      const paths = this.$route.fullPath.split("/");
      paths.pop();
      this.changeSidebarActive(paths.join("/"));
    },
    sidebarMouseEnter() {
      if (!this.sidebarStatic && (isScreen("lg") || isScreen("xl"))) {
        this.switchSidebar(false);
        this.setActiveByRoute();
      }
    },
    sidebarMouseLeave() {
      if (!this.sidebarStatic && (isScreen("lg") || isScreen("xl"))) {
        this.switchSidebar(true);
        this.changeSidebarActive(null);
      }
    },
  },
  created() {
    this.setActiveByRoute();
  },
  computed: {
    ...mapState("layout", {
      sidebarStatic: (state) => state.sidebarStatic,
      sidebarOpened: (state) => !state.sidebarClose,
      activeItem: (state) => state.sidebarActiveElement,
    }),
  },
};
</script>

<!-- Sidebar styles should be scoped -->
<style src="./Sidebar.scss" lang="scss" scoped />
