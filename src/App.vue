<script setup>
import { ref, onMounted } from 'vue'
import { Modal } from 'bootstrap'

const searchValue = ref('')
const showNoData = ref(false)

const proposals = ref([
  {
    no: '001',
    policyNumber: 'POL-20251126-01-536645',
    insuredName: 'Phun Sinath',
    insuranceName: 'Shining Life',
    coverageAmount: '$5,000.00',
    premium: '$849.00',
    applicationDate: '2025-11-26'
  },
  {
    no: '002',
    policyNumber: 'POL-20251125-02-428391',
    insuredName: 'Sok Dara',
    insuranceName: 'Health Plus',
    coverageAmount: '$10,000.00',
    premium: '$1,250.00',
    applicationDate: '2025-11-25'
  },
  {
    no: '003',
    policyNumber: 'POL-20251124-03-912847',
    insuredName: 'Chan Virak',
    insuranceName: 'Future Protect',
    coverageAmount: '$7,500.00',
    premium: '$950.00',
    applicationDate: '2025-11-24'
  }
])

const filteredProposals = ref([...proposals.value])

function searchPolicy () {
  filteredProposals.value = proposals.value.filter(p =>
    p.policyNumber.toLowerCase().includes(searchValue.value.toLowerCase())
  )

  showNoData.value = filteredProposals.value.length === 0
}

const modalProposalNumber = ref('')
const policyOwnerName = ref('')
const productName = ref('')
const proposalDate = ref('2025-10-01')
const expiryDate = ref('2025-10-30')
const insuredName = ref('')
const sumInsured = ref('1,000,000.00')
const dob = ref('1985-07-01')
const age = ref(40)
const policyTerm = ref(20)
const gender = ref('Male')
const premiumUSD = ref('144,300.00')

function openEditModal (p) {
  modalProposalNumber.value = p.policyNumber

  const modal = new Modal(document.getElementById('editModal'))
  modal.show()
}

function saveProposal () {
  console.log('Saving:', {
    policyNumber: modalProposalNumber.value,
    owner: policyOwnerName.value,
    product: productName.value,
    proposalDate: proposalDate.value
  })
}

function printPolicy (number) {
  alert('Printing: ' + number)
  window.print()
}

function viewDetail () {
  alert('Go to detail page')
}

function processApplication (number) {
  alert('Processing Application: ' + number)
}

function exportToExcel () {
  alert('Export to Excel coming soon')
}

onMounted(() => {
  document.getElementById('searchInput')?.addEventListener('keypress', e => {
    if (e.key === 'Enter') searchPolicy()
  })
})
</script>

<template>
  <div class="container">
    <div class="header-section">
      <h1 class="page-title">Proposal View</h1>
      <button class="create-new-btn">Create New</button>
    </div>

    <hr />

    <div class="controls-section">
      <div class="search-box">
        <input
          v-model="searchValue"
          type="text"
          class="search-input form-control"
          placeholder="Enter policy number"
          id="searchInput"
        />

        <button class="search-btn" @click="searchPolicy">
          <i class="fa-solid fa-magnifying-glass"></i>
        </button>
      </div>
    </div>

    <div class="table-responsive">
      <table class="proposal-table">
        <thead>
          <tr>
            <th>no.</th>
            <th>Policy Number</th>
            <th>Insured Name</th>
            <th>Insurance Name</th>
            <th>Coverage Amount</th>
            <th>Premium</th>
            <th>Application Date</th>
            <th>Actions</th>
          </tr>
        </thead>

        <tbody>
          <tr v-for="(p, i) in filteredProposals" :key="i">
            <td>{{ p.no }}</td>
            <td>{{ p.policyNumber }}</td>
            <td>{{ p.insuredName }}</td>
            <td>{{ p.insuranceName }}</td>
            <td>{{ p.coverageAmount }}</td>
            <td>{{ p.premium }}</td>
            <td>{{ p.applicationDate }}</td>

            <td>
              <div class="dropdown">
                <button
                  class="view-btn dropdown-toggle"
                  type="button"
                  data-bs-toggle="dropdown"
                  aria-expanded="false"
                >
                  View
                </button>

                <ul class="dropdown-menu">
                  <li>
                    <a class="dropdown-item" href="#" @click="viewDetail()">View Detail</a>
                  </li>
                  <li>
                    <a class="dropdown-item" href="#" @click="openEditModal(p)">Edit</a>
                  </li>
                  <li>
                    <a class="dropdown-item" href="#" @click="printPolicy(p.policyNumber)">Print</a>
                  </li>
                  <li>
                    <a class="dropdown-item" href="#" @click="processApplication(p.policyNumber)">
                      Process to Application
                    </a>
                  </li>
                </ul>
              </div>
            </td>
          </tr>

          <tr v-if="showNoData">
            <td colspan="8" class="no-data-cell">
              <div class="no-data-message">
                <i class="fa-solid fa-folder-open"></i>
                <p>No data found</p>
                <small>No records match your search criteria</small>
              </div>
            </td>
          </tr>
        </tbody>
      </table>
    </div>

    <div class="button-group mt-3">
      <button class="export-btn" @click="exportToExcel">Export Excel</button>
    </div>
  </div>

  <div class="modal fade" id="editModal" tabindex="-1">
    <div class="modal-dialog modal-xl modal-dialog-scrollable">
      <div class="modal-content">
        <div class="modal-header">
          <h5 class="modal-title">Edit Proposal</h5>
          <button type="button" class="btn-close" data-bs-dismiss="modal"></button>
        </div>
        <div class="modal-body">
          <div class="edit-container">
            <div class="edit-header">
              <div class="proposal-number-display">
                <span class="label">Proposal Number:</span>
                <div class="proposal-input">
                  <span class="icon">📄</span>
                  <input v-model="modalProposalNumber" type="text" class="proposal-field" readonly />
                </div>
              </div>
            </div>

            <div class="form-row">
              <label>Policy Owner Name:</label>
              <input v-model="policyOwnerName" type="text" class="form-control" />
            </div>

            <div class="modal-footer">
              <button class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
              <button class="btn btn-primary save-modal-btn" @click="saveProposal()">Save Changes</button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.container {
  max-width: 1200px;
  margin: 0 auto;
  background: white;
  padding: 30px;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.page-title {
  color: #b37e0c;
  font-size: 28px;
  font-weight: 600;
}

.export-btn {
  background: #c9a861;
  color: white;
  border: none;
  padding: 8px 25px;
  border-radius: 3px;
}
</style>
