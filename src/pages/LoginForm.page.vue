<template>
  <n-card>
    <n-tabs
      class="card-tabs"
      default-value="signin"
      size="large"
      animated
      pane-wrapper-style="margin: 0 -4px"
      pane-style="padding-left: 4px; padding-right: 4px; box-sizing: border-box;"
    >
      <!-- Onglet de connexion -->
      <n-tab-pane name="signin" tab="Se connecter">
        <n-form :model="signinForm" ref="signinForm" label-placement="top">
          <n-form-item label="Nom d'utilisateur" prop="username">
            <input v-model="signinForm.username" />
          </n-form-item>
          <n-form-item label="Mot de passe" prop="password">
            <input v-model="signinForm.password" type="password" />
          </n-form-item>
        </n-form>
        <n-button @click="handleSignIn" type="primary" block secondary strong>
          Se connecter
        </n-button>
      </n-tab-pane>

      <!-- Onglet d'inscription -->
      <n-tab-pane name="signup" tab="S'inscrire">
        <n-form :model="signupForm" ref="signupForm" label-placement="top">
          <n-form-item label="Nom d'utilisateur" prop="username">
            <input v-model="signupForm.username" />
          </n-form-item>
          <n-form-item label="Mot de passe" prop="password">
            <input v-model="signupForm.password" type="password" />
          </n-form-item>
          <n-form-item label="Confirmer le mot de passe" prop="confirmPassword">
            <input v-model="signupForm.confirmPassword" type="password" />
          </n-form-item>
        </n-form>
        <n-button @click="handleSignUp" type="primary" block secondary strong>
          S'inscrire
        </n-button>
      </n-tab-pane>
    </n-tabs>
  </n-card>
</template>

<script>
export default {
  data() {
    return {
      signinForm: {
        username: '',
        password: ''
      },
      signupForm: {
        username: '',
        password: '',
        confirmPassword: ''
      }
    };
  },
  methods: {
    // Fonction pour gérer la connexion
    handleSignIn() {
      const { username, password } = this.signinForm;

      // Validation des champs
      if (!username || !password) {
        console.log('Veuillez remplir tous les champs pour la connexion');
        return;
      }

      // Simuler la connexion réussie
      console.log('Connexion réussie avec:', { username, password });
      
      // Après une connexion réussie, redirige vers la page deck-collection (utilise le chemin défini dans router.js)
      this.$router.push('/deck-collection');  // Utilise le chemin de la route '/deck-collection'
    },

    // Fonction pour gérer l'inscription
    handleSignUp() {
      const { username, password, confirmPassword } = this.signupForm;

      // Validation des champs
      if (!username || !password || !confirmPassword) {
        console.log('Veuillez remplir tous les champs pour l\'inscription');
        return;
      }
      if (password !== confirmPassword) {
        console.log('Les mots de passe ne correspondent pas');
        return;
      }

      // Simuler l'inscription réussie
      console.log('Inscription réussie avec:', { username, password });

      // Après une inscription réussie, redirige vers la page de connexion
      this.$router.push('/login');  // Utilise le chemin de la route '/login'
    }
  }
};
</script>

<style scoped>
.card-tabs .n-tabs-nav--bar-type {
  padding-left: 4px;
}

.n-form-item {
  margin-bottom: 16px;
}

.n-button {
  margin-top: 16px;
}
</style>
