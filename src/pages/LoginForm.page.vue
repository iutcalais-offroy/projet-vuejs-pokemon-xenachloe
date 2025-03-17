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
        <n-form :model="signinForm" ref="signinForm" :rules="signinRules" label-placement="top">
          <n-form-item label="Nom d'utilisateur" prop="username">
            <n-input v-model="signinForm.username" />
          </n-form-item>
          <n-form-item label="Mot de passe" prop="password">
            <n-input v-model="signinForm.password" type="password" />
          </n-form-item>
        </n-form>
        <n-button @click="signIn" type="primary" block secondary strong>
          Se connecter
        </n-button>
      </n-tab-pane>

      <!-- Onglet d'inscription -->
      <n-tab-pane name="signup" tab="S'inscrire">
        <n-form :model="signupForm" ref="signupForm" :rules="signupRules" label-placement="top">
          <n-form-item label="Nom d'utilisateur" prop="username">
            <n-input v-model="signupForm.username" />
          </n-form-item>
          <n-form-item label="Mot de passe" prop="password">
            <n-input v-model="signupForm.password" type="password" />
          </n-form-item>
          <n-form-item label="Confirmer le mot de passe" prop="confirmPassword">
            <n-input v-model="signupForm.confirmPassword" type="password" />
          </n-form-item>
        </n-form>
        <n-button @click="signUp" type="primary" block secondary strong>
          S'inscrire
        </n-button>
      </n-tab-pane>
    </n-tabs>
  </n-card>
</template>

<script>
export default {
    methods: {
    // Fonction d'inscription
    signUp() {
      this.$refs.signupForm.validate().then((valid) => {
        if (valid) {
          
          // Supposons que vous recevez un token d'authentification après inscription
          const token = 'votre_token_reçu_du_backend'; // Remplacez ceci par le token réel du backend

          // Sauvegarder le token dans localStorage
          localStorage.setItem('auth_token', token);

          // Rediriger après inscription réussie
          this.$router.push('/deck-collection');
        }
      }).catch(() => {});
    },

    // Fonction de connexion
    signIn() {
      this.$refs.signinForm.validate((valid) => {
        if (valid) {
          // Vérifier si le token est déjà dans localStorage
          const token = localStorage.getItem('auth_token');

          if (token) {
            // Si un token est trouvé, on peut l'utiliser pour l'authentification
            // Par exemple, vous pouvez envoyer le token avec les requêtes API
            // axios.post('/api/login', { token })
            
            // Si l'utilisateur est authentifié, rediriger vers la page de collection
            this.$router.push('/deck-collection');
          } else {
            // Si le token n'est pas présent, envoyer les données de connexion au backend
            // Exemple : axios.post('/api/login', this.signinForm)
            
            // Supposons que vous recevez un token d'authentification du backend
            const token = 'votre_token_reçu_du_backend'; // Remplacez ceci par le token réel du backend

            // Sauvegarder le token dans localStorage
            localStorage.setItem('auth_token', token);

            // Rediriger vers la page de collection après une connexion réussie
            this.$router.push('/deck-collection');
          }
        } else {
          // Si le formulaire est invalide, afficher une alerte ou un message d'erreur
          console.error('Veuillez vérifier les champs du formulaire.');
          alert('Veuillez vérifier les champs du formulaire.');
        }
      });
    },

    // Validation du mot de passe de confirmation (assurez-vous que les mots de passe correspondent)
    validatePasswordConfirm(rule, value, callback) {
      if (value !== this.signupForm.password) {
        callback(new Error('Les mots de passe ne correspondent pas'));
      } else {
        callback();
      }
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
