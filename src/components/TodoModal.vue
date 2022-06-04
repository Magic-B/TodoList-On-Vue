<template>
  <div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
    <div class="modal-dialog">
      <div class="modal-content">
        <div class="modal-header">
          <h5 class="modal-title" id="exampleModalLabel">Вы действительно хотите удалить все задачи?</h5>
          <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
        </div>
        <div class="modal-body">
          Все задачи будут утеряны!
        </div>
        <div class="modal-footer">
          <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Нет</button>
          <button type="button" class="btn btn-primary" @click="clearLocalStorage">Да</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
    methods: {
        clearLocalStorage() {
            localStorage.clear();
            location.reload();
        }
    }
}
</script>