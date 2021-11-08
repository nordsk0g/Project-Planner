<template>
  <div class="project" :class="{ complete: project.complete }">
      <div class="actions">
          <h3 @click="toggleDetails" >{{ project.title }}</h3>
          <div class="icons">
            <span @click="toggleStatus" class="material-icons-sharp tick">done</span>
            <router-link :to="{ name: 'EditProject', params: { id: project.id } }">
                <span class="material-icons-sharp">edit</span>
            </router-link>
            <span @click="deleteProject" class="material-icons-sharp">delete</span>
          </div>
      </div>
      <div v-if="showDetails" class="details">
          <p>{{ project.details }}</p>
      </div>
  </div>
</template>

<script>
export default {
    props: ['project'],
    data() {
        return {
            showDetails: false,
            uri: `http://localhost:3000/projects/${this.project.id}`
        }
    },
    methods: {
        toggleDetails() {
            this.showDetails = !this.showDetails
        },
        deleteProject() {
            fetch(this.uri, { method: 'DELETE' })
            .then(() => this.$emit('delete', this.project.id))
            .catch(err => console.err(err.message))
        },
        toggleStatus() {
            fetch(this.uri, { 
                method: 'PATCH',
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify({ complete: !this.project.complete}) 
                })
            .then(() => this.$emit('status', this.project.id))
            .catch(err => console.error(err.message))
        }
    }
}
</script>

<style>
 .project {
     margin: 1.25em auto;
     background: white;
     padding: 0.75em 1.25em;
     border-radius: 0.25em;
     box-shadow: 1px 2px 3px rgba(0,0,0,0.05);
     border-left: 0.25em solid #e90074;
 }

.project.complete {
    border-left-color: #00e975;
}

.project.complete .tick {
    color: #00e975;
}
 
h3 {
    cursor: pointer;
}

.actions {
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.material-icons-sharp {
    font-size: 1.5em;
    margin-left: 0.75em;
    color: #bbb;
    cursor: pointer;
}

.material-icons-sharp:hover {
    color: #777;
}

</style>