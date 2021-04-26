<template lang="html">
  <div class="about">
    <h1>About</h1>
    <p>
      Clicking the button below or the "Home" link will "delay" the navigation and show a toast
      below instead, which would allow the user to either navigate, or cancel.
    </p>
    <p>
      This does not work as expected: the URL changes immediately and doesn’t change back. Also,
      going back multiple times will eventually unload the Vue app.
    </p>
    <button @click="$router.back()">Go Back</button>
    <ul class="toasts">
      <li v-for="(toast, index) in toasts" :key="index">
        {{ toast.message }}
        <button @click="handleToastAction(index)">{{ toast.actionLabel }}</button>
        <button @click="closeToast(index)">Close</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  beforeRouteLeave(to, from, next) {
    this.addToast({
      message: 'You have unsaved changes, would you like to leave and discard them?',
      action: next,
      actionLabel: 'Discard and leave',
    });
  },
  data() {
    return {
      toasts: [],
    };
  },
  methods: {
    addToast(toast) {
      this.toasts.push(toast);
    },
    closeToast(index) {
      const toast = this.toasts.splice(index, 1)[0];
      toast.action(false);
    },
    handleToastAction(index) {
      const toast = this.toasts.splice(index, 1)[0];
      toast.action();
    },
  },
};
</script>
