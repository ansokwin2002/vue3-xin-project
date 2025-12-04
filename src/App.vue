<script setup>
import { ref, onMounted, onBeforeUnmount, watch } from 'vue'
import { Modal } from 'bootstrap'
import ProposalCreate from './views/proposal/ProposalCreate.vue'

const showCreatePage = ref(false)
const searchValue = ref('')
const showNoData = ref(false)
const openDropdownIndex = ref(null)
const dropdownPosition = ref({ top: 0, left: 0 })
const dropdownData = ref(null)
const dropdownArrowOffset = ref(20)

function toggleDropdown (index, event) {
  if (openDropdownIndex.value === index) {
    closeDropdown()
    return
  }

  const buttonRect = event.currentTarget.getBoundingClientRect()
  dropdownPosition.value = {
    top: buttonRect.bottom + window.scrollY + 10,
    left: buttonRect.left + window.scrollX
  }
  dropdownArrowOffset.value = Math.min(buttonRect.width / 2 + 10, 40)
  dropdownData.value = filteredProposals.value[index]
  openDropdownIndex.value = index
}

function closeDropdown () {
  openDropdownIndex.value = null
  dropdownData.value = null
}

function handleClickOutside (event) {
  if (!event.target.closest('.dropdown') && !event.target.closest('.floating-dropdown')) {
    closeDropdown()
  }
}

onMounted(() => {
  document.getElementById('searchInput')?.addEventListener('keypress', e => {
    if (e.key === 'Enter') searchPolicy()
  })

  document.addEventListener('click', handleClickOutside)
})

watch(showCreatePage, value => {
  if (value) closeDropdown()
})

onBeforeUnmount(() => {
  document.removeEventListener('click', handleClickOutside)
})

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

watch(filteredProposals, () => {
  closeDropdown()
})

function searchPolicy () {
  filteredProposals.value = proposals.value.filter(p =>
    p.policyNumber.toLowerCase().includes(searchValue.value.toLowerCase())
  )

  showNoData.value = filteredProposals.value.length === 0
}

const modalProposalNumber = ref('')
const policyOwnerName = ref('')
const baseProductName = ref('Lovely Family (A)')
const proposalDate = ref('2025-10-01')
const expiryDate = ref('2025-10-30')
const lifeInsuredName = ref('')
const sumInsured = ref('1,000,000.00')
const dob = ref('1985-07-01')
const age = ref(40)
const policyTerm = ref(20)
const gender = ref('Male')
const premiumUSD = ref('144,300.00')

const coverageSummary = [
  { term: 1, age: 40, premium: '144,300.00', death: '1,000,000.00', disability: '1,300,000.00', surrender: '92,053.39' },
  { term: 2, age: 41, premium: '-', death: '1,000,000.00', disability: '1,300,000.00', surrender: '8,125.03' },
  { term: 3, age: 42, premium: '-', death: '1,000,000.00', disability: '1,300,000.00', surrender: '102,188.55' },
  { term: 4, age: 43, premium: '-', death: '1,000,000.00', disability: '1,300,000.00', surrender: '104,289.75' },
  { term: 5, age: 44, premium: '-', death: '1,000,000.00', disability: '1,300,000.00', surrender: '106,408.69' },
  { term: 6, age: 45, premium: '-', death: '1,000,000.00', disability: '1,300,000.00', surrender: '103,433.61' },
  { term: 7, age: 46, premium: '-', death: '1,000,000.00', disability: '1,300,000.00', surrender: '103,523.87' },
  { term: 8, age: 47, premium: '-', death: '1,000,000.00', disability: '1,300,000.00', surrender: '86,320.84' },
  { term: 9, age: 48, premium: '-', death: '1,000,000.00', disability: '1,300,000.00', surrender: '94,829.59' },
  { term: 10, age: 49, premium: '-', death: '1,000,000.00', disability: '1,300,000.00', surrender: '85,896.79' },
  { term: 11, age: 50, premium: '-', death: '1,000,000.00', disability: '1,300,000.00', surrender: '66,325.76' },
  { term: 12, age: 51, premium: '-', death: '1,000,000.00', disability: '1,300,000.00', surrender: '81,317.70' },
  { term: 13, age: 52, premium: '-', death: '1,000,000.00', disability: '1,300,000.00', surrender: '74,420.61' },
  { term: 14, age: 53, premium: '-', death: '1,000,000.00', disability: '1,300,000.00', surrender: '68,816.16' },
  { term: 15, age: 54, premium: '-', death: '1,000,000.00', disability: '1,300,000.00', surrender: '60,709.34' },
  { term: 16, age: 55, premium: '-', death: '1,000,000.00', disability: '1,300,000.00', surrender: '51,770.38' },
  { term: 17, age: 56, premium: '-', death: '1,000,000.00', disability: '1,300,000.00', surrender: '41,847.18' },
  { term: 18, age: 57, premium: '-', death: '1,000,000.00', disability: '1,300,000.00', surrender: '30,668.42' },
  { term: 19, age: 58, premium: '-', death: '1,000,000.00', disability: '1,300,000.00', surrender: '16,754.60' },
  { term: 20, age: 59, premium: '-', death: '1,000,000.00', disability: '1,300,000.00', surrender: '-' }
]

function openEditModal (p) {
  modalProposalNumber.value = p.policyNumber
  policyOwnerName.value = p.insuredName
  lifeInsuredName.value = p.insuredName

  closeDropdown()

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
  closeDropdown()
  alert('Printing: ' + number)
  window.print()
}

function viewDetail () {
  closeDropdown()
  alert('Go to detail page')
}

function processApplication (number) {
  closeDropdown()
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
  <ProposalCreate v-if="showCreatePage" @back="showCreatePage = false" />

  <div v-else class="container">
    <div class="header-section">
      <h1 class="page-title">Proposal View</h1>
      <button class="create-new-btn" @click="showCreatePage = true">Create New</button>
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
              <div class="dropdown" @click.stop>
                <button class="view-btn" type="button" @click="toggleDropdown(i, $event)">
                  View
                  <i class="fa-solid fa-caret-down ms-2"></i>
                </button>
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

  <transition name="dropdown">
    <div
      v-if="openDropdownIndex !== null && dropdownData"
      class="floating-dropdown"
      :style="{ top: dropdownPosition.top + 'px', left: dropdownPosition.left + 'px', '--arrow-left': dropdownArrowOffset + 'px' }"
    >
      <button class="dropdown-option" @click="viewDetail()">
        <i class="fa-solid fa-eye"></i>
        View Detail
      </button>
      <button class="dropdown-option" @click="openEditModal(dropdownData)">
        <i class="fa-solid fa-pen-to-square"></i>
        Edit
      </button>
      <button class="dropdown-option" @click="printPolicy(dropdownData.policyNumber)">
        <i class="fa-solid fa-print"></i>
        Print
      </button>
      <button class="dropdown-option" @click="processApplication(dropdownData.policyNumber)">
        <i class="fa-solid fa-diagram-project"></i>
        Process to Application
      </button>
    </div>
  </transition>

  <div class="modal fade" id="editModal" tabindex="-1">
    <div class="modal-dialog modal-xl modal-dialog-scrollable">
      <div class="modal-content proposal-modal">
        <div class="modal-body p-0">
          <div class="proposal-detail">
            <div class="header">
              <div class="header-right">
                <div class="proposal-number">
                  <span class="label">Proposal Number:</span>
                  <div class="proposal-input">
                    <span class="icon">📄</span>
                    <input v-model="modalProposalNumber" type="text" class="proposal-field" readonly />
                  </div>
                </div>
              </div>
            </div>

            <div class="warning-banner">
              THE INFORMATION CONTAINED HEREIN IS FOR ILLUSTRATING POLICY VALUE, BENEFITS, AND RELEVANT INFORMATION. THE POLICY
              PROVISION OF THE CONTRACT SHALL PREVAIL.
            </div>

            <div class="section">
              <div class="section-header">
                <h2>1. Policy Owner's Information</h2>
              </div>

              <div class="form-content">
                <div class="form-row">
                  <div class="form-group">
                    <label>Full Name of Policy Owner:</label>
                    <div class="input-with-icon">
                      <span class="icon">👤</span>
                      <input v-model="policyOwnerName" type="text" class="form-control" />
                    </div>
                  </div>
                </div>

                <div class="form-row">
                  <div class="form-group">
                    <label>Base Product Name:</label>
                    <div class="input-with-icon">
                      <span class="icon">📋</span>
                      <select v-model="baseProductName" class="form-control">
                        <option>Lovely Family (A)</option>
                        <option>Living Twenty (A)</option>
                        <option>Shining Life</option>
                      </select>
                    </div>
                  </div>
                </div>

                <div class="form-row two-columns">
                  <div class="form-group">
                    <label>Proposal Date:</label>
                    <input v-model="proposalDate" type="date" class="form-control" />
                  </div>
                  <div class="form-group">
                    <label>Expiry Date:</label>
                    <input v-model="expiryDate" type="date" class="form-control" />
                  </div>
                </div>
              </div>
            </div>

            <div class="warning-banner">
              THE INFORMATION CONTAINED HEREIN IS FOR ILLUSTRATING POLICY VALUE, BENEFITS, AND RELEVANT INFORMATION. THE POLICY
              PROVISION OF THE CONTRACT SHALL PREVAIL.
            </div>

            <div class="section">
              <div class="section-header">
                <h2>2. Proposal Summary</h2>
              </div>

              <div class="form-content">
                <div class="form-row two-columns">
                  <div class="form-group">
                    <label>Full Name of Life Insured:</label>
                    <div class="input-with-icon">
                      <span class="icon">👤</span>
                      <input v-model="lifeInsuredName" type="text" class="form-control" />
                    </div>
                  </div>
                  <div class="form-group">
                    <label>Sum Insured (USD):</label>
                    <div class="input-with-icon">
                      <span class="icon">💰</span>
                      <input v-model="sumInsured" type="text" class="form-control" />
                    </div>
                  </div>
                </div>

                <div class="form-row three-columns">
                  <div class="form-group">
                    <label>Date of Birth:</label>
                    <input v-model="dob" type="date" class="form-control" />
                  </div>
                  <div class="form-group">
                    <label>Age / Years old:</label>
                    <input v-model="age" type="number" class="form-control" />
                  </div>
                  <div class="form-group">
                    <label>Policy Term (year):</label>
                    <div class="input-with-icon">
                      <span class="icon">📊</span>
                      <select v-model="policyTerm" class="form-control">
                        <option value="10">10</option>
                        <option value="15">15</option>
                        <option value="20">20</option>
                        <option value="30">30</option>
                      </select>
                    </div>
                  </div>
                </div>

                <div class="form-row two-columns">
                  <div class="form-group">
                    <label>Gender:</label>
                    <div class="input-with-icon">
                      <span class="icon">⚧</span>
                      <select v-model="gender" class="form-control">
                        <option>Male</option>
                        <option>Female</option>
                        <option>Other</option>
                      </select>
                    </div>
                  </div>
                  <div class="form-group">
                    <label>Premium (USD):</label>
                    <div class="input-with-icon">
                      <span class="icon">💵</span>
                      <input v-model="premiumUSD" type="text" class="form-control" />
                    </div>
                  </div>
                </div>
              </div>
            </div>

            <div class="section">
              <div class="section-header">
                <h2>3. Coverage Summary</h2>
              </div>

              <div class="table-responsive">
                <table class="coverage-table">
                  <thead>
                    <tr>
                      <th>Policy Term</th>
                      <th>Insurance Age</th>
                      <th>Insurance Premium</th>
                      <th>Death Benefit</th>
                      <th>Total and Permanent Disability Benefit</th>
                      <th>Policy Surrender Value</th>
                    </tr>
                  </thead>
                  <tbody>
                    <tr v-for="row in coverageSummary" :key="row.term">
                      <td>{{ row.term }}</td>
                      <td>{{ row.age }}</td>
                      <td>{{ row.premium }}</td>
                      <td>{{ row.death }}</td>
                      <td>{{ row.disability }}</td>
                      <td>{{ row.surrender }}</td>
                    </tr>
                  </tbody>
                </table>
              </div>

              <p class="note">
                * The Policy Surrender Value stated above is after the policy year represents year-end value.
              </p>
            </div>

            <div class="notes-section">
              <ol>
                <li>Young Family + is the insurance product with a coverage of 21 years.</li>
                <li>
                  Total and Permanent Disability Benefit will be paid based on the higher of the insured's own occupation or any occupation.
                  If the life insured dies after receiving TPD benefit, the policy terminates.
                </li>
                <li>
                  Policy Surrender Value is payable if the policy owner has maintained the policy without lapse for at least 3 years and requests termination after the policy anniversary.
                </li>
                <li>The illustration shown above assumes all premium payments are made on time.</li>
              </ol>
            </div>

            <div class="button-container">
              <button class="save-btn" @click="saveProposal()">
                <i class="fa-solid fa-floppy-disk me-2"></i>
                Save Changes
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: 'Battambang', 'Kantumruy Pro', Arial, sans-serif;
  background-color: #f5f5f5;
  padding: 20px;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  background-color: white;
  padding: 30px;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.header-section {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 15px;
}

hr {
  border: none;
  border-top: 1px solid #e0e0e0;
  margin: 0 0 20px 0;
}

.page-title {
  color: #b37e0c;
  font-size: 28px;
  font-weight: 600;
}

.create-new-btn {
  background-color: #f5f0e6;
  border: 1px solid #ddd;
  padding: 8px 25px;
  border-radius: 3px;
  cursor: pointer;
  font-size: 13px;
  transition: background-color 0.3s;
}

.create-new-btn:hover {
  background-color: #e8e8e8;
}

.controls-section {
  display: flex;
  justify-content: flex-end;
  align-items: center;
  margin-bottom: 20px;
}

.button-group {
  display: flex;
  gap: 10px;
}

.export-btn {
  background-color: #c9a861;
  color: white;
  border: none;
  padding: 8px 25px;
  border-radius: 3px;
  cursor: pointer;
  font-size: 13px;
  transition: background-color 0.3s;
}

.export-btn:hover {
  background-color: #b8974f;
}

.search-box {
  display: flex;
  max-width: 400px;
  gap: 10px;
}

.search-input {
  flex: 1;
  padding: 8px 12px;
  border: 1px solid #ddd;
  border-radius: 3px;
  font-size: 13px;
  min-width: 250px;
}

.search-btn {
  background-color: white;
  border: 1px solid #ddd;
  padding: 8px 12px;
  border-radius: 3px;
  cursor: pointer;
  font-size: 16px;
  transition: background-color 0.3s;
}

.search-btn:hover {
  background-color: #f5f5f5;
}

.table-responsive {
  overflow: visible;
  position: relative;
  margin-bottom: 10px;
}

.proposal-table {
  width: 100%;
  border-collapse: collapse;
  font-size: 13px;
  margin-bottom: 0;
}

.proposal-table thead {
  background-color: #f5f5f5;
}

.proposal-table th {
  padding: 10px 12px;
  text-align: center;
  font-weight: 600;
  color: #333;
  white-space: nowrap;
  border: 1px solid #ddd;
  font-size: 13px;
}

.proposal-table td {
  padding: 10px 12px;
  color: #555;
  border: 1px solid #ddd;
  text-align: center;
}

.proposal-table tbody tr:nth-child(even) {
  background-color: #fafafa;
}

.proposal-table tbody tr {
  position: relative;
}

.proposal-table tbody tr:hover {
  background-color: #f9f9f9;
}

.view-btn {
  background-color: #c9a861;
  color: white;
  border: none;
  padding: 6px 16px;
  border-radius: 4px;
  cursor: pointer;
  font-size: 13px;
  transition: background-color 0.3s;
  font-family: 'Battambang', 'Kantumruy Pro', Arial, sans-serif;
}

.view-btn:hover {
  background-color: #b8974f;
}

.dropdown {
  position: relative;
}

.floating-dropdown,
.custom-dropdown {
  font-family: 'Battambang', 'Kantumruy Pro', Arial, sans-serif;
  font-size: 14px;
  border-radius: 8px;
  box-shadow: 0 8px 24px rgba(0, 0, 0, 0.15);
  border: 1px solid #e0e0e0;
  min-width: 220px;
  background-color: white;
  padding: 8px 0;
}

.custom-dropdown {
  position: absolute;
  z-index: 1050;
  left: 0;
  top: calc(100% + 10px);
}

.floating-dropdown {
  position: absolute;
  z-index: 2000;
}

.custom-dropdown::before,
.floating-dropdown::before {
  content: '';
  position: absolute;
  top: -10px;
  left: var(--arrow-left, 20px);
  border-width: 0 10px 10px 10px;
  border-style: solid;
  border-color: transparent transparent white transparent;
}

.custom-dropdown::after,
.floating-dropdown::after {
  content: '';
  position: absolute;
  top: -11px;
  left: var(--arrow-left, 20px);
  border-width: 0 10px 10px 10px;
  border-style: solid;
  border-color: transparent transparent #e0e0e0 transparent;
  z-index: -1;
}

.dropdown-option {
  width: 100%;
  background: transparent;
  border: none;
  display: flex;
  align-items: center;
  gap: 10px;
  padding: 10px 16px;
  font-size: 13px;
  color: #444;
  cursor: pointer;
  transition: background-color 0.2s, color 0.2s;
}

.dropdown-option i {
  color: #c9a861;
}

.dropdown-option:hover {
  background-color: #fff7e6;
  color: #b37e0c;
}

.dropdown-enter-active,
.dropdown-leave-active {
  transition: opacity 0.2s ease, transform 0.2s ease;
}

.dropdown-enter-from,
.dropdown-leave-to {
  opacity: 0;
  transform: translateY(12px);
}

.dropdown-enter-to,
.dropdown-leave-from {
  opacity: 1;
  transform: translateY(0);
}

.no-data-cell {
  text-align: center;
  padding: 0 !important;
  border: none !important;
}

.no-data-message {
  text-align: center;
  padding: 60px 20px;
  color: #999;
}

.no-data-message i {
  font-size: 64px;
  color: #ddd;
  margin-bottom: 20px;
}

.no-data-message p {
  font-size: 18px;
  font-weight: 500;
  color: #666;
  margin: 10px 0 5px 0;
}

.no-data-message small {
  font-size: 14px;
  color: #999;
}

@media (max-width: 992px) {
  .controls-section {
    flex-direction: column;
    align-items: stretch;
  }

  .search-box {
    max-width: 100%;
  }

  .search-input {
    min-width: auto;
  }
}

@media (max-width: 768px) {
  body {
    padding: 10px;
  }

  .container {
    padding: 20px;
  }

  .header-section {
    flex-direction: column;
    align-items: flex-start;
    gap: 15px;
  }

  .page-title {
    font-size: 24px;
  }

  .create-new-btn {
    width: 100%;
  }

  .table-responsive {
    overflow-x: auto;
  }

  .proposal-table {
    font-size: 12px;
    min-width: 800px;
  }

  .proposal-table th,
  .proposal-table td {
    padding: 10px 8px;
  }

  .export-btn {
    width: 100%;
  }
}

@media (max-width: 480px) {
  .container {
    padding: 15px;
  }

  .page-title {
    font-size: 20px;
  }

  .proposal-table {
    font-size: 11px;
  }

  .proposal-table th,
  .proposal-table td {
    padding: 8px 6px;
  }
}

.proposal-modal {
  border-radius: 12px;
  overflow: hidden;
  border: none;
}

.modal-body {
  padding: 0;
  max-height: calc(100vh - 140px);
  overflow-y: auto;
}

.proposal-detail {
  font-family: 'Battambang', 'Kantumruy Pro', Arial, sans-serif;
  background-color: white;
  padding: 30px;
}

.proposal-detail .header {
  display: flex;
  justify-content: flex-end;
  align-items: center;
  margin-bottom: 15px;
}

.proposal-detail .header-right {
  display: flex;
  align-items: center;
  gap: 15px;
  justify-content: flex-end;
}

.proposal-detail .page-title {
  color: #b37e0c;
  font-size: 24px;
  font-weight: 600;
}

.back-btn {
  background-color: #f5f5f5;
  border: 1px solid #ddd;
  padding: 8px 20px;
  border-radius: 4px;
  cursor: pointer;
  font-size: 14px;
  transition: background-color 0.3s;
}

.back-btn:hover {
  background-color: #e8e8e8;
}

.proposal-number {
  display: inline-flex;
  align-items: center;
  gap: 10px;
}

.proposal-number .label {
  font-weight: normal;
  font-size: 14px;
}

.proposal-input {
  position: relative;
  display: inline-flex;
  align-items: center;
}

.proposal-input .icon {
  position: absolute;
  left: 8px;
  font-size: 16px;
  color: #b37e0c;
}

.proposal-field {
  padding: 6px 35px 6px 30px;
  border: 2px solid #b37e0c;
  border-radius: 4px;
  font-size: 14px;
  font-weight: 600;
  color: #b37e0c;
  background-color: white;
  min-width: 180px;
}

.warning-banner {
  background-color: #c9a861;
  color: white;
  padding: 10px;
  text-align: center;
  font-size: 11px;
  margin-bottom: 20px;
  line-height: 1.4;
}

.section {
  margin-bottom: 20px;
}

.section-header {
  background-color: #e8e8e8;
  padding: 10px;
  display: flex;
  align-items: center;
  gap: 15px;
  margin-bottom: 0;
}

.section-left {
  display: flex;
  align-items: center;
  gap: 10px;
}

.section-badge {
  background-color: #c9a861;
  color: white;
  padding: 4px 10px;
  border-radius: 3px;
  font-size: 11px;
  font-weight: 600;
}

.divider {
  color: #999;
}

.section-code {
  color: #333;
  font-weight: 600;
  font-size: 13px;
}

.section-header h2 {
  font-size: 16px;
  margin: 0;
  flex: 1;
  font-weight: 600;
}

.export-btn {
  background-color: #c9a861;
  color: white;
  border: none;
  padding: 6px 16px;
  border-radius: 4px;
  cursor: pointer;
  font-size: 12px;
  transition: background-color 0.3s;
  display: inline-flex;
  align-items: center;
  gap: 8px;
}

.export-btn:hover {
  background-color: #b8974f;
}

.form-content {
  padding: 20px;
  background-color: white;
}

.form-row {
  margin-bottom: 15px;
}

.form-row.two-columns {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 15px;
}

.form-row.three-columns {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  gap: 15px;
}

.form-group {
  display: flex;
  flex-direction: column;
}

.form-group label {
  font-size: 13px;
  margin-bottom: 5px;
  color: #333;
}

.form-control {
  padding: 8px;
  border: 1px solid #ddd;
  border-radius: 3px;
  font-size: 14px;
  font-family: 'Kantumruy Pro', Arial, sans-serif;
}

.form-control:focus {
  outline: none;
  border-color: #c9a861;
}

.input-with-icon {
  position: relative;
  display: flex;
  align-items: center;
}

.input-with-icon .icon {
  position: absolute;
  left: 10px;
  font-size: 16px;
  color: #c9a861;
  z-index: 1;
}

.input-with-icon .form-control,
.input-with-icon select {
  padding-left: 35px;
  width: 100%;
}

.input-with-icon select.form-control {
  appearance: none;
  background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='12' height='12' viewBox='0 0 12 12'%3E%3Cpath fill='%23666' d='M6 9L1 4h10z'/%3E%3C/svg%3E");
  background-repeat: no-repeat;
  background-position: right 12px center;
  padding-right: 35px;
}

.table-responsive {
  overflow-x: auto;
  margin-bottom: 10px;
}

.coverage-table {
  width: 100%;
  border-collapse: collapse;
  font-size: 12px;
}

.coverage-table th {
  background-color: #f5f5f5;
  padding: 10px 5px;
  text-align: center;
  border: 1px solid #ddd;
  font-size: 11px;
  font-weight: 600;
}

.coverage-table td {
  padding: 8px 5px;
  text-align: right;
  border: 1px solid #ddd;
}

.coverage-table tbody tr:nth-child(even) {
  background-color: #fafafa;
}

.note {
  font-size: 11px;
  color: #d32f2f;
  margin-top: 5px;
}

.notes-section {
  background-color: #fff9e6;
  padding: 15px;
  margin-bottom: 20px;
}

.notes-section ol {
  margin-left: 20px;
  font-size: 11px;
  line-height: 1.6;
}

.notes-section li {
  margin-bottom: 8px;
}

.button-container {
  text-align: right;
  padding: 20px 0;
}

.save-btn {
  background-color: #c9a861;
  color: white;
  padding: 10px 30px;
  border: none;
  border-radius: 3px;
  cursor: pointer;
  font-size: 14px;
  font-weight: 600;
  display: inline-flex;
  align-items: center;
  gap: 8px;
}

.save-btn:hover {
  background-color: #b8974f;
}

@media (max-width: 768px) {
  .modal-dialog {
    margin: 1rem;
  }

  .proposal-detail {
    padding: 20px;
  }

  .proposal-detail .header {
    flex-direction: column;
    align-items: flex-start;
    gap: 12px;
  }

  .proposal-detail .header-right {
    flex-direction: column;
    align-items: flex-start;
    gap: 10px;
  }

  .form-row.two-columns,
  .form-row.three-columns {
    grid-template-columns: 1fr;
  }

  .coverage-table {
    font-size: 10px;
  }

  .coverage-table th,
  .coverage-table td {
    padding: 6px 3px;
  }
}
</style>
