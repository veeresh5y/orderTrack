<template>
  <div>
    <div class="bs-stepper">
      <div class="bs-stepper-header" role="tablist">
        <!-- your steps here -->
        <div
          class="step step1 webView"
          v-for="stepper in itemsData.statusSteps"
          :key="stepper.stepId"
          data-target="#information-part"
        >
          <button
            type="button"
            class="step-trigger"
            role="tab"
            aria-controls="logins-part"
            id="logins-part-trigger"
            @click="sendData(itemsData, stepper)"
          >
            <div class="stepName" :class="itemsData.titleAlign">
              <span class="bs-stepper-label">{{ stepper.name }}</span>
              <div class="mobileNextLable">{{ stepper.currentStatus }}</div>
            </div>
            <div class="stepCount">
              <i
                class="fa fa-check tickIcon"
                v-show="stepper.completed"
                aria-hidden="true"
              ></i>
              <span
                class="bs-stepper-circle activeColor"
                v-show="!stepper.completed"
                >{{ stepper.title }}</span
              >
              <span class="mobileStepCount"> of 3</span>
            </div>
            <div :key="stepper.stepId" class="line" :id="stepper.name"></div>
          </button>
        </div>
        <div class="mobileView">
          <div class="mobileViewCount">
            <!-- <i
                  class="fa fa-check tickIcon"
                  aria-hidden="true"
                ></i> -->
            <span class="bs-stepper-circle activeColor">{{
              itemsData.currentTitle
            }}</span>
            <span class="mobileStepCount"> of 3</span>
          </div>
          <div class="mobileViewName">
            <span class="bs-stepper-label">{{ itemsData.currentStatus }}</span>
            <div class="mobileNextLable">Next : {{ itemsData.nextStatus }}</div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: "orderDetails",
  props: ["itemsData", "manipulateData"],
  data() {
    return {};
  },
  created() {},
  methods: {
    sendData(itemsData, item) {
      this.manipulateData(itemsData, item);
    }
  }
};
</script>
<style scoped>
.mobileView {
  display: none;
}
.mobileViewCount {
  width: 30%;
  float: left;
}
.mobileViewName {
  width: 70%;
  float: right;
}
.bs-stepper .step-trigger {
  /* padding: 0 0 10px 10px; */
  width: 125px;
  height: 100px;
  text-align: left;
  position: relative;
}
.right {
  right: 0;
  text-align: right;
}
.left {
  right: 0;
  text-align: right;
}
.top {
  top: 0;
}
.bottom {
  bottom: 0;
}
.bs-stepper .line,
.bs-stepper-line {
  position: absolute;
  width: 100%;
  right: -100px;
}
#Review {
  display: none !important;
}
/* Mobile Responsive Start*/
@media only screen and (max-width: 520px) {
  .mobileView {
    display: block;
  }
  .webView {
    display: none;
  }
  .bs-stepper-header {
    display: -ms-flexbox;
    /* display: flex; */
    -ms-flex-align: center;
    /* align-items: center; */
    -ms-flex-direction: column;
    flex-direction: column;
    -ms-flex-align: stretch;
    align-items: stretch;
    margin: 0;
    display: flex;
  }
  .bs-stepper-label {
    color: #038365 !important;
  }
  .bs-stepper .step-trigger {
    display: block !important;
    width: 100% !important;
    flex-direction: initial !important;
  }
  .line {
    display: none;
  }
  .mobileNextLable {
    display: block !important;
  }
  .mobileStepCount {
    display: inline !important;
  }
  .stepCount {
    width: 30% !important;
    float: left;
    padding-left: 0px;
  }
  .stepName {
    width: 70% !important;
    float: right;
    position: absolute;
  }
  .step {
    width: auto !important;
  }
} /* Mobile Responsive End*/
.activeColor {
  background: #038365;
  color: #fff;
}
.mobileNextLable {
  color: #a2a3a7;
  font-size: 13px;
  display: none;
}
.stepCount {
  width: 100%;
  float: left;
  padding-left: 10px;
  position: absolute;
}
.stepName {
  width: 100%;
  float: right;
  position: absolute;
}
.mobileStepCount {
  display: none;
}
.tickIcon {
  background: #038365;
  color: #fff;
  height: 32px;
  width: 32px;
  border-radius: 50%;
  padding-top: 7px;
  text-align: center;
}
.step {
  width: 20%;
}
</style>
