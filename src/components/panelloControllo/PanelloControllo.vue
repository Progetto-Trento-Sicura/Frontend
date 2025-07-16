<template>
  <div class="min-h-screen bg-gradient-to-br from-blue-400 via-indigo-600 to-purple-700 py-12">
    <!-- Header -->
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <div class="text-center mb-10">
        <div class="inline-flex items-center justify-center w-16 h-16 rounded-full bg-indigo-100 mb-4">
          <svg xmlns="http://www.w3.org/2000/svg" class="h-8 w-8 text-indigo-600" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12h6m-6 4h6m2 5H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z" />
          </svg>
        </div>
        <h1 class="text-4xl font-bold text-white mb-2">Pannello di Controllo</h1>
        <p class="text-xl text-indigo-100">Gestione Organizzazione</p>
      </div>

      <!-- Notification Enhanced -->
      <div v-if="notification.show" class="fixed top-6 right-6 z-50 animate-notification-in">
        <div :class="[
          'relative p-5 rounded-2xl shadow-2xl backdrop-blur-lg border border-white/20 flex items-center space-x-4 min-w-[320px] max-w-md',
          notification.type === 'success' 
            ? 'bg-gradient-to-r from-emerald-500/90 to-green-600/90 text-white' 
            : 'bg-gradient-to-r from-red-500/90 to-rose-600/90 text-white'
        ]">
          <!-- Icon with animation -->
          <div :class="[
            'flex-shrink-0 w-10 h-10 rounded-full flex items-center justify-center',
            notification.type === 'success' ? 'bg-white/20' : 'bg-white/20'
          ]">
            <svg v-if="notification.type === 'success'" class="w-6 h-6 animate-bounce-gentle" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2.5" d="M5 13l4 4L19 7"></path>
            </svg>
            <svg v-else class="w-6 h-6 animate-pulse" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2.5" d="M12 9v2m0 4h.01m-6.938 4h13.856c1.54 0 2.502-1.667 1.732-2.5L13.732 4c-.77-.833-1.964-.833-2.732 0L4.082 16.5c-.77.833.192 2.5 1.732 2.5z"></path>
            </svg>
          </div>
          
          <!-- Message -->
          <div class="flex-1">
            <p class="font-semibold text-lg">{{ notification.type === 'success' ? '✅ Successo!' : '⚠️ Attenzione!' }}</p>
            <p class="text-sm opacity-90 mt-1">{{ notification.message }}</p>
          </div>
          
          <!-- Close button -->
          <button @click="notification.show = false" class="flex-shrink-0 p-1 rounded-full hover:bg-white/20 transition-colors duration-200">
            <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"></path>
            </svg>
          </button>
          
          <!-- Progress bar -->
          <div class="absolute bottom-0 left-0 h-1 bg-white/30 rounded-b-2xl overflow-hidden">
            <div class="h-full bg-white animate-progress-bar"></div>
          </div>
        </div>
      </div>

      <!-- Stats Cards -->
      <div class="grid grid-cols-1 md:grid-cols-4 gap-6 mb-8">
        <div class="bg-white rounded-xl shadow-lg p-6">
          <div class="flex items-center">
            <div class="p-3 rounded-full bg-blue-100 text-blue-600">
              <svg class="w-8 h-8" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12h6m-6 4h6m2 5H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z"></path>
              </svg>
            </div>
            <div class="ml-4">
              <p class="text-sm font-medium text-gray-600">Utenti Registrati</p>
              <p class="text-2xl font-bold text-gray-900">{{ users.length }}</p>
            </div>
          </div>
        </div>
        
        <div class="bg-white rounded-xl shadow-lg p-6">
          <div class="flex items-center">
            <div class="p-3 rounded-full bg-yellow-100 text-yellow-600">
              <svg class="w-8 h-8" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 9v2m0 4h.01m-6.938 4h13.856c1.54 0 2.502-1.667 1.732-2.5L13.732 4c-.77-.833-1.964-.833-2.732 0L4.082 16.5c-.77.833.192 2.5 1.732 2.5z"></path>
              </svg>
            </div>
            <div class="ml-4">
              <p class="text-sm font-medium text-gray-600">Segnalazioni Totali</p>
              <p class="text-2xl font-bold text-gray-900">{{ reports.length }}</p>
            </div>
          </div>
        </div>
        
        <div class="bg-white rounded-xl shadow-lg p-6">
          <div class="flex items-center">
            <div class="p-3 rounded-full bg-red-100 text-red-600">
              <svg class="w-8 h-8" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8v4m0 4h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z"></path>
              </svg>
            </div>
            <div class="ml-4">
              <p class="text-sm font-medium text-gray-600">In Attesa</p>
              <p class="text-2xl font-bold text-gray-900">{{ pendingReports }}</p>
            </div>
          </div>
        </div>
        
        <!-- Nuova card per segnalazioni in corso -->
        <div class="bg-white rounded-xl shadow-lg p-6">
          <div class="flex items-center">
            <div class="p-3 rounded-full bg-orange-100 text-orange-600">
              <svg class="w-8 h-8" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 10V3L4 14h7v7l9-11h-7z"></path>
              </svg>
            </div>
            <div class="ml-4">
              <p class="text-sm font-medium text-gray-600">In Corso</p>
              <p class="text-2xl font-bold text-gray-900">{{ inProgressReports }}</p>
            </div>
          </div>
        </div>
      </div>

      <!-- Main Content -->
      <div class="bg-white rounded-xl shadow-lg overflow-hidden">
        <!-- Tabs -->
        <div class="border-b border-gray-200">
          <nav class="-mb-px flex space-x-8 px-6">
            <button 
              @click="activeTab = 'reports'"
              :class="[
                'py-4 px-1 border-b-2 font-medium text-sm',
                activeTab === 'reports' 
                  ? 'border-indigo-500 text-indigo-600' 
                  : 'border-transparent text-gray-500 hover:text-gray-700 hover:border-gray-300'
              ]"
            >
              Gestione Segnalazioni
            </button>
            <button 
              @click="activeTab = 'users'"
              :class="[
                'py-4 px-1 border-b-2 font-medium text-sm',
                activeTab === 'users' 
                  ? 'border-indigo-500 text-indigo-600' 
                  : 'border-transparent text-gray-500 hover:text-gray-700 hover:border-gray-300'
              ]"
            >
              Gestione Utenti
            </button>
          </nav>
        </div>

        <!-- Gestione Segnalazioni -->
        <div v-if="activeTab === 'reports'" class="p-6">
          <div class="mb-4 flex justify-between items-center">
            <h3 class="text-lg font-semibold text-gray-900">Gestione Segnalazioni</h3>
            <div class="flex items-center space-x-4">
              <!-- Filtro per stato -->
              <div class="flex items-center space-x-2">
                <label class="text-sm font-medium text-gray-700">Stato:</label>
                <select v-model="reportFilter" class="border border-gray-300 rounded px-3 py-1 text-sm">
                  <option value="all">Tutte</option>
                  <option value="pending">In Attesa</option>
                  <option value="in_progress">In Corso</option>
                  <option value="resolved">Risolte</option>
                </select>
              </div>
              
              <!-- Filtro per categoria -->
              <div class="flex items-center space-x-2">
                <label class="text-sm font-medium text-gray-700">Categoria:</label>
                <select v-model="categoryFilter" class="border border-gray-300 rounded px-3 py-1 text-sm">
                  <option value="all">Tutte</option>
                  <option value="Sicurezza">Sicurezza</option>
                  <option value="Infrastrutture">Infrastrutture</option>
                  <option value="Ambiente">Ambiente</option>
                  <option value="Traffico">Traffico</option>
                  <option value="Altro">Altro</option>
                </select>
              </div>
              
              <!-- Filtro per data -->
              <div class="flex items-center space-x-2">
                <label class="text-sm font-medium text-gray-700">Data:</label>
                <input 
                  v-model="dateFilter" 
                  type="date" 
                  class="border border-gray-300 rounded px-3 py-1 text-sm"
                />
                <button 
                  @click="clearDateFilter" 
                  class="text-sm text-gray-500 hover:text-gray-700"
                >
                  Cancella
                </button>
              </div>
            </div>
          </div>
          
          <div class="overflow-x-auto">
            <table class="min-w-full divide-y divide-gray-200">
              <thead class="bg-gray-50">
                <tr>
                  <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Titolo</th>
                  <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Utente</th>
                  <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Categoria</th>
                  <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Stato</th>
                  <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Descrizione</th>
                  <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Azioni</th>
                </tr>
              </thead>
              <tbody class="bg-white divide-y divide-gray-200">
                <tr v-for="report in filteredReports" :key="report._id">
                  <td class="px-6 py-4 whitespace-nowrap text-sm font-medium text-gray-900">{{ report.title }}</td>
                  <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">{{ report.username || 'Utente sconosciuto' }}</td>
                  <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">
                    <span class="inline-flex px-2 py-1 text-xs font-semibold rounded-full bg-blue-100 text-blue-800">
                      {{ report.category }}
                    </span>
                  </td>
                  <td class="px-6 py-4 whitespace-nowrap">
                    <select 
                      v-model="report.status" 
                      @change="updateReportStatus(report)"
                      :class="[
                        'text-sm border border-gray-300 rounded px-2 py-1 font-semibold',
                        getStatusColor(report.status)
                      ]"
                    >
                      <option value="pending">In Attesa</option>
                      <option value="in_progress">In Corso</option>
                      <option value="resolved">Risolto</option>
                    </select>
                  </td>
                  <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">
                    <button 
                      @click="showDescriptionModal(report)"
                      class="text-indigo-600 hover:text-indigo-900 underline cursor-pointer"
                    >
                      Visualizza descrizione
                    </button>
                  </td>
                  <td class="px-6 py-4 whitespace-nowrap text-sm font-medium">
                    <button 
                      @click="deleteReport(report._id)"
                      class="text-red-600 hover:text-red-900 ml-2"
                    >
                      Elimina
                    </button>
                  </td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>

        <!-- Gestione Utenti -->
        <div v-if="activeTab === 'users'" class="p-6">
          <div class="mb-4">
            <h3 class="text-lg font-semibold text-gray-900">Gestione Utenti</h3>
          </div>
          
          <!-- Barra di ricerca utenti -->
          <div class="mb-6">
            <div class="relative max-w-md">
              <div class="absolute inset-y-0 left-0 pl-3 flex items-center pointer-events-none">
                <svg class="h-5 w-5 text-gray-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z"></path>
                </svg>
              </div>
              <input 
                v-model="userSearchQuery"
                type="text" 
                placeholder="Cerca utenti per username o email..."
                class="block w-full pl-10 pr-3 py-2 border border-gray-300 rounded-md leading-5 bg-white placeholder-gray-500 focus:outline-none focus:placeholder-gray-400 focus:ring-1 focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm"
              >
            </div>
            <p class="mt-2 text-sm text-gray-500">Trovati {{ filteredUsers.length }} utenti</p>
          </div>
          
          <div class="overflow-x-auto">
            <table class="min-w-full divide-y divide-gray-200">
              <thead class="bg-gray-50">
                <tr>
                  <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Username</th>
                  <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Email</th>
                  <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Stato</th>
                  <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Segnalazioni</th>
                  <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Azioni</th>
                </tr>
              </thead>
              <tbody class="bg-white divide-y divide-gray-200">
                <tr v-for="user in filteredUsers" :key="user._id">
                  <td class="px-6 py-4 whitespace-nowrap text-sm font-medium text-gray-900">{{ user.username }}</td>
                  <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">{{ user.email }}</td>
                  <td class="px-6 py-4 whitespace-nowrap">
                    <span class="px-2 inline-flex text-xs leading-5 font-semibold rounded-full" :class="[
                      user.status === 'suspended' ? 'bg-red-100 text-red-800' : 'bg-green-100 text-green-800'
                    ]">
                      {{ user.status === 'suspended' ? 'Sospeso' : 'Attivo' }}
                    </span>
                  </td>
                  <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">{{ getUserReportsCount(user._id) }}</td>
                  <td class="px-6 py-4 whitespace-nowrap text-sm font-medium space-x-2">
                    <button 
                      v-if="user.status !== 'suspended'"
                      @click="suspendUser(user._id)"
                      class="text-yellow-600 hover:text-yellow-900"
                    >
                      Sospendi
                    </button>
                    <button 
                      v-else
                      @click="reactivateUser(user._id)"
                      class="text-green-600 hover:text-green-900"
                    >
                      Riattiva
                    </button>
                    <button 
                      @click="deleteUser(user._id)"
                      class="text-red-600 hover:text-red-900"
                    >
                      Elimina
                    </button>
                  </td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>
      </div>
    </div>

    <!-- Modal per la descrizione -->
    <div v-if="showModal" class="fixed inset-0 bg-gray-600 bg-opacity-50 overflow-y-auto h-full w-full z-50" @click="closeModal">
      <div class="relative top-20 mx-auto p-5 border w-11/12 md:w-1/2 shadow-lg rounded-md bg-white" @click.stop>
        <div class="mt-3">
          <div class="flex justify-between items-center mb-4">
            <h3 class="text-lg font-medium text-gray-900">Descrizione Segnalazione</h3>
            <button @click="closeModal" class="text-gray-400 hover:text-gray-600">
              <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"></path>
              </svg>
            </button>
          </div>
          <div class="mb-4">
            <h4 class="font-semibold text-gray-800 mb-2">{{ selectedReport?.title }}</h4>
            <div class="bg-gray-50 p-4 rounded-lg">
              <p class="text-gray-700 leading-relaxed">{{ selectedReport?.description }}</p>
            </div>
          </div>
          <div class="flex justify-between items-center text-sm text-gray-500">
            <span>Categoria: <strong>{{ selectedReport?.category }}</strong></span>
            <span>Data: <strong>{{ formatDate(selectedReport?.date) }}</strong></span>
          </div>
        </div>
      </div>
    </div>
    <!-- Modal per conferma sospensione -->
    <div v-if="showSuspendModal" class="fixed inset-0 bg-gray-600 bg-opacity-50 overflow-y-auto h-full w-full z-50" @click="closeSuspendModal">
      <div class="relative top-20 mx-auto p-5 border w-96 shadow-lg rounded-md bg-white" @click.stop>
        <div class="mt-3 text-center">
          <div class="mx-auto flex items-center justify-center h-12 w-12 rounded-full bg-yellow-100">
            <svg class="h-6 w-6 text-yellow-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 9v2m0 4h.01m-6.938 4h13.856c1.54 0 2.502-1.667 1.732-2.5L13.732 4c-.77-.833-1.964-.833-2.732 0L4.082 16.5c-.77.833.192 2.5 1.732 2.5z"></path>
            </svg>
          </div>
          <h3 class="text-lg leading-6 font-medium text-gray-900 mt-4">Conferma Sospensione</h3>
          <div class="mt-2 px-7 py-3">
            <p class="text-sm text-gray-500">
              Sei sicuro di voler sospendere questo utente? L'utente non potrà più accedere al sistema.
            </p>
          </div>
          <div class="flex justify-center space-x-4 px-4 py-3">
            <button @click="closeSuspendModal" class="px-4 py-2 bg-gray-300 text-gray-800 text-base font-medium rounded-md shadow-sm hover:bg-gray-400 focus:outline-none focus:ring-2 focus:ring-gray-300">
              Annulla
            </button>
            <button @click="confirmSuspendUser" class="px-4 py-2 bg-yellow-600 text-white text-base font-medium rounded-md shadow-sm hover:bg-yellow-700 focus:outline-none focus:ring-2 focus:ring-yellow-500">
              Sospendi
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import api from '@/utils/api'

export default {
  name: 'PanelloControllo',
  data() {
    return {
      activeTab: 'reports',
      reportFilter: 'all',
      categoryFilter: 'all',
      dateFilter: '',
      userSearchQuery: '', // Aggiungi questa riga
      users: [],
      reports: [],
      showModal: false,
      selectedReport: null,
      showSuspendModal: false,
      userToSuspend: null,
      notification: {
        show: false,
        type: 'success',
        message: ''
      }
    }
  },
  computed: {
    filteredReports() {
      let filtered = this.reports
      
      // Filtro per stato
      if (this.reportFilter !== 'all') {
        filtered = filtered.filter(report => report.status === this.reportFilter)
      }
      
      // Filtro per categoria
      // Nel computed filteredReports (circa linea 330)
      if (this.categoryFilter !== 'all') {
      filtered = filtered.filter(report => report.category === this.categoryFilter)  // ✅ Questo rimarrà category perché ora mappiamo correttamente
      }
      
      // Filtro per data
      if (this.dateFilter) {
        filtered = filtered.filter(report => {
          const reportDate = new Date(report.date).toISOString().split('T')[0]
          return reportDate === this.dateFilter
        })
      }
      
      return filtered
    },
    filteredUsers() {
      if (!this.userSearchQuery) {
        return this.users
      }
      
      const query = this.userSearchQuery.toLowerCase()
      return this.users.filter(user => 
        user.username.toLowerCase().includes(query) ||
        user.email.toLowerCase().includes(query)
      )
    },
    
    pendingReports() {
      return this.reports.filter(report => report.status === 'pending').length
    },
    inProgressReports() {
      return this.reports.filter(report => report.status === 'in_progress').length
    }
  },
  async mounted() {
    await this.loadData()
  },
  methods: {
    async loadData() {
      try {
        await Promise.all([
          this.fetchUsers(),
          this.fetchReports()
        ])
      } catch (error) {
        this.showNotification('Errore nel caricamento dei dati', 'error')
      }
    },
    
    async fetchUsers() {
      try {
        const response = await api.get('/orgs')
        console.log('Dati utenti ricevuti:', response.data.users) // Aggiungi questo
        this.users = response.data.users
      } catch (error) {
        console.error('Errore nel recupero utenti:', error)
      }
    },
    
    async fetchReports() {
      try {
        // Cambia da fetch a api.get
        const response = await api.get('/reports/users')
        this.reports = response.data.map(report => ({
          _id: report._id,
          title: report.title,
          description: report.description,
          category: report.tags,
          status: report.status,
          date: report.createdAt,
          user: report.user._id,
          username: report.user.username
        }))
      } catch (error) {
        console.error('Errore nel recupero segnalazioni:', error)
        this.showNotification('Errore nel recupero delle segnalazioni', 'error')
      }
    },
    
    async updateReportStatus(report) {
      try {
        const fullReport = this.reports.find(r => r._id === report._id)
        
        // Cambia da fetch a api.patch
        const response = await api.patch(`/orgs/reports/${report._id}`, {
          reportData: {
            title: fullReport.title,
            description: fullReport.description,
            tags: fullReport.category,
            status: report.status,
            location: fullReport.location
          }
        })
        
        if (response.status === 200) {
          const index = this.reports.findIndex(r => r._id === report._id)
          if (index !== -1) {
            this.reports[index].status = report.status
          }
          this.showNotification('Stato aggiornato', 'success')
        }
      } catch (error) {
        console.error('Errore aggiornamento:', error)
        this.showNotification('Errore nell\'aggiornamento', 'error')
      }
    },
    
    async deleteReport(reportId) {
      if (!confirm('Sei sicuro di voler eliminare questa segnalazione?')) return
      
      try {
        // Cambia da fetch a api.delete
        await api.delete(`/orgs/reports/${reportId}`)
        this.reports = this.reports.filter(r => r._id !== reportId)
        this.showNotification('Segnalazione eliminata', 'success')
      } catch (error) {
        this.showNotification('Errore nell\'eliminazione', 'error')
      }
    },
    
    async suspendUser(userId) {
      
      this.showSuspendModal = true
      this.userToSuspend = userId
    },
    
    async confirmSuspendUser() {
      if (!this.userToSuspend) return
      
      try {
        const response = await api.patch(`/orgs/users/${this.userToSuspend}/suspend`)
        
        const user = this.users.find(u => u._id === this.userToSuspend)
        if (user) user.status = 'suspended'
        this.showNotification('Utente sospeso', 'success')
        this.closeSuspendModal()
      } catch (error) {
        console.error('Errore sospensione:', error)
        this.showNotification('Errore nella sospensione', 'error')
      }
    },
    
    closeSuspendModal() {
      this.showSuspendModal = false
      this.userToSuspend = null
    },
    
    async reactivateUser(userId) {
      try {
        // Usa api invece di fetch
        const response = await api.patch(`/orgs/users/${userId}/reactivate`)
        
        const user = this.users.find(u => u._id === userId)
        if (user) user.status = 'active'
        this.showNotification('Utente riattivato', 'success')
      } catch (error) {
        console.error('Errore riattivazione:', error)
        this.showNotification('Errore nella riattivazione', 'error')
      }
    },
    
    async deleteUser(userId) {
      if (!confirm('Sei sicuro di voler eliminare questo utente? Questa azione è irreversibile.')) return
      
      try {
        // Usa api invece di fetch
        await api.delete(`/orgs/users/${userId}`)
        
        this.users = this.users.filter(u => u._id !== userId)
        this.showNotification('Utente eliminato', 'success')
      } catch (error) {
        console.error('Errore eliminazione:', error)
        this.showNotification('Errore nell\'eliminazione', 'error')
      }
    },
    
    getUserName(userId) {
      // Se il report ha già il nome utente popolato, usalo
      const report = this.reports.find(r => r.user === userId)
      if (report && report.username) {
        return report.username
      }
      
      // Altrimenti cerca nell'array users
      const user = this.users.find(u => u._id === userId)
      return user ? user.username : 'Utente sconosciuto'
    },
    
    getUserReportsCount(userId) {
      return this.reports.filter(r => r.user === userId).length
    },
    
    formatDate(dateString) {
      return new Date(dateString).toLocaleDateString('it-IT')
    },
    
    getStatusColor(status) {
      switch(status) {
        case 'pending':
          return 'bg-red-100 text-red-800 border-red-300'
        case 'in_progress':
          return 'bg-yellow-100 text-yellow-800 border-yellow-300'
        case 'resolved':
          return 'bg-green-100 text-green-800 border-green-300'
        default:
          return 'bg-gray-100 text-gray-800 border-gray-300'
      }
    },
    
    showDescriptionModal(report) {
      this.selectedReport = report
      this.showModal = true
    },
    
    clearDateFilter() {
      this.dateFilter = ''
    },
    
    closeModal() {
      this.showModal = false
      this.selectedReport = null
    },
    
    showNotification(message, type = 'success') {
      this.notification = {
        show: true,
        type,
        message
      }
      
      setTimeout(() => {
        this.notification.show = false
      }, 3000)
    }
  }
}
</script>

<style scoped>
/* Animazioni esistenti */
.animate-slide-in {
  animation: slideIn 0.3s ease-out;
}

@keyframes slideIn {
  from {
    transform: translateX(100%);
    opacity: 0;
  }
  to {
    transform: translateX(0);
    opacity: 1;
  }
}

/* Nuove animazioni per notifiche migliorate */
.animate-notification-in {
  animation: notificationIn 0.5s cubic-bezier(0.68, -0.55, 0.265, 1.55);
}

@keyframes notificationIn {
  0% {
    transform: translateX(100%) scale(0.8);
    opacity: 0;
  }
  100% {
    transform: translateX(0) scale(1);
    opacity: 1;
  }
}

.animate-bounce-gentle {
  animation: bounceGentle 1s ease-in-out;
}

@keyframes bounceGentle {
  0%, 100% {
    transform: scale(1);
  }
  50% {
    transform: scale(1.1);
  }
}

.animate-progress-bar {
  animation: progressBar 3s linear forwards;
  width: 0;
}

@keyframes progressBar {
  0% {
    width: 100%;
  }
  100% {
    width: 0;
  }
}
</style>