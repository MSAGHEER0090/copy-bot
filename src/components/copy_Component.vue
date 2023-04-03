<template>
  <div>
    <!-- <input type="file" ref="fileInput" @change="onFileSelected" /> -->
    <div v-if="selectedFile">
      <h3>Selected file: {{ selectedFile.name }}</h3>
      <h1>Check console</h1>
      <h3>Copy the file with updated username and password</h3>
      <form @submit.prevent="onCopySubmit">
        <div>
          <label for="username">Username:</label>
          <input type="text" id="username" v-model="username" />
        </div>
        <div>
          <label for="password">Password:</label>
          <input type="text" id="password" v-model="password" />
        </div>
        <div>
          <p>Select Max_Trade</p>
          <input type="radio" id="1" name="max_trade" value="1" v-model="max_trade">
          <label for="1">Max_Trade: 1</label><br>
          <input type="radio" id="2" name="max_trade" value="2" v-model="max_trade">
          <label for="2">Max_Trade: 2</label><br>
          <input type="radio" id="3" name="max_trade" value="3" v-model="max_trade">
          <label for="3">Max_Trade: 3</label>
        </div>
        <div>
          <p>Select Stake currency</p>
          <input type="radio" id="USDT" name="stake_currency" value="USDT" v-model="stake_currency">
          <label for="USDT">USDT</label><br>
          <input type="radio" id="USD" name="stake_currency" value="USD" v-model="stake_currency">
          <label for="USD">USD</label><br>
        </div>
        <button type="submit">Copy</button>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  name: "copy_Component",
  data() {
    return {
      selectedFile: null,
      fileContents: null,
      username: "",
      password: "",
      max_trade: 0,
      stake_currency: ""
    };
  }, async mounted() {
  this.selectedFile = await fetch("http://localhost:3000/data");
  const reader = new FileReader();
  reader.onload = () => {
    this.fileContents = reader.result;
    console.log(this.selectedFile);
  };
  reader.readAsText(this.selectedFile);
},


  methods: {
    // onFileSelected(event) {

    // },
    onCopySubmit() {
      const newFileContents = this.fileContents
        .replace(/("username":\s*")\w*"/, `$1${this.username}"`)
        .replace(/("password":\s*")\w*"/, `$1${this.password}"`)
        .replace(/("stake_currency":\s")\w*/, `$1${this.stake_currency}"`)
        .replace(/("max_open_trades":\s*)\d+/, `$1${this.max_trade}`);

      const newFileName = "new_" + this.username;
      const blob = new Blob([newFileContents], { type: "application/json" });
      const link = document.createElement("a");
      link.href = URL.createObjectURL(blob);
      link.download = newFileName;
      link.click();
    },
  },
};
</script>
