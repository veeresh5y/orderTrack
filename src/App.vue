<template>
  <div id="app">
    <div id="nav" v-for="items in itemsList" :key="items.itemId">
      <order-details
        :itemsData="items"
        :manipulateData="manipulate"
      ></order-details>
    </div>
    <router-view />
  </div>
</template>
<script>
export default {
  components: {
    "order-details": () => import("./components/orderDetails.vue")
  },
  data() {
    return {
      itemsList: [
        {
          itemId: "450098",
          titleAlign: "top",
          currentStatus: "Shipping",
          nextStatus: "Payment",
          currentTitle: "1",
          statusSteps: [
            {
              stepId: "SHIPPING",
              icon: "",
              name: "Shipping",
              title: "1",
              subTitle: "",
              completed: true,
              nextStatus: "Payment",
              buttonAction: true
            },
            {
              stepId: "PAYMENT",
              icon: "",
              name: "Payment",
              title: "2",
              subTitle: "",
              completed: false,
              nextStatus: "Review",
              buttonAction: true
            },
            {
              stepId: "REVIEW",
              icon: "",
              name: "Review",
              title: "3",
              subTitle: "",
              completed: false,
              nextStatus: "Done",
              buttonAction: false
            }
          ]
        },
        {
          itemId: "123434",
          titleAlign: "top",
          currentStatus: "Payment",
          nextStatus: "Review",
          currentTitle: "2",
          statusSteps: [
            {
              stepId: "SHIPPING",
              icon: "",
              name: "Shipping",
              title: "1",
              subTitle: "",
              completed: true,
              nextStatus: "Payment",
              buttonAction: true
            },
            {
              stepId: "PAYMENT",
              icon: "",
              name: "Payment",
              title: "2",
              subTitle: "",
              completed: true,
              nextStatus: "Review",
              buttonAction: true
            },
            {
              stepId: "REVIEW",
              icon: "",
              name: "Review",
              title: "3",
              subTitle: "",
              completed: false,
              nextStatus: "Done",
              buttonAction: true
            }
          ]
        },
        {
          itemId: "6995504",
          titleAlign: "top",
          currentStatus: "Review",
          nextStatus: "Done",
          currentTitle: "3",
          statusSteps: [
            {
              stepId: "SHIPPING",
              icon: "",
              name: "Shipping",
              title: "1",
              subTitle: "",
              completed: true,
              nextStatus: "Payment",
              buttonAction: true
            },
            {
              stepId: "PAYMENT",
              icon: "",
              name: "Payment",
              title: "2",
              subTitle: "",
              completed: true,
              nextStatus: "Review",
              buttonAction: true
            },
            {
              stepId: "REVIEW",
              icon: "",
              name: "Review",
              title: "3",
              subTitle: "",
              completed: true,
              nextStatus: "Done",
              buttonAction: true
            }
          ]
        }
      ]
    };
  },
  methods: {
    manipulate(itemsData, item) {
      let selectedIndex = this.itemsList.findIndex(
        obj => obj.itemId == itemsData.itemId
      );
      let indexedValue = this.itemsList[selectedIndex].statusSteps.findIndex(
        obj => obj.stepId == item.stepId
      );
      console.log("selected status is:::", item.name);
      // console.log("selected label value:::", item.title);
      console.log("selected indexed value:::", indexedValue);
      this.itemsList[selectedIndex].statusSteps.forEach(element => {
        element.completed = false;
      });
      this.itemsList[selectedIndex].statusSteps.some(selectedStep => {
        selectedStep.completed = true;
        if (selectedStep.stepId === item.stepId) {
          selectedStep.completed = true;
          this.itemsList[selectedIndex].nextStatus = selectedStep.nextStatus;
          this.itemsList[selectedIndex].currentStatus = selectedStep.name;
          this.itemsList[selectedIndex].currentTitle = selectedStep.title;
          return true;
        }
      });
    }
  }
};
</script>
<style lang="scss">
@import "../node_modules/bootstrap/dist/css/bootstrap.min.css";
@import "../node_modules/bootstrap-vue/dist/bootstrap-vue.css";
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
#nav {
  padding: 30px 30px 0 30px;
}
#nav a {
  font-weight: bold;
  color: #2c3e50;
}
#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
