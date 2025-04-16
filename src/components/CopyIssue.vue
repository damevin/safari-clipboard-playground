<template>
  <div>
    <h3>Liste des utilisateurs</h3>
    <div
      v-for="user in users"
      :key="user.id"
      class="user-item"
    >
      <!-- Utilisation d'un <span> pour imiter le problème initial -->
      <span
        class="copy-link"
        @click="copyUserInfo(user)"
      >
        Copier les infos
      </span>
      <p>{{ user.name }} (ID: {{ user.id }})</p>
    </div>
  </div>
</template>

<script>
export default {
  // Props simulées
  props: {
    users: {
      type: Array,
      default: () => [
        { id: 1, name: 'Alice', email: 'alice@example.com' },
        { id: 2, name: 'Bob', email: 'bob@example.com' },
      ],
    },
  },

  methods: {
    // Simule une requête asynchrone (comme getDialInAccessInfos)
    async fetchUserDetails(userId) {
      // Fausse requête avec un délai
      await new Promise(resolve => setTimeout(resolve, 1000))
      return {
        accessCode: `CODE-${userId}`,
        dialInNumber: '+1-555-123-4567',
      }
    },

    // Génère le texte à copier (similaire à accessInformations)
    generateUserInfo(user, details) {
      const intro = `Bonjour ${user.name}, voici vos informations d'accès :`
      const link = `https://example.com/access/${user.email}`
      const dialIn = details
        ? `\nNuméro: ${details.dialInNumber}\nCode: ${details.accessCode}`
        : ''
      return `${intro}\n${link}${dialIn}`
    },

    // Méthode problématique pour reproduire l'échec sur Safari
    async copyUserInfo(user) {
      try {
        // Simule l'appel asynchrone
        const details = await this.fetchUserDetails(user.id)
        const textToCopy = this.generateUserInfo(user, details)

        // Utilisation de navigator.clipboard.writeText dans un contexte asynchrone
        await navigator.clipboard.writeText(textToCopy)
        console.log('Texte copié !')
        // Simule une notification
        alert('Informations copiées !')
      } catch (err) {
        console.error('Erreur lors de la copie :', err)
        // Simule une notification d'erreur
        alert('Erreur lors de la copie.')
      }
    },
  },
}
</script>

<style scoped>
.user-item {
  margin: 10px 0;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 4px;
}

.copy-link {
  color: blue;
  text-decoration: underline;
  cursor: pointer;
}
</style>
