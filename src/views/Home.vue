<template>
  <div class="home">
    <FilterNav :current="current" @showProjectsType="updateFilter" />
    <div v-if="projects.length">
      <h2>Projects</h2>
      <div class="projects">
        <SingleProject
          v-for="(project, index) in filterUpdated"
          :style="{'animation-delay': `${(index * 0.1).toFixed(1)}s`}"
          :key="project.id"
          :project="project"
          @delete="handleDelete"
          @complete="handleComplete"
        />
      </div>
    </div>
  </div>
</template>

<script>
import FilterNav from '../components/FilterNav.vue';
import SingleProject from '../components/SingleProject.vue';

export default {
  name: 'Home',
  components: {
    SingleProject,
    FilterNav
  },
  data() {
    return {
      projects: [],
      current: 'all',
    };
  },
  methods: {
    redrawProjects() {
      fetch('http://localhost:3000/projects')
      .then(res => res.json())
      .then(data => {
        const dataToArray = data.slice(0);
        this.projects = dataToArray.sort((a, b) => {
          return a.complete > b.complete;
        });
      })
      .catch(err => console.log(err));
    },
    handleDelete(id) {
      this.projects = this.projects.filter(project => {
        return project.id !== id;
      });
    },
    handleComplete() {
      this.redrawProjects();
    },
    updateFilter(projectsType) {
      this.current = projectsType;
    }
  },
  mounted() {
    this.redrawProjects();
  },
  computed: {
    filterUpdated() {
      if (this.current === 'ongoing') {
        return this.projects.filter(project => !project.complete);
      } else if (this.current === 'completed') {
        return this.projects.filter(project => project.complete);
      }
      return this.projects;
    }
  }
}
</script>

<style lang="scss" scoped>

</style>