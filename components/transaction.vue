<template>
  <section v-if="transactionInProgress">
    <article class="animate__animated animate__slideInDown card accent-border">
      Transaction status:
      <template v-if="transactionStatus < 0">
        <span
          ><kbd>Initializing</kbd><br /><small
            >Waiting for transaction approval.</small
          ></span
        >
        <progress indeterminate>Initializing...</progress>
      </template>

      <template v-else-if="transactionStatus < 2">
        <span
          ><kbd>Pending</kbd><br /><small
            >The transaction has been received by a collector but not yet
            finalized in a block.</small
          ></span
        >
        <progress indeterminate>Executing</progress>
      </template>

      <template v-else-if="transactionStatus === 2">
        <span
          ><kbd>Finalized</kbd><br /><small
            >The consensus nodes have finalized the block that the transaction
            is included in.</small
          ></span
        >
        <progress min="0" max="100" value="80">Executing...</progress>
      </template>
      <template v-else-if="transactionStatus === 3">
        <span
          ><kbd>Executed</kbd><br /><small>
            The execution nodes have produced a result for the
            transaction.</small
          ></span
        >
        <progress min="0" max="100" value="80">Sealing...</progress>
      </template>
      <template v-else-if="transactionStatus === 4">
        <span
          ><kbd>✓ Sealed</kbd><br /><small
            >The verification nodes have verified the transaction, and the seal
            is included in the latest block.</small
          ></span
        >
        <progress min="0" max="100" value="100">Sealed!</progress>
      </template>
      <template v-else-if="transactionStatus === 5">
        <span
          ><kbd>Expired</kbd><br /><small
            >The transaction was submitted past its expiration block
            height.</small
          ></span
        >
      </template>
      <template v-else>
        <span data-theme="invalid">Error!</span>
      </template>
    </article>
    <small><a href="https://docs.onflow.org/access-api/">More info</a></small>
  </section>
</template>

<script>
export default {
  props: ["transactionInProgress", "transactionStatus"],
};
</script>
<style>
progress {
  margin-top: 1em;
}

small {
  opacity: 0.8;
}
</style>