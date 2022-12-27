<template>
  <section class="tip-calculator">
    <!-- BILL AMOUNT -->
    <div class="bill-wrapper">
      <h2>Bill</h2>
      <div class="ctrl bill-ctrl">
        <input type="number" name="bill" id="bill" />
      </div>
    </div>

    <!-- TIP SELECTION -->
    <div class="tips-wrapper">
      <h2>Select Tip %</h2>
      <div class="tips">
        <button class="btn btn-tip active">5%</button>
        <button class="btn btn-tip">10%</button>
        <button class="btn btn-tip">15%</button>
        <button class="btn btn-tip">25%</button>
        <button class="btn btn-tip">50%</button>
        <div class="custom-tip-wrapper">
          <button v-if="!customTip" class="btn btn-tip">Custom</button>
          <input v-if="customTip" type="number" name="customTip" id="custom-tip" />
        </div>
      </div>
    </div>

    <!-- PERSON SELECTION -->
    <div class="persons-wrapper">
      <h2>Number of People</h2>
      <div class="ctrl person-ctrl">
        <input type="number" name="bill" id="bill" />
      </div>
    </div>

    <!-- TIP CALCULATION -->
    <div class="tip-amount-wrapper">
      <div class="tip-amount">
        <div class="label">
          <h2>Tip Amount</h2>
          <p>/ person</p>
        </div>
        <div class="value">{{ tipValue }}</div>
      </div>

      <div class="total-amount">
        <div class="label">
          <h2>Total</h2>
          <p>/ person Reset</p>
        </div>
        <div class="value">{{ totalValue }}</div>
      </div>

      <div class="tip-reset">
        <button class="btn btn-reset">RESET</button>
      </div>
    </div>
  </section>
</template>

<script lang="tsx">
export default {
  name: "TipCalculator",
  data() {
    return {
      tipValue: 0,
      totalValue: 0,
      customTip: false
    };
  },
};
</script>
