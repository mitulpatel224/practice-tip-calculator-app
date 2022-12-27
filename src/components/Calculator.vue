<template>
  <section class="tip-calculator">
    <form @reset="resetForm">
      <div class="form-ctrl-wrapper">
        <!-- BILL AMOUNT -->
        <div class="bill-wrapper">
          <div class="ctrl bill-ctrl">
            <label for="bill">Bill</label>
            <input type="number" name="bill" id="bill" v-model="billAmount" @change="billChange" placeholder="0" />
          </div>
        </div>

        <!-- TIP SELECTION -->
        <div class="tips-wrapper">
          <div class="ctrl tips-ctrl">
            <label for="r1">Select Tip %</label>
            <div class="radio-group">
              <div class="radio-ctrl">
                <label for="r1">5%</label>
                <input type="radio" name="r1" id="r1" value="5" v-model="selectedTip" @change="tipChange">
              </div>
              <div class="radio-ctrl">
                <label for="r2">10%</label>
                <input type="radio" name="r1" id="r2" value="10" v-model="selectedTip" @change="tipChange">
              </div>
              <div class="radio-ctrl">
                <label for="r3">15%</label>
                <input type="radio" name="r1" id="r3" value="15" v-model="selectedTip" @change="tipChange">
              </div>
              <div class="radio-ctrl">
                <label for="r4">25%</label>
                <input type="radio" name="r1" id="r4" value="25" v-model="selectedTip" @change="tipChange">
              </div>
              <div class="radio-ctrl">
                <label for="r5">50%</label>
                <input type="radio" name="r1" id="r5" value="50" v-model="selectedTip" @change="tipChange">
              </div>
              <div class="radio-ctrl">
                <input type="number" name="customTip" id="custom-tip" placeholder="Custom" v-model="customTip"
                  @change="customTipChange($event)" />
              </div>
            </div>
          </div>
        </div>

        <!-- PERSON SELECTION -->
        <div class="persons-wrapper">
          <div class="ctrl person-ctrl">
            <label for="person">Number of People</label>
            <input type="number" name="person" id="person" v-model="totalPerson" @change="personChange"
              placeholder="0" />
          </div>
        </div>
      </div>
      <!-- TIP CALCULATION -->
      <div class="tip-amount-wrapper">
        <div class="amount-wrapper">
          <div class="tip-amount">
            <div class="label">
              <label>Tip Amount</label>
              <p>/ person</p>
            </div>
            <div class="value"><span>$</span>{{ calculatedTipValue }}</div>
          </div>

          <div class="total-amount">
            <div class="label">
              <label>Total</label>
              <p>/ person</p>
            </div>
            <div class="value"><span>$</span>{{ calculatedTotal }}</div>
          </div>
        </div>
        <div class="tip-reset">
          <button type="reset">RESET</button>
        </div>
      </div>
    </form>
  </section>
</template>

<script lang="ts">
export default {
  name: "TipCalculator",
  data() {
    return {
      billAmount: null,
      totalPerson: null,
      selectedTip: null,
      customTip: null,
      total: {
        tipValue: 0,
        totalValue: 0,
      },
    };
  },
  computed: {
    calculatedTipValue() {
      const person = this.totalPerson || 1;
      const totalTip = this.total.tipValue / person;
      return totalTip || 0;
    },
    calculatedTotal() {
      const person = this.totalPerson || 1;
      const total = this.total.totalValue / person;
      return total || 0;
    }
  },
  methods: {
    resetForm: function (ev) {
      console.log('reset', ev);
      this.billAmount = null;
      this.totalPerson = null;
      this.selectedTip = null;
      this.customTip = null;
      this.total = {
        tipValue: 0,
        totalValue: 0,
      };
    },
    /**
     * Custom tip change event handler
     * @param param0 Event
     */
    customTipChange: function ({ target: { value } }: Event) {
      console.log('custom-change');

      this.selectedTip = null;
      this.removeActiveRadio();
      this.customTip = value;
      this.controlChange();
    },
    /**
     * Tip(Radio control) change event handler
     * Remove "active" class from all radio-controls
     * Add "active" class for the clicked radio-control
     * @param event Event
     */
    tipChange: function (event: Event) {
      console.log('radio-change');
      this.customTip = null;
      const { parentElement } = <HTMLElement>event?.target;

      this.removeActiveRadio();
      (<HTMLElement>parentElement).classList.add('active');
      this.controlChange();
    },
    billChange: function () {
      console.log('bill-change');
      this.controlChange();
    },
    personChange: function () {
      console.log('person-change');
      this.controlChange();
    },
    controlChange: function () {
      this.calculateTip();
      this.calculateTotal();
    },
    /**
     * To remove active state of an old Radio control
     */
    removeActiveRadio: function () {
      const radioList = document.getElementsByClassName('radio-ctrl');
      for (const el of radioList) {
        el.classList.remove('active');
      }
    },
    getTotalTip: function () {
      const bill = this.billAmount || 0;
      const tip = Number(this.selectedTip || this.customTip || 0);
      const totalTip = ((bill * tip) / 100);
      return totalTip || 0;
    },
    calculateTip: function () {
      const totalTip = this.getTotalTip();
      this.total.tipValue = totalTip || 0;
    },
    calculateTotal: function () {
      const bill = this.billAmount || 0;
      const totalAmount = this.getTotalTip() + bill;
      this.total.totalValue = totalAmount || 0
    }
  }
};
</script>
