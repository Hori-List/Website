<script setup lang="ts">
import {Appwrite} from 'appwrite';

const appwrite = new Appwrite();

const endpoint = import.meta.env.VITE_APPWRITE_ENDPOINT as string;
const project = import.meta.env.VITE_APPWRITE_PROJECT as string;

appwrite.setEndpoint(endpoint).setProject(project);

const parameters = new URLSearchParams(window.location.search);

let error = '';
let success = false;

if (parameters.has('userId') && parameters.has('secret')) {
  const userId = parameters.get('userId') as string;
  const secret = parameters.get('secret') as string;

  appwrite.account.updateVerification(userId, secret).then((res) => {
    console.log(res)
  }, (err) => {
    error = err;
    console.log(err);
  });
  success = true;
}
</script>

<template>
  <p v-if="successful">Your email has successfully been verified.</p>
  <p v-else>Welcome.</p>
</template>

<style>
</style>
