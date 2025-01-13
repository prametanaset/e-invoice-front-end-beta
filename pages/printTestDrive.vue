<template>
  <div>
    <!-- Button to trigger print -->
    <button @click="printContent(printSection.innerHTML)">Print</button>

    <!-- Content to print -->
    <div ref="printSection" class="print-content">
      <h1>Invoice</h1>
      <p>This is the content to print.</p>
    </div>
  </div>
</template>

<script setup lang="ts">

const printSection = ref<HTMLElement | null>(null);

const printContent = () => {
  if (!printSection.value) return;

  // Create a hidden iframe
  const iframe = document.createElement("iframe");
  iframe.style.position = "absolute";
  iframe.style.top = "-10000px";
  document.body.appendChild(iframe);

  // Write the content to the iframe
  const doc = iframe.contentWindow?.document;
  if (doc) {
    doc.open();
    doc.write(`
      <!DOCTYPE html>
      <html>
      <head>
        <title>Print</title>
        <style>
          /* Add print-specific styles here */
          body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 20px;
          }
          h1 {
            color: #333;
          }
        </style>
      </head>
      <body>
        ${printSection.value.innerHTML}
      </body>
      </html>
    `);
    doc.close();
  }

  // Trigger the print
  iframe.contentWindow?.focus();
  iframe.contentWindow?.print();

  // Cleanup the iframe after printing
  setTimeout(() => {
    document.body.removeChild(iframe);
  }, 1000);
};
</script>

<style>
/* Styles for the component */
.print-content {
  padding: 20px;
  border: 1px solid #ddd;
  background-color: #f9f9f9;
}
</style>
