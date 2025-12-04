<template>
  <div class="proposal-create">
    <div class="container">
      <div class="header">
        <div class="proposal-number">
          <span class="label">Proposal Number:</span>
          <div class="proposal-input">
            <span class="icon">📄</span>
            <input type="text" class="proposal-field" value="A20210030036" readonly />
          </div>
        </div>
      </div>

      <div class="warning-banner">
        THE INFORMATION CONTAINED HEREIN IS FOR ILLUSTRATING POLICY VALUE, BENEFITS,
        AND RELEVANT INFORMATION. THE POLICY PROVISION OF THE CONTRACT SHALL PREVAIL.
      </div>

      <div class="section">
        <h2>1. Policy Owner's Information</h2>
        <div class="form-row">
          <div class="form-group">
            <label>Full Name of Policy Owner:</label>
            <div class="input-with-icon">
              <span class="icon">👤</span>
              <input type="text" class="form-control" />
            </div>
          </div>
        </div>
        <div class="form-row">
          <div class="form-group">
            <label>Base Product Name:</label>
            <div class="input-with-icon error">
              <span class="icon">🛡️</span>
              <select class="form-control">
                <option>Lovely Family AV</option>
              </select>
            </div>
          </div>
        </div>
        <div class="form-row two-columns">
          <div class="form-group">
            <label>Proposal Date:</label>
            <input type="date" class="form-control" value="2025-10-01" />
          </div>
          <div class="form-group">
            <label>Expiry Date:</label>
            <input type="date" class="form-control" value="2035-10-30" />
          </div>
        </div>
      </div>

      <div class="warning-banner">
        THE INFORMATION CONTAINED HEREIN IS FOR ILLUSTRATING POLICY VALUE, BENEFITS,
        AND RELEVANT INFORMATION. THE POLICY PROVISION OF THE CONTRACT SHALL PREVAIL.
      </div>

      <div class="section">
        <h2>2. Proposal Summary</h2>
        <div class="form-row two-columns">
          <div class="form-group">
            <label>Full Name of Life Insured:</label>
            <div class="input-with-icon">
              <span class="icon">👤</span>
              <input type="text" class="form-control" />
            </div>
          </div>
          <div class="form-group">
            <label>Sum Insured (USD):</label>
            <div class="input-with-icon">
              <span class="icon">💰</span>
              <input type="text" class="form-control" value="1,050,000.00" />
            </div>
          </div>
        </div>
        <div class="form-row two-columns">
          <div class="form-group">
            <label>Date of Birth:</label>
            <input type="date" class="form-control" value="1985-07-30" />
          </div>
          <div class="form-group">
            <label>Age / Years old:</label>
            <input type="text" class="form-control" value="40" />
          </div>
          <div class="form-group">
            <label>Policy Term (year):</label>
            <div class="radio-group">
              <input type="radio" name="policyTerm" checked /> 30
            </div>
          </div>
        </div>
        <div class="form-row two-columns">
          <div class="form-group">
            <label>Gender:</label>
            <div class="input-with-icon">
              <span class="icon">👨</span>
              <select class="form-control">
                <option>Male</option>
                <option>Female</option>
              </select>
            </div>
          </div>
          <div class="form-group">
            <label>Premium (USD):</label>
            <div class="input-with-icon">
              <span class="icon">💵</span>
              <input type="text" class="form-control" value="144,300.00" />
            </div>
          </div>
        </div>
      </div>

      <div class="section">
        <h2>3. Coverage Summary</h2>
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
              <tr v-for="year in tableData" :key="year.term">
                <td>{{ year.term }}</td>
                <td>{{ year.age }}</td>
                <td>{{ year.premium }}</td>
                <td>{{ year.deathBenefit }}</td>
                <td>{{ year.disabilityBenefit }}</td>
                <td>{{ year.surrenderValue }}</td>
              </tr>
              <tr class="total-row">
                <td colspan="2"><strong>Sub Total</strong></td>
                <td><strong>144,300.00</strong></td>
                <td colspan="3"></td>
              </tr>
            </tbody>
          </table>
        </div>
        <p class="note">
          * The Policy Surrender Value stated above is under the assumption of premium payment year-end value.
        </p>
      </div>

      <div class="notes-section">
        <ol>
          <li>"Lovely Family" is a life insurance product with a coverage of 0-20 years.</li>
          <li>
            Death Benefit: The benefit will be provided by the basis of the sum assured death benefit or total
            and permanent disability of the life insured. If the event is death, the beneficiary will be paid the
            sum assured death benefit, plus the premium-paid revert value (PV). The policy shall be automatically
            terminated after the death or total permanent disability benefit is paid.
          </li>
          <li>
            Policy Surrender Value: This policy surrender value is payable to cede this policy after the policy year
            declines to terminate this policy during the policy term, and it will be automatically terminated with the
            surrender value payable, not less than the policy anniversary date of the sum assured payable at maturity.
          </li>
          <li>The illustration stated above is under the assumption of premium payment made on time.</li>
        </ol>
      </div>

      <div class="button-container">
        <button class="back-btn" @click="emit('back')">
          <i class="fa-solid fa-arrow-left"></i>
          Back to list
        </button>
        <button class="generate-btn">Confirm to Cover</button>
      </div>
    </div>
  </div>
</template>

<script setup>
const emit = defineEmits(['back'])

const tableData = [
  { term: 1, age: 40, premium: '144,300.00', deathBenefit: '1,050,000.00', disabilityBenefit: '1,300,000.00', surrenderValue: '93,053.28' },
  { term: 2, age: 41, premium: '-', deathBenefit: '1,050,000.00', disabilityBenefit: '1,300,000.00', surrenderValue: '99,873.07' },
  { term: 3, age: 42, premium: '-', deathBenefit: '1,050,000.00', disabilityBenefit: '1,300,000.00', surrenderValue: '102,988.93' },
  { term: 4, age: 43, premium: '-', deathBenefit: '1,050,000.00', disabilityBenefit: '1,300,000.00', surrenderValue: '101,388.75' },
  { term: 5, age: 44, premium: '-', deathBenefit: '1,050,000.00', disabilityBenefit: '1,300,000.00', surrenderValue: '105,281.88' },
  { term: 6, age: 45, premium: '-', deathBenefit: '1,050,000.00', disabilityBenefit: '1,300,000.00', surrenderValue: '106,147.01' },
  { term: 7, age: 46, premium: '-', deathBenefit: '1,050,000.00', disabilityBenefit: '1,300,000.00', surrenderValue: '101,923.87' },
  { term: 8, age: 47, premium: '-', deathBenefit: '1,050,000.00', disabilityBenefit: '1,300,000.00', surrenderValue: '95,923.85' },
  { term: 9, age: 48, premium: '-', deathBenefit: '1,050,000.00', disabilityBenefit: '1,300,000.00', surrenderValue: '84,803.98' },
  { term: 10, age: 49, premium: '-', deathBenefit: '1,050,000.00', disabilityBenefit: '1,300,000.00', surrenderValue: '70,088.33' },
  { term: 11, age: 50, premium: '-', deathBenefit: '1,050,000.00', disabilityBenefit: '1,300,000.00', surrenderValue: '66,201.78' },
  { term: 12, age: 51, premium: '-', deathBenefit: '1,050,000.00', disabilityBenefit: '1,300,000.00', surrenderValue: '91,347.70' },
  { term: 13, age: 52, premium: '-', deathBenefit: '1,050,000.00', disabilityBenefit: '1,300,000.00', surrenderValue: '74,410.81' },
  { term: 14, age: 53, premium: '-', deathBenefit: '1,050,000.00', disabilityBenefit: '1,300,000.00', surrenderValue: '69,659.55' },
  { term: 15, age: 54, premium: '-', deathBenefit: '1,050,000.00', disabilityBenefit: '1,300,000.00', surrenderValue: '80,788.94' },
  { term: 16, age: 55, premium: '-', deathBenefit: '1,050,000.00', disabilityBenefit: '1,300,000.00', surrenderValue: '57,278.88' },
  { term: 17, age: 56, premium: '-', deathBenefit: '1,050,000.00', disabilityBenefit: '1,300,000.00', surrenderValue: '49,401.53' },
  { term: 18, age: 57, premium: '-', deathBenefit: '1,050,000.00', disabilityBenefit: '1,300,000.00', surrenderValue: '38,671.88' },
  { term: 19, age: 58, premium: '-', deathBenefit: '1,050,000.00', disabilityBenefit: '1,300,000.00', surrenderValue: '-' },
  { term: 20, age: 59, premium: '-', deathBenefit: '1,050,000.00', disabilityBenefit: '1,300,000.00', surrenderValue: '70,754.61' }
]
</script>

<style scoped>
.proposal-create {
  font-family: 'Battambang', 'Kantumruy Pro', Arial, sans-serif;
  background-color: #f5f5f5;
  padding: 20px 0;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  background-color: white;
  padding: 20px;
}

.header {
  text-align: right;
  margin-bottom: 10px;
}

.proposal-number {
  display: inline-flex;
  align-items: center;
  gap: 10px;
}

.proposal-number .label {
  font-weight: normal;
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
  padding: 6px 10px 6px 35px;
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

.section h2 {
  background-color: #e8e8e8;
  padding: 10px;
  font-size: 16px;
  margin-bottom: 15px;
}

.form-row {
  margin-bottom: 15px;
}

.form-row.two-columns {
  display: grid;
  grid-template-columns: 1fr 1fr;
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
}

.input-with-icon .form-control,
.input-with-icon select {
  padding-left: 35px;
  width: 100%;
}

.input-with-icon.error {
  color: #d32f2f;
}

.radio-group {
  padding: 8px;
  border: 1px solid #ddd;
  border-radius: 3px;
  background-color: white;
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
}

.coverage-table td {
  padding: 8px 5px;
  text-align: right;
  border: 1px solid #ddd;
}

.coverage-table tbody tr:nth-child(even) {
  background-color: #fafafa;
}

.total-row {
  background-color: #f5f5f5 !important;
  font-weight: bold;
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

.back-btn {
  background-color: #f5f0e6;
  border: 1px solid #ddd;
  color: #555;
  padding: 10px 20px;
  border-radius: 3px;
  cursor: pointer;
  font-size: 14px;
  display: inline-flex;
  align-items: center;
  gap: 8px;
  margin-right: 10px;
  transition: background-color 0.3s;
}

.back-btn:hover {
  background-color: #e8e8e8;
}

.generate-btn {
  background-color: #c9a861;
  color: white;
  padding: 10px 30px;
  border: none;
  border-radius: 3px;
  cursor: pointer;
  font-size: 14px;
}

.generate-btn:hover {
  background-color: #b8974f;
}

@media (max-width: 768px) {
  .proposal-create {
    padding: 10px 0;
  }

  .container {
    padding: 15px;
  }

  .header {
    text-align: center;
    margin-bottom: 15px;
  }

  .proposal-number {
    flex-direction: column;
    gap: 8px;
    width: 100%;
  }

  .proposal-input {
    width: 100%;
  }

  .proposal-field {
    width: 100%;
    min-width: unset;
  }

  .warning-banner {
    font-size: 10px;
    padding: 8px;
  }

  .section h2 {
    font-size: 14px;
    padding: 8px;
  }

  .form-row.two-columns {
    grid-template-columns: 1fr;
    gap: 10px;
  }

  .form-group label {
    font-size: 12px;
  }

  .form-control {
    font-size: 13px;
    padding: 7px;
  }

  .input-with-icon .form-control,
  .input-with-icon select {
    padding-left: 32px;
  }

  .coverage-table {
    font-size: 9px;
  }

  .coverage-table th,
  .coverage-table td {
    padding: 6px 3px;
  }

  .notes-section {
    padding: 12px;
  }

  .notes-section ol {
    margin-left: 15px;
    font-size: 10px;
  }

  .generate-btn {
    width: 100%;
    padding: 12px;
    font-size: 15px;
  }

  .button-container {
    padding: 15px 0;
  }
}

@media (max-width: 480px) {
  .container {
    padding: 10px;
  }

  .coverage-table {
    font-size: 8px;
  }

  .coverage-table th,
  .coverage-table td {
    padding: 4px 2px;
  }

  .form-control {
    font-size: 12px;
  }
}
</style>
