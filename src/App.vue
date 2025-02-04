<script setup>
  import todos from './data/todos';
</script>

<template>
  <div class="todoapp">
    <h1 class="todoapp__title">todos {{ todos.length }}</h1>

      <div class="todoapp__content">
        <header class="todoapp__header">
          <!-- this button should have `active` class only if all todos are completed -->
          <button
            type="button"
            class="todoapp__toggle-all active"
            data-cy="ToggleAllButton"
          />

          <!-- Add a todo on form submit -->
          <form>
            <input
              data-cy="NewTodoField"
              type="text"
              class="todoapp__new-todo"
              placeholder="What needs to be done?"
            />
          </form>
        </header>

        <section class="todoapp__main" data-cy="TodoList">
          <div
            v-for="todo in todos"
            :key="todo.id"
            class="todo"
            :class="{ completed: todo.completed }"
          >
            <label class="todo__status-label">
              <input
                data-cy="TodoStatus"
                type="checkbox"
                class="todo__status"
                :checked="todo.completed"
              />
            </label>

            <span data-cy="TodoTitle" class="todo__title">
              {{ todo.title }}
            </span>
            <button
              type="button"
              class="todo__remove" 
              data-cy="TodoDelete"
              @click="removeTodo(todo.id)"
            >
              ×
            </button>

            <!-- overlay will cover the todo while it is being deleted or updated -->
            <div data-cy="TodoLoader" class="modal overlay">
              <div class="modal-background has-background-white-ter" />
              <div class="loader" />
            </div>
          </div>

          <!-- This todo is an active todo -->
          <div data-cy="Todo" class="todo">
            <label class="todo__status-label">
              <input
                data-cy="TodoStatus"
                type="checkbox"
                class="todo__status"
              />
            </label>

            <span data-cy="TodoTitle" class="todo__title">
              Not Completed Todo
            </span>
            <button type="button" class="todo__remove" data-cy="TodoDelete">
              ×
            </button>

            <div data-cy="TodoLoader" class="modal overlay">
              <div class="modal-background has-background-white-ter" />
              <div class="loader" />
            </div>
          </div>

          <!-- This todo is being edited -->
          <div data-cy="Todo" class="todo">
            <label class="todo__status-label">
              <input
                data-cy="TodoStatus"
                type="checkbox"
                class="todo__status"
              />
            </label>

            <!-- This form is shown instead of the title and remove button -->
            <form>
              <input
                data-cy="TodoTitleField"
                type="text"
                class="todo__title-field"
                placeholder="Empty todo will be deleted"
                value="Todo is being edited now"
              />
            </form>

            <div data-cy="TodoLoader" class="modal overlay">
              <div class="modal-background has-background-white-ter" />
              <div class="loader" />
            </div>
          </div>

          <!-- This todo is in loadind state -->
          <div data-cy="Todo" class="todo">
            <label class="todo__status-label">
              <input
                data-cy="TodoStatus"
                type="checkbox"
                class="todo__status"
              />
            </label>

            <span data-cy="TodoTitle" class="todo__title">
              Todo is being saved now
            </span>

            <button type="button" class="todo__remove" data-cy="TodoDelete">
              ×
            </button>

            <!-- 'is-active' class puts this modal on top of the todo -->
            <div data-cy="TodoLoader" class="modal overlay is-active">
              <div class="modal-background has-background-white-ter" />
              <div class="loader" />
            </div>
          </div>
        </section>

        <!-- Hide the footer if there are no todos -->
        <footer class="todoapp__footer" data-cy="Footer">
          <span class="todo-count" data-cy="TodosCounter">
            3 items left
          </span>

          <!-- Active link should have the 'selected' class -->
          <nav class="filter" data-cy="Filter">
            <a
              href="#/"
              class="filter__link selected"
              data-cy="FilterLinkAll"
            >
              All
            </a>

            <a
              href="#/active"
              class="filter__link"
              data-cy="FilterLinkActive"
            >
              Active
            </a>

            <a
              href="#/completed"
              class="filter__link"
              data-cy="FilterLinkCompleted"
            >
              Completed
            </a>
          </nav>

          <!-- this button should be disabled if there are no completed todos -->
          <button
            type="button"
            class="todoapp__clear-completed"
            data-cy="ClearCompletedButton"
          >
            Clear completed
          </button>
        </footer>
      </div>

      <!-- DON'T use conditional rendering to hide the notification -->
      <!-- Add the 'hidden' class to hide the message smoothly -->
      <div
        data-cy="ErrorNotification"
        class="notification is-danger is-light has-text-weight-normal"
      >
        <button data-cy="HideErrorButton" type="button" class="delete" />
        <!-- show only one message at a time -->
        Unable to load todos
        <br />
        Title should not be empty
        <br />
        Unable to add a todo
        <br />
        Unable to delete a todo
        <br />
        Unable to update a todo
      </div>
    </div>
</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
