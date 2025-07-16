<template>
  <div class="min-h-screen bg-gradient-to-br from-blue-500 via-indigo-600 to-purple-700 relative overflow-hidden">
    <!-- Background Pattern -->
    <div class="absolute inset-0 overflow-hidden pointer-events-none">
      <div class="absolute top-20 left-20 w-32 h-32 bg-white bg-opacity-10 rounded-full animate-float"></div>
      <div class="absolute top-40 right-32 w-24 h-24 bg-white bg-opacity-15 rounded-full animate-float-delayed"></div>
      <div class="absolute bottom-32 left-40 w-28 h-28 bg-white bg-opacity-8 rounded-full animate-float-slow"></div>
      <div class="absolute bottom-20 right-20 w-20 h-20 bg-white bg-opacity-20 rounded-full animate-float-fast"></div>
      <div class="absolute top-1/2 left-1/3 w-36 h-36 bg-purple-300 bg-opacity-10 rounded-full animate-float-slow"></div>
      <div class="absolute bottom-1/4 right-1/4 w-40 h-40 bg-blue-300 bg-opacity-15 rounded-full animate-float"></div>
    </div>

    <div class="max-w-4xl mx-auto py-16 px-4 sm:px-6 relative z-10">
      <!-- Header -->
      <div class="text-center mb-12 animate-fade-in-up">
        <div class="w-24 h-24 bg-gradient-to-r from-indigo-500 to-purple-600 rounded-full flex items-center justify-center mx-auto mb-8">
          <svg xmlns="http://www.w3.org/2000/svg" class="h-12 w-12 text-white" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M16 7a4 4 0 11-8 0 4 4 0 018 0zM12 14a7 7 0 00-7 7h14a7 7 0 00-7-7z" />
          </svg>
        </div>
        <h1 class="text-4xl md:text-5xl font-bold bg-gradient-to-r from-white to-indigo-100 bg-clip-text text-transparent mb-4">✏️ Modifica Profilo</h1>
        <p class="text-indigo-100 text-xl leading-relaxed max-w-2xl mx-auto">{{ isOrganization ? '🏢 Aggiorna le informazioni della tua organizzazione' : '👤 Aggiorna le tue informazioni personali' }}</p>
      </div>

      <!-- Profile Form -->
      <div class="card-enhanced animate-fade-in-up backdrop-blur-md" style="animation-delay: 0.1s">
        <form @submit.prevent="saveProfile" class="space-y-8">
          
          <!-- Basic Information -->
          <div class="space-y-6">
            <div class="flex items-center mb-8">
              <div class="w-12 h-12 bg-gradient-to-r from-indigo-500 to-purple-600 rounded-full flex items-center justify-center mr-4">
                <svg class="w-6 h-6 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M16 7a4 4 0 11-8 0 4 4 0 018 0zM12 14a7 7 0 00-7 7h14a7 7 0 00-7-7z" />
                </svg>
              </div>
              <h2 class="text-2xl font-bold text-gray-800">📋 Informazioni Base</h2>
            </div>
            
            <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
              <!-- Username Field -->
              <div class="form-group-enhanced">
                <label class="label-enhanced">👤 Username</label>
                <input 
                  v-model="profile.username"
                  class="input-field-enhanced" 
                  type="text"
                  placeholder="Il tuo username"
                  required
                />
              </div>

              <!-- Email Field -->
              <div class="form-group-enhanced">
                <label class="label-enhanced">📧 Email</label>
                <input 
                  v-model="profile.email"
                  class="input-field-enhanced" 
                  type="email"
                  placeholder="tua@email.com"
                  required
                />
              </div>

              <!-- Phone Field -->
              <div class="form-group-enhanced">
                <label class="label-enhanced">
                  📱 Telefono {{ isOrganization ? '(obbligatorio)' : '(opzionale)' }}
                </label>
                <input 
                  v-model="profile.phone"
                  class="input-field-enhanced"
                  type="tel"
                  placeholder="+39 123 456 7890"
                  :required="isOrganization"
                />
              </div>

              <!-- Password Field -->
              <div class="form-group-enhanced">
                <label class="label-enhanced">🔒 Password</label>
                <div class="relative">
                  <input 
                    v-model="profile.password"
                    class="input-field-enhanced pr-12" 
                    :type="showPassword ? 'text' : 'password'"
                    placeholder="Nuova password (opzionale)"
                  />
                  <button
                    type="button"
                    @click="togglePasswordVisibility"
                    class="absolute right-3 top-1/2 transform -translate-y-1/2 text-gray-500 hover:text-gray-700 focus:outline-none transition-colors duration-200"
                  >
                    <svg v-if="showPassword" class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13.875 18.825A10.05 10.05 0 0112 19c-4.478 0-8.268-2.943-9.543-7a9.97 9.97 0 011.563-3.029m5.858.908a3 3 0 114.243 4.243M9.878 9.878l4.242 4.242M9.878 9.878L3 3m6.878 6.878L21 21"></path>
                    </svg>
                    <svg v-else class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 12a3 3 0 11-6 0 3 3 0 016 0z"></path>
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M2.458 12C3.732 7.943 7.523 5 12 5c4.478 0 8.268 2.943 9.542 7-1.274 4.057-5.064 7-9.542 7-4.477 0-8.268-2.943-9.542-7z"></path>
                    </svg>
                  </button>
                </div>
                <p class="mt-2 text-sm text-gray-500 flex items-center">
                  <svg class="w-4 h-4 mr-1 text-gray-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 16h-1v-4h-1m1-4h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z"></path>
                  </svg>
                  Lascia vuoto per mantenere la password attuale
                </p>
              </div>
            </div>
          </div>

          <!-- Organization-specific fields -->
          <div v-if="isOrganization" class="space-y-6">
            <div class="flex items-center mb-8">
              <div class="w-12 h-12 bg-gradient-to-r from-indigo-500 to-purple-600 rounded-full flex items-center justify-center mr-4">
                <svg class="w-6 h-6 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 21V5a2 2 0 00-2-2H7a2 2 0 00-2 2v16m14 0h2m-2 0h-5m-9 0H3m2 0h5M9 7h1m-1 4h1m4-4h1m-1 4h1m-5 10v-5a1 1 0 011-1h2a1 1 0 011 1v5m-4 0h4" />
                </svg>
              </div>
              <h2 class="text-2xl font-bold text-gray-800"> Informazioni Organizzazione</h2>
            </div>
            
            <div class="space-y-6">
              <!-- Address Field -->
              <div class="form-group-enhanced">
                <label class="label-enhanced">📍 Indirizzo (obbligatorio)</label>
                <input 
                  v-model="profile.indirizzo"
                  class="input-field-enhanced" 
                  type="text"
                  placeholder="Via Roma 123, 38122 Trento TN"
                  required
                />
              </div>

              <!-- Description Field -->
              <div class="form-group-enhanced">
                <label class="label-enhanced">📝 Descrizione (obbligatorio)</label>
                <textarea 
                  v-model="profile.descrizione"
                  class="input-field-enhanced"  
                  placeholder="Descrivi di cosa si occupa la tua organizzazione..."
                  required
                  rows="4"
                ></textarea>
              </div>
            </div>
          </div>

          <!-- User-specific fields -->
          <div v-if="!isOrganization" class="space-y-6">
            <div class="flex items-center mb-8">
              <div class="w-12 h-12 bg-gradient-to-r from-indigo-500 to-purple-600 rounded-full flex items-center justify-center mr-4">
                <svg class="w-6 h-6 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10.325 4.317c.426-1.756 2.924-1.756 3.35 0a1.724 1.724 0 002.573 1.066c1.543-.94 3.31.826 2.37 2.37a1.724 1.724 0 001.065 2.572c1.756.426 1.756 2.924 0 3.35a1.724 1.724 0 00-1.066 2.573c.94 1.543-.826 3.31-2.37 2.37a1.724 1.724 0 00-2.572 1.065c-.426 1.756-2.924 1.756-3.35 0a1.724 1.724 0 00-2.573-1.066c-1.543.94-3.31-.826-2.37-2.37a1.724 1.724 0 00-1.065-2.572c-1.756-.426-1.756-2.924 0-3.35a1.724 1.724 0 001.066-2.573c-.94-1.543.826-3.31 2.37-2.37.996.608 2.296.07 2.572-1.065z" />
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 12a3 3 0 11-6 0 3 3 0 016 0z" />
                </svg>
              </div>
              <h2 class="text-2xl font-bold text-gray-800">👤 Preferenze Utente</h2>
            </div>
            
            <div class="flex items-start space-x-3">
              <input 
                v-model="profile.posizione"
                type="checkbox"
                class="mt-1 h-5 w-5 text-indigo-600 focus:ring-indigo-500 border-gray-300 rounded transition-all duration-200"
              />
              <div class="text-sm">
                <label class="label-enhanced">📍 Condividi la mia posizione per segnalazioni più precise</label>
              </div>
            </div>
          </div>
          
          <!-- Action Buttons -->
          <div class="flex flex-col sm:flex-row justify-end space-y-4 sm:space-y-0 sm:space-x-4 pt-8">
            <router-link 
              to="/profilo" 
              class="btn-enhanced btn-secondary-enhanced flex items-center justify-center"
            >
              <svg class="w-5 h-5 mr-2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"></path>
              </svg>
               Annulla
            </router-link>
            <button 
              type="submit" 
              class="btn-enhanced btn-primary-enhanced flex items-center justify-center"
              :disabled="isSaving"
            >
              <svg v-if="isSaving" class="animate-spin -ml-1 mr-2 h-5 w-5 text-white" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24">
                <circle class="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" stroke-width="4"></circle>
                <path class="opacity-75" fill="currentColor" d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042 1.135 5.824 3 7.938l3-2.647z"></path>
              </svg>
              <svg v-else class="w-5 h-5 mr-2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7"></path>
              </svg>
              <span v-if="isSaving">🔄 Salvataggio...</span>
              <span v-else>💾 Salva Modifiche</span>
            </button>
          </div>
        </form>
      </div>
    </div>

    <!-- Toast Notifications -->
    <transition name="slide-fade">
      <div class="fixed top-6 right-6 z-50 space-y-4">
        <!-- Success Toast -->
        <div v-if="showSuccess" class="success-message-enhanced">
          <div class="flex items-center justify-center">
            <div class="w-8 h-8 bg-green-500 rounded-full flex items-center justify-center mr-4">
              <svg class="w-5 h-5 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7" />
              </svg>
            </div>
            <span class="font-bold text-lg">✅ Profilo aggiornato con successo!</span>
          </div>
        </div>
        
        <!-- Error Toast -->
        <div v-if="showError" class="error-message-enhanced">
          <div class="flex items-center justify-center">
            <div class="w-8 h-8 bg-red-500 rounded-full flex items-center justify-center mr-4">
              <svg class="w-5 h-5 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8v4m0 4h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
              </svg>
            </div>
            <span class="font-bold text-lg">❌ {{ errorMessage }}</span>
          </div>
        </div>
      </div>
    </transition>
  </div>
</template>

<script>
import api from '@/utils/api';

export default {
  name: 'EditProfile',
  data() {
    return {
      profile: {
        username: '',
        email: '',
        password: '',
        phone: '',
        indirizzo: '', // for organizations
        descrizione: '', // for organizations
        posizione: false // for users
      },
      showPassword: false,
      userId: null,
      isOrganization: false,
      isSaving: false,
      showSuccess: false,
      showError: false,
      errorMessage: ''
    }
  },
  mounted() {
    const userData = sessionStorage.getItem('userData');
    
    if (userData) {
      const user = JSON.parse(userData);
      this.userId = user._id;
      this.isOrganization = user.accountType === 'organization' || user.accountType === 'org';
      
      // Set common fields
      this.profile.username = user.username;
      this.profile.email = user.email;
      this.profile.phone = user.phone || '';
      
      // Set organization-specific fields
      if (this.isOrganization) {
        this.profile.indirizzo = user.indirizzo || '';
        this.profile.descrizione = user.descrizione || '';
      } else {
        // Set user-specific fields
        this.profile.posizione = user.posizione || false;
      }
    }
  },
  methods: {
    async saveProfile() {
      this.isSaving = true;
      try {
        const updateData = {
          username: this.profile.username,
          email: this.profile.email,
          phone: this.profile.phone
        };
        
        // Add organization-specific fields
        if (this.isOrganization) {
          updateData.indirizzo = this.profile.indirizzo;
          updateData.descrizione = this.profile.descrizione;
        } else {
          // Add user-specific fields
          updateData.posizione = this.profile.posizione;
        }
        
        // Only include password if it's not empty
        if (this.profile.password) {
          updateData.password = this.profile.password;
        }

        // Use the correct endpoint based on account type
        const endpoint = this.isOrganization ? `/orgs/${this.userId}` : `/users/${this.userId}`;
        const response = await api.put(endpoint, updateData);
        
        if (response.status === 200) {
          // Update sessionStorage with the updated user/organization
          const updatedData = this.isOrganization ? response.data.organization : response.data.user;
          const originalUserData = JSON.parse(sessionStorage.getItem('userData'));
          updatedData.accountType = originalUserData.accountType;
          sessionStorage.setItem('userData', JSON.stringify(updatedData));
          
          // Show success animation
          this.showSuccess = true;
          
          // Redirect after 3 seconds
          setTimeout(() => {
            this.$router.push('/profilo');
          }, 3000);
        }
      } catch (error) {
        console.error('Error updating profile:', error);
        
        // Show error message
        const errorMsg = error.response?.data?.message || error.message;
        this.errorMessage = `Errore: ${errorMsg}`;
        this.showError = true;
        
        // Auto-hide error after 5 seconds
        setTimeout(() => {
          this.showError = false;
        }, 5000);
      } finally {
        this.isSaving = false;
      }
    }
  }
}
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&display=swap');

* {
  font-family: 'Inter', sans-serif;
}

/* Card Styles Enhanced */
.card-enhanced {
  background: linear-gradient(135deg, rgba(255, 255, 255, 0.95) 0%, rgba(255, 255, 255, 0.9) 100%);
  backdrop-filter: blur(20px);
  border-radius: 24px;
  padding: 3rem;
  box-shadow: 0 20px 60px rgba(0, 0, 0, 0.15), 0 8px 25px rgba(0, 0, 0, 0.1);
  border: 2px solid rgba(255, 255, 255, 0.3);
  margin-bottom: 2rem;
  transition: all 0.4s ease;
}

.card-enhanced:hover {
  transform: translateY(-5px);
  box-shadow: 0 30px 80px rgba(0, 0, 0, 0.2), 0 12px 35px rgba(0, 0, 0, 0.15);
}

/* Button Styles Enhanced */
.btn-enhanced {
  padding: 1rem 2rem;
  border-radius: 16px;
  font-weight: 700;
  font-size: 1rem;
  transition: all 0.3s ease;
  border: none;
  cursor: pointer;
  text-transform: none;
  letter-spacing: 0.5px;
  box-shadow: 0 8px 25px rgba(0, 0, 0, 0.15);
  transform: translateY(0);
  text-decoration: none;
}

.btn-primary-enhanced {
  background: linear-gradient(135deg, #6366f1 0%, #8b5cf6 50%, #ec4899 100%);
  color: white;
  border: 2px solid rgba(255, 255, 255, 0.3);
}

.btn-primary-enhanced:hover {
  background: linear-gradient(135deg, #4f46e5 0%, #7c3aed 50%, #db2777 100%);
  transform: translateY(-3px);
  box-shadow: 0 15px 40px rgba(99, 102, 241, 0.4);
}

.btn-secondary-enhanced {
  background: linear-gradient(135deg, rgba(255, 255, 255, 0.9) 0%, rgba(248, 250, 252, 0.9) 100%);
  color: #4f46e5;
  border: 2px solid rgba(99, 102, 241, 0.3);
}

.btn-secondary-enhanced:hover {
  background: linear-gradient(135deg, rgba(255, 255, 255, 1) 0%, rgba(241, 245, 249, 1) 100%);
  border-color: rgba(99, 102, 241, 0.6);
  transform: translateY(-3px);
  box-shadow: 0 15px 40px rgba(99, 102, 241, 0.2);
}

/* Form Styles Enhanced */
.form-group-enhanced {
  margin-bottom: 2rem;
}

.label-enhanced {
  display: block;
  color: #374151;
  font-weight: 700;
  font-size: 1rem;
  margin-bottom: 0.75rem;
  letter-spacing: 0.5px;
}

.input-field-enhanced {
  width: 100%;
  padding: 1rem 1.5rem;
  border-radius: 16px;
  border: 2px solid #e5e7eb;
  font-size: 1rem;
  font-weight: 500;
  transition: all 0.3s ease;
  background: linear-gradient(135deg, rgba(255, 255, 255, 0.9) 0%, rgba(248, 250, 252, 0.9) 100%);
  backdrop-filter: blur(10px);
}

.input-field-enhanced:focus {
  border-color: #6366f1;
  outline: none;
  box-shadow: 0 0 0 4px rgba(99, 102, 241, 0.1), 0 8px 25px rgba(99, 102, 241, 0.15);
  background: rgba(255, 255, 255, 0.95);
  transform: translateY(-2px);
}

/* Success Message Enhanced */
.success-message-enhanced {
  background: linear-gradient(135deg, #d1fae5 0%, #a7f3d0 100%);
  color: #065f46;
  border-radius: 20px;
  padding: 1.5rem 2rem;
  text-align: center;
  animation: slideInFromTop 0.6s ease-out, fadeOutDelayed 5s forwards;
  font-weight: 600;
  border: 2px solid #10b981;
  box-shadow: 0 10px 30px rgba(16, 185, 129, 0.2);
}

/* Error Message Enhanced */
.error-message-enhanced {
  background: linear-gradient(135deg, #fee2e2 0%, #fecaca 100%);
  color: #991b1b;
  border-radius: 20px;
  padding: 1.5rem 2rem;
  text-align: center;
  animation: slideInFromTop 0.6s ease-out, fadeOutDelayed 5s forwards;
  font-weight: 600;
  border: 2px solid #ef4444;
  box-shadow: 0 10px 30px rgba(239, 68, 68, 0.2);
}

/* Enhanced Animations */
@keyframes slideInFromTop {
  from {
    opacity: 0;
    transform: translateY(-50px) scale(0.9);
  }
  to {
    opacity: 1;
    transform: translateY(0) scale(1);
  }
}

@keyframes fadeOutDelayed {
  0%, 80% { opacity: 1; transform: scale(1); }
  100% { opacity: 0; transform: scale(0.95); }
}

@keyframes fade-in-up {
  from {
    opacity: 0;
    transform: translateY(40px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@keyframes float {
  0% { transform: translateY(0) translateX(0) rotate(0deg); opacity: 0.8; }
  50% { transform: translateY(-25px) translateX(20px) rotate(180deg); opacity: 0.4; }
  100% { transform: translateY(0) translateX(0) rotate(360deg); opacity: 0.8; }
}

.animate-fade-in-up {
  animation: fade-in-up 1s ease-out forwards;
}

.animate-float {
  animation: float 12s ease-in-out infinite;
}

.animate-float-delayed {
  animation: float 14s ease-in-out infinite 2s;
}

.animate-float-slow {
  animation: float 18s ease-in-out infinite;
}

.animate-float-fast {
  animation: float 10s ease-in-out infinite;
}

/* Transitions */
.slide-fade-enter-active {
  transition: all 0.3s ease-out;
}

.slide-fade-leave-active {
  transition: all 0.3s cubic-bezier(1.0, 0.5, 0.8, 1.0);
}

.slide-fade-enter-from,
.slide-fade-leave-to {
  transform: translateX(20px);
  opacity: 0;
}

/* Responsive Design */
@media (max-width: 768px) {
  .card-enhanced {
    padding: 2rem 1.5rem;
    margin: 1rem;
  }
  
  .btn-enhanced {
    padding: 0.875rem 1.5rem;
    font-size: 0.9rem;
  }
}
</style>
