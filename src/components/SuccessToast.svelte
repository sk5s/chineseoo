<script>
  import { Toast, ToastHeader, ToastBody } from 'sveltestrap'
  export let messageText = ""
</script>

<div class="p-3 mb-3 position-fixed bottom-0 end-0">
  <Toast class="me-1">
    <ToastHeader icon="success">Success</ToastHeader>
    <ToastBody>
      {messageText}
    </ToastBody>
  </Toast>
</div>