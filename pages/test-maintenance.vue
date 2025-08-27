<script setup>
// Simulate 503 error
throw createError({
  statusCode: 503,
  statusMessage: 'Service Unavailable'
})
</script>
