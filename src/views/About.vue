<template>
  <v-container class="loan-calculator">
    <h2>Loan Payoff Calculator</h2>

    <!-- Input fields -->
    <v-row>
      <v-col cols="12" md="6">
        <v-text-field v-model="loanAmount" label="Loan Amount" type="number"></v-text-field>
      </v-col>
      <v-col cols="12" md="6">
        <v-text-field v-model="interestRate" label="Interest Rate" type="number"></v-text-field>
      </v-col>
      <v-col cols="12" md="6">
        <v-text-field v-model="loanTerm" label="Loan Term (in months)" type="number"></v-text-field>
      </v-col>
      <v-col cols="12" md="6">
        <v-text-field v-model="downPayment" label="Down Payment (optional)" type="number"></v-text-field>
      </v-col>
    </v-row>

    <!-- Calculate button -->
    <v-btn color="primary" @click="calculatePayoff">Calculate</v-btn>

    <!-- Results -->
    <v-card v-if="showResults">
      <v-card-title>
        <h3>Loan Payoff Details:</h3>
      </v-card-title>
      <v-card-text>
        <p>Monthly Installment: {{ monthlyInstallment }}</p>
        <p>Total Interest Paid: {{ totalInterestPaid }}</p>
      </v-card-text>
      <v-card-actions>
        <v-btn color="primary" @click="toggleAmortization">
          {{ showAmortization ? 'Hide Amortization Chart' : 'Show Amortization Chart' }}
        </v-btn>
      </v-card-actions>
      <v-expand-transition>
        <v-card v-show="showAmortization">
          <!-- Render the amortization chart here -->
        </v-card>
      </v-expand-transition>
    </v-card>
  </v-container>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';

@Component
export default class LoanPayoffCalculator extends Vue {
  loanAmount: number = 0;
  interestRate: number = 0;
  loanTerm: number = 0;
  downPayment: number = 0;
  showResults: boolean = false;
  showAmortization: boolean = false;
  monthlyInstallment: number = 0;
  totalInterestPaid: number = 0;
  amortizationData: any[] = [];

  calculatePayoff(): void {
    const loanAmount = this.loanAmount - this.downPayment;
    const interestRate = this.interestRate / 100;
    const monthlyInterestRate = interestRate / 12;
    const numberOfPayments = this.loanTerm * 12;

    const numerator = loanAmount * monthlyInterestRate;
    const denominator = 1 - Math.pow(1 + monthlyInterestRate, -numberOfPayments);

    this.monthlyInstallment = numerator / denominator;
    this.totalInterestPaid = (this.monthlyInstallment * numberOfPayments) - loanAmount;

    // Generate the amortization data
    this.amortizationData = this.generateAmortizationData(loanAmount, monthlyInterestRate, numberOfPayments);

    this.showResults = true;
  }

  generateAmortizationData(loanAmount: number, monthlyInterestRate: number, numberOfPayments: number): any[] {
    // Implement your logic here to generate the amortization data based on loan details
    // Return an array containing the amortization data for each payment
    // Each element of the array should include details such as payment number, principal paid, interest paid, remaining balance, etc.
    return [];
  }

  toggleAmortization(): void {
    this.showAmortization = !this.showAmortization;
  }
}
</script>

<style scoped>
/* Add your desired CSS styling for the component here */
</style>
