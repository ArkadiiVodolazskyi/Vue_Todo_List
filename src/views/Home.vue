<template>
  <div class="home">
    <div v-if="projects.length">
      <h2>Projects</h2>
      <div class="projects">
        <SingleProject
          v-for="(project, index) in projects"
          :style="{'animation-delay': `${index * 0.1}s`}"
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
import SingleProject from '../components/SingleProject.vue';

export default {
  name: 'Home',
  components: {
    SingleProject
  },
  data() {
    return {
      projects: [],
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
    }
  },
  mounted() {
    this.redrawProjects();
  }
}
</script>