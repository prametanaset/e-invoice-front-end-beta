<template>
  <div>
    <!-- Button to trigger print -->
    <button @click="printComponent(printSection.innerHTML)">Print</button>
    <button @click="printComponent(htmlInvoice)">Print</button>

    <!-- Content to print -->
    <div ref="printSection" class="print-content">
      <h1>Invoice</h1>
      <p>This is the content to print.</p>
    </div>
  </div>
</template>

<script setup lang="ts">
import printComponent from "@/utils/printComponent";

const printSection = ref<HTMLElement | null>(null);
const htmlInvoice = `
  <h4>เอกสารนี้ได้จัดทำและส่งข้อมูลให้แก่กรมสรรพากรด้วยวิธีการทางอิเล็กทรอนิกส์</h4>

  <h1>Invoice Test Drive</h1>
      <p>This is the content to print.</p>
`;
/*
const printContent = () => {
  if (!printSection.value) return;

  // Create a hidden iframe
  const iframe = document.createElement("iframe");
  iframe.style.position = "absolute";
  iframe.style.top = "-10000px";
  iframe.style.width = "0";
  iframe.style.height = "0";
  iframe.style.border = "none";
  document.body.appendChild(iframe);

  // Get the iframe's document
  const iframeDoc = iframe.contentDocument || iframe.contentWindow?.document;
  if (!iframeDoc) {
    console.error("Failed to access iframe document");
    return;
  }

  // Build the HTML structure inside the iframe
  const html = iframeDoc.createElement("html");
  const head = iframeDoc.createElement("head");
  const body = iframeDoc.createElement("body");

  // Add custom styles
  const style = iframeDoc.createElement("style");
  style.textContent = `
    body {
      font-family: Arial, sans-serif;
      margin: 20px;
    }
    h1 {
      color: #333;
    }
  `;
  head.appendChild(style);

  // Copy content to the iframe body
  if (printSection.value) {
    // body.innerHTML = printSection.value.innerHTML;
    body.innerHTML = `
      <h1>Invoice</h1>
      <p>This is the content to print.</p>
    `
  }

  // Append head and body to the HTML element
  html.appendChild(head);
  html.appendChild(body);

  // Replace the iframe's content with the newly built HTML
  iframeDoc.documentElement.innerHTML = html.outerHTML;

  // Trigger the print
  iframe.contentWindow?.focus();
  iframe.contentWindow?.print();

  // Cleanup the iframe after printing
  setTimeout(() => {
    document.body.removeChild(iframe);
  }, 1000);
};
*/


</script>

<style scoped>
/* Styles for the main component */
.print-content {
  padding: 20px;
  border: 1px solid #ddd;
  background-color: #f9f9f9;
}
</style>
